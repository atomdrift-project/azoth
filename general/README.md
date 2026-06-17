# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,413 features) extracted from cleave reports.
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
- Calibration corpus: 8,028,377 rows (2,619,304 malware, 5,409,073 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 57.82% | 0.00 | routed |
| 1 | 1.0 | 57.92% | 507386.6 | routed |
| 2 | 2.0 | 57.92% | 507386.6 | routed |
| 3 | 3.0 | 57.92% | 507386.6 | routed |
| 4 | 4.0 | 57.92% | 507386.6 | routed |
| 5 | 5.0 | 57.92% | 507386.6 | routed |
| 10 | 10.0 | 66.42% | 513157.4 | routed |
| 20 | 20.0 | 68.40% | 525586.8 | routed |
| 30 | 30.0 | 69.33% | 537128.4 | routed |
| 40 | 40.0 | 69.75% | 834546.7 | routed |
| 50 | 50.0 | 70.91% | 848899.7 | routed |
| 60 | 60.0 | 71.41% | 866952.0 | routed |
| 70 | 70.0 | 71.71% | 875978.1 | routed |
| 80 | 80.0 | 72.31% | 886188.0 | routed |
| 90 | 90.0 | 72.59% | 894622.2 | routed |
| 100 | 100.0 | 72.93% | 902464.6 | routed |
| 200 | 200.0 | 73.99% | 1191596.5 | routed |
| 300 | 300.0 | 75.12% | 1266469.0 | routed |
| 500 | 500.0 | 76.23% | 1428495.3 | routed |
| 1000 | 1000.0 | 77.63% | 1661546.9 | routed |
| 2000 | 2000.0 | 79.00% | 2426992.0 | routed |
| 5000 | 5000.0 | 70.59% | 2161683.1 | routed |
| 7500 | 7500.0 | 71.87% | 1924932.2 | routed |
| 10000 | 10000.0 | 72.80% | 1551901.7 | routed |
| 15000 | 15000.0 | 73.96% | 1343561.0 | routed |
| 20000 | 20000.0 | 74.84% | 1310415.9 | routed |
| 25000 | 25000.0 | 75.38% | 1080027.7 | routed |
