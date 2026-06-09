# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (7,874 features) extracted from cleave reports.
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
| 0 | - | 60.71% | 0.00 | routed |
| 1 | 1.0 | 60.72% | 496314.4 | routed |
| 2 | 2.0 | 60.72% | 496314.4 | routed |
| 3 | 3.0 | 60.72% | 496314.4 | routed |
| 4 | 4.0 | 60.73% | 496314.4 | routed |
| 5 | 5.0 | 60.73% | 496314.4 | routed |
| 10 | 10.0 | 62.19% | 640995.3 | routed |
| 20 | 20.0 | 67.40% | 658932.3 | routed |
| 30 | 30.0 | 67.83% | 672638.9 | routed |
| 40 | 40.0 | 69.27% | 824596.1 | routed |
| 50 | 50.0 | 70.10% | 838302.7 | routed |
| 60 | 60.0 | 77.27% | 848794.2 | routed |
| 70 | 70.0 | 77.78% | 859116.4 | routed |
| 80 | 80.0 | 78.28% | 1097374.4 | routed |
| 90 | 90.0 | 78.56% | 1107696.7 | routed |
| 100 | 100.0 | 79.44% | 1118018.9 | routed |
| 200 | 200.0 | 82.33% | 1214980.5 | routed |
| 300 | 300.0 | 84.56% | 1296374.0 | routed |
| 500 | 500.0 | 85.90% | 1449684.9 | routed |
| 1000 | 1000.0 | 87.55% | 1816548.1 | routed |
| 2000 | 2000.0 | 89.92% | 2230453.7 | routed |
| 5000 | 5000.0 | 90.85% | 2313031.8 | routed |
| 7500 | 7500.0 | 84.19% | 1857329.5 | routed |
| 10000 | 10000.0 | 85.10% | 1648853.7 | routed |
| 15000 | 15000.0 | 84.38% | 1347985.3 | routed |
| 20000 | 20000.0 | 85.18% | 1310757.5 | routed |
| 25000 | 25000.0 | 85.59% | 1320741.3 | routed |
