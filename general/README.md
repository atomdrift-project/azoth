# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (80,203 features) extracted from cleave reports.
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
- Calibration corpus: 6,899,010 rows (2,511,611 malware, 4,387,399 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 64.65% | 0.00 | routed |
| 1 | 1.0 | 64.73% | 17702653.2 | routed |
| 2 | 2.0 | 64.73% | 17702653.2 | routed |
| 3 | 3.0 | 64.73% | 17702653.2 | routed |
| 4 | 4.0 | 64.73% | 17702653.2 | routed |
| 5 | 5.0 | 64.73% | 17702653.2 | routed |
| 10 | 10.0 | 65.09% | 17857253.5 | routed |
| 20 | 20.0 | 67.05% | 17872203.1 | routed |
| 30 | 30.0 | 68.43% | 17884235.7 | routed |
| 40 | 40.0 | 69.55% | 18143665.3 | routed |
| 50 | 50.0 | 70.08% | 18159344.1 | routed |
| 60 | 60.0 | 70.33% | 18170100.5 | routed |
| 70 | 70.0 | 71.06% | 18181586.1 | routed |
| 80 | 80.0 | 71.23% | 18800899.2 | routed |
| 90 | 90.0 | 71.26% | 18847571.0 | routed |
| 100 | 100.0 | 71.50% | 18859785.9 | routed |
| 200 | 200.0 | 72.92% | 18949300.9 | routed |
| 300 | 300.0 | 73.79% | 19041368.4 | routed |
| 500 | 500.0 | 75.43% | 19199250.3 | routed |
| 1000 | 1000.0 | 77.53% | 19665239.2 | routed |
| 2000 | 2000.0 | 79.98% | 20109168.3 | routed |
| 5000 | 5000.0 | 82.26% | 20104428.2 | routed |
| 7500 | 7500.0 | 74.18% | 19478369.6 | routed |
| 10000 | 10000.0 | 75.14% | 19353668.4 | routed |
