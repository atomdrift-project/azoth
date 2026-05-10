# Azoth Filegroup — `media`

Specialist classifier for `bmp`, `gif`, `jpeg`, `jpg`, `mp3`, `mp4`, `png`, `svg`, `webp`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


> ⚠ Benchmark AUC is degenerate on this split — keep the artifact for coverage, but rely on routed full-corpus calibration before relying on it.
## Single-model performance

Training-time benchmark (no test-bucket-only metric on file):

- ROC AUC / PR AUC / F1: 0.3906 / 0.0583 / 0.1081
- Benchmark rows: 8965 (497 malware, 8468 benign).

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
- Training rows: 477 (246 malware, 231 benign).
- Internal training-time benchmark rows: 8965 (497 malware, 8468 benign).
- Internal training-time benchmark AUC/AP/F1: 0.3906 / 0.0583 / 0.1081.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 1.21% | 0.00 | 0.961643 | 8.0 | 1.41% | 118.09 | 0.955624 |
| 1 | 1.0 | 1.41% | 118.09 | 0.955624 | 16.0 | 1.41% | 118.09 | 0.955624 |
| 2 | 2.0 | 1.41% | 118.09 | 0.955624 | 24.0 | 1.41% | 118.09 | 0.955624 |
| 3 | 3.0 | 1.41% | 118.09 | 0.955624 | 32.0 | 1.41% | 118.09 | 0.955624 |
| 4 | 4.0 | 1.41% | 118.09 | 0.955624 | 40.0 | 1.41% | 118.09 | 0.955624 |
| 5 | 5.0 | 1.41% | 118.09 | 0.955624 | 48.0 | 1.41% | 118.09 | 0.955624 |
| 6 | 6.0 | 1.41% | 118.09 | 0.955624 | 56.0 | 1.41% | 118.09 | 0.955624 |
| 7 | 7.0 | 1.41% | 118.09 | 0.955624 | 64.0 | 1.41% | 118.09 | 0.955624 |
| 8 | 8.0 | 1.41% | 118.09 | 0.955624 | 72.0 | 1.41% | 118.09 | 0.955624 |
| 9 | 9.0 | 1.41% | 118.09 | 0.955624 | 80.0 | 1.41% | 118.09 | 0.955624 |
