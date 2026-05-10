# Azoth Filetype — `perl`

Specialist classifier for `perl`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

On `perl` test-bucket rows (n=2761, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.9953 | — | - |
| PR AUC | 0.9484 | — | - |
| F1 | 0.9714 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `perl` is `specialist_primary_with_escape`.
Routes consulted (max-of-thresholds): `general`, `filegroups/scripts`, `filetypes/perl`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.9992**, PR AUC = **0.9471**, F1 = **0.9189**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

## Training

- Inputs: shared general `feature_spec.json` (49112 features); feature-spec policy `general_shared`.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=48, max_depth=12, min_child_samples=140, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.5, reg_lambda=4.0, early_stop=50, device=cpu.
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
- Training rows: 25798 (133 malware, 25665 benign).
- Internal training-time benchmark rows: 3721 (18 malware, 3703 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9994 / 0.9608 / 0.9714.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.44% | 0.00 | 0.992144 | 8.0 | 94.44% | 270.05 | 0.910061 |
| 1 | 1.0 | 94.44% | 270.05 | 0.910061 | 16.0 | 94.44% | 270.05 | 0.910061 |
| 2 | 2.0 | 94.44% | 270.05 | 0.910061 | 24.0 | 94.44% | 270.05 | 0.910061 |
| 3 | 3.0 | 94.44% | 270.05 | 0.910061 | 32.0 | 94.44% | 270.05 | 0.910061 |
| 4 | 4.0 | 94.44% | 270.05 | 0.910061 | 40.0 | 94.44% | 270.05 | 0.910061 |
| 5 | 5.0 | 94.44% | 270.05 | 0.910061 | 48.0 | 94.44% | 270.05 | 0.910061 |
| 6 | 6.0 | 94.44% | 270.05 | 0.910061 | 56.0 | 94.44% | 270.05 | 0.910061 |
| 7 | 7.0 | 94.44% | 270.05 | 0.910061 | 64.0 | 94.44% | 270.05 | 0.910061 |
| 8 | 8.0 | 94.44% | 270.05 | 0.910061 | 72.0 | 94.44% | 270.05 | 0.910061 |
| 9 | 9.0 | 94.44% | 270.05 | 0.910061 | 80.0 | 94.44% | 270.05 | 0.910061 |

## Routed policy decisions

What the ensemble actually does with this route at each operating level.

| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 5 | suspicious | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 9 | hostile | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 9 | suspicious | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
