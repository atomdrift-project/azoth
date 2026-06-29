# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (229 features) extracted from cleave reports.
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
- Calibration corpus: 12,461,279 rows (2,635,645 malware, 9,825,634 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 68.45% | 0.00 | routed |
| 1 | 1.0 | 68.70% | 18956899.8 | routed |
| 2 | 2.0 | 68.70% | 18956899.8 | routed |
| 3 | 3.0 | 68.71% | 18956899.8 | routed |
| 4 | 4.0 | 68.71% | 18956899.8 | routed |
| 5 | 5.0 | 68.72% | 18956899.8 | routed |
| 10 | 10.0 | 70.14% | 19055606.9 | routed |
| 20 | 20.0 | 73.63% | 19063513.3 | routed |
| 30 | 30.0 | 74.48% | 19211777.7 | routed |
| 40 | 40.0 | 74.88% | 19308121.0 | routed |
| 50 | 50.0 | 75.41% | 19312604.0 | routed |
| 60 | 60.0 | 76.15% | 19392808.6 | routed |
| 70 | 70.0 | 76.32% | 19397210.1 | routed |
| 80 | 80.0 | 76.52% | 19403975.3 | routed |
| 90 | 90.0 | 76.57% | 19407724.7 | routed |
| 100 | 100.0 | 76.69% | 19411881.7 | routed |
| 200 | 200.0 | 77.59% | 19939650.9 | routed |
| 300 | 300.0 | 78.04% | 19973069.5 | routed |
| 500 | 500.0 | 78.76% | 20216699.2 | routed |
| 1000 | 1000.0 | 79.67% | 20479891.0 | routed |
| 2000 | 2000.0 | 80.50% | 20628726.0 | routed |
| 5000 | 5000.0 | 76.42% | 20649999.8 | routed |
| 7500 | 7500.0 | 77.67% | 20517385.0 | routed |
| 10000 | 10000.0 | 78.44% | 20317770.1 | routed |
| 15000 | 15000.0 | 79.01% | 20009096.4 | routed |
| 20000 | 20000.0 | 79.44% | 19973314.0 | routed |
| 25000 | 25000.0 | 79.83% | 19486299.2 | routed |
