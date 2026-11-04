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
- Calibration corpus: 21,277,296 rows (3,067,444 malware, 18,209,852 benign).

| L | Nominal level | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 74.48% | 0.00 | routed |
| 1 | 1.0 | 74.49% | 3655.8 | routed |
| 2 | 2.0 | 74.51% | 3655.8 | routed |
| 3 | 3.0 | 74.54% | 3655.8 | routed |
| 4 | 4.0 | 74.56% | 3655.8 | routed |
| 5 | 5.0 | 74.58% | 3655.8 | routed |
| 10 | 10.0 | 74.66% | 3655.8 | routed |
| 15 | 15.0 | 74.76% | 3655.8 | routed |
| 20 | 20.0 | 74.85% | 3655.8 | routed |
| 25 | 25.0 | 74.97% | 3655.8 | routed |
| 30 | 30.0 | 75.08% | 3655.8 | routed |
| 40 | 40.0 | 75.27% | 3655.8 | routed |
| 50 | 50.0 | 75.51% | 3655.8 | routed |
| 60 | 60.0 | 75.75% | 3655.8 | routed |
| 70 | 70.0 | 76.03% | 3655.8 | routed |
| 80 | 80.0 | 76.26% | 3655.8 | routed |
| 90 | 90.0 | 76.47% | 3699.9 | routed |
| 100 | 100.0 | 76.54% | 3699.9 | routed |
| 125 | 125.0 | 76.70% | 3699.9 | routed |
| 150 | 150.0 | 76.93% | 3743.9 | routed |
| 175 | 175.0 | 77.21% | 3743.9 | routed |
| 200 | 200.0 | 77.53% | 3788.0 | routed |
| 250 | 250.0 | 78.11% | 3832.0 | routed |
| 300 | 300.0 | 78.60% | 3964.2 | routed |
| 500 | 500.0 | 81.08% | 4228.4 | routed |
| 750 | 750.0 | 83.78% | 4668.9 | routed |
| 1000 | 1000.0 | 84.99% | 5153.4 | routed |
| 1250 | 1250.0 | 86.14% | 5505.8 | routed |
| 1500 | 1500.0 | 86.97% | 6034.3 | routed |
| 1750 | 1750.0 | 87.59% | 6562.9 | routed |
| 2000 | 2000.0 | 88.19% | 7135.5 | routed |
| 2250 | 2250.0 | 88.82% | 7620.0 | routed |
| 2500 | 2500.0 | 89.27% | 8280.7 | routed |
| 3000 | 3000.0 | 89.89% | 9381.8 | routed |
| 4000 | 4000.0 | 91.10% | 11980.6 | routed |
| 5000 | 5000.0 | 91.92% | 13786.5 | routed |
| 6000 | 6000.0 | 92.40% | 15680.4 | routed |
| 7500 | 7500.0 | 92.89% | 19204.1 | routed |
| 10000 | 10000.0 | 93.61% | 24754.0 | routed |
| 15000 | 15000.0 | 94.61% | 35721.5 | routed |
| 20000 | 20000.0 | 95.14% | 46644.9 | routed |
| 25000 | 25000.0 | 95.52% | 59110.0 | routed |
