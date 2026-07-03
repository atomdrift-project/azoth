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
- Calibration corpus: 12,910,342 rows (2,642,872 malware, 10,267,470 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 66.12% | 0.00 | routed |
| 1 | 1.0 | 66.33% | 1527801.9 | routed |
| 2 | 2.0 | 66.33% | 1527801.9 | routed |
| 3 | 3.0 | 66.34% | 1527801.9 | routed |
| 4 | 4.0 | 66.34% | 1527801.9 | routed |
| 5 | 5.0 | 66.35% | 1527801.9 | routed |
| 10 | 10.0 | 72.72% | 1530532.2 | routed |
| 20 | 20.0 | 75.36% | 1539347.2 | routed |
| 30 | 30.0 | 76.05% | 1703711.7 | routed |
| 40 | 40.0 | 76.18% | 1861913.5 | routed |
| 50 | 50.0 | 76.47% | 1866204.0 | routed |
| 60 | 60.0 | 76.55% | 1871196.6 | routed |
| 70 | 70.0 | 76.76% | 1932901.5 | routed |
| 80 | 80.0 | 76.86% | 1936958.0 | routed |
| 90 | 90.0 | 77.07% | 1952403.7 | routed |
| 100 | 100.0 | 77.20% | 1956928.2 | routed |
| 200 | 200.0 | 78.12% | 2285891.3 | routed |
| 300 | 300.0 | 78.54% | 2314130.4 | routed |
| 500 | 500.0 | 79.33% | 3063872.8 | routed |
| 1000 | 1000.0 | 80.24% | 3321145.8 | routed |
| 2000 | 2000.0 | 81.23% | 3442059.4 | routed |
| 5000 | 5000.0 | 78.13% | 3438939.0 | routed |
| 7500 | 7500.0 | 79.15% | 3257490.6 | routed |
| 10000 | 10000.0 | 79.72% | 2926187.3 | routed |
| 15000 | 15000.0 | 80.43% | 14890627.8 | routed |
| 20000 | 20000.0 | 80.90% | 14836099.7 | routed |
| 25000 | 25000.0 | 81.21% | 14788358.3 | routed |
