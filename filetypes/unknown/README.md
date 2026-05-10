# Azoth Filetype — `unknown`

Specialist classifier for `unknown`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


> ⚠ Benchmark AUC is degenerate on this split — keep the artifact for coverage, but rely on routed full-corpus calibration before relying on it.
## Single-model performance

On `unknown` test-bucket rows (n=1797, SHA256-deterministic 12.5% holdout):

| Metric | Specialist (this model alone) | EMBER 2024 reference | Δ |
|---|---:|---:|---:|
| ROC AUC | 0.6569 | — | - |
| PR AUC | 0.0386 | — | - |
| F1 | 0.1569 | — | — |
| Brier (calibration) | - | — | — |

## How the ensemble uses this specialist

At the default operating level, the deployed routing policy for `unknown` is `no_policy`.

Ensemble's headline numbers on this filetype's test bucket: ROC AUC = **0.6569**, PR AUC = **0.0386**, F1 = **0.1569**. When the ensemble lags the specialist, the router is being conservative for FP/M-budget reasons; the specialist alone is what production would get if you bypassed routing.

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
- Training rows: 12426 (105 malware, 12321 benign).
- Internal training-time benchmark rows: 1800 (12 malware, 1788 benign).
- Internal training-time benchmark AUC/AP/F1: 0.4688 / 0.0154 / 0.0930.

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
| 5 | suspicious | general_only | 7.87% | 1 | 70.95 | `{"general": 0.053820181638002396}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | general_only | 7.87% | 1 | 70.95 | `{"general": 0.053820181638002396}` |
