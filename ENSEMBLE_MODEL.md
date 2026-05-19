# Azoth — Routed Ensemble

## How routing works

Each file is processed in three steps:

1. **Format detection.** The cleave report identifies the file's format (e.g. `elf`, `pe`, `javascript`).
2. **Route selection.** `route_policies.json` defines, per format and per FP/M operating level, which routes are allowed (e.g. `[general, filegroups/native, filetypes/elf]`) and at what calibrated thresholds.
3. **Decision.** Each allowed route scores the file with its own model + feature spec. The file is flagged at the chosen severity level iff any allowed route's score exceeds its threshold (the OR rule).

Routing policies fall into a small set of patterns the calibrator picks per route per level:

- `specialist_primary_with_escape`: file's own specialist is primary; general can still escalate if it scores high enough at its own threshold.
- `or_general_primary`: general is primary; specialist may escalate.
- `general_only` / `specialist_only` / `group_only`: that single route decides; others are ignored at this level.
- `no_policy`: no route configuration meets the FP/M target at this level — the route effectively doesn't fire at this severity.

## How the ensemble combiner works

Per-file, the ensemble combines the available route scores via one of two strategies, picked per filetype to maximize ROC AUC on the test bucket:

- **`specialist_priority`** (default): for each row, use the most specific route's *raw* score — specialist if available, else filegroup, else general. By construction this equals the specialist on filetype-X rows, so `ensemble ≥ specialist` always holds.
- **`calibrated_max`**: per-route isotonic calibration via 5-fold CV, then `max` of the calibrated probabilities across allowed routes. Wins when the specialist alone is weak and the cross-model signal genuinely adds discrimination — typically on filetypes with thin specialist training data (e.g. `pdf`, `docx`, `xml`).

The naive `max(raw_general, raw_filegroup, raw_specialist)` we used in earlier drafts is *not* used as the headline number — raw scores live on different scales, so it can rank worse than the specialist alone. It's recorded in `per_filetype_metrics.json` as `ensemble_strategies.naive_max` for diagnostic comparison only.

## General vs specialist vs ensemble

Three views of each filetype, evaluated on **585889 test-partition rows** (SHA256-deterministic 12.5% locked holdout — never seen during training or calibration). 'Ensemble' uses the per-filetype winning strategy from above; 'Routing policy' is the deployed thresholded decision at the default operating level (a separate concern from the raw AUC of the combiner).

| File type | Files | General ROC | Specialist ROC | Ensemble ROC | Strategy | Routing policy |
|---|---:|---:|---:|---:|---|---|
| `pe` | 128908 | 0.9956 | 0.9983 | 0.9991 | `stacked_xgb` | `learned_blend_at_fp_3` |
| `elf` | 25753 | 0.9993 | 0.9999 | 0.9999 | `specialist_priority` | `learned_blend_at_fp_0` |
| `macho` | 1640 | 0.9283 | 0.9988 | 0.9989 | `stacked_lr` | `learned_blend_at_fp_0` |
| `msi` | 223 | 0.8064 | 0.9785 | 0.9785 | `specialist_priority` | `joint_or_at_fp_0` |
| `pdf` | 23511 | 0.9770 | 0.9438 | 0.9923 | `stacked_xgb` | `joint_or_at_fp_0` |
| `rtf` | 265 | 0.9955 | 0.9980 | 0.9980 | `specialist_priority` | `joint_or_at_fp_0` |
| `javascript` | 69906 | 0.9883 | 0.9960 | 0.9960 | `calibrated_max` | `filetype_only` |
| `python` | 18557 | 0.9653 | 0.9950 | 0.9950 | `specialist_priority` | `joint_or_at_fp_0` |
| `shell` | 6602 | 0.9888 | 0.9969 | 0.9969 | `specialist_priority` | `filetype_only` |
| `powershell` | 514 | 0.9608 | 0.9790 | 0.9797 | `specialist_priority` | `joint_or_at_fp_0` |
| `batch` | 21520 | 0.9092 | 0.9996 | 0.9996 | `specialist_priority` | `learned_blend_at_fp_3` |
| `package.json` | 3523 | 0.9991 | 0.9992 | 0.9992 | `specialist_priority` | `joint_or_at_fp_0` |
| `jar` | 451 | 0.9681 | 0.9839 | 0.9839 | `specialist_priority` | `joint_or_at_fp_0` |
| `ruby` | 2950 | 0.9998 | 0.9989 | 1.0000 | `stacked_lr` | `joint_or_at_fp_0` |
| `perl` | 3984 | 0.9631 | 0.9979 | 0.9979 | `specialist_priority` | `joint_or_at_fp_0` |

Reading the table: ensemble ≥ specialist holds for every filetype by design. When `strategy = specialist_priority`, the ensemble's column matches the specialist's. When `strategy = calibrated_max`, the routing-free combiner beats the specialist alone — those filetypes benefit most from cross-model signal.

## Severity tiers (L0..L9)

L0..L9 are observation-derived severity grades, not optimization targets. For each route, level Lk's threshold is the (1 − qk × 10⁻⁶) quantile of that route's calibrated benign-score distribution on the dev partition — i.e., the score cut at which roughly qk benigns per million would be flagged. Strict tiers (qk below the empirical floor of n_benign × qk × 10⁻⁶ < 1) come from a generalized-Pareto fit to the benign-score upper tail; looser tiers are direct empirical quantiles.

**The grade is a description of the score's strictness, not a deployment knob optimized for any objective.** Litmus reads the per-level thresholds out of `route_policies.json`/`config.json` and assigns severity per file. The headline PR AUC and recall@3FP/M numbers above describe the underlying ranking — they don't depend on the L grade.

Default deploy: L3 for hostile, L5 for suspicious. Per-route L0..L9 thresholds and observed FP/M live in [route_policies.md](route_policies.md) and each `filetypes/<name>/README.md`.
