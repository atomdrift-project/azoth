# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,245 features) extracted from cleave reports.
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
- Calibration corpus: 17,074,459 rows (2,672,405 malware, 14,402,054 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 74.17% | 0.00 | routed |
| 1 | 1.0 | 74.19% | 4670.4 | routed |
| 2 | 2.0 | 74.19% | 4670.4 | routed |
| 3 | 3.0 | 74.19% | 4670.4 | routed |
| 4 | 4.0 | 74.20% | 4670.4 | routed |
| 5 | 5.0 | 74.20% | 4670.4 | routed |
| 10 | 10.0 | 74.20% | 4670.4 | routed |
| 15 | 15.0 | 74.22% | 4670.4 | routed |
| 20 | 20.0 | 74.23% | 4670.4 | routed |
| 25 | 25.0 | 74.24% | 4670.4 | routed |
| 30 | 30.0 | 74.26% | 4670.4 | routed |
| 40 | 40.0 | 74.28% | 4670.4 | routed |
| 50 | 50.0 | 74.29% | 4670.4 | routed |
| 60 | 60.0 | 74.31% | 4726.0 | routed |
| 70 | 70.0 | 74.33% | 4726.0 | routed |
| 80 | 80.0 | 74.35% | 4726.0 | routed |
| 90 | 90.0 | 74.37% | 4726.0 | routed |
| 100 | 100.0 | 74.38% | 4726.0 | routed |
| 125 | 125.0 | 74.41% | 4781.6 | routed |
| 150 | 150.0 | 74.43% | 4781.6 | routed |
| 175 | 175.0 | 74.47% | 4781.6 | routed |
| 200 | 200.0 | 74.53% | 4781.6 | routed |
| 250 | 250.0 | 74.60% | 4837.2 | routed |
| 300 | 300.0 | 74.64% | 4892.8 | routed |
| 500 | 500.0 | 75.02% | 5115.2 | routed |
| 750 | 750.0 | 75.19% | 5671.2 | routed |
| 1000 | 1000.0 | 75.36% | 6004.8 | routed |
| 1250 | 1250.0 | 75.48% | 6282.8 | routed |
| 1500 | 1500.0 | 75.60% | 6727.6 | routed |
| 1750 | 1750.0 | 75.81% | 7116.8 | routed |
| 2000 | 2000.0 | 75.99% | 7506.0 | routed |
| 2250 | 2250.0 | 76.11% | 8006.4 | routed |
| 2500 | 2500.0 | 76.22% | 8340.0 | routed |
| 3000 | 3000.0 | 76.39% | 9396.4 | routed |
| 4000 | 4000.0 | 76.77% | 10897.6 | routed |
| 5000 | 5000.0 | 77.15% | 12398.8 | routed |
| 6000 | 6000.0 | 77.57% | 14011.2 | routed |
| 7500 | 7500.0 | 77.87% | 15512.4 | routed |
| 10000 | 10000.0 | 78.39% | 20294.0 | routed |
| 15000 | 15000.0 | 79.03% | 28467.2 | routed |
| 20000 | 20000.0 | 79.43% | 35083.6 | routed |
| 25000 | 25000.0 | 79.81% | 43757.2 | routed |
