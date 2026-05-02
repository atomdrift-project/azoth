# Azoth Filegroup `native`
Specialist model for `elf`, `macho`, `pe`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 420454 (233564 malware, 186890 benign).
- Benchmark rows: 59395 (31769 malware, 27626 benign).
- Benchmark AUC/AP/F1: 0.9998 / 0.9998 / 0.9956.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 81.87% | 0.00 | 0.998520 | 8.0 | 84.83% | 36.20 | 0.997905 |
| 1 | 1.0 | 84.83% | 36.20 | 0.997905 | 16.0 | 84.83% | 36.20 | 0.997905 |
| 2 | 2.0 | 84.83% | 36.20 | 0.997905 | 24.0 | 84.83% | 36.20 | 0.997905 |
| 3 | 3.0 | 84.83% | 36.20 | 0.997905 | 32.0 | 84.83% | 36.20 | 0.997905 |
| 4 | 4.0 | 84.83% | 36.20 | 0.997905 | 40.0 | 84.83% | 36.20 | 0.997905 |
| 5 | 5.0 | 84.83% | 36.20 | 0.997905 | 48.0 | 84.83% | 36.20 | 0.997905 |
| 6 | 6.0 | 84.83% | 36.20 | 0.997905 | 56.0 | 84.83% | 36.20 | 0.997905 |
| 7 | 7.0 | 84.83% | 36.20 | 0.997905 | 64.0 | 84.83% | 36.20 | 0.997905 |
| 8 | 8.0 | 84.83% | 36.20 | 0.997905 | 72.0 | 84.83% | 36.20 | 0.997905 |
| 9 | 9.0 | 84.83% | 36.20 | 0.997905 | 80.0 | 87.47% | 72.40 | 0.997016 |
