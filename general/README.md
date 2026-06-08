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
| 0 | - | 60.88% | 0.00 | routed |
| 1 | 1.0 | 60.92% | 1827128.4 | routed |
| 2 | 2.0 | 60.92% | 1827128.4 | routed |
| 3 | 3.0 | 60.92% | 1827128.4 | routed |
| 4 | 4.0 | 60.92% | 1827128.4 | routed |
| 5 | 5.0 | 60.92% | 1827128.4 | routed |
| 10 | 10.0 | 62.02% | 1982458.0 | routed |
| 20 | 20.0 | 63.41% | 1997772.2 | routed |
| 30 | 30.0 | 65.18% | 2009804.7 | routed |
| 40 | 40.0 | 66.97% | 2269781.3 | routed |
| 50 | 50.0 | 67.82% | 2285460.1 | routed |
| 60 | 60.0 | 75.16% | 2297492.7 | routed |
| 70 | 70.0 | 75.80% | 2625289.2 | routed |
| 80 | 80.0 | 75.89% | 2634951.7 | routed |
| 90 | 90.0 | 76.61% | 2681805.8 | routed |
| 100 | 100.0 | 77.18% | 2691650.7 | routed |
| 200 | 200.0 | 80.27% | 2785541.2 | routed |
| 300 | 300.0 | 81.59% | 2878702.5 | routed |
| 500 | 500.0 | 83.95% | 3038225.3 | routed |
| 1000 | 1000.0 | 86.05% | 3495098.5 | routed |
| 2000 | 2000.0 | 88.63% | 3924989.7 | routed |
| 5000 | 5000.0 | 90.59% | 3914233.3 | routed |
| 7500 | 7500.0 | 81.79% | 3294555.6 | routed |
| 10000 | 10000.0 | 82.86% | 3170036.7 | routed |
| 15000 | 15000.0 | 83.76% | 3023458.1 | routed |
| 20000 | 20000.0 | 84.05% | 2923368.9 | routed |
| 25000 | 25000.0 | 84.70% | 2889276.6 | routed |
