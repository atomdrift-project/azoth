# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,228 features) extracted from cleave reports.
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
- Calibration corpus: 17,606,816 rows (2,679,214 malware, 14,927,602 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 37.33% | 0.00 | routed |
| 1 | 1.0 | 37.46% | 2605.9 | routed |
| 2 | 2.0 | 37.52% | 2605.9 | routed |
| 3 | 3.0 | 37.58% | 2605.9 | routed |
| 4 | 4.0 | 37.65% | 2605.9 | routed |
| 5 | 5.0 | 37.74% | 2605.9 | routed |
| 10 | 10.0 | 37.96% | 2612.6 | routed |
| 15 | 15.0 | 38.28% | 2619.3 | routed |
| 20 | 20.0 | 38.79% | 2619.3 | routed |
| 25 | 25.0 | 39.07% | 2626.0 | routed |
| 30 | 30.0 | 39.24% | 2632.7 | routed |
| 40 | 40.0 | 39.49% | 2646.1 | routed |
| 50 | 50.0 | 39.83% | 2652.8 | routed |
| 60 | 60.0 | 40.54% | 2659.5 | routed |
| 70 | 70.0 | 40.93% | 2686.3 | routed |
| 80 | 80.0 | 41.31% | 2699.7 | routed |
| 90 | 90.0 | 41.57% | 2733.2 | routed |
| 100 | 100.0 | 41.87% | 2760.0 | routed |
| 125 | 125.0 | 42.73% | 2806.9 | routed |
| 150 | 150.0 | 43.47% | 2860.5 | routed |
| 175 | 175.0 | 44.34% | 2900.7 | routed |
| 200 | 200.0 | 45.21% | 2947.6 | routed |
| 250 | 250.0 | 46.43% | 3041.3 | routed |
| 300 | 300.0 | 47.47% | 3121.7 | routed |
| 500 | 500.0 | 52.07% | 3557.2 | routed |
| 750 | 750.0 | 54.86% | 3202.1 | routed |
| 1000 | 1000.0 | 57.78% | 3624.2 | routed |
| 1250 | 1250.0 | 60.12% | 4166.8 | routed |
| 1500 | 1500.0 | 61.46% | 4702.7 | routed |
| 1750 | 1750.0 | 62.41% | 5138.1 | routed |
| 2000 | 2000.0 | 63.18% | 5640.6 | routed |
| 2250 | 2250.0 | 63.87% | 6029.1 | routed |
| 2500 | 2500.0 | 64.44% | 6524.8 | routed |
| 3000 | 3000.0 | 65.45% | 7576.6 | routed |
| 4000 | 4000.0 | 66.81% | 9378.6 | routed |
| 5000 | 5000.0 | 67.78% | 11435.2 | routed |
| 6000 | 6000.0 | 68.70% | 13109.9 | routed |
| 7500 | 7500.0 | 69.49% | 15514.9 | routed |
| 10000 | 10000.0 | 70.39% | 20130.5 | routed |
| 15000 | 15000.0 | 71.79% | 29067.0 | routed |
| 20000 | 20000.0 | 73.48% | 37862.7 | routed |
| 25000 | 25000.0 | 75.56% | 46799.2 | routed |
