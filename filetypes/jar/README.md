# Azoth Filetype `jar`
Specialist model for `jar`.
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
- Training rows: 612 (403 malware, 209 benign).
- Benchmark rows: 209 (96 malware, 113 benign).
- Benchmark AUC/AP/F1: 0.9744 / 0.9767 / 0.9684.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 60.42% | 0.00 | 0.931112 | 8.0 | 88.54% | 8849.6 | 0.587661 |
| 1 | 1.0 | 88.54% | 8849.6 | 0.587661 | 16.0 | 88.54% | 8849.6 | 0.587661 |
| 2 | 2.0 | 88.54% | 8849.6 | 0.587661 | 24.0 | 88.54% | 8849.6 | 0.587661 |
| 3 | 3.0 | 88.54% | 8849.6 | 0.587661 | 32.0 | 88.54% | 8849.6 | 0.587661 |
| 4 | 4.0 | 88.54% | 8849.6 | 0.587661 | 40.0 | 88.54% | 8849.6 | 0.587661 |
| 5 | 5.0 | 88.54% | 8849.6 | 0.587661 | 48.0 | 88.54% | 8849.6 | 0.587661 |
| 6 | 6.0 | 88.54% | 8849.6 | 0.587661 | 56.0 | 88.54% | 8849.6 | 0.587661 |
| 7 | 7.0 | 88.54% | 8849.6 | 0.587661 | 64.0 | 88.54% | 8849.6 | 0.587661 |
| 8 | 8.0 | 88.54% | 8849.6 | 0.587661 | 72.0 | 88.54% | 8849.6 | 0.587661 |
| 9 | 9.0 | 88.54% | 8849.6 | 0.587661 | 80.0 | 88.54% | 8849.6 | 0.587661 |
