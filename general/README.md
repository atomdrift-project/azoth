# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,194 features) extracted from cleave reports.
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
- Calibration corpus: 18,322,760 rows (2,682,277 malware, 15,640,483 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 39.98% | 0.00 | routed |
| 1 | 1.0 | 40.09% | 1796.6 | routed |
| 2 | 2.0 | 40.17% | 1796.6 | routed |
| 3 | 3.0 | 40.33% | 1796.6 | routed |
| 4 | 4.0 | 40.43% | 1796.6 | routed |
| 5 | 5.0 | 40.51% | 1796.6 | routed |
| 10 | 10.0 | 40.86% | 1803.0 | routed |
| 15 | 15.0 | 41.17% | 1809.4 | routed |
| 20 | 20.0 | 41.34% | 1809.4 | routed |
| 25 | 25.0 | 41.53% | 1815.8 | routed |
| 30 | 30.0 | 41.87% | 1822.2 | routed |
| 40 | 40.0 | 42.45% | 1835.0 | routed |
| 50 | 50.0 | 42.80% | 1841.4 | routed |
| 60 | 60.0 | 43.00% | 1867.0 | routed |
| 70 | 70.0 | 43.20% | 1867.0 | routed |
| 80 | 80.0 | 43.35% | 1873.3 | routed |
| 90 | 90.0 | 43.50% | 1892.5 | routed |
| 100 | 100.0 | 43.94% | 1911.7 | routed |
| 125 | 125.0 | 44.79% | 1956.5 | routed |
| 150 | 150.0 | 45.63% | 1988.4 | routed |
| 175 | 175.0 | 46.35% | 2020.4 | routed |
| 200 | 200.0 | 47.13% | 2058.8 | routed |
| 250 | 250.0 | 48.55% | 2141.9 | routed |
| 300 | 300.0 | 49.83% | 2212.2 | routed |
| 500 | 500.0 | 53.20% | 2570.3 | routed |
| 750 | 750.0 | 55.58% | 2953.9 | routed |
| 1000 | 1000.0 | 57.89% | 3382.2 | routed |
| 1250 | 1250.0 | 59.53% | 3823.4 | routed |
| 1500 | 1500.0 | 60.64% | 4232.6 | routed |
| 1750 | 1750.0 | 61.39% | 4641.8 | routed |
| 2000 | 2000.0 | 62.14% | 5063.8 | routed |
| 2250 | 2250.0 | 62.89% | 5402.6 | routed |
| 2500 | 2500.0 | 63.60% | 5850.2 | routed |
| 3000 | 3000.0 | 64.68% | 6790.1 | routed |
| 4000 | 4000.0 | 65.99% | 8605.9 | routed |
| 5000 | 5000.0 | 66.93% | 9954.9 | routed |
| 6000 | 6000.0 | 67.59% | 11591.7 | routed |
| 7500 | 7500.0 | 68.50% | 13880.6 | routed |
| 10000 | 10000.0 | 69.99% | 18516.1 | routed |
| 15000 | 15000.0 | 72.64% | 26655.2 | routed |
| 20000 | 20000.0 | 73.61% | 34461.9 | routed |
| 25000 | 25000.0 | 74.56% | 40184.2 | routed |
