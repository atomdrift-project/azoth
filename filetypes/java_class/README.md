# Azoth Filetype `java_class`
Specialist model for `java_class`.
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
- Training rows: 458 (220 malware, 238 benign).
- Benchmark rows: 881 (28 malware, 853 benign).
- Benchmark AUC/AP/F1: 1.0000 / 0.9988 / 0.9825.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.43% | 0.00 | 0.416656 | 8.0 | 100.00% | 1172.3 | 0.114683 |
| 1 | 1.0 | 100.00% | 1172.3 | 0.114683 | 16.0 | 100.00% | 1172.3 | 0.114683 |
| 2 | 2.0 | 100.00% | 1172.3 | 0.114683 | 24.0 | 100.00% | 1172.3 | 0.114683 |
| 3 | 3.0 | 100.00% | 1172.3 | 0.114683 | 32.0 | 100.00% | 1172.3 | 0.114683 |
| 4 | 4.0 | 100.00% | 1172.3 | 0.114683 | 40.0 | 100.00% | 1172.3 | 0.114683 |
| 5 | 5.0 | 100.00% | 1172.3 | 0.114683 | 48.0 | 100.00% | 1172.3 | 0.114683 |
| 6 | 6.0 | 100.00% | 1172.3 | 0.114683 | 56.0 | 100.00% | 1172.3 | 0.114683 |
| 7 | 7.0 | 100.00% | 1172.3 | 0.114683 | 64.0 | 100.00% | 1172.3 | 0.114683 |
| 8 | 8.0 | 100.00% | 1172.3 | 0.114683 | 72.0 | 100.00% | 1172.3 | 0.114683 |
| 9 | 9.0 | 100.00% | 1172.3 | 0.114683 | 80.0 | 100.00% | 1172.3 | 0.114683 |
