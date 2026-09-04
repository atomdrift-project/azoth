# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,231 features) extracted from cleave reports.
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
- Calibration corpus: 17,626,984 rows (2,679,336 malware, 14,947,648 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 35.88% | 0.00 | routed |
| 1 | 1.0 | 36.06% | 2589.0 | routed |
| 2 | 2.0 | 36.31% | 2589.0 | routed |
| 3 | 3.0 | 36.51% | 2589.0 | routed |
| 4 | 4.0 | 36.72% | 2589.0 | routed |
| 5 | 5.0 | 36.94% | 2589.0 | routed |
| 10 | 10.0 | 37.63% | 2595.7 | routed |
| 15 | 15.0 | 37.88% | 2602.4 | routed |
| 20 | 20.0 | 38.44% | 2602.4 | routed |
| 25 | 25.0 | 39.17% | 2609.1 | routed |
| 30 | 30.0 | 39.66% | 2615.8 | routed |
| 40 | 40.0 | 40.18% | 2635.9 | routed |
| 50 | 50.0 | 40.38% | 2642.6 | routed |
| 60 | 60.0 | 40.95% | 2649.2 | routed |
| 70 | 70.0 | 41.42% | 2682.7 | routed |
| 80 | 80.0 | 41.80% | 2689.4 | routed |
| 90 | 90.0 | 42.11% | 2702.8 | routed |
| 100 | 100.0 | 42.61% | 2729.5 | routed |
| 125 | 125.0 | 43.67% | 2776.4 | routed |
| 150 | 150.0 | 44.42% | 2809.8 | routed |
| 175 | 175.0 | 45.23% | 2849.9 | routed |
| 200 | 200.0 | 45.94% | 2896.8 | routed |
| 250 | 250.0 | 47.49% | 2970.4 | routed |
| 300 | 300.0 | 48.86% | 3090.8 | routed |
| 500 | 500.0 | 52.17% | 3418.6 | routed |
| 750 | 750.0 | 54.69% | 3860.1 | routed |
| 1000 | 1000.0 | 57.01% | 4321.8 | routed |
| 1250 | 1250.0 | 58.86% | 4803.4 | routed |
| 1500 | 1500.0 | 60.15% | 5198.1 | routed |
| 1750 | 1750.0 | 61.13% | 5592.9 | routed |
| 2000 | 2000.0 | 62.06% | 6128.1 | routed |
| 2250 | 2250.0 | 62.89% | 6656.6 | routed |
| 2500 | 2500.0 | 63.58% | 7024.5 | routed |
| 3000 | 3000.0 | 64.67% | 7867.5 | routed |
| 4000 | 4000.0 | 66.34% | 9573.4 | routed |
| 5000 | 5000.0 | 67.32% | 11399.8 | routed |
| 6000 | 6000.0 | 68.11% | 12978.6 | routed |
| 7500 | 7500.0 | 69.11% | 14952.2 | routed |
| 10000 | 10000.0 | 70.27% | 19046.5 | routed |
| 15000 | 15000.0 | 73.24% | 27649.8 | routed |
| 20000 | 20000.0 | 74.21% | 35510.6 | routed |
| 25000 | 25000.0 | 75.74% | 44127.3 | routed |
