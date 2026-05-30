# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (63,983 features) extracted from cleave reports.
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
- Calibration corpus: 5,591,524 rows (1,834,873 malware, 3,756,651 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 22.02% | 0.00 | 0.999024 | 8.0 | 45.30% | 7.99 | 0.995880 |
| 1 | 1.0 | 27.39% | 0.80 | 0.998590 | 16.0 | 50.50% | 15.97 | 0.994015 |
| 2 | 2.0 | 34.37% | 1.86 | 0.997921 | 24.0 | 52.93% | 23.96 | 0.992847 |
| 3 | 3.0 | 37.46% | 2.93 | 0.997524 | 32.0 | 53.91% | 30.88 | 0.992153 |
| 4 | 4.0 | 39.43% | 3.99 | 0.997211 | 40.0 | 54.75% | 39.93 | 0.991481 |
| 5 | 5.0 | 40.42% | 4.79 | 0.997018 | 48.0 | 55.91% | 47.65 | 0.990672 |
| 6 | 6.0 | 42.19% | 5.86 | 0.996665 | 56.0 | 56.54% | 55.90 | 0.990002 |
| 7 | 7.0 | 44.48% | 6.92 | 0.996080 | 64.0 | 57.18% | 63.89 | 0.989208 |
| 8 | 8.0 | 45.30% | 7.99 | 0.995880 | 72.0 | 57.80% | 71.87 | 0.988468 |
| 9 | 9.0 | 46.44% | 8.52 | 0.995598 | 80.0 | 58.34% | 79.86 | 0.987724 |
| 10 | 10.0 | 46.70% | 9.85 | 0.995506 | 88.0 | 58.76% | 87.84 | 0.987104 |
| 11 | 11.0 | 47.52% | 10.91 | 0.995232 | 96.0 | 59.24% | 95.83 | 0.986231 |
| 12 | 12.0 | 47.89% | 11.98 | 0.995059 | 104.0 | 59.61% | 103.82 | 0.985500 |
| 13 | 13.0 | 48.29% | 12.78 | 0.994867 | 112.0 | 59.69% | 105.41 | 0.985339 |
| 14 | 14.0 | 49.25% | 13.84 | 0.994513 | 120.0 | 60.15% | 119.79 | 0.984342 |
| 15 | 15.0 | 49.84% | 14.91 | 0.994226 | 128.0 | 60.75% | 127.77 | 0.982957 |
| 16 | 16.0 | 50.50% | 15.97 | 0.994015 | 136.0 | 61.14% | 135.76 | 0.981927 |
| 17 | 17.0 | 50.78% | 16.77 | 0.993896 | 144.0 | 61.44% | 143.75 | 0.981425 |
| 18 | 18.0 | 51.47% | 17.84 | 0.993650 | 152.0 | 61.56% | 152.00 | 0.981059 |
| 19 | 19.0 | 51.49% | 18.90 | 0.993636 | 160.0 | 61.77% | 159.98 | 0.980379 |
| 20 | 20.0 | 51.93% | 19.96 | 0.993452 | 168.0 | 61.88% | 167.97 | 0.979948 |
