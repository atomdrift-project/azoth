# Azoth Filetype `tar`
Specialist model for `tar`.
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
- Training rows: 1050 (911 malware, 139 benign).
- Benchmark rows: 152 (109 malware, 43 benign).
- Benchmark AUC/AP/F1: 0.9811 / 0.9930 / 0.9765.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 95.41% | 0.00 | 0.479538 | 8.0 | 95.41% | 0.00 | 0.479538 |
| 1 | 1.0 | 95.41% | 0.00 | 0.479538 | 16.0 | 95.41% | 0.00 | 0.479538 |
| 2 | 2.0 | 95.41% | 0.00 | 0.479538 | 24.0 | 95.41% | 0.00 | 0.479538 |
| 3 | 3.0 | 95.41% | 0.00 | 0.479538 | 32.0 | 95.41% | 0.00 | 0.479538 |
| 4 | 4.0 | 95.41% | 0.00 | 0.479538 | 40.0 | 95.41% | 0.00 | 0.479538 |
| 5 | 5.0 | 95.41% | 0.00 | 0.479538 | 48.0 | 95.41% | 0.00 | 0.479538 |
| 6 | 6.0 | 95.41% | 0.00 | 0.479538 | 56.0 | 95.41% | 0.00 | 0.479538 |
| 7 | 7.0 | 95.41% | 0.00 | 0.479538 | 64.0 | 95.41% | 0.00 | 0.479538 |
| 8 | 8.0 | 95.41% | 0.00 | 0.479538 | 72.0 | 95.41% | 0.00 | 0.479538 |
| 9 | 9.0 | 95.41% | 0.00 | 0.479538 | 80.0 | 95.41% | 0.00 | 0.479538 |
