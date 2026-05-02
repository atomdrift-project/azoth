# Azoth Filetype `csharp`
Specialist model for `csharp`.
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
- Training rows: 482 (327 malware, 155 benign).
- Benchmark rows: 4118 (88 malware, 4030 benign).
- Benchmark AUC/AP/F1: 0.9596 / 0.7246 / 0.7246.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 56.82% | 0.00 | 0.846850 | 8.0 | 56.82% | 248.14 | 0.654347 |
| 1 | 1.0 | 56.82% | 248.14 | 0.654347 | 16.0 | 56.82% | 248.14 | 0.654347 |
| 2 | 2.0 | 56.82% | 248.14 | 0.654347 | 24.0 | 56.82% | 248.14 | 0.654347 |
| 3 | 3.0 | 56.82% | 248.14 | 0.654347 | 32.0 | 56.82% | 248.14 | 0.654347 |
| 4 | 4.0 | 56.82% | 248.14 | 0.654347 | 40.0 | 56.82% | 248.14 | 0.654347 |
| 5 | 5.0 | 56.82% | 248.14 | 0.654347 | 48.0 | 56.82% | 248.14 | 0.654347 |
| 6 | 6.0 | 56.82% | 248.14 | 0.654347 | 56.0 | 56.82% | 248.14 | 0.654347 |
| 7 | 7.0 | 56.82% | 248.14 | 0.654347 | 64.0 | 56.82% | 248.14 | 0.654347 |
| 8 | 8.0 | 56.82% | 248.14 | 0.654347 | 72.0 | 56.82% | 248.14 | 0.654347 |
| 9 | 9.0 | 56.82% | 248.14 | 0.654347 | 80.0 | 56.82% | 248.14 | 0.654347 |
