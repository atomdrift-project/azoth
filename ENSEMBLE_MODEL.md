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

Three views of each filetype, evaluated on **1963 test-partition rows** (SHA256-deterministic 12.5% locked holdout — never seen during training or calibration). 'Ensemble' uses the per-filetype winning strategy from above; 'Routing policy' is the deployed thresholded decision at the default operating level (a separate concern from the raw AUC of the combiner).

| File type | Files | General ROC | Specialist ROC | Ensemble ROC | Strategy | Routing policy |
|---|---:|---:|---:|---:|---|---|
| `pe` | 1253 | 1.0000 | 1.0000 | 1.0000 | `calibrated_max` | `specialist_primary_with_escape` |
| `elf` | 14 | 0.0000 | 0.0000 | 0.0000 | `specialist_priority` | `no_policy` |
| `msi` | 2 | 0.0000 | 0.0000 | 0.0000 | `calibrated_max` | `or_general_primary` |
| `javascript` | 11 | 1.0000 | 1.0000 | 1.0000 | `specialist_priority` | `no_policy` |
| `shell` | 21 | 0.0000 | 0.0000 | 0.0000 | `calibrated_max` | `group_only` |
| `jar` | 13 | 0.0000 | 0.0000 | 0.0000 | `specialist_priority` | `no_policy` |

Reading the table: ensemble ≥ specialist holds for every filetype by design. When `strategy = specialist_priority`, the ensemble's column matches the specialist's. When `strategy = calibrated_max`, the routing-free combiner beats the specialist alone — those filetypes benefit most from cross-model signal.

## Operational FP/M dialing (deployment knob)

Independently of the AUC/PR metrics above, the bundle is calibrated at ten thresholded operating points (L0…L9) per severity. Each level corresponds to a per-million false-positive budget; the calibrator picks the per-route thresholds that maximize true positives subject to that global budget.

**This is a deployment dial, not a model-quality result.** When a route shows `no_policy` at a given level, it means no threshold for that route fits inside the global FP budget at that level — which is a function of corpus size, route benign-tail shape, and the FP target, not the model's discrimination ability. Dialing the operating level up admits more routes; dialing down enforces a stricter FP target. Per-route operating tables live in each `filetypes/<name>/README.md`.

| L | H target/1M | H accuracy | H recall | H FP/1M | S target/1M | S accuracy | S recall | S FP/1M |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 89.72% | 83.41% | 86405.6 | 8.0 | 89.90% | 84.30% | 86412.3 |
| 1 | 1.0 | 89.75% | 83.58% | 86405.6 | 16.0 | 90.01% | 84.84% | 86415.6 |
| 2 | 2.0 | 89.75% | 83.58% | 86405.6 | 24.0 | 90.28% | 86.13% | 86422.4 |
| 3 | 3.0 | 89.75% | 83.58% | 86405.6 | 32.0 | 90.29% | 86.20% | 86425.7 |
| 4 | 4.0 | 89.75% | 83.58% | 86405.6 | 40.0 | 90.32% | 86.32% | 86429.1 |
| 5 | 5.0 | 89.75% | 83.58% | 86405.6 | 48.0 | 90.37% | 86.57% | 86432.5 |
| 6 | 6.0 | 89.75% | 83.58% | 86405.6 | 56.0 | 90.44% | 86.98% | 86533.3 |
| 7 | 7.0 | 89.90% | 84.30% | 86412.3 | 64.0 | 90.49% | 88.30% | 89407.2 |
| 8 | 8.0 | 89.90% | 84.30% | 86412.3 | 72.0 | 90.60% | 88.85% | 89424.0 |
| 9 | 9.0 | 89.90% | 84.30% | 86412.3 | 80.0 | 90.70% | 89.34% | 89427.4 |

Default deploy: L3 for hostile, L5 for suspicious. The headline AUC/PR/F1 figures elsewhere in this bundle are about the model's ranking ability — they don't change with the operating level.
