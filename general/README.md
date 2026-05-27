# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (62,607 features) extracted from cleave reports.
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
- Calibration corpus: 5,053,489 rows (1,766,770 malware, 3,286,719 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 20.52% | 0.00 | 0.999227 | 8.0 | 44.53% | 7.91 | 0.996343 |
| 1 | 1.0 | 32.35% | 0.91 | 0.998313 | 16.0 | 49.41% | 15.82 | 0.995059 |
| 2 | 2.0 | 36.26% | 1.83 | 0.997888 | 24.0 | 52.19% | 23.73 | 0.993817 |
| 3 | 3.0 | 37.87% | 2.74 | 0.997642 | 32.0 | 54.20% | 31.95 | 0.992533 |
| 4 | 4.0 | 40.81% | 3.96 | 0.997109 | 40.0 | 55.44% | 39.86 | 0.991557 |
| 5 | 5.0 | 41.30% | 4.87 | 0.997001 | 48.0 | 56.15% | 47.46 | 0.990971 |
| 6 | 6.0 | 41.57% | 5.78 | 0.996951 | 56.0 | 56.89% | 55.98 | 0.990187 |
| 7 | 7.0 | 42.44% | 7.00 | 0.996775 | 64.0 | 57.69% | 63.89 | 0.989237 |
| 8 | 8.0 | 44.53% | 7.91 | 0.996343 | 72.0 | 58.32% | 71.80 | 0.988377 |
| 9 | 9.0 | 45.09% | 8.82 | 0.996184 | 80.0 | 58.61% | 79.71 | 0.987902 |
| 10 | 10.0 | 45.73% | 9.74 | 0.995998 | 88.0 | 59.05% | 87.93 | 0.987196 |
| 11 | 11.0 | 46.21% | 10.95 | 0.995845 | 96.0 | 59.35% | 95.84 | 0.986633 |
| 12 | 12.0 | 47.30% | 11.87 | 0.995661 | 104.0 | 59.62% | 103.75 | 0.986121 |
| 13 | 13.0 | 47.55% | 12.78 | 0.995556 | 112.0 | 59.75% | 111.97 | 0.985871 |
| 14 | 14.0 | 48.98% | 14.00 | 0.995228 | 120.0 | 60.02% | 119.88 | 0.985263 |
| 15 | 15.0 | 49.37% | 14.91 | 0.995079 | 128.0 | 60.24% | 127.48 | 0.984829 |
| 16 | 16.0 | 49.41% | 15.82 | 0.995059 | 136.0 | 60.44% | 135.70 | 0.984375 |
| 17 | 17.0 | 49.70% | 16.73 | 0.994925 | 144.0 | 60.73% | 143.91 | 0.983790 |
| 18 | 18.0 | 50.20% | 17.95 | 0.994728 | 152.0 | 60.85% | 151.82 | 0.983450 |
| 19 | 19.0 | 50.49% | 18.86 | 0.994632 | 160.0 | 61.10% | 159.73 | 0.982732 |
| 20 | 20.0 | 51.06% | 19.78 | 0.994365 | 168.0 | 61.30% | 167.95 | 0.982079 |
