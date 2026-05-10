# Azoth Filetype — `rust`

Specialist classifier for `rust`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `rust` test-bucket rows (n=7927, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.7134 | — | - |
| PR AUC | 0.2434 | — | - |
| F1 | 0.3529 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `rust` is `group_only`.
Routes consulted (max-of-thresholds): `filegroups/source`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.7134**, PR AUC = **0.2434**, F1 = **0.3529**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 55681 (45 malware, 55636 benign).
- Internal training-time benchmark rows: 7928 (7 malware, 7921 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9931 / 0.1496 / 0.2500.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | 14.29% | 126.25 | 1.000000 |
| 1 | 1.0 | 14.29% | 126.25 | 1.000000 | 16.0 | 14.29% | 126.25 | 1.000000 |
| 2 | 2.0 | 14.29% | 126.25 | 1.000000 | 24.0 | 14.29% | 126.25 | 1.000000 |
| 3 | 3.0 | 14.29% | 126.25 | 1.000000 | 32.0 | 14.29% | 126.25 | 1.000000 |
| 4 | 4.0 | 14.29% | 126.25 | 1.000000 | 40.0 | 14.29% | 126.25 | 1.000000 |
| 5 | 5.0 | 14.29% | 126.25 | 1.000000 | 48.0 | 14.29% | 126.25 | 1.000000 |
| 6 | 6.0 | 14.29% | 126.25 | 1.000000 | 56.0 | 14.29% | 126.25 | 1.000000 |
| 7 | 7.0 | 14.29% | 126.25 | 1.000000 | 64.0 | 14.29% | 126.25 | 1.000000 |
| 8 | 8.0 | 14.29% | 126.25 | 1.000000 | 72.0 | 14.29% | 126.25 | 1.000000 |
| 9 | 9.0 | 14.29% | 126.25 | 1.000000 | 80.0 | 14.29% | 126.25 | 1.000000 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_only | 26.92% | 0 | 0.00 | `{"filegroups/source": 0.5780653357505798}` |
| 5 | suspicious | group_only | 26.92% | 0 | 0.00 | `{"filegroups/source": 0.5780653357505798}` |
| 9 | hostile | group_only | 26.92% | 0 | 0.00 | `{"filegroups/source": 0.5780653357505798}` |
| 9 | suspicious | group_only | 26.92% | 0 | 0.00 | `{"filegroups/source": 0.5780653357505798}` |
