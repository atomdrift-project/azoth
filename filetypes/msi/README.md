# Azoth Filetype — `msi`

Specialist classifier for `msi`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `msi` test-bucket rows (n=18, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 1.0000 | — | - |
| PR AUC | 1.0000 | — | - |
| F1 | 1.0000 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `msi` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **1.0000**, PR AUC = **1.0000**, F1 = **1.0000**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 336 (272 malware, 64 benign).
- Internal training-time benchmark rows: 36 (30 malware, 6 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9722 / 0.9950 / 0.9667.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 93.33% | 0.00 | 0.717560 | 8.0 | 96.67% | 166666.7 | 0.176595 |
| 1 | 1.0 | 96.67% | 166666.7 | 0.176595 | 16.0 | 96.67% | 166666.7 | 0.176595 |
| 2 | 2.0 | 96.67% | 166666.7 | 0.176595 | 24.0 | 96.67% | 166666.7 | 0.176595 |
| 3 | 3.0 | 96.67% | 166666.7 | 0.176595 | 32.0 | 96.67% | 166666.7 | 0.176595 |
| 4 | 4.0 | 96.67% | 166666.7 | 0.176595 | 40.0 | 96.67% | 166666.7 | 0.176595 |
| 5 | 5.0 | 96.67% | 166666.7 | 0.176595 | 48.0 | 96.67% | 166666.7 | 0.176595 |
| 6 | 6.0 | 96.67% | 166666.7 | 0.176595 | 56.0 | 96.67% | 166666.7 | 0.176595 |
| 7 | 7.0 | 96.67% | 166666.7 | 0.176595 | 64.0 | 96.67% | 166666.7 | 0.176595 |
| 8 | 8.0 | 96.67% | 166666.7 | 0.176595 | 72.0 | 96.67% | 166666.7 | 0.176595 |
| 9 | 9.0 | 96.67% | 166666.7 | 0.176595 | 80.0 | 96.67% | 166666.7 | 0.176595 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 56.02% | 1 | 32258.1 | `{"filegroups/archive": 0.9901114702224731, "filetypes/msi": 0.51080322265625}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 56.02% | 1 | 32258.1 | `{"filegroups/archive": 0.9901114702224731, "filetypes/msi": 0.51080322265625}` |
