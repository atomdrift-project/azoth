# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (8,595 features) extracted from cleave reports.
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
- Calibration corpus: 6,720,544 rows (2,496,311 malware, 4,224,233 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 57.78% | 0.00 | routed |
| 1 | 1.0 | 57.82% | 17100114.2 | routed |
| 2 | 2.0 | 57.82% | 17100114.2 | routed |
| 3 | 3.0 | 57.82% | 17100114.2 | routed |
| 4 | 4.0 | 57.82% | 17100114.2 | routed |
| 5 | 5.0 | 57.82% | 17100114.2 | routed |
| 10 | 10.0 | 62.24% | 17248919.5 | routed |
| 20 | 20.0 | 68.65% | 17262929.1 | routed |
| 30 | 30.0 | 69.48% | 17528355.4 | routed |
| 40 | 40.0 | 70.45% | 17549180.5 | routed |
| 50 | 50.0 | 72.03% | 17561107.7 | routed |
| 60 | 60.0 | 72.22% | 17572088.2 | routed |
| 70 | 70.0 | 72.58% | 17586665.8 | routed |
| 80 | 80.0 | 72.95% | 17597267.7 | routed |
| 90 | 90.0 | 73.07% | 17627748.2 | routed |
| 100 | 100.0 | 73.13% | 17638350.1 | routed |
| 200 | 200.0 | 74.64% | 17972310.1 | routed |
| 300 | 300.0 | 75.82% | 18055232.1 | routed |
| 500 | 500.0 | 77.02% | 18223348.0 | routed |
| 1000 | 1000.0 | 78.87% | 20546679.6 | routed |
| 2000 | 2000.0 | 80.45% | 21058978.8 | routed |
| 5000 | 5000.0 | 82.45% | 20904115.2 | routed |
| 7500 | 7500.0 | 72.32% | 20409233.5 | routed |
| 10000 | 10000.0 | 73.60% | 18321983.6 | routed |
