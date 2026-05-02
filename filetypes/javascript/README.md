# Azoth Filetype `javascript`
Specialist model for `javascript`.
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
- Training rows: 70045 (46998 malware, 23047 benign).
- Benchmark rows: 49028 (7162 malware, 41866 benign).
- Benchmark AUC/AP/F1: 0.9882 / 0.9758 / 0.9708.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 92.77% | 0.00 | 0.978567 | 8.0 | 93.09% | 23.89 | 0.969794 |
| 1 | 1.0 | 93.09% | 23.89 | 0.969794 | 16.0 | 93.09% | 23.89 | 0.969794 |
| 2 | 2.0 | 93.09% | 23.89 | 0.969794 | 24.0 | 93.09% | 23.89 | 0.969794 |
| 3 | 3.0 | 93.09% | 23.89 | 0.969794 | 32.0 | 93.09% | 23.89 | 0.969794 |
| 4 | 4.0 | 93.09% | 23.89 | 0.969794 | 40.0 | 93.09% | 23.89 | 0.969794 |
| 5 | 5.0 | 93.09% | 23.89 | 0.969794 | 48.0 | 93.47% | 47.77 | 0.940567 |
| 6 | 6.0 | 93.09% | 23.89 | 0.969794 | 56.0 | 93.47% | 47.77 | 0.940567 |
| 7 | 7.0 | 93.09% | 23.89 | 0.969794 | 64.0 | 93.47% | 47.77 | 0.940567 |
| 8 | 8.0 | 93.09% | 23.89 | 0.969794 | 72.0 | 93.80% | 71.66 | 0.887986 |
| 9 | 9.0 | 93.09% | 23.89 | 0.969794 | 80.0 | 93.80% | 71.66 | 0.887986 |
