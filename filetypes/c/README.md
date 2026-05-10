# Azoth Filetype — `c`

Specialist classifier for `c`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `c` test-bucket rows (n=53001, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.6626 | — | - |
| PR AUC | 0.3166 | — | - |
| F1 | 0.5156 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `c` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.6626**, PR AUC = **0.3166**, F1 = **0.5156**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 369376 (5840 malware, 363536 benign).
- Internal training-time benchmark rows: 53020 (820 malware, 52200 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9413 / 0.5243 / 0.5892.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | - | - | - |
| 1 | 1.0 | - | - | - | 16.0 | - | - | - |
| 2 | 2.0 | - | - | - | 24.0 | - | - | - |
| 3 | 3.0 | - | - | - | 32.0 | - | - | - |
| 4 | 4.0 | - | - | - | 40.0 | - | - | - |
| 5 | 5.0 | - | - | - | 48.0 | - | - | - |
| 6 | 6.0 | - | - | - | 56.0 | - | - | - |
| 7 | 7.0 | - | - | - | 64.0 | - | - | - |
| 8 | 8.0 | - | - | - | 72.0 | - | - | - |
| 9 | 9.0 | - | - | - | 80.0 | - | - | - |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 37.28% | 19 | 45.71 | `{"filegroups/source": 0.9536082148551941, "general": 0.9373036026954651}` |
| 9 | hostile | group_primary_with_escape | 28.85% | 3 | 7.22 | `{"filegroups/source": 0.9845402240753174, "general": 0.9909083247184753}` |
| 9 | suspicious | group_primary_with_escape | 37.76% | 33 | 79.39 | `{"filegroups/source": 0.9020361304283142, "general": 0.9866744875907898}` |
