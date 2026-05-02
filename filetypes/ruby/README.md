# Azoth Filetype `ruby`
Specialist model for `ruby`.
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
- Training rows: 849 (62 malware, 787 benign).
- Benchmark rows: 1453 (7 malware, 1446 benign).
- Benchmark AUC/AP/F1: 0.9999 / 0.9821 / 0.9333.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 85.71% | 0.00 | 0.984930 | 8.0 | 100.00% | 691.56 | 0.769525 |
| 1 | 1.0 | 100.00% | 691.56 | 0.769525 | 16.0 | 100.00% | 691.56 | 0.769525 |
| 2 | 2.0 | 100.00% | 691.56 | 0.769525 | 24.0 | 100.00% | 691.56 | 0.769525 |
| 3 | 3.0 | 100.00% | 691.56 | 0.769525 | 32.0 | 100.00% | 691.56 | 0.769525 |
| 4 | 4.0 | 100.00% | 691.56 | 0.769525 | 40.0 | 100.00% | 691.56 | 0.769525 |
| 5 | 5.0 | 100.00% | 691.56 | 0.769525 | 48.0 | 100.00% | 691.56 | 0.769525 |
| 6 | 6.0 | 100.00% | 691.56 | 0.769525 | 56.0 | 100.00% | 691.56 | 0.769525 |
| 7 | 7.0 | 100.00% | 691.56 | 0.769525 | 64.0 | 100.00% | 691.56 | 0.769525 |
| 8 | 8.0 | 100.00% | 691.56 | 0.769525 | 72.0 | 100.00% | 691.56 | 0.769525 |
| 9 | 9.0 | 100.00% | 691.56 | 0.769525 | 80.0 | 100.00% | 691.56 | 0.769525 |
