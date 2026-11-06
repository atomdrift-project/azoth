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
- Calibration corpus: 21,277,296 rows (3,065,673 malware, 18,211,623 benign).

| L | Nominal level | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 76.51% | 0.00 | routed |
| 1 | 1.0 | 76.52% | 3567.1 | routed |
| 2 | 2.0 | 76.56% | 3567.1 | routed |
| 3 | 3.0 | 76.59% | 3567.1 | routed |
| 4 | 4.0 | 76.61% | 3567.1 | routed |
| 5 | 5.0 | 76.63% | 3567.1 | routed |
| 10 | 10.0 | 76.76% | 3567.1 | routed |
| 15 | 15.0 | 76.91% | 3567.1 | routed |
| 20 | 20.0 | 77.04% | 3567.1 | routed |
| 25 | 25.0 | 77.15% | 3567.1 | routed |
| 30 | 30.0 | 77.29% | 3567.1 | routed |
| 40 | 40.0 | 77.58% | 3567.1 | routed |
| 50 | 50.0 | 77.79% | 3611.1 | routed |
| 60 | 60.0 | 77.84% | 3611.1 | routed |
| 70 | 70.0 | 77.88% | 3611.1 | routed |
| 80 | 80.0 | 77.93% | 3611.1 | routed |
| 90 | 90.0 | 77.97% | 3655.2 | routed |
| 100 | 100.0 | 78.02% | 3655.2 | routed |
| 125 | 125.0 | 78.14% | 3655.2 | routed |
| 150 | 150.0 | 78.25% | 3699.2 | routed |
| 175 | 175.0 | 78.36% | 3699.2 | routed |
| 200 | 200.0 | 78.61% | 3699.2 | routed |
| 250 | 250.0 | 79.05% | 3743.2 | routed |
| 300 | 300.0 | 79.55% | 3875.4 | routed |
| 500 | 500.0 | 82.37% | 4183.6 | routed |
| 750 | 750.0 | 84.90% | 4535.9 | routed |
| 1000 | 1000.0 | 86.17% | 5284.6 | routed |
| 1250 | 1250.0 | 87.08% | 5636.9 | routed |
| 1500 | 1500.0 | 87.56% | 6341.5 | routed |
| 1750 | 1750.0 | 87.89% | 6914.0 | routed |
| 2000 | 2000.0 | 88.31% | 7662.6 | routed |
| 2250 | 2250.0 | 88.86% | 8014.9 | routed |
| 2500 | 2500.0 | 89.31% | 8631.5 | routed |
| 3000 | 3000.0 | 89.94% | 9600.3 | routed |
| 4000 | 4000.0 | 91.05% | 11934.3 | routed |
| 5000 | 5000.0 | 91.81% | 14004.1 | routed |
| 6000 | 6000.0 | 92.28% | 15897.8 | routed |
| 7500 | 7500.0 | 92.94% | 19641.0 | routed |
| 10000 | 10000.0 | 93.63% | 24617.3 | routed |
| 15000 | 15000.0 | 94.70% | 35891.1 | routed |
| 20000 | 20000.0 | 95.31% | 46416.2 | routed |
| 25000 | 25000.0 | 95.66% | 57998.2 | routed |
