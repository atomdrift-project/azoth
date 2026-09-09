# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,195 features) extracted from cleave reports.
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
- Calibration corpus: 18,146,634 rows (2,680,655 malware, 15,465,979 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 40.12% | 0.00 | routed |
| 1 | 1.0 | 40.30% | 1648.8 | routed |
| 2 | 2.0 | 40.35% | 1648.8 | routed |
| 3 | 3.0 | 40.38% | 1648.8 | routed |
| 4 | 4.0 | 40.40% | 1648.8 | routed |
| 5 | 5.0 | 40.77% | 1648.8 | routed |
| 10 | 10.0 | 41.14% | 1655.2 | routed |
| 15 | 15.0 | 41.58% | 1661.7 | routed |
| 20 | 20.0 | 41.74% | 1661.7 | routed |
| 25 | 25.0 | 41.87% | 1668.2 | routed |
| 30 | 30.0 | 42.03% | 1668.2 | routed |
| 40 | 40.0 | 42.77% | 1687.6 | routed |
| 50 | 50.0 | 42.89% | 1694.0 | routed |
| 60 | 60.0 | 43.11% | 1719.9 | routed |
| 70 | 70.0 | 43.49% | 1726.4 | routed |
| 80 | 80.0 | 43.99% | 1745.8 | routed |
| 90 | 90.0 | 44.31% | 1758.7 | routed |
| 100 | 100.0 | 44.69% | 1765.2 | routed |
| 125 | 125.0 | 45.48% | 1823.4 | routed |
| 150 | 150.0 | 46.21% | 1868.6 | routed |
| 175 | 175.0 | 47.09% | 1894.5 | routed |
| 200 | 200.0 | 47.75% | 1933.3 | routed |
| 250 | 250.0 | 48.89% | 2036.7 | routed |
| 300 | 300.0 | 49.72% | 2101.4 | routed |
| 500 | 500.0 | 53.03% | 2437.6 | routed |
| 750 | 750.0 | 55.77% | 2890.2 | routed |
| 1000 | 1000.0 | 57.59% | 3388.1 | routed |
| 1250 | 1250.0 | 59.04% | 3911.8 | routed |
| 1500 | 1500.0 | 60.36% | 4396.7 | routed |
| 1750 | 1750.0 | 61.54% | 4784.7 | routed |
| 2000 | 2000.0 | 62.60% | 5224.4 | routed |
| 2250 | 2250.0 | 63.38% | 5657.6 | routed |
| 2500 | 2500.0 | 63.99% | 6013.2 | routed |
| 3000 | 3000.0 | 64.95% | 7067.1 | routed |
| 4000 | 4000.0 | 66.25% | 8709.4 | routed |
| 5000 | 5000.0 | 67.21% | 10287.1 | routed |
| 6000 | 6000.0 | 67.93% | 12026.4 | routed |
| 7500 | 7500.0 | 68.82% | 14599.8 | routed |
| 10000 | 10000.0 | 70.02% | 18822.0 | routed |
| 15000 | 15000.0 | 72.95% | 27460.3 | routed |
| 20000 | 20000.0 | 74.18% | 34799.0 | routed |
| 25000 | 25000.0 | 75.72% | 41355.3 | routed |
