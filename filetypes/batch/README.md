# Azoth Filetype — `batch`

Specialist classifier for `batch`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `batch` test-bucket rows (n=205, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9753 | — | - |
| PR AUC | 0.9512 | — | - |
| F1 | 0.9048 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `batch` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9753**, PR AUC = **0.9512**, F1 = **0.9048**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 2167 (333 malware, 1834 benign).
- Internal training-time benchmark rows: 290 (60 malware, 230 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9951 / 0.9836 / 0.9492.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 70.00% | 0.00 | 0.994239 | 8.0 | 88.33% | 4347.8 | 0.936692 |
| 1 | 1.0 | 88.33% | 4347.8 | 0.936692 | 16.0 | 88.33% | 4347.8 | 0.936692 |
| 2 | 2.0 | 88.33% | 4347.8 | 0.936692 | 24.0 | 88.33% | 4347.8 | 0.936692 |
| 3 | 3.0 | 88.33% | 4347.8 | 0.936692 | 32.0 | 88.33% | 4347.8 | 0.936692 |
| 4 | 4.0 | 88.33% | 4347.8 | 0.936692 | 40.0 | 88.33% | 4347.8 | 0.936692 |
| 5 | 5.0 | 88.33% | 4347.8 | 0.936692 | 48.0 | 88.33% | 4347.8 | 0.936692 |
| 6 | 6.0 | 88.33% | 4347.8 | 0.936692 | 56.0 | 88.33% | 4347.8 | 0.936692 |
| 7 | 7.0 | 88.33% | 4347.8 | 0.936692 | 64.0 | 88.33% | 4347.8 | 0.936692 |
| 8 | 8.0 | 88.33% | 4347.8 | 0.936692 | 72.0 | 88.33% | 4347.8 | 0.936692 |
| 9 | 9.0 | 88.33% | 4347.8 | 0.936692 | 80.0 | 88.33% | 4347.8 | 0.936692 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 79.22% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9955556988716125, "general": 0.8541349172592163}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 79.22% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9955556988716125, "general": 0.8541349172592163}` |
