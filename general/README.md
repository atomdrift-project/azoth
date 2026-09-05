# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,230 features) extracted from cleave reports.
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
- Calibration corpus: 17,755,836 rows (2,694,836 malware, 15,061,000 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 34.16% | 0.00 | routed |
| 1 | 1.0 | 34.39% | 1560.3 | routed |
| 2 | 2.0 | 34.46% | 1560.3 | routed |
| 3 | 3.0 | 34.59% | 1560.3 | routed |
| 4 | 4.0 | 34.68% | 1560.3 | routed |
| 5 | 5.0 | 34.76% | 1560.3 | routed |
| 10 | 10.0 | 35.12% | 1567.0 | routed |
| 15 | 15.0 | 35.41% | 1573.6 | routed |
| 20 | 20.0 | 35.82% | 1573.6 | routed |
| 25 | 25.0 | 36.21% | 1580.2 | routed |
| 30 | 30.0 | 36.56% | 1586.9 | routed |
| 40 | 40.0 | 37.56% | 1606.8 | routed |
| 50 | 50.0 | 38.12% | 1620.1 | routed |
| 60 | 60.0 | 38.94% | 1626.7 | routed |
| 70 | 70.0 | 39.65% | 1653.3 | routed |
| 80 | 80.0 | 40.31% | 1659.9 | routed |
| 90 | 90.0 | 40.83% | 1686.5 | routed |
| 100 | 100.0 | 41.61% | 1699.8 | routed |
| 125 | 125.0 | 43.22% | 1766.2 | routed |
| 150 | 150.0 | 44.25% | 1812.6 | routed |
| 175 | 175.0 | 45.05% | 1839.2 | routed |
| 200 | 200.0 | 45.74% | 1859.1 | routed |
| 250 | 250.0 | 46.82% | 1972.0 | routed |
| 300 | 300.0 | 47.71% | 2051.7 | routed |
| 500 | 500.0 | 51.62% | 2377.0 | routed |
| 750 | 750.0 | 55.44% | 2795.3 | routed |
| 1000 | 1000.0 | 57.59% | 3260.1 | routed |
| 1250 | 1250.0 | 59.22% | 3704.9 | routed |
| 1500 | 1500.0 | 60.44% | 4136.5 | routed |
| 1750 | 1750.0 | 61.41% | 4475.1 | routed |
| 2000 | 2000.0 | 62.23% | 4966.5 | routed |
| 2250 | 2250.0 | 62.84% | 5457.8 | routed |
| 2500 | 2500.0 | 63.37% | 5869.5 | routed |
| 3000 | 3000.0 | 64.31% | 6785.7 | routed |
| 4000 | 4000.0 | 65.79% | 8492.1 | routed |
| 5000 | 5000.0 | 66.89% | 10191.9 | routed |
| 6000 | 6000.0 | 67.73% | 11871.7 | routed |
| 7500 | 7500.0 | 68.93% | 14394.8 | routed |
| 10000 | 10000.0 | 70.02% | 18650.8 | routed |
| 15000 | 15000.0 | 71.44% | 26518.8 | routed |
| 20000 | 20000.0 | 75.12% | 35123.8 | routed |
| 25000 | 25000.0 | 75.89% | 42268.1 | routed |
