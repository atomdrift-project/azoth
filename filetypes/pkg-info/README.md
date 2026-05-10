# Azoth Filetype — `pkg-info`

Specialist classifier for `pkg-info`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `pkg-info` test-bucket rows (n=523, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9991 | — | - |
| PR AUC | 0.9998 | — | - |
| F1 | 0.9977 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `pkg-info` is `filetype_only`.
Routes consulted (max-of-thresholds): `filetypes/pkg-info`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9991**, PR AUC = **0.9998**, F1 = **0.9977**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 3947 (3240 malware, 707 benign).
- Internal training-time benchmark rows: 535 (441 malware, 94 benign).
- Internal training-time benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.608399 | 8.0 | 100.00% | 10638.3 | 0.076727 |
| 1 | 1.0 | 100.00% | 10638.3 | 0.076727 | 16.0 | 100.00% | 10638.3 | 0.076727 |
| 2 | 2.0 | 100.00% | 10638.3 | 0.076727 | 24.0 | 100.00% | 10638.3 | 0.076727 |
| 3 | 3.0 | 100.00% | 10638.3 | 0.076727 | 32.0 | 100.00% | 10638.3 | 0.076727 |
| 4 | 4.0 | 100.00% | 10638.3 | 0.076727 | 40.0 | 100.00% | 10638.3 | 0.076727 |
| 5 | 5.0 | 100.00% | 10638.3 | 0.076727 | 48.0 | 100.00% | 10638.3 | 0.076727 |
| 6 | 6.0 | 100.00% | 10638.3 | 0.076727 | 56.0 | 100.00% | 10638.3 | 0.076727 |
| 7 | 7.0 | 100.00% | 10638.3 | 0.076727 | 64.0 | 100.00% | 10638.3 | 0.076727 |
| 8 | 8.0 | 100.00% | 10638.3 | 0.076727 | 72.0 | 100.00% | 10638.3 | 0.076727 |
| 9 | 9.0 | 100.00% | 10638.3 | 0.076727 | 80.0 | 100.00% | 10638.3 | 0.076727 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 5 | suspicious | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 9 | hostile | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 9 | suspicious | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
