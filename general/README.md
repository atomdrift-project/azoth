# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,276 features) extracted from cleave reports.
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
- Calibration corpus: 16,054,337 rows (2,665,816 malware, 13,388,521 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 37.10% | 0.00 | routed |
| 1 | 1.0 | 37.33% | 3704.7 | routed |
| 2 | 2.0 | 37.43% | 3704.7 | routed |
| 3 | 3.0 | 37.54% | 3704.7 | routed |
| 4 | 4.0 | 37.64% | 3704.7 | routed |
| 5 | 5.0 | 37.82% | 3704.7 | routed |
| 10 | 10.0 | 39.01% | 3712.1 | routed |
| 15 | 15.0 | 39.24% | 3712.1 | routed |
| 20 | 20.0 | 39.36% | 3727.1 | routed |
| 25 | 25.0 | 39.45% | 3727.1 | routed |
| 30 | 30.0 | 39.60% | 3727.1 | routed |
| 40 | 40.0 | 39.99% | 3756.9 | routed |
| 50 | 50.0 | 40.44% | 3764.4 | routed |
| 60 | 60.0 | 42.20% | 3771.9 | routed |
| 70 | 70.0 | 42.98% | 3786.8 | routed |
| 80 | 80.0 | 43.45% | 3816.7 | routed |
| 90 | 90.0 | 43.90% | 3816.7 | routed |
| 100 | 100.0 | 44.32% | 3831.6 | routed |
| 125 | 125.0 | 45.46% | 3869.0 | routed |
| 150 | 150.0 | 46.35% | 3921.3 | routed |
| 175 | 175.0 | 47.28% | 3981.0 | routed |
| 200 | 200.0 | 48.12% | 4010.9 | routed |
| 250 | 250.0 | 49.72% | 4122.9 | routed |
| 300 | 300.0 | 50.83% | 4205.1 | routed |
| 500 | 500.0 | 54.69% | 4541.2 | routed |
| 750 | 750.0 | 58.65% | 5049.1 | routed |
| 1000 | 1000.0 | 61.00% | 5482.3 | routed |
| 1250 | 1250.0 | 62.90% | 5952.9 | routed |
| 1500 | 1500.0 | 64.43% | 6326.3 | routed |
| 1750 | 1750.0 | 65.41% | 6811.8 | routed |
| 2000 | 2000.0 | 66.37% | 7342.1 | routed |
| 2250 | 2250.0 | 67.23% | 7745.4 | routed |
| 2500 | 2500.0 | 67.90% | 8118.9 | routed |
| 3000 | 3000.0 | 68.92% | 9037.6 | routed |
| 4000 | 4000.0 | 70.40% | 10972.1 | routed |
| 5000 | 5000.0 | 71.40% | 12675.0 | routed |
| 6000 | 6000.0 | 72.08% | 14594.6 | routed |
| 7500 | 7500.0 | 72.90% | 17373.1 | routed |
| 10000 | 10000.0 | 73.87% | 21667.8 | routed |
| 15000 | 15000.0 | 75.14% | 32117.1 | routed |
| 20000 | 20000.0 | 76.10% | 41087.4 | routed |
| 25000 | 25000.0 | 76.68% | 47010.4 | routed |
