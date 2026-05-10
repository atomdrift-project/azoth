# Azoth Filetype — `png`

Specialist classifier for `png`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `png` test-bucket rows (n=8105, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.5396 | — | - |
| PR AUC | 0.0661 | — | - |
| F1 | 0.1058 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `png` is `general_only`.
Routes consulted (max-of-thresholds): `general`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.5396**, PR AUC = **0.0661**, F1 = **0.1058**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (37595 features); feature-spec policy `general_shared`.
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
- Training rows: 55747 (3075 malware, 52672 benign).
- Internal training-time benchmark rows: 8126 (432 malware, 7694 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9247 / 0.5767 / 0.5330.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 0.69% | 0.00 | 0.304066 | 8.0 | 9.03% | 129.97 | 0.291697 |
| 1 | 1.0 | 9.03% | 129.97 | 0.291697 | 16.0 | 9.03% | 129.97 | 0.291697 |
| 2 | 2.0 | 9.03% | 129.97 | 0.291697 | 24.0 | 9.03% | 129.97 | 0.291697 |
| 3 | 3.0 | 9.03% | 129.97 | 0.291697 | 32.0 | 9.03% | 129.97 | 0.291697 |
| 4 | 4.0 | 9.03% | 129.97 | 0.291697 | 40.0 | 9.03% | 129.97 | 0.291697 |
| 5 | 5.0 | 9.03% | 129.97 | 0.291697 | 48.0 | 9.03% | 129.97 | 0.291697 |
| 6 | 6.0 | 9.03% | 129.97 | 0.291697 | 56.0 | 9.03% | 129.97 | 0.291697 |
| 7 | 7.0 | 9.03% | 129.97 | 0.291697 | 64.0 | 9.03% | 129.97 | 0.291697 |
| 8 | 8.0 | 9.03% | 129.97 | 0.291697 | 72.0 | 9.03% | 129.97 | 0.291697 |
| 9 | 9.0 | 9.03% | 129.97 | 0.291697 | 80.0 | 9.03% | 129.97 | 0.291697 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | general_only | 0.03% | 0 | 0.00 | `{"general": 0.8867951035499573}` |
| 5 | suspicious | or_general_primary | 1.23% | 1 | 16.60 | `{"filegroups/media": 0.9699244499206543, "general": 0.8867951035499573}` |
| 9 | hostile | general_only | 0.03% | 0 | 0.00 | `{"general": 0.8867951035499573}` |
| 9 | suspicious | or_general_primary | 1.23% | 1 | 16.60 | `{"filegroups/media": 0.9699244499206543, "general": 0.8867951035499573}` |
