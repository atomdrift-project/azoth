# Azoth Filetype — `tar.gz`

Specialist classifier for `tar.gz`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `tar.gz` test-bucket rows (n=2563, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9992 | — | - |
| PR AUC | 0.9993 | — | - |
| F1 | 0.9915 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `tar.gz` is `or_general_primary`.
Routes consulted (max-of-thresholds): `general`, `filegroups/archive`, `filetypes/tar.gz`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9990**, PR AUC = **0.9992**, F1 = **0.9917**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 28291 (17896 malware, 10395 benign).
- Internal training-time benchmark rows: 2966 (1478 malware, 1488 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9996 / 0.9996 / 0.9959.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 98.11% | 0.00 | 0.959872 | 8.0 | 98.85% | 672.04 | 0.868223 |
| 1 | 1.0 | 98.85% | 672.04 | 0.868223 | 16.0 | 98.85% | 672.04 | 0.868223 |
| 2 | 2.0 | 98.85% | 672.04 | 0.868223 | 24.0 | 98.85% | 672.04 | 0.868223 |
| 3 | 3.0 | 98.85% | 672.04 | 0.868223 | 32.0 | 98.85% | 672.04 | 0.868223 |
| 4 | 4.0 | 98.85% | 672.04 | 0.868223 | 40.0 | 98.85% | 672.04 | 0.868223 |
| 5 | 5.0 | 98.85% | 672.04 | 0.868223 | 48.0 | 98.85% | 672.04 | 0.868223 |
| 6 | 6.0 | 98.85% | 672.04 | 0.868223 | 56.0 | 98.85% | 672.04 | 0.868223 |
| 7 | 7.0 | 98.85% | 672.04 | 0.868223 | 64.0 | 98.85% | 672.04 | 0.868223 |
| 8 | 8.0 | 98.85% | 672.04 | 0.868223 | 72.0 | 98.85% | 672.04 | 0.868223 |
| 9 | 9.0 | 98.85% | 672.04 | 0.868223 | 80.0 | 98.85% | 672.04 | 0.868223 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 93.67% | 1 | 108.04 | `{"filegroups/archive": 0.9990630745887756, "filetypes/tar.gz": 0.9358141422271729, "general": 0.9858265519142151}` |
| 5 | suspicious | or_general_primary | 93.67% | 1 | 108.04 | `{"filegroups/archive": 0.9990630745887756, "filetypes/tar.gz": 0.9358141422271729, "general": 0.9858265519142151}` |
| 9 | hostile | or_general_primary | 93.67% | 1 | 108.04 | `{"filegroups/archive": 0.9990630745887756, "filetypes/tar.gz": 0.9358141422271729, "general": 0.9858265519142151}` |
| 9 | suspicious | or_general_primary | 93.67% | 1 | 108.04 | `{"filegroups/archive": 0.9990630745887756, "filetypes/tar.gz": 0.9358141422271729, "general": 0.9858265519142151}` |
