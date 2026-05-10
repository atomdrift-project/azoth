# Azoth Filetype — `jar`

Specialist classifier for `jar`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `jar` test-bucket rows (n=221, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9974 | — | - |
| PR AUC | 0.9963 | — | - |
| F1 | 0.9901 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `jar` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9974**, PR AUC = **0.9963**, F1 = **0.9901**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 1875 (498 malware, 1377 benign).
- Internal training-time benchmark rows: 288 (106 malware, 182 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9981 / 0.9965 / 0.9860.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 80.19% | 0.00 | 0.984308 | 8.0 | 91.51% | 5494.5 | 0.942888 |
| 1 | 1.0 | 91.51% | 5494.5 | 0.942888 | 16.0 | 91.51% | 5494.5 | 0.942888 |
| 2 | 2.0 | 91.51% | 5494.5 | 0.942888 | 24.0 | 91.51% | 5494.5 | 0.942888 |
| 3 | 3.0 | 91.51% | 5494.5 | 0.942888 | 32.0 | 91.51% | 5494.5 | 0.942888 |
| 4 | 4.0 | 91.51% | 5494.5 | 0.942888 | 40.0 | 91.51% | 5494.5 | 0.942888 |
| 5 | 5.0 | 91.51% | 5494.5 | 0.942888 | 48.0 | 91.51% | 5494.5 | 0.942888 |
| 6 | 6.0 | 91.51% | 5494.5 | 0.942888 | 56.0 | 91.51% | 5494.5 | 0.942888 |
| 7 | 7.0 | 91.51% | 5494.5 | 0.942888 | 64.0 | 91.51% | 5494.5 | 0.942888 |
| 8 | 8.0 | 91.51% | 5494.5 | 0.942888 | 72.0 | 91.51% | 5494.5 | 0.942888 |
| 9 | 9.0 | 91.51% | 5494.5 | 0.942888 | 80.0 | 91.51% | 5494.5 | 0.942888 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 86.07% | 1 | 942.51 | `{"filegroups/portable": 0.8746400475502014, "filetypes/jar": 0.9847872853279114, "general": 0.9430660009384155}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 86.07% | 1 | 942.51 | `{"filegroups/portable": 0.8746400475502014, "filetypes/jar": 0.9847872853279114, "general": 0.9430660009384155}` |
