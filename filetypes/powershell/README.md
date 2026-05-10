# Azoth Filetype — `powershell`

Specialist classifier for `powershell`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `powershell` test-bucket rows (n=159, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9932 | — | - |
| PR AUC | 0.9811 | — | - |
| F1 | 0.9495 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `powershell` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9932**, PR AUC = **0.9811**, F1 = **0.9495**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 1499 (385 malware, 1114 benign).
- Internal training-time benchmark rows: 233 (59 malware, 174 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9981 / 0.9947 / 0.9744.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 83.05% | 0.00 | 0.991387 | 8.0 | 96.61% | 5747.1 | 0.890786 |
| 1 | 1.0 | 96.61% | 5747.1 | 0.890786 | 16.0 | 96.61% | 5747.1 | 0.890786 |
| 2 | 2.0 | 96.61% | 5747.1 | 0.890786 | 24.0 | 96.61% | 5747.1 | 0.890786 |
| 3 | 3.0 | 96.61% | 5747.1 | 0.890786 | 32.0 | 96.61% | 5747.1 | 0.890786 |
| 4 | 4.0 | 96.61% | 5747.1 | 0.890786 | 40.0 | 96.61% | 5747.1 | 0.890786 |
| 5 | 5.0 | 96.61% | 5747.1 | 0.890786 | 48.0 | 96.61% | 5747.1 | 0.890786 |
| 6 | 6.0 | 96.61% | 5747.1 | 0.890786 | 56.0 | 96.61% | 5747.1 | 0.890786 |
| 7 | 7.0 | 96.61% | 5747.1 | 0.890786 | 64.0 | 96.61% | 5747.1 | 0.890786 |
| 8 | 8.0 | 96.61% | 5747.1 | 0.890786 | 72.0 | 96.61% | 5747.1 | 0.890786 |
| 9 | 9.0 | 96.61% | 5747.1 | 0.890786 | 80.0 | 96.61% | 5747.1 | 0.890786 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 78.64% | 1 | 1146.8 | `{"filegroups/scripts": 0.9928010106086731, "filetypes/powershell": 0.9705975651741028}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 78.64% | 1 | 1146.8 | `{"filegroups/scripts": 0.9928010106086731, "filetypes/powershell": 0.9705975651741028}` |
