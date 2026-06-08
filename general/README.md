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
| 0 | - | 36.17% | 0.00 | routed |
| 1 | 1.0 | 36.50% | 30268.5 | routed |
| 2 | 2.0 | 36.55% | 30268.5 | routed |
| 3 | 3.0 | 36.59% | 30268.5 | routed |
| 4 | 4.0 | 36.63% | 30268.5 | routed |
| 5 | 5.0 | 36.68% | 30268.5 | routed |
| 10 | 10.0 | 39.09% | 30747.1 | routed |
| 20 | 20.0 | 41.19% | 32000.7 | routed |
| 30 | 30.0 | 43.75% | 32912.4 | routed |
| 40 | 40.0 | 44.69% | 34188.8 | routed |
| 50 | 50.0 | 45.46% | 35465.2 | routed |
| 60 | 60.0 | 46.40% | 36490.9 | routed |
| 70 | 70.0 | 47.25% | 37493.7 | routed |
| 80 | 80.0 | 47.50% | 40775.9 | routed |
| 90 | 90.0 | 47.76% | 41733.2 | routed |
| 100 | 100.0 | 48.03% | 42599.3 | routed |
| 200 | 200.0 | 50.85% | 51374.4 | routed |
| 300 | 300.0 | 51.99% | 63226.5 | routed |
| 500 | 500.0 | 54.98% | 79226.9 | routed |
| 1000 | 1000.0 | 58.82% | 282673.2 | routed |
| 2000 | 2000.0 | 63.34% | 371586.9 | routed |
| 5000 | 5000.0 | 67.40% | 375119.7 | routed |
| 7500 | 7500.0 | 69.58% | 312394.7 | routed |
| 10000 | 10000.0 | 70.14% | 164562.2 | routed |
