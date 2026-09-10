# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,177 features) extracted from cleave reports.
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
- Calibration corpus: 18,454,063 rows (2,682,878 malware, 15,771,185 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 37.13% | 0.00 | routed |
| 1 | 1.0 | 37.35% | 1686.6 | routed |
| 2 | 2.0 | 37.48% | 1686.6 | routed |
| 3 | 3.0 | 37.61% | 1686.6 | routed |
| 4 | 4.0 | 37.76% | 1686.6 | routed |
| 5 | 5.0 | 38.01% | 1686.6 | routed |
| 10 | 10.0 | 38.73% | 1686.6 | routed |
| 15 | 15.0 | 39.25% | 1693.0 | routed |
| 20 | 20.0 | 39.56% | 1693.0 | routed |
| 25 | 25.0 | 39.62% | 1693.0 | routed |
| 30 | 30.0 | 39.98% | 1705.6 | routed |
| 40 | 40.0 | 40.51% | 1724.7 | routed |
| 50 | 50.0 | 40.75% | 1731.0 | routed |
| 60 | 60.0 | 41.70% | 1756.4 | routed |
| 70 | 70.0 | 42.10% | 1762.7 | routed |
| 80 | 80.0 | 42.45% | 1775.4 | routed |
| 90 | 90.0 | 42.80% | 1800.8 | routed |
| 100 | 100.0 | 43.28% | 1819.8 | routed |
| 125 | 125.0 | 44.29% | 1870.5 | routed |
| 150 | 150.0 | 45.28% | 1908.5 | routed |
| 175 | 175.0 | 46.34% | 1946.6 | routed |
| 200 | 200.0 | 47.32% | 2003.7 | routed |
| 250 | 250.0 | 48.64% | 2124.1 | routed |
| 300 | 300.0 | 49.66% | 2174.9 | routed |
| 500 | 500.0 | 52.85% | 2568.0 | routed |
| 750 | 750.0 | 55.93% | 3119.6 | routed |
| 1000 | 1000.0 | 58.40% | 3563.5 | routed |
| 1250 | 1250.0 | 59.88% | 4191.2 | routed |
| 1500 | 1500.0 | 60.89% | 4654.1 | routed |
| 1750 | 1750.0 | 61.71% | 5066.2 | routed |
| 2000 | 2000.0 | 62.47% | 5522.7 | routed |
| 2250 | 2250.0 | 63.13% | 5953.9 | routed |
| 2500 | 2500.0 | 63.62% | 6182.2 | routed |
| 3000 | 3000.0 | 64.54% | 7114.2 | routed |
| 4000 | 4000.0 | 65.94% | 8876.9 | routed |
| 5000 | 5000.0 | 66.88% | 10665.0 | routed |
| 6000 | 6000.0 | 67.64% | 12598.9 | routed |
| 7500 | 7500.0 | 68.50% | 15262.0 | routed |
| 10000 | 10000.0 | 69.68% | 19656.1 | routed |
| 15000 | 15000.0 | 71.11% | 28450.6 | routed |
| 20000 | 20000.0 | 72.06% | 37289.5 | routed |
| 25000 | 25000.0 | 73.24% | 44036.0 | routed |
