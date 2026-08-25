# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,072 features) extracted from cleave reports.
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
- Calibration corpus: 17,132,677 rows (2,673,344 malware, 14,459,333 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 37.16% | 0.00 | routed |
| 1 | 1.0 | 37.37% | 2469.0 | routed |
| 2 | 2.0 | 37.49% | 2469.0 | routed |
| 3 | 3.0 | 37.59% | 2469.0 | routed |
| 4 | 4.0 | 37.68% | 2469.0 | routed |
| 5 | 5.0 | 37.82% | 2469.0 | routed |
| 10 | 10.0 | 38.44% | 2475.9 | routed |
| 15 | 15.0 | 39.54% | 2482.8 | routed |
| 20 | 20.0 | 39.67% | 2482.8 | routed |
| 25 | 25.0 | 40.42% | 2482.8 | routed |
| 30 | 30.0 | 41.26% | 2489.7 | routed |
| 40 | 40.0 | 41.79% | 2517.4 | routed |
| 50 | 50.0 | 42.90% | 2524.3 | routed |
| 60 | 60.0 | 43.39% | 2531.2 | routed |
| 70 | 70.0 | 43.84% | 2558.9 | routed |
| 80 | 80.0 | 44.26% | 2565.8 | routed |
| 90 | 90.0 | 44.63% | 2586.6 | routed |
| 100 | 100.0 | 45.02% | 2607.3 | routed |
| 125 | 125.0 | 45.81% | 2635.0 | routed |
| 150 | 150.0 | 46.67% | 2690.3 | routed |
| 175 | 175.0 | 47.39% | 2738.7 | routed |
| 200 | 200.0 | 48.11% | 2801.0 | routed |
| 250 | 250.0 | 49.18% | 2877.0 | routed |
| 300 | 300.0 | 50.15% | 2953.1 | routed |
| 500 | 500.0 | 54.06% | 3430.3 | routed |
| 750 | 750.0 | 57.79% | 3942.1 | routed |
| 1000 | 1000.0 | 60.30% | 4433.1 | routed |
| 1250 | 1250.0 | 62.07% | 4979.5 | routed |
| 1500 | 1500.0 | 63.57% | 5394.4 | routed |
| 1750 | 1750.0 | 64.75% | 5933.9 | routed |
| 2000 | 2000.0 | 65.80% | 6480.2 | routed |
| 2250 | 2250.0 | 66.71% | 7081.9 | routed |
| 2500 | 2500.0 | 67.37% | 7517.6 | routed |
| 3000 | 3000.0 | 68.72% | 8548.1 | routed |
| 4000 | 4000.0 | 70.31% | 10450.0 | routed |
| 5000 | 5000.0 | 71.26% | 13375.4 | routed |
| 6000 | 6000.0 | 72.09% | 15346.5 | routed |
| 7500 | 7500.0 | 72.96% | 19060.4 | routed |
| 10000 | 10000.0 | 74.00% | 22808.8 | routed |
| 15000 | 15000.0 | 75.34% | 32076.2 | routed |
| 20000 | 20000.0 | 76.22% | 38895.3 | routed |
| 25000 | 25000.0 | 76.80% | 46800.2 | routed |
