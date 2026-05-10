# Azoth Filetype — `elf`

Specialist classifier for `elf`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `elf` test-bucket rows (n=13994, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9999 | 0.9933 | +0.0066 |
| PR AUC | 0.9995 | 0.9933 | +0.0062 |
| F1 | 0.9936 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `elf` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filegroups/native`, `filetypes/elf`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9999**, PR AUC = **0.9995**, F1 = **0.9936**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (49112 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=160, max_depth=12, min_child_samples=60, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
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
- Training rows: 116885 (19171 malware, 97714 benign).
- Internal training-time benchmark rows: 16876 (2733 malware, 14143 benign).
- Internal training-time benchmark AUC/AP/F1: 1.0000 / 0.9999 / 0.9984.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.93% | 0.00 | 0.997047 | 8.0 | 98.79% | 70.71 | 0.987395 |
| 1 | 1.0 | 98.79% | 70.71 | 0.987395 | 16.0 | 98.79% | 70.71 | 0.987395 |
| 2 | 2.0 | 98.79% | 70.71 | 0.987395 | 24.0 | 98.79% | 70.71 | 0.987395 |
| 3 | 3.0 | 98.79% | 70.71 | 0.987395 | 32.0 | 98.79% | 70.71 | 0.987395 |
| 4 | 4.0 | 98.79% | 70.71 | 0.987395 | 40.0 | 98.79% | 70.71 | 0.987395 |
| 5 | 5.0 | 98.79% | 70.71 | 0.987395 | 48.0 | 98.79% | 70.71 | 0.987395 |
| 6 | 6.0 | 98.79% | 70.71 | 0.987395 | 56.0 | 98.79% | 70.71 | 0.987395 |
| 7 | 7.0 | 98.79% | 70.71 | 0.987395 | 64.0 | 98.79% | 70.71 | 0.987395 |
| 8 | 8.0 | 98.79% | 70.71 | 0.987395 | 72.0 | 98.79% | 70.71 | 0.987395 |
| 9 | 9.0 | 98.79% | 70.71 | 0.987395 | 80.0 | 98.79% | 70.71 | 0.987395 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 92.84% | 1 | 10.49 | `{"filegroups/native": 0.9987809062004089, "filetypes/elf": 0.993222713470459, "general": 0.932529628276825}` |
| 5 | suspicious | group_primary_with_escape | 93.99% | 4 | 41.96 | `{"filegroups/native": 0.9980961084365845, "filetypes/elf": 0.993222713470459, "general": 0.932529628276825}` |
| 9 | hostile | or_general_primary | 92.84% | 1 | 10.49 | `{"filegroups/native": 0.9987809062004089, "filetypes/elf": 0.993222713470459, "general": 0.932529628276825}` |
| 9 | suspicious | group_primary_with_escape | 94.53% | 7 | 73.43 | `{"filegroups/native": 0.9975190162658691, "filetypes/elf": 0.993222713470459, "general": 0.932529628276825}` |
