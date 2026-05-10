# Azoth Filetype — `ruby`

Specialist classifier for `ruby`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `ruby` test-bucket rows (n=1466, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9998 | — | - |
| PR AUC | 0.9617 | — | - |
| F1 | 0.9333 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `ruby` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9998**, PR AUC = **0.9617**, F1 = **0.9333**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 20365 (63 malware, 20302 benign).
- Internal training-time benchmark rows: 2813 (7 malware, 2806 benign).
- Internal training-time benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.975179 | 8.0 | 100.00% | 356.38 | 0.662422 |
| 1 | 1.0 | 100.00% | 356.38 | 0.662422 | 16.0 | 100.00% | 356.38 | 0.662422 |
| 2 | 2.0 | 100.00% | 356.38 | 0.662422 | 24.0 | 100.00% | 356.38 | 0.662422 |
| 3 | 3.0 | 100.00% | 356.38 | 0.662422 | 32.0 | 100.00% | 356.38 | 0.662422 |
| 4 | 4.0 | 100.00% | 356.38 | 0.662422 | 40.0 | 100.00% | 356.38 | 0.662422 |
| 5 | 5.0 | 100.00% | 356.38 | 0.662422 | 48.0 | 100.00% | 356.38 | 0.662422 |
| 6 | 6.0 | 100.00% | 356.38 | 0.662422 | 56.0 | 100.00% | 356.38 | 0.662422 |
| 7 | 7.0 | 100.00% | 356.38 | 0.662422 | 64.0 | 100.00% | 356.38 | 0.662422 |
| 8 | 8.0 | 100.00% | 356.38 | 0.662422 | 72.0 | 100.00% | 356.38 | 0.662422 |
| 9 | 9.0 | 100.00% | 356.38 | 0.662422 | 80.0 | 100.00% | 356.38 | 0.662422 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 95.65% | 1 | 83.72 | `{"filegroups/scripts": 0.9614102840423584, "filetypes/ruby": 0.9984004497528076}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 95.65% | 1 | 83.72 | `{"filegroups/scripts": 0.9614102840423584, "filetypes/ruby": 0.9984004497528076}` |
