# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (60,810 features) extracted from cleave reports.
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
- Calibration corpus: 4,731,967 rows (1,703,780 malware, 3,028,187 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 29.43% | 0.00 | 0.998445 | 8.0 | 46.19% | 7.93 | 0.995752 |
| 1 | 1.0 | 32.93% | 0.99 | 0.998074 | 16.0 | 51.09% | 15.85 | 0.993946 |
| 2 | 2.0 | 36.25% | 1.98 | 0.997617 | 24.0 | 53.71% | 23.78 | 0.992589 |
| 3 | 3.0 | 38.60% | 2.97 | 0.997239 | 32.0 | 55.05% | 31.70 | 0.991500 |
| 4 | 4.0 | 41.79% | 3.96 | 0.996659 | 40.0 | 56.77% | 39.96 | 0.989756 |
| 5 | 5.0 | 42.41% | 4.95 | 0.996503 | 48.0 | 57.53% | 47.88 | 0.988825 |
| 6 | 6.0 | 43.73% | 5.61 | 0.996177 | 56.0 | 58.19% | 55.81 | 0.987847 |
| 7 | 7.0 | 44.66% | 6.93 | 0.996081 | 64.0 | 58.83% | 63.73 | 0.986853 |
| 8 | 8.0 | 46.19% | 7.93 | 0.995752 | 72.0 | 59.56% | 71.99 | 0.985810 |
| 9 | 9.0 | 46.95% | 8.92 | 0.995529 | 80.0 | 60.19% | 79.92 | 0.984917 |
| 10 | 10.0 | 47.90% | 9.91 | 0.995165 | 88.0 | 60.55% | 87.84 | 0.984108 |
| 11 | 11.0 | 48.06% | 10.90 | 0.995118 | 96.0 | 60.97% | 95.77 | 0.983048 |
| 12 | 12.0 | 48.24% | 11.89 | 0.995059 | 104.0 | 61.30% | 103.69 | 0.982206 |
| 13 | 13.0 | 49.20% | 12.88 | 0.994737 | 112.0 | 61.49% | 111.29 | 0.981653 |
| 14 | 14.0 | 50.25% | 13.87 | 0.994325 | 120.0 | 61.79% | 119.87 | 0.980822 |
| 15 | 15.0 | 50.43% | 14.86 | 0.994230 | 128.0 | 62.08% | 127.80 | 0.979987 |
| 16 | 16.0 | 51.09% | 15.85 | 0.993946 | 136.0 | 62.29% | 135.39 | 0.979296 |
| 17 | 17.0 | 51.55% | 16.84 | 0.993769 | 144.0 | 62.48% | 142.66 | 0.978573 |
| 18 | 18.0 | 51.72% | 17.83 | 0.993697 | 152.0 | 62.77% | 151.91 | 0.977454 |
| 19 | 19.0 | 52.37% | 18.82 | 0.993387 | 160.0 | 62.91% | 159.83 | 0.976813 |
| 20 | 20.0 | 52.70% | 19.81 | 0.993165 | 168.0 | 63.12% | 167.76 | 0.975983 |
