# Azoth Filetype — `javascript`

Specialist classifier for `javascript`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `javascript` test-bucket rows (n=49128, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9990 | — | - |
| PR AUC | 0.9959 | — | - |
| F1 | 0.9707 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `javascript` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filegroups/scripts`, `filetypes/javascript`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9990**, PR AUC = **0.9959**, F1 = **0.9707**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 377820 (50138 malware, 327682 benign).
- Internal training-time benchmark rows: 54591 (7288 malware, 47303 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9999 / 0.9996 / 0.9936.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.98% | 0.00 | 0.995460 | 8.0 | 94.99% | 21.14 | 0.995389 |
| 1 | 1.0 | 94.99% | 21.14 | 0.995389 | 16.0 | 94.99% | 21.14 | 0.995389 |
| 2 | 2.0 | 94.99% | 21.14 | 0.995389 | 24.0 | 94.99% | 21.14 | 0.995389 |
| 3 | 3.0 | 94.99% | 21.14 | 0.995389 | 32.0 | 94.99% | 21.14 | 0.995389 |
| 4 | 4.0 | 94.99% | 21.14 | 0.995389 | 40.0 | 94.99% | 21.14 | 0.995389 |
| 5 | 5.0 | 94.99% | 21.14 | 0.995389 | 48.0 | 95.64% | 42.28 | 0.993515 |
| 6 | 6.0 | 94.99% | 21.14 | 0.995389 | 56.0 | 95.64% | 42.28 | 0.993515 |
| 7 | 7.0 | 94.99% | 21.14 | 0.995389 | 64.0 | 96.21% | 63.42 | 0.989387 |
| 8 | 8.0 | 94.99% | 21.14 | 0.995389 | 72.0 | 96.21% | 63.42 | 0.989387 |
| 9 | 9.0 | 94.99% | 21.14 | 0.995389 | 80.0 | 96.21% | 63.42 | 0.989387 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 90.04% | 1 | 3.00 | `{"filetypes/javascript": 0.9970327615737915, "general": 0.9862461090087891}` |
| 5 | suspicious | specialist_primary_with_escape | 91.70% | 15 | 45.03 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9896018505096436, "general": 0.9840287566184998}` |
| 9 | hostile | or_general_primary | 90.13% | 2 | 6.00 | `{"filetypes/javascript": 0.9970327615737915, "general": 0.9840287566184998}` |
| 9 | suspicious | specialist_primary_with_escape | 92.19% | 26 | 78.05 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9832349419593811, "general": 0.9824105501174927}` |
