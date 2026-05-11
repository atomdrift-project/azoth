# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (47621 features) extracted from cleave reports.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - format-group hints
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Calibration corpus: 3285920 rows (699360 malware, 2586560 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 39.25% | 0.00 | 0.999337 | 8.0 | 66.49% | 7.73 | 0.996596 |
| 1 | 1.0 | 47.90% | 0.77 | 0.998923 | 16.0 | 70.64% | 15.85 | 0.995480 |
| 2 | 2.0 | 55.81% | 1.93 | 0.998219 | 24.0 | 72.60% | 23.97 | 0.994802 |
| 3 | 3.0 | 56.85% | 2.71 | 0.998111 | 32.0 | 73.73% | 31.70 | 0.994235 |
| 4 | 4.0 | 63.04% | 3.87 | 0.997180 | 40.0 | 74.86% | 39.82 | 0.993490 |
| 5 | 5.0 | 63.19% | 4.64 | 0.997147 | 48.0 | 75.99% | 47.94 | 0.992773 |
| 6 | 6.0 | 65.65% | 5.80 | 0.996797 | 56.0 | 76.68% | 55.67 | 0.992268 |
| 7 | 7.0 | 65.88% | 6.96 | 0.996739 | 64.0 | 77.42% | 63.79 | 0.991689 |
| 8 | 8.0 | 66.49% | 7.73 | 0.996596 | 72.0 | 77.84% | 71.91 | 0.991296 |
| 9 | 9.0 | 66.71% | 8.89 | 0.996552 | 80.0 | 78.08% | 78.87 | 0.991075 |
