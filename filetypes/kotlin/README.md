# Azoth Filetype — `kotlin`

Specialist classifier for `kotlin`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `kotlin` test-bucket rows (n=3668, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9504 | — | - |
| PR AUC | 0.8379 | — | - |
| F1 | 0.8657 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `kotlin` is `group_primary_with_escape`.
Routes consulted (max-of-thresholds): `general`, `filegroups/source`, `filetypes/kotlin`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9504**, PR AUC = **0.8379**, F1 = **0.8657**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 31329 (786 malware, 30543 benign).
- Internal training-time benchmark rows: 4486 (121 malware, 4365 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9990 / 0.9825 / 0.9664.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 92.56% | 0.00 | 0.959495 | 8.0 | 94.21% | 229.10 | 0.860931 |
| 1 | 1.0 | 94.21% | 229.10 | 0.860931 | 16.0 | 94.21% | 229.10 | 0.860931 |
| 2 | 2.0 | 94.21% | 229.10 | 0.860931 | 24.0 | 94.21% | 229.10 | 0.860931 |
| 3 | 3.0 | 94.21% | 229.10 | 0.860931 | 32.0 | 94.21% | 229.10 | 0.860931 |
| 4 | 4.0 | 94.21% | 229.10 | 0.860931 | 40.0 | 94.21% | 229.10 | 0.860931 |
| 5 | 5.0 | 94.21% | 229.10 | 0.860931 | 48.0 | 94.21% | 229.10 | 0.860931 |
| 6 | 6.0 | 94.21% | 229.10 | 0.860931 | 56.0 | 94.21% | 229.10 | 0.860931 |
| 7 | 7.0 | 94.21% | 229.10 | 0.860931 | 64.0 | 94.21% | 229.10 | 0.860931 |
| 8 | 8.0 | 94.21% | 229.10 | 0.860931 | 72.0 | 94.21% | 229.10 | 0.860931 |
| 9 | 9.0 | 94.21% | 229.10 | 0.860931 | 80.0 | 94.21% | 229.10 | 0.860931 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 5 | suspicious | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 9 | hostile | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 9 | suspicious | group_primary_with_escape | 63.68% | 2 | 69.28 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.015584520995616913, "general": 0.8890419602394104}` |
