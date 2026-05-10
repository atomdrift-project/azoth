# Azoth Filetype — `csharp`

Specialist classifier for `csharp`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `csharp` test-bucket rows (n=4503, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9620 | — | - |
| PR AUC | 0.7290 | — | - |
| F1 | 0.7429 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `csharp` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9620**, PR AUC = **0.7290**, F1 = **0.7429**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 39487 (673 malware, 38814 benign).
- Internal training-time benchmark rows: 5776 (115 malware, 5661 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9980 / 0.9519 / 0.9132.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 75.65% | 0.00 | 0.984100 | 8.0 | 82.61% | 176.65 | 0.895422 |
| 1 | 1.0 | 82.61% | 176.65 | 0.895422 | 16.0 | 82.61% | 176.65 | 0.895422 |
| 2 | 2.0 | 82.61% | 176.65 | 0.895422 | 24.0 | 82.61% | 176.65 | 0.895422 |
| 3 | 3.0 | 82.61% | 176.65 | 0.895422 | 32.0 | 82.61% | 176.65 | 0.895422 |
| 4 | 4.0 | 82.61% | 176.65 | 0.895422 | 40.0 | 82.61% | 176.65 | 0.895422 |
| 5 | 5.0 | 82.61% | 176.65 | 0.895422 | 48.0 | 82.61% | 176.65 | 0.895422 |
| 6 | 6.0 | 82.61% | 176.65 | 0.895422 | 56.0 | 82.61% | 176.65 | 0.895422 |
| 7 | 7.0 | 82.61% | 176.65 | 0.895422 | 64.0 | 82.61% | 176.65 | 0.895422 |
| 8 | 8.0 | 82.61% | 176.65 | 0.895422 | 72.0 | 82.61% | 176.65 | 0.895422 |
| 9 | 9.0 | 82.61% | 176.65 | 0.895422 | 80.0 | 82.61% | 176.65 | 0.895422 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 55.64% | 1 | 29.00 | `{"filegroups/source": 0.9630320072174072, "filetypes/csharp": 0.995499849319458, "general": 0.9332911372184753}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 56.11% | 2 | 57.99 | `{"filegroups/source": 0.9739324450492859, "filetypes/csharp": 0.992536723613739}` |
