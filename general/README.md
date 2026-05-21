# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (60,790 features) extracted from cleave reports.
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
- Calibration corpus: 4,727,598 rows (1,703,195 malware, 3,024,403 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 26.53% | 0.00 | 0.998954 | 8.0 | 44.50% | 7.94 | 0.996566 |
| 1 | 1.0 | 35.35% | 0.99 | 0.998135 | 16.0 | 48.57% | 15.87 | 0.995326 |
| 2 | 2.0 | 37.48% | 1.98 | 0.997848 | 24.0 | 51.65% | 23.81 | 0.994220 |
| 3 | 3.0 | 39.93% | 2.98 | 0.997425 | 32.0 | 53.23% | 31.74 | 0.993287 |
| 4 | 4.0 | 41.56% | 3.97 | 0.997171 | 40.0 | 55.23% | 39.68 | 0.992351 |
| 5 | 5.0 | 42.63% | 4.96 | 0.996968 | 48.0 | 56.09% | 47.94 | 0.991583 |
| 6 | 6.0 | 42.86% | 5.95 | 0.996926 | 56.0 | 56.89% | 55.88 | 0.990759 |
| 7 | 7.0 | 44.04% | 6.94 | 0.996678 | 64.0 | 57.58% | 63.81 | 0.989903 |
| 8 | 8.0 | 44.50% | 7.94 | 0.996566 | 72.0 | 58.27% | 71.75 | 0.989020 |
| 9 | 9.0 | 44.76% | 8.93 | 0.996510 | 80.0 | 58.80% | 79.69 | 0.988317 |
| 10 | 10.0 | 46.68% | 9.92 | 0.995984 | 88.0 | 59.13% | 87.95 | 0.987773 |
| 11 | 11.0 | 47.27% | 10.91 | 0.995805 | 96.0 | 59.86% | 95.89 | 0.986933 |
| 12 | 12.0 | 47.70% | 11.90 | 0.995650 | 104.0 | 60.09% | 103.82 | 0.986543 |
| 13 | 13.0 | 47.84% | 12.90 | 0.995597 | 112.0 | 60.60% | 111.76 | 0.985706 |
| 14 | 14.0 | 48.16% | 13.56 | 0.995474 | 120.0 | 60.74% | 119.69 | 0.985385 |
| 15 | 15.0 | 48.30% | 14.88 | 0.995411 | 128.0 | 61.08% | 127.96 | 0.984711 |
| 16 | 16.0 | 48.57% | 15.87 | 0.995326 | 136.0 | 61.25% | 135.89 | 0.984355 |
| 17 | 17.0 | 48.63% | 16.86 | 0.995303 | 144.0 | 61.69% | 143.83 | 0.983452 |
| 18 | 18.0 | 49.46% | 17.85 | 0.995043 | 152.0 | 61.83% | 150.11 | 0.983011 |
| 19 | 19.0 | 49.66% | 18.85 | 0.994978 | 160.0 | 62.01% | 159.70 | 0.982482 |
| 20 | 20.0 | 49.77% | 19.84 | 0.994926 | 168.0 | 62.14% | 167.97 | 0.982036 |
