# Azoth Filetype — `makefile`

Specialist classifier for `makefile`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `makefile` test-bucket rows (n=2274, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.5072 | — | - |
| PR AUC | 0.0029 | — | - |
| F1 | 0.0104 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `makefile` is `general_only`.
Routes consulted (max-of-thresholds): `general`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.5072**, PR AUC = **0.0029**, F1 = **0.0104**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 15557 (62 malware, 15495 benign).
- Internal training-time benchmark rows: 2275 (4 malware, 2271 benign).
- Internal training-time benchmark AUC/AP/F1: 0.8778 / 0.3366 / 0.4000.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 25.00% | 0.00 | 0.997118 | 8.0 | 25.00% | 440.33 | 0.987454 |
| 1 | 1.0 | 25.00% | 440.33 | 0.987454 | 16.0 | 25.00% | 440.33 | 0.987454 |
| 2 | 2.0 | 25.00% | 440.33 | 0.987454 | 24.0 | 25.00% | 440.33 | 0.987454 |
| 3 | 3.0 | 25.00% | 440.33 | 0.987454 | 32.0 | 25.00% | 440.33 | 0.987454 |
| 4 | 4.0 | 25.00% | 440.33 | 0.987454 | 40.0 | 25.00% | 440.33 | 0.987454 |
| 5 | 5.0 | 25.00% | 440.33 | 0.987454 | 48.0 | 25.00% | 440.33 | 0.987454 |
| 6 | 6.0 | 25.00% | 440.33 | 0.987454 | 56.0 | 25.00% | 440.33 | 0.987454 |
| 7 | 7.0 | 25.00% | 440.33 | 0.987454 | 64.0 | 25.00% | 440.33 | 0.987454 |
| 8 | 8.0 | 25.00% | 440.33 | 0.987454 | 72.0 | 25.00% | 440.33 | 0.987454 |
| 9 | 9.0 | 25.00% | 440.33 | 0.987454 | 80.0 | 25.00% | 440.33 | 0.987454 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 5 | suspicious | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 9 | hostile | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 9 | suspicious | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
