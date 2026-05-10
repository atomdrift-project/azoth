# Azoth Filetype — `tar`

Specialist classifier for `tar`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `tar` test-bucket rows (n=151, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9750 | — | - |
| PR AUC | 0.9921 | — | - |
| F1 | 0.9770 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `tar` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9750**, PR AUC = **0.9921**, F1 = **0.9770**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 1243 (931 malware, 312 benign).
- Internal training-time benchmark rows: 153 (111 malware, 42 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9760 / 0.9923 / 0.9817.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.40% | 0.00 | 0.268038 | 8.0 | 96.40% | 23809.5 | 0.211336 |
| 1 | 1.0 | 96.40% | 23809.5 | 0.211336 | 16.0 | 96.40% | 23809.5 | 0.211336 |
| 2 | 2.0 | 96.40% | 23809.5 | 0.211336 | 24.0 | 96.40% | 23809.5 | 0.211336 |
| 3 | 3.0 | 96.40% | 23809.5 | 0.211336 | 32.0 | 96.40% | 23809.5 | 0.211336 |
| 4 | 4.0 | 96.40% | 23809.5 | 0.211336 | 40.0 | 96.40% | 23809.5 | 0.211336 |
| 5 | 5.0 | 96.40% | 23809.5 | 0.211336 | 48.0 | 96.40% | 23809.5 | 0.211336 |
| 6 | 6.0 | 96.40% | 23809.5 | 0.211336 | 56.0 | 96.40% | 23809.5 | 0.211336 |
| 7 | 7.0 | 96.40% | 23809.5 | 0.211336 | 64.0 | 96.40% | 23809.5 | 0.211336 |
| 8 | 8.0 | 96.40% | 23809.5 | 0.211336 | 72.0 | 96.40% | 23809.5 | 0.211336 |
| 9 | 9.0 | 96.40% | 23809.5 | 0.211336 | 80.0 | 96.40% | 23809.5 | 0.211336 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 98.56% | 1 | 2958.6 | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5751407146453857}` |
| 9 | hostile | group_primary_with_escape | 98.56% | 1 | 2958.6 | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5751407146453857}` |
| 9 | suspicious | group_primary_with_escape | 98.56% | 1 | 2958.6 | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5751407146453857}` |
