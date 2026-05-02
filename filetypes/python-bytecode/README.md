# Azoth Filetype `python-bytecode`
Specialist model for `python-bytecode`.
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
- Training rows: 116 (65 malware, 51 benign).
- Benchmark rows: 1084 (9 malware, 1075 benign).
- Benchmark AUC/AP/F1: 0.9861 / 0.8940 / 0.9412.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 88.89% | 0.00 | 0.801340 | 8.0 | 88.89% | 0.00 | 0.801340 |
| 1 | 1.0 | 88.89% | 0.00 | 0.801340 | 16.0 | 88.89% | 0.00 | 0.801340 |
| 2 | 2.0 | 88.89% | 0.00 | 0.801340 | 24.0 | 88.89% | 0.00 | 0.801340 |
| 3 | 3.0 | 88.89% | 0.00 | 0.801340 | 32.0 | 88.89% | 0.00 | 0.801340 |
| 4 | 4.0 | 88.89% | 0.00 | 0.801340 | 40.0 | 88.89% | 0.00 | 0.801340 |
| 5 | 5.0 | 88.89% | 0.00 | 0.801340 | 48.0 | 88.89% | 0.00 | 0.801340 |
| 6 | 6.0 | 88.89% | 0.00 | 0.801340 | 56.0 | 88.89% | 0.00 | 0.801340 |
| 7 | 7.0 | 88.89% | 0.00 | 0.801340 | 64.0 | 88.89% | 0.00 | 0.801340 |
| 8 | 8.0 | 88.89% | 0.00 | 0.801340 | 72.0 | 88.89% | 0.00 | 0.801340 |
| 9 | 9.0 | 88.89% | 0.00 | 0.801340 | 80.0 | 88.89% | 0.00 | 0.801340 |
