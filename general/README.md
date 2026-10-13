# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (6,260 features) extracted from cleave reports.
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
- Calibration corpus: 20,801,151 rows (3,078,117 malware, 17,723,034 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 27.97% | 0.00 | routed |
| 1 | 1.0 | 28.16% | 1275.2 | routed |
| 2 | 2.0 | 28.23% | 1275.2 | routed |
| 3 | 3.0 | 28.29% | 1275.2 | routed |
| 4 | 4.0 | 28.36% | 1275.2 | routed |
| 5 | 5.0 | 28.41% | 1275.2 | routed |
| 10 | 10.0 | 28.63% | 1280.8 | routed |
| 15 | 15.0 | 28.80% | 1286.5 | routed |
| 20 | 20.0 | 29.02% | 1286.5 | routed |
| 25 | 25.0 | 29.42% | 1292.1 | routed |
| 30 | 30.0 | 30.33% | 1303.4 | routed |
| 40 | 40.0 | 31.70% | 1309.0 | routed |
| 50 | 50.0 | 32.40% | 1320.3 | routed |
| 60 | 60.0 | 33.08% | 1342.9 | routed |
| 70 | 70.0 | 33.85% | 1359.8 | routed |
| 80 | 80.0 | 34.53% | 1365.5 | routed |
| 90 | 90.0 | 35.10% | 1382.4 | routed |
| 100 | 100.0 | 35.69% | 1405.0 | routed |
| 125 | 125.0 | 37.02% | 1444.4 | routed |
| 150 | 150.0 | 38.29% | 1478.3 | routed |
| 175 | 175.0 | 39.34% | 1534.7 | routed |
| 200 | 200.0 | 40.18% | 1574.2 | routed |
| 250 | 250.0 | 42.28% | 1675.8 | routed |
| 300 | 300.0 | 43.91% | 1737.9 | routed |
| 500 | 500.0 | 47.64% | 2070.8 | routed |
| 750 | 750.0 | 50.77% | 2516.5 | routed |
| 1000 | 1000.0 | 53.05% | 2911.5 | routed |
| 1250 | 1250.0 | 54.70% | 3436.2 | routed |
| 1500 | 1500.0 | 55.96% | 3797.3 | routed |
| 1750 | 1750.0 | 57.18% | 4197.9 | routed |
| 2000 | 2000.0 | 58.05% | 4677.5 | routed |
| 2250 | 2250.0 | 58.79% | 5117.6 | routed |
| 2500 | 2500.0 | 59.39% | 5535.2 | routed |
| 3000 | 3000.0 | 60.44% | 6483.1 | routed |
| 4000 | 4000.0 | 61.89% | 8029.1 | routed |
| 5000 | 5000.0 | 62.92% | 9789.5 | routed |
| 6000 | 6000.0 | 63.66% | 11459.7 | routed |
| 7500 | 7500.0 | 64.54% | 14021.3 | routed |
| 10000 | 10000.0 | 65.48% | 18117.7 | routed |
| 15000 | 15000.0 | 67.08% | 26180.6 | routed |
| 20000 | 20000.0 | 68.25% | 33543.9 | routed |
| 25000 | 25000.0 | 68.94% | 41465.8 | routed |
