# Azoth Filetype `python`
Specialist model for `python`.
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
- Training rows: 16103 (6746 malware, 9357 benign).
- Benchmark rows: 13129 (1010 malware, 12119 benign).
- Benchmark AUC/AP/F1: 0.9960 / 0.9882 / 0.9670.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 69.80% | 0.00 | 0.998307 | 8.0 | 79.01% | 82.52 | 0.997045 |
| 1 | 1.0 | 79.01% | 82.52 | 0.997045 | 16.0 | 79.01% | 82.52 | 0.997045 |
| 2 | 2.0 | 79.01% | 82.52 | 0.997045 | 24.0 | 79.01% | 82.52 | 0.997045 |
| 3 | 3.0 | 79.01% | 82.52 | 0.997045 | 32.0 | 79.01% | 82.52 | 0.997045 |
| 4 | 4.0 | 79.01% | 82.52 | 0.997045 | 40.0 | 79.01% | 82.52 | 0.997045 |
| 5 | 5.0 | 79.01% | 82.52 | 0.997045 | 48.0 | 79.01% | 82.52 | 0.997045 |
| 6 | 6.0 | 79.01% | 82.52 | 0.997045 | 56.0 | 79.01% | 82.52 | 0.997045 |
| 7 | 7.0 | 79.01% | 82.52 | 0.997045 | 64.0 | 79.01% | 82.52 | 0.997045 |
| 8 | 8.0 | 79.01% | 82.52 | 0.997045 | 72.0 | 79.01% | 82.52 | 0.997045 |
| 9 | 9.0 | 79.01% | 82.52 | 0.997045 | 80.0 | 79.01% | 82.52 | 0.997045 |
