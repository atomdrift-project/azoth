# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (6,388 features) extracted from cleave reports.
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
- Technique: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Calibration corpus: 19,811,828 rows (2,960,816 malware, 16,851,012 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 28.04% | 0.00 | routed |
| 1 | 1.0 | 28.17% | 2112.6 | routed |
| 2 | 2.0 | 28.29% | 2112.6 | routed |
| 3 | 3.0 | 28.44% | 2112.6 | routed |
| 4 | 4.0 | 28.56% | 2112.6 | routed |
| 5 | 5.0 | 28.71% | 2112.6 | routed |
| 10 | 10.0 | 29.12% | 2118.6 | routed |
| 15 | 15.0 | 29.32% | 2124.5 | routed |
| 20 | 20.0 | 29.65% | 2130.4 | routed |
| 25 | 25.0 | 30.72% | 2136.4 | routed |
| 30 | 30.0 | 31.31% | 2142.3 | routed |
| 40 | 40.0 | 31.68% | 2160.1 | routed |
| 50 | 50.0 | 32.61% | 2172.0 | routed |
| 60 | 60.0 | 33.22% | 2183.8 | routed |
| 70 | 70.0 | 33.89% | 2195.7 | routed |
| 80 | 80.0 | 34.39% | 2213.5 | routed |
| 90 | 90.0 | 34.97% | 2237.3 | routed |
| 100 | 100.0 | 35.66% | 2249.1 | routed |
| 125 | 125.0 | 37.15% | 2308.5 | routed |
| 150 | 150.0 | 38.45% | 2344.1 | routed |
| 175 | 175.0 | 39.44% | 2379.7 | routed |
| 200 | 200.0 | 40.26% | 2421.2 | routed |
| 250 | 250.0 | 41.69% | 2528.0 | routed |
| 300 | 300.0 | 42.83% | 2623.0 | routed |
| 500 | 500.0 | 46.50% | 3002.8 | routed |
| 750 | 750.0 | 50.27% | 3477.5 | routed |
| 1000 | 1000.0 | 52.77% | 3904.8 | routed |
| 1250 | 1250.0 | 54.48% | 4433.0 | routed |
| 1500 | 1500.0 | 55.97% | 5287.5 | routed |
| 1750 | 1750.0 | 57.02% | 5744.5 | routed |
| 2000 | 2000.0 | 57.98% | 6171.7 | routed |
| 2250 | 2250.0 | 58.78% | 6682.1 | routed |
| 2500 | 2500.0 | 59.62% | 7192.4 | routed |
| 3000 | 3000.0 | 60.63% | 7969.8 | routed |
| 4000 | 4000.0 | 62.08% | 9857.0 | routed |
| 5000 | 5000.0 | 63.01% | 11934.0 | routed |
| 6000 | 6000.0 | 63.67% | 13868.6 | routed |
| 7500 | 7500.0 | 64.55% | 16509.4 | routed |
| 10000 | 10000.0 | 65.57% | 20645.6 | routed |
| 15000 | 15000.0 | 67.27% | 29476.0 | routed |
| 20000 | 20000.0 | 68.15% | 38264.8 | routed |
| 25000 | 25000.0 | 68.84% | 46804.3 | routed |
