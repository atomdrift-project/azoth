# Azoth Filetype — `data`

Specialist classifier for `data`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `data` test-bucket rows (n=1151, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9668 | — | - |
| PR AUC | 0.8860 | — | - |
| F1 | 0.8974 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `data` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filetypes/data`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9668**, PR AUC = **0.8860**, F1 = **0.8974**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (49112 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=64, max_depth=12, min_child_samples=160, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.5, reg_lambda=4.0, early_stop=50, device=cpu.
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
- Training rows: 7885 (303 malware, 7582 benign).
- Internal training-time benchmark rows: 1175 (52 malware, 1123 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9997 / 0.9925 / 0.9720.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.62% | 0.00 | 0.986481 | 8.0 | 84.62% | 890.47 | 0.985045 |
| 1 | 1.0 | 84.62% | 890.47 | 0.985045 | 16.0 | 84.62% | 890.47 | 0.985045 |
| 2 | 2.0 | 84.62% | 890.47 | 0.985045 | 24.0 | 84.62% | 890.47 | 0.985045 |
| 3 | 3.0 | 84.62% | 890.47 | 0.985045 | 32.0 | 84.62% | 890.47 | 0.985045 |
| 4 | 4.0 | 84.62% | 890.47 | 0.985045 | 40.0 | 84.62% | 890.47 | 0.985045 |
| 5 | 5.0 | 84.62% | 890.47 | 0.985045 | 48.0 | 84.62% | 890.47 | 0.985045 |
| 6 | 6.0 | 84.62% | 890.47 | 0.985045 | 56.0 | 84.62% | 890.47 | 0.985045 |
| 7 | 7.0 | 84.62% | 890.47 | 0.985045 | 64.0 | 84.62% | 890.47 | 0.985045 |
| 8 | 8.0 | 84.62% | 890.47 | 0.985045 | 72.0 | 84.62% | 890.47 | 0.985045 |
| 9 | 9.0 | 84.62% | 890.47 | 0.985045 | 80.0 | 84.62% | 890.47 | 0.985045 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 86.96% | 0 | 0.00 | `{"filetypes/data": 0.5138987302780151, "general": 0.9008088707923889}` |
| 5 | suspicious | or_general_primary | 86.96% | 0 | 0.00 | `{"filetypes/data": 0.5138987302780151, "general": 0.9008088707923889}` |
| 9 | hostile | or_general_primary | 86.96% | 0 | 0.00 | `{"filetypes/data": 0.5138987302780151, "general": 0.9008088707923889}` |
| 9 | suspicious | or_general_primary | 86.96% | 0 | 0.00 | `{"filetypes/data": 0.5138987302780151, "general": 0.9008088707923889}` |
