# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (60,358 features) extracted from cleave reports.
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
- Calibration corpus: 4,682,982 rows (1,692,465 malware, 2,990,517 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 10.71% | 0.00 | 0.999757 | 8.0 | 37.67% | 7.69 | 0.998376 |
| 1 | 1.0 | 19.43% | 0.67 | 0.999516 | 16.0 | 42.69% | 15.72 | 0.997754 |
| 2 | 2.0 | 27.32% | 1.67 | 0.999177 | 24.0 | 45.75% | 23.74 | 0.997203 |
| 3 | 3.0 | 30.44% | 2.68 | 0.998989 | 32.0 | 48.28% | 31.77 | 0.996657 |
| 4 | 4.0 | 31.78% | 3.68 | 0.998905 | 40.0 | 49.77% | 39.79 | 0.996288 |
| 5 | 5.0 | 33.86% | 4.68 | 0.998750 | 48.0 | 51.13% | 47.82 | 0.995824 |
| 6 | 6.0 | 35.45% | 5.68 | 0.998613 | 56.0 | 52.15% | 55.84 | 0.995437 |
| 7 | 7.0 | 36.60% | 6.69 | 0.998498 | 64.0 | 53.06% | 63.87 | 0.995059 |
| 8 | 8.0 | 37.67% | 7.69 | 0.998376 | 72.0 | 54.16% | 71.89 | 0.994518 |
| 9 | 9.0 | 37.91% | 8.69 | 0.998352 | 80.0 | 54.75% | 79.92 | 0.994181 |
| 10 | 10.0 | 39.00% | 9.70 | 0.998242 | 88.0 | 55.30% | 87.94 | 0.993893 |
| 11 | 11.0 | 39.89% | 10.70 | 0.998151 | 96.0 | 55.84% | 95.97 | 0.993562 |
| 12 | 12.0 | 40.58% | 11.70 | 0.998070 | 104.0 | 56.28% | 104.00 | 0.993266 |
| 13 | 13.0 | 41.33% | 12.71 | 0.997958 | 112.0 | 56.77% | 111.02 | 0.992914 |
| 14 | 14.0 | 41.66% | 13.71 | 0.997907 | 120.0 | 56.82% | 119.71 | 0.992880 |
| 15 | 15.0 | 42.41% | 14.71 | 0.997796 | 128.0 | 57.08% | 127.74 | 0.992651 |
| 16 | 16.0 | 42.69% | 15.72 | 0.997754 | 136.0 | 57.31% | 135.76 | 0.992448 |
| 17 | 17.0 | 42.86% | 16.72 | 0.997729 | 144.0 | 57.76% | 143.79 | 0.992062 |
| 18 | 18.0 | 43.46% | 17.72 | 0.997634 | 152.0 | 58.00% | 151.81 | 0.991822 |
| 19 | 19.0 | 43.99% | 18.73 | 0.997549 | 160.0 | 58.44% | 159.84 | 0.991497 |
| 20 | 20.0 | 44.38% | 19.73 | 0.997484 | 168.0 | 58.80% | 167.86 | 0.991116 |
