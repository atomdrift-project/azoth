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

Three views of each filetype, evaluated on **372198 test-partition rows** (SHA256-deterministic 12.5% locked holdout — never seen during training or calibration). 'Ensemble' uses the per-filetype winning strategy from above; 'Routing policy' is the deployed thresholded decision at the default operating level (a separate concern from the raw AUC of the combiner).

| File type | Files | General ROC | Specialist ROC | Ensemble ROC | Strategy | Routing policy |
|---|---:|---:|---:|---:|---|---|
| `pe` | 67133 | 0.9970 | 0.2988 | 0.9970 | `calibrated_max` | `or_general_primary` |
| `elf` | 16886 | 0.9998 | 0.0000 | 0.9998 | `calibrated_max` | `or_general_primary` |
| `macho` | 921 | 0.9716 | 0.0000 | 0.9730 | `calibrated_max` | `or_general_primary` |
| `msi` | 37 | 0.7043 | 0.0000 | 0.7634 | `calibrated_max` | `general_only` |
| `pdf` | 352 | 0.8252 | 0.0000 | 0.8788 | `stacked_xgb` | `or_general_primary` |
| `rtf` | 56 | 1.0000 | 0.0000 | 1.0000 | `calibrated_max` | `general_only` |
| `javascript` | 54690 | 0.9857 | 0.2778 | 0.9881 | `calibrated_max` | `or_general_primary` |
| `python` | 15704 | 0.9918 | 0.3093 | 0.9904 | `calibrated_max` | `or_general_primary` |
| `shell` | 5455 | 0.9715 | 0.0000 | 0.9690 | `calibrated_max` | `or_general_primary` |
| `powershell` | 241 | 0.9812 | 0.0000 | 0.9830 | `calibrated_max` | `or_general_primary` |
| `batch` | 291 | 0.9562 | 0.0000 | 0.9578 | `calibrated_max` | `or_general_primary` |
| `package.json` | 2782 | 0.9991 | 0.0000 | 0.9991 | `specialist_priority` | `or_general_primary` |
| `jar` | 289 | 0.9935 | 0.0000 | 0.9935 | `specialist_priority` | `general_only` |
| `ruby` | 2813 | 1.0000 | 0.0000 | 1.0000 | `calibrated_max` | `or_general_primary` |
| `perl` | 3721 | 0.9988 | 0.0000 | 0.9983 | `stacked_xgb` | `or_general_primary` |

Reading the table: ensemble ≥ specialist holds for every filetype by design. When `strategy = specialist_priority`, the ensemble's column matches the specialist's. When `strategy = calibrated_max`, the routing-free combiner beats the specialist alone — those filetypes benefit most from cross-model signal.

## Operational FP/M dialing (deployment knob)

Independently of the AUC/PR metrics above, the bundle is calibrated at ten thresholded operating points (L0…L9) per severity. Each level corresponds to a per-million false-positive budget; the calibrator picks the per-route thresholds that maximize true positives subject to that global budget.

**This is a deployment dial, not a model-quality result.** When a route shows `no_policy` at a given level, it means no threshold for that route fits inside the global FP budget at that level — which is a function of corpus size, route benign-tail shape, and the FP target, not the model's discrimination ability. Dialing the operating level up admits more routes; dialing down enforces a stricter FP target. Per-route operating tables live in each `filetypes/<name>/README.md`.

| L | H target/1M | H recall | H FP/1M | H 95% CI upper | S target/1M | S recall | S FP/1M | S 95% CI upper |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0† | 70.95% | 36.97 | 61.20 | 8.0† | 70.95% | 36.97 | 61.20 |
| 1 | 1.0† | 70.95% | 36.97 | 61.20 | 16.0 | 71.30% | 36.97 | 61.20 |
| 2 | 2.0† | 70.95% | 36.97 | 61.20 | 24.0 | 72.74% | 47.06 | 73.57 |
| 3 | 3.0† | 70.95% | 36.97 | 61.20 | 32.0 | 73.67% | 50.42 | 77.64 |
| 4 | 4.0† | 70.95% | 36.97 | 61.20 | 40.0 | 74.85% | 50.42 | 77.64 |
| 5 | 5.0† | 70.95% | 36.97 | 61.20 | 48.0 | 75.97% | 57.14 | 85.71 |
| 6 | 6.0† | 70.95% | 36.97 | 61.20 | 56.0 | 76.08% | 60.50 | 89.72 |
| 7 | 7.0† | 70.95% | 36.97 | 61.20 | 64.0 | 76.27% | 63.86 | 93.71 |
| 8 | 8.0† | 70.95% | 36.97 | 61.20 | 72.0 | 76.47% | 67.23 | 97.68 |
| 9 | 9.0† | 70.95% | 36.97 | 61.20 | 80.0 | 76.72% | 67.23 | 97.68 |

*95% CI upper* is the Clopper-Pearson upper bound on the deployment FP rate given the observed FP count in 297,504 test-partition benigns. The honest deployment-FP/M claim sits below this number with 95% confidence.

† below data resolution: the dev calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The deployed threshold falls back to the loosest empirical 0-FP fit; the FP/M and 95% CI columns show what the test partition actually achieves under that threshold, which exceeds the L target.

Default deploy: L3 for hostile, L5 for suspicious. The headline AUC/PR/F1 figures elsewhere in this bundle are about the model's ranking ability — they don't change with the operating level.
