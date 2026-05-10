# Azoth Filegroup — `source`

Specialist classifier for `c`, `cpp`, `csharp`, `go`, `java`, `kotlin`, `makefile`, `rust`, `scala`, `swift`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

Training-time benchmark (no test-bucket-only metric on file):

- ROC AUC / PR AUC / F1: 0.9203 / 0.6229 / 0.6615
- Benchmark rows: 88277 (1112 malware, 87165 benign).

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
- Training rows: 10578 (3532 malware, 7046 benign).
- Internal training-time benchmark rows: 88277 (1112 malware, 87165 benign).
- Internal training-time benchmark AUC/AP/F1: 0.9203 / 0.6229 / 0.6615.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 45.41% | 0.00 | 0.955159 | 8.0 | 45.86% | 11.47 | 0.951228 |
| 1 | 1.0 | 45.86% | 11.47 | 0.951228 | 16.0 | 45.86% | 11.47 | 0.951228 |
| 2 | 2.0 | 45.86% | 11.47 | 0.951228 | 24.0 | 46.40% | 22.94 | 0.945250 |
| 3 | 3.0 | 45.86% | 11.47 | 0.951228 | 32.0 | 46.40% | 22.94 | 0.945250 |
| 4 | 4.0 | 45.86% | 11.47 | 0.951228 | 40.0 | 46.40% | 34.42 | 0.944820 |
| 5 | 5.0 | 45.86% | 11.47 | 0.951228 | 48.0 | 46.67% | 45.89 | 0.941164 |
| 6 | 6.0 | 45.86% | 11.47 | 0.951228 | 56.0 | 46.67% | 45.89 | 0.941164 |
| 7 | 7.0 | 45.86% | 11.47 | 0.951228 | 64.0 | 46.76% | 57.36 | 0.940335 |
| 8 | 8.0 | 45.86% | 11.47 | 0.951228 | 72.0 | 47.93% | 68.83 | 0.935077 |
| 9 | 9.0 | 45.86% | 11.47 | 0.951228 | 80.0 | 47.93% | 68.83 | 0.935077 |
