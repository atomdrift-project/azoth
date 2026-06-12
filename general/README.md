# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,519 features) extracted from cleave reports.
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
- Calibration corpus: 7,416,064 rows (2,543,560 malware, 4,872,504 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 67.64% | 0.00 | routed |
| 1 | 1.0 | 67.65% | 502690.0 | routed |
| 2 | 2.0 | 67.65% | 502690.0 | routed |
| 3 | 3.0 | 67.66% | 502690.0 | routed |
| 4 | 4.0 | 67.66% | 502690.0 | routed |
| 5 | 5.0 | 67.66% | 502690.0 | routed |
| 10 | 10.0 | 68.88% | 656732.2 | routed |
| 20 | 20.0 | 70.37% | 670691.3 | routed |
| 30 | 30.0 | 70.74% | 681365.8 | routed |
| 40 | 40.0 | 71.56% | 698609.4 | routed |
| 50 | 50.0 | 72.64% | 1028371.4 | routed |
| 60 | 60.0 | 72.85% | 1038224.8 | routed |
| 70 | 70.0 | 73.11% | 1047421.4 | routed |
| 80 | 80.0 | 73.41% | 1055796.8 | routed |
| 90 | 90.0 | 73.46% | 1064336.4 | routed |
| 100 | 100.0 | 73.60% | 1074518.3 | routed |
| 200 | 200.0 | 74.95% | 1471612.2 | routed |
| 300 | 300.0 | 76.12% | 1547483.8 | routed |
| 500 | 500.0 | 77.75% | 2362199.6 | routed |
| 1000 | 1000.0 | 79.17% | 2565837.4 | routed |
| 2000 | 2000.0 | 80.71% | 5424158.0 | routed |
| 5000 | 5000.0 | 74.92% | 4380349.6 | routed |
| 7500 | 7500.0 | 75.87% | 4088359.1 | routed |
| 10000 | 10000.0 | 76.44% | 2474528.8 | routed |
| 15000 | 15000.0 | 77.49% | 2167594.0 | routed |
| 20000 | 20000.0 | 78.41% | 2133106.9 | routed |
| 25000 | 25000.0 | 79.15% | 2141318.1 | routed |
