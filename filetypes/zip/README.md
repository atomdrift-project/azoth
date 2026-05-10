# Azoth Filetype — `zip`

Specialist classifier for `zip`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `zip` test-bucket rows (n=4053, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9698 | — | - |
| PR AUC | 0.9974 | — | - |
| F1 | 0.9714 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `zip` is `specialist_primary_with_escape`.
Routes consulted (max-of-thresholds): `general`, `filegroups/archive`, `filetypes/zip`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9797**, PR AUC = **0.9980**, F1 = **0.9772**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 33762 (28881 malware, 4881 benign).
- Internal training-time benchmark rows: 4595 (3926 malware, 669 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9984 / 0.9997 / 0.9950.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 77.59% | 0.00 | 0.998992 | 8.0 | 90.98% | 1494.8 | 0.985054 |
| 1 | 1.0 | 90.98% | 1494.8 | 0.985054 | 16.0 | 90.98% | 1494.8 | 0.985054 |
| 2 | 2.0 | 90.98% | 1494.8 | 0.985054 | 24.0 | 90.98% | 1494.8 | 0.985054 |
| 3 | 3.0 | 90.98% | 1494.8 | 0.985054 | 32.0 | 90.98% | 1494.8 | 0.985054 |
| 4 | 4.0 | 90.98% | 1494.8 | 0.985054 | 40.0 | 90.98% | 1494.8 | 0.985054 |
| 5 | 5.0 | 90.98% | 1494.8 | 0.985054 | 48.0 | 90.98% | 1494.8 | 0.985054 |
| 6 | 6.0 | 90.98% | 1494.8 | 0.985054 | 56.0 | 90.98% | 1494.8 | 0.985054 |
| 7 | 7.0 | 90.98% | 1494.8 | 0.985054 | 64.0 | 90.98% | 1494.8 | 0.985054 |
| 8 | 8.0 | 90.98% | 1494.8 | 0.985054 | 72.0 | 90.98% | 1494.8 | 0.985054 |
| 9 | 9.0 | 90.98% | 1494.8 | 0.985054 | 80.0 | 90.98% | 1494.8 | 0.985054 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 85.32% | 1 | 352.73 | `{"filegroups/archive": 0.9988322257995605, "filetypes/zip": 0.9926757216453552, "general": 0.9974381327629089}` |
| 5 | suspicious | specialist_primary_with_escape | 85.32% | 1 | 352.73 | `{"filegroups/archive": 0.9988322257995605, "filetypes/zip": 0.9926757216453552, "general": 0.9974381327629089}` |
| 9 | hostile | specialist_primary_with_escape | 85.32% | 1 | 352.73 | `{"filegroups/archive": 0.9988322257995605, "filetypes/zip": 0.9926757216453552, "general": 0.9974381327629089}` |
| 9 | suspicious | specialist_primary_with_escape | 85.32% | 1 | 352.73 | `{"filegroups/archive": 0.9988322257995605, "filetypes/zip": 0.9926757216453552, "general": 0.9974381327629089}` |
