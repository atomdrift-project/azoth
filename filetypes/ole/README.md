# Azoth Filetype — `ole`

Specialist classifier for `ole`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `ole` test-bucket rows (n=680, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9999 | — | - |
| PR AUC | 0.9973 | — | - |
| F1 | 0.9804 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `ole` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9999**, PR AUC = **0.9973**, F1 = **0.9804**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (49112 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=50, device=cpu.
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
- Training rows: 4918 (229 malware, 4689 benign).
- Internal training-time benchmark rows: 688 (30 malware, 658 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9999 / 0.9979 / 0.9831.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.67% | 0.00 | 0.831924 | 8.0 | 96.67% | 1519.8 | 0.775652 |
| 1 | 1.0 | 96.67% | 1519.8 | 0.775652 | 16.0 | 96.67% | 1519.8 | 0.775652 |
| 2 | 2.0 | 96.67% | 1519.8 | 0.775652 | 24.0 | 96.67% | 1519.8 | 0.775652 |
| 3 | 3.0 | 96.67% | 1519.8 | 0.775652 | 32.0 | 96.67% | 1519.8 | 0.775652 |
| 4 | 4.0 | 96.67% | 1519.8 | 0.775652 | 40.0 | 96.67% | 1519.8 | 0.775652 |
| 5 | 5.0 | 96.67% | 1519.8 | 0.775652 | 48.0 | 96.67% | 1519.8 | 0.775652 |
| 6 | 6.0 | 96.67% | 1519.8 | 0.775652 | 56.0 | 96.67% | 1519.8 | 0.775652 |
| 7 | 7.0 | 96.67% | 1519.8 | 0.775652 | 64.0 | 96.67% | 1519.8 | 0.775652 |
| 8 | 8.0 | 96.67% | 1519.8 | 0.775652 | 72.0 | 96.67% | 1519.8 | 0.775652 |
| 9 | 9.0 | 96.67% | 1519.8 | 0.775652 | 80.0 | 96.67% | 1519.8 | 0.775652 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 82.77% | 1 | 188.61 | `{"filetypes/ole": 0.9965583682060242, "general": 0.9733341336250305}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 82.77% | 1 | 188.61 | `{"filetypes/ole": 0.9965583682060242, "general": 0.9733341336250305}` |
