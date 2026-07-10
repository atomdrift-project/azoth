# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,307 features) extracted from cleave reports.
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
- Calibration corpus: 13,597,415 rows (2,653,623 malware, 10,943,792 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 35.32% | 0.00 | routed |
| 1 | 1.0 | 35.48% | 1972515.6 | routed |
| 2 | 2.0 | 35.60% | 1972515.6 | routed |
| 3 | 3.0 | 35.72% | 1972515.6 | routed |
| 4 | 4.0 | 35.84% | 1972515.6 | routed |
| 5 | 5.0 | 36.01% | 1972515.6 | routed |
| 10 | 10.0 | 37.02% | 1972744.0 | routed |
| 15 | 15.0 | 37.32% | 1972945.0 | routed |
| 20 | 20.0 | 37.76% | 1973164.3 | routed |
| 25 | 25.0 | 38.12% | 1973520.7 | routed |
| 30 | 30.0 | 38.36% | 1973721.7 | routed |
| 40 | 40.0 | 38.82% | 1974151.2 | routed |
| 50 | 50.0 | 39.43% | 1974662.9 | routed |
| 60 | 60.0 | 40.61% | 1975549.2 | routed |
| 70 | 70.0 | 41.57% | 1976006.1 | routed |
| 80 | 80.0 | 42.86% | 1976463.0 | routed |
| 90 | 90.0 | 43.13% | 1976855.9 | routed |
| 100 | 100.0 | 43.56% | 1977367.6 | routed |
| 125 | 125.0 | 44.50% | 1983791.4 | routed |
| 150 | 150.0 | 45.29% | 1989941.0 | routed |
| 175 | 175.0 | 45.72% | 1992563.5 | routed |
| 200 | 200.0 | 46.19% | 1993559.5 | routed |
| 250 | 250.0 | 47.57% | 1995204.2 | routed |
| 300 | 300.0 | 48.68% | 2059743.1 | routed |
| 500 | 500.0 | 52.17% | 2107742.9 | routed |
| 750 | 750.0 | 55.89% | 2113938.2 | routed |
| 1000 | 1000.0 | 57.87% | 2119420.8 | routed |
| 1250 | 1250.0 | 59.24% | 2123806.8 | routed |
| 1500 | 1500.0 | 60.80% | 2127178.6 | routed |
| 1750 | 1750.0 | 61.96% | 2129709.7 | routed |
| 2000 | 2000.0 | 62.83% | 2132021.5 | routed |
| 2250 | 2250.0 | 63.52% | 2134205.4 | routed |
| 2500 | 2500.0 | 64.23% | 2138618.9 | routed |
| 3000 | 3000.0 | 65.36% | 2141488.1 | routed |
| 4000 | 4000.0 | 66.78% | 2148533.2 | routed |
| 5000 | 5000.0 | 67.75% | 2145837.6 | routed |
| 6000 | 6000.0 | 68.60% | 2137047.2 | routed |
| 7500 | 7500.0 | 69.45% | 2076729.9 | routed |
| 10000 | 10000.0 | 70.52% | 2033189.2 | routed |
| 15000 | 15000.0 | 71.96% | 2034322.3 | routed |
| 20000 | 20000.0 | 72.99% | 2044839.7 | routed |
| 25000 | 25000.0 | 73.90% | 2042829.4 | routed |
