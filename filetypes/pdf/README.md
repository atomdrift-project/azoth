# Azoth Filetype — `pdf`

Specialist classifier for `pdf`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `pdf` test-bucket rows (n=286, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.4919 | 0.9912 | -0.4993 |
| PR AUC | 0.0669 | 0.9933 | -0.9264 |
| F1 | 0.2222 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `pdf` is `general_only`.
Routes consulted (max-of-thresholds): `general`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.6237**, PR AUC = **0.0581**, F1 = **0.1667**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 1915 (74 malware, 1841 benign).
- Internal training-time benchmark rows: 287 (10 malware, 277 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9733 / 0.6095 / 0.6667.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 20.00% | 0.00 | 0.994641 | 8.0 | 20.00% | 3610.1 | 0.989707 |
| 1 | 1.0 | 20.00% | 3610.1 | 0.989707 | 16.0 | 20.00% | 3610.1 | 0.989707 |
| 2 | 2.0 | 20.00% | 3610.1 | 0.989707 | 24.0 | 20.00% | 3610.1 | 0.989707 |
| 3 | 3.0 | 20.00% | 3610.1 | 0.989707 | 32.0 | 20.00% | 3610.1 | 0.989707 |
| 4 | 4.0 | 20.00% | 3610.1 | 0.989707 | 40.0 | 20.00% | 3610.1 | 0.989707 |
| 5 | 5.0 | 20.00% | 3610.1 | 0.989707 | 48.0 | 20.00% | 3610.1 | 0.989707 |
| 6 | 6.0 | 20.00% | 3610.1 | 0.989707 | 56.0 | 20.00% | 3610.1 | 0.989707 |
| 7 | 7.0 | 20.00% | 3610.1 | 0.989707 | 64.0 | 20.00% | 3610.1 | 0.989707 |
| 8 | 8.0 | 20.00% | 3610.1 | 0.989707 | 72.0 | 20.00% | 3610.1 | 0.989707 |
| 9 | 9.0 | 20.00% | 3610.1 | 0.989707 | 80.0 | 20.00% | 3610.1 | 0.989707 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | general_only | 9.76% | 0 | 0.00 | `{"general": 0.2338547259569168}` |
| 5 | suspicious | general_only | 9.76% | 0 | 0.00 | `{"general": 0.2338547259569168}` |
| 9 | hostile | general_only | 9.76% | 0 | 0.00 | `{"general": 0.2338547259569168}` |
| 9 | suspicious | general_only | 9.76% | 0 | 0.00 | `{"general": 0.2338547259569168}` |
