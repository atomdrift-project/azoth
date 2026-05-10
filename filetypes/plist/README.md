# Azoth Filetype — `plist`

Specialist classifier for `plist`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `plist` test-bucket rows (n=1157, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.7469 | — | - |
| PR AUC | 0.1744 | — | - |
| F1 | 0.2500 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `plist` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.7469**, PR AUC = **0.1744**, F1 = **0.2500**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 8187 (416 malware, 7771 benign).
- Internal training-time benchmark rows: 1159 (58 malware, 1101 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9908 / 0.9114 / 0.8522.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 24.14% | 0.00 | 0.993849 | 8.0 | 63.79% | 908.27 | 0.952783 |
| 1 | 1.0 | 63.79% | 908.27 | 0.952783 | 16.0 | 63.79% | 908.27 | 0.952783 |
| 2 | 2.0 | 63.79% | 908.27 | 0.952783 | 24.0 | 63.79% | 908.27 | 0.952783 |
| 3 | 3.0 | 63.79% | 908.27 | 0.952783 | 32.0 | 63.79% | 908.27 | 0.952783 |
| 4 | 4.0 | 63.79% | 908.27 | 0.952783 | 40.0 | 63.79% | 908.27 | 0.952783 |
| 5 | 5.0 | 63.79% | 908.27 | 0.952783 | 48.0 | 63.79% | 908.27 | 0.952783 |
| 6 | 6.0 | 63.79% | 908.27 | 0.952783 | 56.0 | 63.79% | 908.27 | 0.952783 |
| 7 | 7.0 | 63.79% | 908.27 | 0.952783 | 64.0 | 63.79% | 908.27 | 0.952783 |
| 8 | 8.0 | 63.79% | 908.27 | 0.952783 | 72.0 | 63.79% | 908.27 | 0.952783 |
| 9 | 9.0 | 63.79% | 908.27 | 0.952783 | 80.0 | 63.79% | 908.27 | 0.952783 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 8.76% | 1 | 112.83 | `{"filegroups/config": 0.13222765922546387, "filetypes/plist": 0.6069956421852112, "general": 0.16379986703395844}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 8.76% | 1 | 112.83 | `{"filegroups/config": 0.13222765922546387, "filetypes/plist": 0.6069956421852112, "general": 0.16379986703395844}` |
