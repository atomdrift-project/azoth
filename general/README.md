# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (60,778 features) extracted from cleave reports.
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
- Calibration corpus: 4,727,335 rows (1,702,977 malware, 3,024,358 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 32.12% | 0.00 | 0.998589 | 8.0 | 47.29% | 7.94 | 0.996094 |
| 1 | 1.0 | 34.03% | 0.99 | 0.998375 | 16.0 | 51.38% | 15.87 | 0.994702 |
| 2 | 2.0 | 39.49% | 1.98 | 0.997664 | 24.0 | 54.21% | 23.81 | 0.993520 |
| 3 | 3.0 | 42.00% | 2.98 | 0.997287 | 32.0 | 55.45% | 31.41 | 0.992661 |
| 4 | 4.0 | 43.92% | 3.97 | 0.996907 | 40.0 | 56.19% | 36.37 | 0.992105 |
| 5 | 5.0 | 44.30% | 4.96 | 0.996829 | 48.0 | 57.06% | 47.94 | 0.991228 |
| 6 | 6.0 | 45.57% | 5.95 | 0.996478 | 56.0 | 57.83% | 55.88 | 0.990456 |
| 7 | 7.0 | 46.00% | 6.94 | 0.996368 | 64.0 | 58.61% | 63.82 | 0.989495 |
| 8 | 8.0 | 47.29% | 7.94 | 0.996094 | 72.0 | 59.20% | 71.75 | 0.988737 |
| 9 | 9.0 | 47.39% | 8.93 | 0.996054 | 80.0 | 59.68% | 79.03 | 0.987962 |
| 10 | 10.0 | 48.17% | 9.92 | 0.995798 | 88.0 | 60.27% | 87.95 | 0.987187 |
| 11 | 11.0 | 48.62% | 10.91 | 0.995644 | 96.0 | 60.80% | 95.89 | 0.986240 |
| 12 | 12.0 | 49.37% | 11.90 | 0.995389 | 104.0 | 61.16% | 103.82 | 0.985439 |
| 13 | 13.0 | 49.95% | 12.90 | 0.995201 | 112.0 | 61.45% | 111.76 | 0.984835 |
| 14 | 14.0 | 50.21% | 13.89 | 0.995075 | 120.0 | 61.70% | 119.69 | 0.984183 |
| 15 | 15.0 | 51.22% | 14.88 | 0.994802 | 128.0 | 62.05% | 127.96 | 0.983260 |
| 16 | 16.0 | 51.38% | 15.87 | 0.994702 | 136.0 | 62.22% | 135.90 | 0.982713 |
| 17 | 17.0 | 51.84% | 16.86 | 0.994588 | 144.0 | 62.44% | 143.83 | 0.982018 |
| 18 | 18.0 | 52.31% | 17.86 | 0.994452 | 152.0 | 62.63% | 151.77 | 0.981373 |
| 19 | 19.0 | 52.48% | 18.85 | 0.994389 | 160.0 | 62.80% | 159.70 | 0.980679 |
| 20 | 20.0 | 52.62% | 19.84 | 0.994308 | 168.0 | 62.95% | 167.64 | 0.980053 |
