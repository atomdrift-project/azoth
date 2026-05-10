# Azoth Filegroup — `portable`

Specialist classifier for `dex`, `jar`, `java_class`, `pyc`, `wasm`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

Training-time benchmark (no test-bucket-only metric on file):

- ROC AUC / PR AUC / F1: 0.9879 / 0.9806 / 0.9648
- Benchmark rows: 1140 (142 malware, 998 benign).

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
- Training rows: 1220 (751 malware, 469 benign).
- Internal training-time benchmark rows: 1140 (142 malware, 998 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9879 / 0.9806 / 0.9648.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 79.58% | 0.00 | 0.846355 | 8.0 | 93.66% | 1002.0 | 0.425958 |
| 1 | 1.0 | 93.66% | 1002.0 | 0.425958 | 16.0 | 93.66% | 1002.0 | 0.425958 |
| 2 | 2.0 | 93.66% | 1002.0 | 0.425958 | 24.0 | 93.66% | 1002.0 | 0.425958 |
| 3 | 3.0 | 93.66% | 1002.0 | 0.425958 | 32.0 | 93.66% | 1002.0 | 0.425958 |
| 4 | 4.0 | 93.66% | 1002.0 | 0.425958 | 40.0 | 93.66% | 1002.0 | 0.425958 |
| 5 | 5.0 | 93.66% | 1002.0 | 0.425958 | 48.0 | 93.66% | 1002.0 | 0.425958 |
| 6 | 6.0 | 93.66% | 1002.0 | 0.425958 | 56.0 | 93.66% | 1002.0 | 0.425958 |
| 7 | 7.0 | 93.66% | 1002.0 | 0.425958 | 64.0 | 93.66% | 1002.0 | 0.425958 |
| 8 | 8.0 | 93.66% | 1002.0 | 0.425958 | 72.0 | 93.66% | 1002.0 | 0.425958 |
| 9 | 9.0 | 93.66% | 1002.0 | 0.425958 | 80.0 | 93.66% | 1002.0 | 0.425958 |
