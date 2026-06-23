# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,341 features) extracted from cleave reports.
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
- Calibration corpus: 8,312,102 rows (2,614,009 malware, 5,698,093 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 57.45% | 0.00 | routed |
| 1 | 1.0 | 57.58% | 1793102.1 | routed |
| 2 | 2.0 | 57.58% | 1793102.1 | routed |
| 3 | 3.0 | 57.58% | 1793102.1 | routed |
| 4 | 4.0 | 57.59% | 1793102.1 | routed |
| 5 | 5.0 | 57.59% | 1793102.1 | routed |
| 10 | 10.0 | 60.80% | 1798299.9 | routed |
| 20 | 20.0 | 68.77% | 2221991.2 | routed |
| 30 | 30.0 | 70.56% | 2666895.2 | routed |
| 40 | 40.0 | 71.23% | 2681224.3 | routed |
| 50 | 50.0 | 71.49% | 2688950.7 | routed |
| 60 | 60.0 | 71.78% | 2702717.9 | routed |
| 70 | 70.0 | 72.32% | 2712130.1 | routed |
| 80 | 80.0 | 72.54% | 2719294.7 | routed |
| 90 | 90.0 | 73.00% | 2727583.1 | routed |
| 100 | 100.0 | 73.15% | 2734185.7 | routed |
| 200 | 200.0 | 74.19% | 3799876.1 | routed |
| 300 | 300.0 | 75.24% | 4063278.4 | routed |
| 500 | 500.0 | 76.47% | 4166813.0 | routed |
| 1000 | 1000.0 | 78.35% | 4357024.6 | routed |
| 2000 | 2000.0 | 79.98% | 4633913.0 | routed |
| 5000 | 5000.0 | 70.10% | 4541757.3 | routed |
| 7500 | 7500.0 | 72.31% | 4158524.6 | routed |
| 10000 | 10000.0 | 73.33% | 4162317.6 | routed |
| 15000 | 15000.0 | 74.44% | 3184989.9 | routed |
| 20000 | 20000.0 | 75.34% | 2993373.5 | routed |
| 25000 | 25000.0 | 76.08% | 2696536.7 | routed |
