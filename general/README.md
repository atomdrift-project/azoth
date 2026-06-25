# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,330 features) extracted from cleave reports.
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
- Calibration corpus: 8,638,497 rows (2,614,576 malware, 6,023,921 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 61.55% | 0.00 | routed |
| 1 | 1.0 | 61.62% | 1717414.5 | routed |
| 2 | 2.0 | 61.62% | 1717414.5 | routed |
| 3 | 3.0 | 61.62% | 1717414.5 | routed |
| 4 | 4.0 | 61.62% | 1717414.5 | routed |
| 5 | 5.0 | 61.62% | 1717414.5 | routed |
| 10 | 10.0 | 66.40% | 1722463.4 | routed |
| 20 | 20.0 | 68.76% | 2122387.4 | routed |
| 30 | 30.0 | 69.33% | 2318097.7 | routed |
| 40 | 40.0 | 69.96% | 2586219.5 | routed |
| 50 | 50.0 | 71.00% | 2598044.5 | routed |
| 60 | 60.0 | 71.73% | 2606946.5 | routed |
| 70 | 70.0 | 72.07% | 2613988.3 | routed |
| 80 | 80.0 | 72.23% | 2621030.2 | routed |
| 90 | 90.0 | 72.52% | 2629002.1 | routed |
| 100 | 100.0 | 72.64% | 2635911.0 | routed |
| 200 | 200.0 | 74.16% | 3621371.6 | routed |
| 300 | 300.0 | 75.19% | 3694978.9 | routed |
| 500 | 500.0 | 76.60% | 3788781.7 | routed |
| 1000 | 1000.0 | 78.24% | 4002295.9 | routed |
| 2000 | 2000.0 | 79.59% | 4280382.6 | routed |
| 5000 | 5000.0 | 70.86% | 4387206.2 | routed |
| 7500 | 7500.0 | 72.79% | 3980107.4 | routed |
| 10000 | 10000.0 | 73.68% | 3474954.3 | routed |
| 15000 | 15000.0 | 74.81% | 3279509.7 | routed |
| 20000 | 20000.0 | 75.36% | 3032779.2 | routed |
| 25000 | 25000.0 | 75.89% | 2580107.7 | routed |
