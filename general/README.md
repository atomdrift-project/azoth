# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,304 features) extracted from cleave reports.
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
- Calibration corpus: 15,612,661 rows (2,667,318 malware, 12,945,343 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 67.55% | 0.00 | routed |
| 1 | 1.0 | 67.56% | 1917.9 | routed |
| 2 | 2.0 | 67.58% | 1917.9 | routed |
| 3 | 3.0 | 67.59% | 1917.9 | routed |
| 4 | 4.0 | 67.61% | 1917.9 | routed |
| 5 | 5.0 | 67.62% | 1917.9 | routed |
| 10 | 10.0 | 67.70% | 1917.9 | routed |
| 15 | 15.0 | 67.75% | 1917.9 | routed |
| 20 | 20.0 | 67.82% | 1917.9 | routed |
| 25 | 25.0 | 67.88% | 1917.9 | routed |
| 30 | 30.0 | 67.96% | 1917.9 | routed |
| 40 | 40.0 | 68.07% | 1917.9 | routed |
| 50 | 50.0 | 68.19% | 1917.9 | routed |
| 60 | 60.0 | 68.28% | 1917.9 | routed |
| 70 | 70.0 | 68.34% | 1979.7 | routed |
| 80 | 80.0 | 68.38% | 1979.7 | routed |
| 90 | 90.0 | 68.44% | 1979.7 | routed |
| 100 | 100.0 | 68.50% | 1979.7 | routed |
| 125 | 125.0 | 68.63% | 1979.7 | routed |
| 150 | 150.0 | 68.76% | 1979.7 | routed |
| 175 | 175.0 | 68.90% | 1979.7 | routed |
| 200 | 200.0 | 69.02% | 2041.6 | routed |
| 250 | 250.0 | 69.26% | 2103.5 | routed |
| 300 | 300.0 | 69.55% | 2165.3 | routed |
| 500 | 500.0 | 70.41% | 2536.5 | routed |
| 750 | 750.0 | 71.39% | 2969.6 | routed |
| 1000 | 1000.0 | 72.16% | 3588.3 | routed |
| 1250 | 1250.0 | 72.40% | 3959.5 | routed |
| 1500 | 1500.0 | 72.53% | 4516.3 | routed |
| 1750 | 1750.0 | 72.70% | 4825.6 | routed |
| 2000 | 2000.0 | 72.92% | 5382.4 | routed |
| 2250 | 2250.0 | 73.10% | 5753.6 | routed |
| 2500 | 2500.0 | 73.23% | 6372.3 | routed |
| 3000 | 3000.0 | 74.40% | 7362.1 | routed |
| 4000 | 4000.0 | 75.50% | 9341.9 | routed |
| 5000 | 5000.0 | 76.04% | 10641.1 | routed |
| 6000 | 6000.0 | 76.53% | 12435.2 | routed |
| 7500 | 7500.0 | 77.06% | 15528.6 | routed |
| 10000 | 10000.0 | 77.50% | 19673.6 | routed |
| 15000 | 15000.0 | 78.31% | 29263.0 | routed |
| 20000 | 20000.0 | 79.03% | 37491.3 | routed |
| 25000 | 25000.0 | 79.42% | 46771.3 | routed |
