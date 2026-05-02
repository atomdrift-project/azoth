# Azoth Filetype `php`
Specialist model for `php`.
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
- Training rows: 1630 (1007 malware, 623 benign).
- Benchmark rows: 2001 (156 malware, 1845 benign).
- Benchmark AUC/AP/F1: 0.9995 / 0.9955 / 0.9775.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 93.59% | 0.00 | 0.769494 | 8.0 | 96.15% | 542.01 | 0.527555 |
| 1 | 1.0 | 96.15% | 542.01 | 0.527555 | 16.0 | 96.15% | 542.01 | 0.527555 |
| 2 | 2.0 | 96.15% | 542.01 | 0.527555 | 24.0 | 96.15% | 542.01 | 0.527555 |
| 3 | 3.0 | 96.15% | 542.01 | 0.527555 | 32.0 | 96.15% | 542.01 | 0.527555 |
| 4 | 4.0 | 96.15% | 542.01 | 0.527555 | 40.0 | 96.15% | 542.01 | 0.527555 |
| 5 | 5.0 | 96.15% | 542.01 | 0.527555 | 48.0 | 96.15% | 542.01 | 0.527555 |
| 6 | 6.0 | 96.15% | 542.01 | 0.527555 | 56.0 | 96.15% | 542.01 | 0.527555 |
| 7 | 7.0 | 96.15% | 542.01 | 0.527555 | 64.0 | 96.15% | 542.01 | 0.527555 |
| 8 | 8.0 | 96.15% | 542.01 | 0.527555 | 72.0 | 96.15% | 542.01 | 0.527555 |
| 9 | 9.0 | 96.15% | 542.01 | 0.527555 | 80.0 | 96.15% | 542.01 | 0.527555 |
