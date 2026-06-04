# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (21,496 features) extracted from cleave reports.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Calibration corpus: 6,710,141 rows (2,491,517 malware, 4,218,624 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 52.42% | 0.00 | routed |
| 1 | 1.0 | 53.19% | 15792803.5 | routed |
| 2 | 2.0 | 53.19% | 15792803.5 | routed |
| 3 | 3.0 | 53.19% | 15792803.5 | routed |
| 4 | 4.0 | 53.19% | 15792803.5 | routed |
| 5 | 5.0 | 53.19% | 15792803.5 | routed |
| 10 | 10.0 | 53.19% | 15792803.5 | routed |
| 20 | 20.0 | 53.19% | 15792803.5 | routed |
| 30 | 30.0 | 53.50% | 15792827.2 | routed |
| 40 | 40.0 | 53.50% | 15792827.2 | routed |
| 50 | 50.0 | 53.57% | 15792850.9 | routed |
| 60 | 60.0 | 53.57% | 15792850.9 | routed |
| 70 | 70.0 | 53.57% | 15792850.9 | routed |
| 80 | 80.0 | 53.96% | 15792874.6 | routed |
| 90 | 90.0 | 53.96% | 15792874.6 | routed |
| 100 | 100.0 | 54.25% | 15792922.1 | routed |
| 200 | 200.0 | 56.26% | 15793064.3 | routed |
| 300 | 300.0 | 57.32% | 15793159.1 | routed |
| 500 | 500.0 | 58.14% | 15793491.0 | routed |
| 1000 | 1000.0 | 61.46% | 15794391.7 | routed |
| 2000 | 2000.0 | 65.68% | 15796288.1 | routed |
| 5000 | 5000.0 | 69.53% | 15802261.6 | routed |
| 7500 | 7500.0 | 70.87% | 15807144.7 | routed |
| 10000 | 10000.0 | 71.84% | 15812075.2 | routed |
