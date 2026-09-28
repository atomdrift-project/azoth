# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (6,391 features) extracted from cleave reports.
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
- Calibration corpus: 19,922,689 rows (2,963,955 malware, 16,958,734 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 27.95% | 0.00 | routed |
| 1 | 1.0 | 28.25% | 2063.8 | routed |
| 2 | 2.0 | 28.35% | 2063.8 | routed |
| 3 | 3.0 | 28.42% | 2063.8 | routed |
| 4 | 4.0 | 28.50% | 2063.8 | routed |
| 5 | 5.0 | 28.58% | 2063.8 | routed |
| 10 | 10.0 | 28.92% | 2069.7 | routed |
| 15 | 15.0 | 29.21% | 2075.6 | routed |
| 20 | 20.0 | 29.59% | 2081.5 | routed |
| 25 | 25.0 | 30.04% | 2087.4 | routed |
| 30 | 30.0 | 30.50% | 2087.4 | routed |
| 40 | 40.0 | 31.73% | 2099.2 | routed |
| 50 | 50.0 | 32.56% | 2111.0 | routed |
| 60 | 60.0 | 33.39% | 2122.8 | routed |
| 70 | 70.0 | 34.11% | 2140.5 | routed |
| 80 | 80.0 | 34.73% | 2152.3 | routed |
| 90 | 90.0 | 35.30% | 2170.0 | routed |
| 100 | 100.0 | 35.87% | 2175.9 | routed |
| 125 | 125.0 | 36.99% | 2217.1 | routed |
| 150 | 150.0 | 38.07% | 2246.6 | routed |
| 175 | 175.0 | 39.08% | 2317.4 | routed |
| 200 | 200.0 | 39.85% | 2346.9 | routed |
| 250 | 250.0 | 41.18% | 2453.0 | routed |
| 300 | 300.0 | 42.24% | 2535.6 | routed |
| 500 | 500.0 | 45.95% | 2865.8 | routed |
| 750 | 750.0 | 49.82% | 3319.8 | routed |
| 1000 | 1000.0 | 52.43% | 3768.0 | routed |
| 1250 | 1250.0 | 54.12% | 4186.6 | routed |
| 1500 | 1500.0 | 55.44% | 4699.6 | routed |
| 1750 | 1750.0 | 56.67% | 5153.7 | routed |
| 2000 | 2000.0 | 57.68% | 5584.1 | routed |
| 2250 | 2250.0 | 58.51% | 5985.1 | routed |
| 2500 | 2500.0 | 59.24% | 6504.0 | routed |
| 3000 | 3000.0 | 60.42% | 7359.0 | routed |
| 4000 | 4000.0 | 61.87% | 9010.1 | routed |
| 5000 | 5000.0 | 62.80% | 10643.5 | routed |
| 6000 | 6000.0 | 63.50% | 12459.7 | routed |
| 7500 | 7500.0 | 64.30% | 15160.3 | routed |
| 10000 | 10000.0 | 65.37% | 19347.0 | routed |
| 15000 | 15000.0 | 66.75% | 27962.0 | routed |
| 20000 | 20000.0 | 67.53% | 36105.3 | routed |
| 25000 | 25000.0 | 68.11% | 45050.5 | routed |
