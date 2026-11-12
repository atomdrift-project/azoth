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
| 0 | - | 75.74% | 0.00 | routed |
| 1 | 1.0 | 75.75% | 4044.4 | routed |
| 2 | 2.0 | 75.76% | 4044.4 | routed |
| 3 | 3.0 | 75.77% | 4044.4 | routed |
| 4 | 4.0 | 75.78% | 4044.4 | routed |
| 5 | 5.0 | 75.80% | 4044.4 | routed |
| 10 | 10.0 | 75.87% | 4044.4 | routed |
| 15 | 15.0 | 75.94% | 4044.4 | routed |
| 20 | 20.0 | 76.02% | 4044.4 | routed |
| 25 | 25.0 | 76.10% | 4044.4 | routed |
| 30 | 30.0 | 76.17% | 4044.4 | routed |
| 40 | 40.0 | 76.33% | 4044.4 | routed |
| 50 | 50.0 | 76.59% | 4044.4 | routed |
| 60 | 60.0 | 77.04% | 4044.4 | routed |
| 70 | 70.0 | 77.48% | 4044.4 | routed |
| 80 | 80.0 | 78.01% | 4044.4 | routed |
| 90 | 90.0 | 78.51% | 4088.3 | routed |
| 100 | 100.0 | 78.64% | 4088.3 | routed |
| 125 | 125.0 | 78.93% | 4088.3 | routed |
| 150 | 150.0 | 79.11% | 4132.3 | routed |
| 175 | 175.0 | 79.26% | 4132.3 | routed |
| 200 | 200.0 | 79.42% | 4176.3 | routed |
| 250 | 250.0 | 79.84% | 4220.2 | routed |
| 300 | 300.0 | 80.22% | 4352.1 | routed |
| 500 | 500.0 | 82.09% | 4659.8 | routed |
| 750 | 750.0 | 84.57% | 5055.5 | routed |
| 1000 | 1000.0 | 85.90% | 5495.1 | routed |
| 1250 | 1250.0 | 86.89% | 6110.5 | routed |
| 1500 | 1500.0 | 87.46% | 6682.0 | routed |
| 1750 | 1750.0 | 88.01% | 7121.6 | routed |
| 2000 | 2000.0 | 88.62% | 7649.1 | routed |
| 2250 | 2250.0 | 89.20% | 8220.6 | routed |
| 2500 | 2500.0 | 89.72% | 8924.0 | routed |
| 3000 | 3000.0 | 90.40% | 9803.2 | routed |
| 4000 | 4000.0 | 91.29% | 12045.2 | routed |
| 5000 | 5000.0 | 92.15% | 13627.8 | routed |
| 6000 | 6000.0 | 92.69% | 16133.5 | routed |
| 7500 | 7500.0 | 93.28% | 19518.5 | routed |
| 10000 | 10000.0 | 93.96% | 24793.8 | routed |
| 15000 | 15000.0 | 94.89% | 35300.4 | routed |
| 20000 | 20000.0 | 95.48% | 47213.7 | routed |
| 25000 | 25000.0 | 95.86% | 57808.2 | routed |
