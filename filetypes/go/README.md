# Azoth Filetype — `go`

Specialist classifier for `go`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `go` test-bucket rows (n=10669, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9161 | — | - |
| PR AUC | 0.5317 | — | - |
| F1 | 0.5663 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `go` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9161**, PR AUC = **0.5317**, F1 = **0.5663**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 78598 (987 malware, 77611 benign).
- Internal training-time benchmark rows: 11392 (161 malware, 11231 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9957 / 0.7641 / 0.6787.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 24.84% | 0.00 | 0.753477 | 8.0 | 29.19% | 89.04 | 0.745860 |
| 1 | 1.0 | 29.19% | 89.04 | 0.745860 | 16.0 | 29.19% | 89.04 | 0.745860 |
| 2 | 2.0 | 29.19% | 89.04 | 0.745860 | 24.0 | 29.19% | 89.04 | 0.745860 |
| 3 | 3.0 | 29.19% | 89.04 | 0.745860 | 32.0 | 29.19% | 89.04 | 0.745860 |
| 4 | 4.0 | 29.19% | 89.04 | 0.745860 | 40.0 | 29.19% | 89.04 | 0.745860 |
| 5 | 5.0 | 29.19% | 89.04 | 0.745860 | 48.0 | 29.19% | 89.04 | 0.745860 |
| 6 | 6.0 | 29.19% | 89.04 | 0.745860 | 56.0 | 29.19% | 89.04 | 0.745860 |
| 7 | 7.0 | 29.19% | 89.04 | 0.745860 | 64.0 | 29.19% | 89.04 | 0.745860 |
| 8 | 8.0 | 29.19% | 89.04 | 0.745860 | 72.0 | 29.19% | 89.04 | 0.745860 |
| 9 | 9.0 | 29.19% | 89.04 | 0.745860 | 80.0 | 29.19% | 89.04 | 0.745860 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 46.52% | 2 | 24.00 | `{"filegroups/source": 0.9554978609085083, "filetypes/go": 0.29252898693084717, "general": 0.9522479176521301}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 46.89% | 6 | 72.01 | `{"filegroups/source": 0.9001978635787964, "general": 0.957764208316803}` |
