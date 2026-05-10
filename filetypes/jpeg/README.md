# Azoth Filetype — `jpeg`

Specialist classifier for `jpeg`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `jpeg` test-bucket rows (n=833, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.5483 | — | - |
| PR AUC | 0.1245 | — | - |
| F1 | 0.1920 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `jpeg` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filegroups/media`, `filetypes/jpeg`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.6510**, PR AUC = **0.1143**, F1 = **0.2295**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 7071 (618 malware, 6453 benign).
- Internal training-time benchmark rows: 969 (90 malware, 879 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9937 / 0.9446 / 0.8649.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 44.44% | 0.00 | 0.992693 | 8.0 | 63.33% | 1137.7 | 0.984403 |
| 1 | 1.0 | 63.33% | 1137.7 | 0.984403 | 16.0 | 63.33% | 1137.7 | 0.984403 |
| 2 | 2.0 | 63.33% | 1137.7 | 0.984403 | 24.0 | 63.33% | 1137.7 | 0.984403 |
| 3 | 3.0 | 63.33% | 1137.7 | 0.984403 | 32.0 | 63.33% | 1137.7 | 0.984403 |
| 4 | 4.0 | 63.33% | 1137.7 | 0.984403 | 40.0 | 63.33% | 1137.7 | 0.984403 |
| 5 | 5.0 | 63.33% | 1137.7 | 0.984403 | 48.0 | 63.33% | 1137.7 | 0.984403 |
| 6 | 6.0 | 63.33% | 1137.7 | 0.984403 | 56.0 | 63.33% | 1137.7 | 0.984403 |
| 7 | 7.0 | 63.33% | 1137.7 | 0.984403 | 64.0 | 63.33% | 1137.7 | 0.984403 |
| 8 | 8.0 | 63.33% | 1137.7 | 0.984403 | 72.0 | 63.33% | 1137.7 | 0.984403 |
| 9 | 9.0 | 63.33% | 1137.7 | 0.984403 | 80.0 | 63.33% | 1137.7 | 0.984403 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 5 | suspicious | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 9 | hostile | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 9 | suspicious | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
