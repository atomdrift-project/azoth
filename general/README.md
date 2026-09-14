# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,164 features) extracted from cleave reports.
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
- Calibration corpus: 19,413,768 rows (2,958,322 malware, 16,455,446 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 28.12% | 0.00 | routed |
| 1 | 1.0 | 28.42% | 2242.4 | routed |
| 2 | 2.0 | 29.32% | 2242.4 | routed |
| 3 | 3.0 | 29.98% | 2242.4 | routed |
| 4 | 4.0 | 30.42% | 2242.4 | routed |
| 5 | 5.0 | 31.29% | 2242.4 | routed |
| 10 | 10.0 | 33.50% | 2248.5 | routed |
| 15 | 15.0 | 34.69% | 2254.6 | routed |
| 20 | 20.0 | 35.09% | 2260.6 | routed |
| 25 | 25.0 | 35.26% | 2260.6 | routed |
| 30 | 30.0 | 35.57% | 2266.7 | routed |
| 40 | 40.0 | 36.62% | 2278.9 | routed |
| 50 | 50.0 | 37.17% | 2285.0 | routed |
| 60 | 60.0 | 37.85% | 2303.2 | routed |
| 70 | 70.0 | 38.75% | 2309.3 | routed |
| 80 | 80.0 | 39.51% | 2327.5 | routed |
| 90 | 90.0 | 40.09% | 2364.0 | routed |
| 100 | 100.0 | 40.65% | 2382.2 | routed |
| 125 | 125.0 | 41.68% | 2430.8 | routed |
| 150 | 150.0 | 42.81% | 2473.3 | routed |
| 175 | 175.0 | 43.96% | 2509.8 | routed |
| 200 | 200.0 | 44.92% | 2546.3 | routed |
| 250 | 250.0 | 46.52% | 2625.3 | routed |
| 300 | 300.0 | 47.91% | 2716.4 | routed |
| 500 | 500.0 | 51.42% | 3154.0 | routed |
| 750 | 750.0 | 54.45% | 3579.4 | routed |
| 1000 | 1000.0 | 56.34% | 4004.8 | routed |
| 1250 | 1250.0 | 57.70% | 4515.2 | routed |
| 1500 | 1500.0 | 58.83% | 5001.4 | routed |
| 1750 | 1750.0 | 59.96% | 5511.9 | routed |
| 2000 | 2000.0 | 60.92% | 5949.4 | routed |
| 2250 | 2250.0 | 61.58% | 6739.4 | routed |
| 2500 | 2500.0 | 62.20% | 7213.4 | routed |
| 3000 | 3000.0 | 63.81% | 8076.4 | routed |
| 4000 | 4000.0 | 65.57% | 9899.5 | routed |
| 5000 | 5000.0 | 66.70% | 12743.5 | routed |
| 6000 | 6000.0 | 67.46% | 14700.3 | routed |
| 7500 | 7500.0 | 68.45% | 17477.5 | routed |
| 10000 | 10000.0 | 69.77% | 21694.9 | routed |
| 15000 | 15000.0 | 71.88% | 29990.1 | routed |
| 20000 | 20000.0 | 73.11% | 37294.6 | routed |
| 25000 | 25000.0 | 73.90% | 44404.8 | routed |
