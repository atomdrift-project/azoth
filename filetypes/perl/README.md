# Azoth Filetype `perl`
Specialist model for `perl`.
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
- Training rows: 1147 (108 malware, 1039 benign).
- Benchmark rows: 2661 (17 malware, 2644 benign).
- Benchmark AUC/AP/F1: 0.9493 / 0.9306 / 0.9412.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 76.47% | 0.00 | 0.989605 | 8.0 | 94.12% | 378.21 | 0.781196 |
| 1 | 1.0 | 94.12% | 378.21 | 0.781196 | 16.0 | 94.12% | 378.21 | 0.781196 |
| 2 | 2.0 | 94.12% | 378.21 | 0.781196 | 24.0 | 94.12% | 378.21 | 0.781196 |
| 3 | 3.0 | 94.12% | 378.21 | 0.781196 | 32.0 | 94.12% | 378.21 | 0.781196 |
| 4 | 4.0 | 94.12% | 378.21 | 0.781196 | 40.0 | 94.12% | 378.21 | 0.781196 |
| 5 | 5.0 | 94.12% | 378.21 | 0.781196 | 48.0 | 94.12% | 378.21 | 0.781196 |
| 6 | 6.0 | 94.12% | 378.21 | 0.781196 | 56.0 | 94.12% | 378.21 | 0.781196 |
| 7 | 7.0 | 94.12% | 378.21 | 0.781196 | 64.0 | 94.12% | 378.21 | 0.781196 |
| 8 | 8.0 | 94.12% | 378.21 | 0.781196 | 72.0 | 94.12% | 378.21 | 0.781196 |
| 9 | 9.0 | 94.12% | 378.21 | 0.781196 | 80.0 | 94.12% | 378.21 | 0.781196 |
