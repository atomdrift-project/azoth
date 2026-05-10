# Azoth Filetype — `java_class`

Specialist classifier for `java_class`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `java_class` test-bucket rows (n=918, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9991 | — | - |
| PR AUC | 0.9895 | — | - |
| F1 | 0.9877 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `java_class` is `group_only`.
Routes consulted (max-of-thresholds): `filegroups/portable`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9991**, PR AUC = **0.9895**, F1 = **0.9877**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (49112 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - format-group hints
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Training rows: 161127 (528 malware, 160599 benign).
- Internal training-time benchmark rows: 22784 (75 malware, 22709 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9927 / 0.9746 / 0.9865.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 97.33% | 0.00 | 0.930347 | 8.0 | 97.33% | 44.04 | 0.620390 |
| 1 | 1.0 | 97.33% | 44.04 | 0.620390 | 16.0 | 97.33% | 44.04 | 0.620390 |
| 2 | 2.0 | 97.33% | 44.04 | 0.620390 | 24.0 | 97.33% | 44.04 | 0.620390 |
| 3 | 3.0 | 97.33% | 44.04 | 0.620390 | 32.0 | 97.33% | 44.04 | 0.620390 |
| 4 | 4.0 | 97.33% | 44.04 | 0.620390 | 40.0 | 97.33% | 44.04 | 0.620390 |
| 5 | 5.0 | 97.33% | 44.04 | 0.620390 | 48.0 | 97.33% | 44.04 | 0.620390 |
| 6 | 6.0 | 97.33% | 44.04 | 0.620390 | 56.0 | 97.33% | 44.04 | 0.620390 |
| 7 | 7.0 | 97.33% | 44.04 | 0.620390 | 64.0 | 97.33% | 44.04 | 0.620390 |
| 8 | 8.0 | 97.33% | 44.04 | 0.620390 | 72.0 | 97.33% | 44.04 | 0.620390 |
| 9 | 9.0 | 97.33% | 44.04 | 0.620390 | 80.0 | 97.33% | 44.04 | 0.620390 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 5 | suspicious | group_primary_with_escape | 96.43% | 1 | 137.70 | `{"filegroups/portable": 0.8742847442626953, "filetypes/java_class": 0.2499084323644638}` |
| 9 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 9 | suspicious | group_primary_with_escape | 96.43% | 1 | 137.70 | `{"filegroups/portable": 0.8742847442626953, "filetypes/java_class": 0.2499084323644638}` |
