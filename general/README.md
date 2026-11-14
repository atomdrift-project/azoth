# Azoth General

General malware detector used for every routed decision.

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

- Inputs: shared `feature_spec.json` (128,071 features) extracted from cleave reports.
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
- Calibration corpus: 21,325,042 rows (3,081,175 malware, 18,243,867 benign).

| L | Nominal level | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 75.89% | 0.00 | routed |
| 1 | 1.0 | 75.90% | 3824.6 | routed |
| 2 | 2.0 | 75.93% | 3824.6 | routed |
| 3 | 3.0 | 75.95% | 3824.6 | routed |
| 4 | 4.0 | 75.98% | 3824.6 | routed |
| 5 | 5.0 | 76.00% | 3824.6 | routed |
| 10 | 10.0 | 76.13% | 3824.6 | routed |
| 15 | 15.0 | 76.27% | 3824.6 | routed |
| 20 | 20.0 | 76.44% | 3824.6 | routed |
| 25 | 25.0 | 76.59% | 3824.6 | routed |
| 30 | 30.0 | 76.74% | 3824.6 | routed |
| 40 | 40.0 | 77.08% | 3824.6 | routed |
| 50 | 50.0 | 77.39% | 3868.5 | routed |
| 60 | 60.0 | 77.61% | 3868.5 | routed |
| 70 | 70.0 | 77.83% | 3868.5 | routed |
| 80 | 80.0 | 78.03% | 3868.5 | routed |
| 90 | 90.0 | 78.30% | 3912.5 | routed |
| 100 | 100.0 | 78.46% | 3912.5 | routed |
| 125 | 125.0 | 78.85% | 3912.5 | routed |
| 150 | 150.0 | 79.05% | 4000.4 | routed |
| 175 | 175.0 | 79.21% | 4000.4 | routed |
| 200 | 200.0 | 79.41% | 4000.4 | routed |
| 250 | 250.0 | 79.77% | 4044.4 | routed |
| 300 | 300.0 | 80.28% | 4176.3 | routed |
| 500 | 500.0 | 82.59% | 4396.1 | routed |
| 750 | 750.0 | 85.04% | 4835.7 | routed |
| 1000 | 1000.0 | 86.04% | 5319.2 | routed |
| 1250 | 1250.0 | 86.90% | 5802.8 | routed |
| 1500 | 1500.0 | 87.55% | 6462.2 | routed |
| 1750 | 1750.0 | 88.06% | 7033.7 | routed |
| 2000 | 2000.0 | 88.51% | 7649.1 | routed |
| 2250 | 2250.0 | 89.04% | 8088.8 | routed |
| 2500 | 2500.0 | 89.52% | 8704.2 | routed |
| 3000 | 3000.0 | 90.39% | 9627.4 | routed |
| 4000 | 4000.0 | 91.54% | 12001.3 | routed |
| 5000 | 5000.0 | 92.24% | 13979.5 | routed |
| 6000 | 6000.0 | 92.69% | 16353.4 | routed |
| 7500 | 7500.0 | 93.22% | 19430.6 | routed |
| 10000 | 10000.0 | 93.90% | 25497.2 | routed |
| 15000 | 15000.0 | 94.87% | 35652.1 | routed |
| 20000 | 20000.0 | 95.42% | 47917.1 | routed |
| 25000 | 25000.0 | 95.79% | 58467.6 | routed |
