# Azoth Filetype `zip`
Specialist model for `zip`.
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
- Training rows: 23595 (22380 malware, 1215 benign).
- Benchmark rows: 3913 (3612 malware, 301 benign).
- Benchmark AUC/AP/F1: 0.9079 / 0.9918 / 0.9732.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 72.23% | 0.00 | 0.960845 | 8.0 | 75.36% | 3322.3 | 0.884762 |
| 1 | 1.0 | 75.36% | 3322.3 | 0.884762 | 16.0 | 75.36% | 3322.3 | 0.884762 |
| 2 | 2.0 | 75.36% | 3322.3 | 0.884762 | 24.0 | 75.36% | 3322.3 | 0.884762 |
| 3 | 3.0 | 75.36% | 3322.3 | 0.884762 | 32.0 | 75.36% | 3322.3 | 0.884762 |
| 4 | 4.0 | 75.36% | 3322.3 | 0.884762 | 40.0 | 75.36% | 3322.3 | 0.884762 |
| 5 | 5.0 | 75.36% | 3322.3 | 0.884762 | 48.0 | 75.36% | 3322.3 | 0.884762 |
| 6 | 6.0 | 75.36% | 3322.3 | 0.884762 | 56.0 | 75.36% | 3322.3 | 0.884762 |
| 7 | 7.0 | 75.36% | 3322.3 | 0.884762 | 64.0 | 75.36% | 3322.3 | 0.884762 |
| 8 | 8.0 | 75.36% | 3322.3 | 0.884762 | 72.0 | 75.36% | 3322.3 | 0.884762 |
| 9 | 9.0 | 75.36% | 3322.3 | 0.884762 | 80.0 | 75.36% | 3322.3 | 0.884762 |
