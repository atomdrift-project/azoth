# Azoth Filetype — `package.json`

Specialist classifier for `package.json`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `package.json` test-bucket rows (n=2666, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9995 | — | - |
| PR AUC | 0.9998 | — | - |
| F1 | 0.9976 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `package.json` is `group_primary_with_escape`.
Routes consulted (max-of-thresholds): `general`, `filegroups/config`, `filetypes/package.json`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9995**, PR AUC = **0.9998**, F1 = **0.9976**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 19983 (13777 malware, 6206 benign).
- Internal training-time benchmark rows: 2775 (1875 malware, 900 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9998 / 0.9999 / 0.9981.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 88.00% | 0.00 | 0.998667 | 8.0 | 93.01% | 1111.1 | 0.996908 |
| 1 | 1.0 | 93.01% | 1111.1 | 0.996908 | 16.0 | 93.01% | 1111.1 | 0.996908 |
| 2 | 2.0 | 93.01% | 1111.1 | 0.996908 | 24.0 | 93.01% | 1111.1 | 0.996908 |
| 3 | 3.0 | 93.01% | 1111.1 | 0.996908 | 32.0 | 93.01% | 1111.1 | 0.996908 |
| 4 | 4.0 | 93.01% | 1111.1 | 0.996908 | 40.0 | 93.01% | 1111.1 | 0.996908 |
| 5 | 5.0 | 93.01% | 1111.1 | 0.996908 | 48.0 | 93.01% | 1111.1 | 0.996908 |
| 6 | 6.0 | 93.01% | 1111.1 | 0.996908 | 56.0 | 93.01% | 1111.1 | 0.996908 |
| 7 | 7.0 | 93.01% | 1111.1 | 0.996908 | 64.0 | 93.01% | 1111.1 | 0.996908 |
| 8 | 8.0 | 93.01% | 1111.1 | 0.996908 | 72.0 | 93.01% | 1111.1 | 0.996908 |
| 9 | 9.0 | 93.01% | 1111.1 | 0.996908 | 80.0 | 93.01% | 1111.1 | 0.996908 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 98.76% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 5 | suspicious | group_primary_with_escape | 98.76% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 9 | hostile | group_primary_with_escape | 98.76% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 9 | suspicious | group_primary_with_escape | 98.76% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
