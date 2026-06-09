# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,527 features) extracted from cleave reports.
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
- Calibration corpus: 7,260,408 rows (2,532,241 malware, 4,728,167 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 65.18% | 0.00 | routed |
| 1 | 1.0 | 65.19% | 499021.9 | routed |
| 2 | 2.0 | 65.19% | 499021.9 | routed |
| 3 | 3.0 | 65.19% | 499021.9 | routed |
| 4 | 4.0 | 65.20% | 499021.9 | routed |
| 5 | 5.0 | 65.20% | 499021.9 | routed |
| 10 | 10.0 | 66.93% | 643195.1 | routed |
| 20 | 20.0 | 68.99% | 661301.3 | routed |
| 30 | 30.0 | 69.92% | 674669.5 | routed |
| 40 | 40.0 | 70.51% | 686514.7 | routed |
| 50 | 50.0 | 70.79% | 700559.8 | routed |
| 60 | 60.0 | 70.99% | 711220.5 | routed |
| 70 | 70.0 | 71.17% | 721373.5 | routed |
| 80 | 80.0 | 71.34% | 960308.4 | routed |
| 90 | 90.0 | 71.73% | 1248316.3 | routed |
| 100 | 100.0 | 71.88% | 1258130.9 | routed |
| 200 | 200.0 | 73.09% | 1349339.0 | routed |
| 300 | 300.0 | 73.79% | 1441731.7 | routed |
| 500 | 500.0 | 74.70% | 1586074.1 | routed |
| 1000 | 1000.0 | 75.76% | 1867651.7 | routed |
| 2000 | 2000.0 | 77.44% | 4365976.5 | routed |
| 5000 | 5000.0 | 79.60% | 4469537.5 | routed |
| 7500 | 7500.0 | 75.92% | 4009097.1 | routed |
| 10000 | 10000.0 | 76.58% | 1762060.1 | routed |
| 15000 | 15000.0 | 77.00% | 1489620.2 | routed |
| 20000 | 20000.0 | 77.71% | 1453238.5 | routed |
| 25000 | 25000.0 | 78.14% | 1462545.4 | routed |
