# Azoth Filegroup — `native`

Specialist classifier for `elf`, `macho`, `pe`. Used by the routed ensemble — see [../../ENSEMBLE_MODEL.md](../../ENSEMBLE_MODEL.md).


## Single-model performance

Training-time benchmark (no test-bucket-only metric on file):

- ROC AUC / PR AUC / F1: 1.0000 / 1.0000 / 0.9984
- Benchmark rows: 75513 (43284 malware, 32229 benign).

## Training

- Inputs: shared general `feature_spec.json` (39115 features); feature-spec policy `route_specific`.
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
- Training rows: 541780 (317097 malware, 224683 benign).
- Internal training-time benchmark rows: 75513 (43284 malware, 32229 benign).
- Internal training-time benchmark AUC/AP/F1: 1.0000 / 1.0000 / 0.9984.

## Operational policy levels (advanced)

Per-FP/M-target operating points for this specialist. Default deploy uses L3 hostile, L5 suspicious; lower levels = stricter FP budget. Useful when you need to tune deployed sensitivity.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.96% | 0.00 | 0.999447 | 8.0 | 90.92% | 31.03 | 0.998666 |
| 1 | 1.0 | 90.92% | 31.03 | 0.998666 | 16.0 | 90.92% | 31.03 | 0.998666 |
| 2 | 2.0 | 90.92% | 31.03 | 0.998666 | 24.0 | 90.92% | 31.03 | 0.998666 |
| 3 | 3.0 | 90.92% | 31.03 | 0.998666 | 32.0 | 90.92% | 31.03 | 0.998666 |
| 4 | 4.0 | 90.92% | 31.03 | 0.998666 | 40.0 | 90.92% | 31.03 | 0.998666 |
| 5 | 5.0 | 90.92% | 31.03 | 0.998666 | 48.0 | 90.92% | 31.03 | 0.998666 |
| 6 | 6.0 | 90.92% | 31.03 | 0.998666 | 56.0 | 90.92% | 31.03 | 0.998666 |
| 7 | 7.0 | 90.92% | 31.03 | 0.998666 | 64.0 | 91.03% | 62.06 | 0.998643 |
| 8 | 8.0 | 90.92% | 31.03 | 0.998666 | 72.0 | 91.03% | 62.06 | 0.998643 |
| 9 | 9.0 | 90.92% | 31.03 | 0.998666 | 80.0 | 91.03% | 62.06 | 0.998643 |
