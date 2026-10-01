# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (6,307 features) extracted from cleave reports.
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
- Calibration corpus: 19,975,007 rows (2,965,083 malware, 17,009,924 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 26.01% | 0.00 | routed |
| 1 | 1.0 | 26.22% | 1587.3 | routed |
| 2 | 2.0 | 26.56% | 1587.3 | routed |
| 3 | 3.0 | 26.71% | 1587.3 | routed |
| 4 | 4.0 | 26.85% | 1587.3 | routed |
| 5 | 5.0 | 26.96% | 1587.3 | routed |
| 10 | 10.0 | 27.35% | 1593.2 | routed |
| 15 | 15.0 | 27.89% | 1599.1 | routed |
| 20 | 20.0 | 28.33% | 1599.1 | routed |
| 25 | 25.0 | 28.75% | 1604.9 | routed |
| 30 | 30.0 | 29.79% | 1610.8 | routed |
| 40 | 40.0 | 30.76% | 1628.5 | routed |
| 50 | 50.0 | 31.34% | 1640.2 | routed |
| 60 | 60.0 | 32.24% | 1657.9 | routed |
| 70 | 70.0 | 32.98% | 1669.6 | routed |
| 80 | 80.0 | 33.60% | 1675.5 | routed |
| 90 | 90.0 | 34.20% | 1716.6 | routed |
| 100 | 100.0 | 34.76% | 1728.4 | routed |
| 125 | 125.0 | 35.95% | 1787.2 | routed |
| 150 | 150.0 | 36.97% | 1828.3 | routed |
| 175 | 175.0 | 37.92% | 1881.3 | routed |
| 200 | 200.0 | 38.78% | 1904.8 | routed |
| 250 | 250.0 | 40.41% | 2022.3 | routed |
| 300 | 300.0 | 41.53% | 2122.3 | routed |
| 500 | 500.0 | 46.39% | 2557.3 | routed |
| 750 | 750.0 | 50.22% | 3104.1 | routed |
| 1000 | 1000.0 | 53.00% | 3556.7 | routed |
| 1250 | 1250.0 | 54.91% | 4144.6 | routed |
| 1500 | 1500.0 | 56.49% | 4603.2 | routed |
| 1750 | 1750.0 | 57.53% | 5079.4 | routed |
| 2000 | 2000.0 | 58.46% | 5490.9 | routed |
| 2250 | 2250.0 | 59.23% | 6114.1 | routed |
| 2500 | 2500.0 | 59.90% | 6531.5 | routed |
| 3000 | 3000.0 | 61.02% | 7507.4 | routed |
| 4000 | 4000.0 | 62.41% | 9394.5 | routed |
| 5000 | 5000.0 | 63.29% | 12298.7 | routed |
| 6000 | 6000.0 | 63.91% | 13427.5 | routed |
| 7500 | 7500.0 | 64.77% | 15996.5 | routed |
| 10000 | 10000.0 | 65.68% | 20846.7 | routed |
| 15000 | 15000.0 | 66.84% | 29688.6 | routed |
| 20000 | 20000.0 | 67.63% | 36884.4 | routed |
| 25000 | 25000.0 | 68.17% | 45079.6 | routed |
