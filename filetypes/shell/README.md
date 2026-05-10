# Azoth Filetype — `shell`

Specialist classifier for `shell`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `shell` test-bucket rows (n=4723, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9795 | — | - |
| PR AUC | 0.9390 | — | - |
| F1 | 0.9274 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `shell` is `group_primary_with_escape`.
Routes consulted (max-of-thresholds): `general`, `filegroups/scripts`, `filetypes/shell`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9859**, PR AUC = **0.9452**, F1 = **0.9228**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 33221 (1491 malware, 31730 benign).
- Internal training-time benchmark rows: 4802 (306 malware, 4496 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9911 / 0.9657 / 0.9465.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.64% | 0.00 | 0.992294 | 8.0 | 88.56% | 222.42 | 0.970824 |
| 1 | 1.0 | 88.56% | 222.42 | 0.970824 | 16.0 | 88.56% | 222.42 | 0.970824 |
| 2 | 2.0 | 88.56% | 222.42 | 0.970824 | 24.0 | 88.56% | 222.42 | 0.970824 |
| 3 | 3.0 | 88.56% | 222.42 | 0.970824 | 32.0 | 88.56% | 222.42 | 0.970824 |
| 4 | 4.0 | 88.56% | 222.42 | 0.970824 | 40.0 | 88.56% | 222.42 | 0.970824 |
| 5 | 5.0 | 88.56% | 222.42 | 0.970824 | 48.0 | 88.56% | 222.42 | 0.970824 |
| 6 | 6.0 | 88.56% | 222.42 | 0.970824 | 56.0 | 88.56% | 222.42 | 0.970824 |
| 7 | 7.0 | 88.56% | 222.42 | 0.970824 | 64.0 | 88.56% | 222.42 | 0.970824 |
| 8 | 8.0 | 88.56% | 222.42 | 0.970824 | 72.0 | 88.56% | 222.42 | 0.970824 |
| 9 | 9.0 | 88.56% | 222.42 | 0.970824 | 80.0 | 88.56% | 222.42 | 0.970824 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 71.01% | 1 | 28.11 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9583697319030762, "general": 0.9515489339828491}` |
| 5 | suspicious | group_primary_with_escape | 71.01% | 1 | 28.11 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9583697319030762, "general": 0.9515489339828491}` |
| 9 | hostile | group_primary_with_escape | 71.01% | 1 | 28.11 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9583697319030762, "general": 0.9515489339828491}` |
| 9 | suspicious | specialist_primary_with_escape | 73.12% | 2 | 56.22 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9342930316925049, "general": 0.9515489339828491}` |
