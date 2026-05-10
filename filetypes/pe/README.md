# Azoth Filetype — `pe`

Specialist classifier for `pe`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `pe` test-bucket rows (n=51179, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9989 | 0.9982 | +0.0007 |
| PR AUC | 0.9995 | 0.9983 | +0.0012 |
| F1 | 0.9906 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `pe` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filegroups/native`, `filetypes/pe`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9989**, PR AUC = **0.9995**, F1 = **0.9906**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 476539 (353276 malware, 123263 benign).
- Internal training-time benchmark rows: 66060 (48516 malware, 17544 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9999 / 1.0000 / 0.9990.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 67.20% | 0.00 | 0.999878 | 8.0 | 83.18% | 57.00 | 0.999598 |
| 1 | 1.0 | 83.18% | 57.00 | 0.999598 | 16.0 | 83.18% | 57.00 | 0.999598 |
| 2 | 2.0 | 83.18% | 57.00 | 0.999598 | 24.0 | 83.18% | 57.00 | 0.999598 |
| 3 | 3.0 | 83.18% | 57.00 | 0.999598 | 32.0 | 83.18% | 57.00 | 0.999598 |
| 4 | 4.0 | 83.18% | 57.00 | 0.999598 | 40.0 | 83.18% | 57.00 | 0.999598 |
| 5 | 5.0 | 83.18% | 57.00 | 0.999598 | 48.0 | 83.18% | 57.00 | 0.999598 |
| 6 | 6.0 | 83.18% | 57.00 | 0.999598 | 56.0 | 83.18% | 57.00 | 0.999598 |
| 7 | 7.0 | 83.18% | 57.00 | 0.999598 | 64.0 | 83.18% | 57.00 | 0.999598 |
| 8 | 8.0 | 83.18% | 57.00 | 0.999598 | 72.0 | 83.18% | 57.00 | 0.999598 |
| 9 | 9.0 | 83.18% | 57.00 | 0.999598 | 80.0 | 83.18% | 57.00 | 0.999598 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 63.70% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9997933506965637, "general": 0.9993268251419067}` |
| 5 | suspicious | specialist_primary_with_escape | 79.11% | 6 | 45.10 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.99945068359375, "general": 0.9996013045310974}` |
| 9 | hostile | or_general_primary | 63.70% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9997933506965637, "general": 0.9993268251419067}` |
| 9 | suspicious | specialist_primary_with_escape | 84.41% | 10 | 75.17 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9992316961288452, "general": 0.9993268251419067}` |
