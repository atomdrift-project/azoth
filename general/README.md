# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,309 features) extracted from cleave reports.
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
- Calibration corpus: 13,546,141 rows (2,651,358 malware, 10,894,783 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 65.23% | 0.00 | routed |
| 1 | 1.0 | 65.41% | 18376621.8 | routed |
| 2 | 2.0 | 65.41% | 18376621.8 | routed |
| 3 | 3.0 | 65.42% | 18376621.8 | routed |
| 4 | 4.0 | 65.42% | 18376621.8 | routed |
| 5 | 5.0 | 65.43% | 18376621.8 | routed |
| 10 | 10.0 | 67.09% | 18379710.4 | routed |
| 15 | 15.0 | 68.33% | 19749218.8 | routed |
| 20 | 20.0 | 68.41% | 19793047.8 | routed |
| 25 | 25.0 | 68.74% | 20082422.0 | routed |
| 30 | 30.0 | 68.82% | 20085069.4 | routed |
| 40 | 40.0 | 69.75% | 20093158.6 | routed |
| 50 | 50.0 | 70.25% | 20097644.5 | routed |
| 60 | 60.0 | 70.35% | 20102351.0 | routed |
| 70 | 70.0 | 70.62% | 20243177.3 | routed |
| 80 | 80.0 | 70.81% | 20247810.2 | routed |
| 90 | 90.0 | 71.20% | 20329658.6 | routed |
| 100 | 100.0 | 71.35% | 20477471.1 | routed |
| 125 | 125.0 | 71.63% | 20487545.9 | routed |
| 150 | 150.0 | 71.94% | 20497179.4 | routed |
| 175 | 175.0 | 72.20% | 20505121.6 | routed |
| 200 | 200.0 | 72.51% | 22495589.5 | routed |
| 250 | 250.0 | 72.95% | 22509120.6 | routed |
| 300 | 300.0 | 73.17% | 22524122.5 | routed |
| 500 | 500.0 | 74.06% | 22567436.7 | routed |
| 750 | 750.0 | 74.87% | 23108974.6 | routed |
| 1000 | 1000.0 | 75.52% | 23142287.5 | routed |
| 1250 | 1250.0 | 75.94% | 23175527.0 | routed |
| 1500 | 1500.0 | 76.27% | 24118585.3 | routed |
| 1750 | 1750.0 | 76.52% | 24142632.4 | routed |
| 2000 | 2000.0 | 77.06% | 24163885.1 | routed |
| 2250 | 2250.0 | 77.34% | 24182490.3 | routed |
| 2500 | 2500.0 | 77.59% | 24198448.2 | routed |
| 3000 | 3000.0 | 78.09% | 24217641.8 | routed |
| 4000 | 4000.0 | 78.71% | 24247719.0 | routed |
| 5000 | 5000.0 | 74.85% | 20997462.2 | routed |
| 6000 | 6000.0 | 75.16% | 20999006.5 | routed |
| 7500 | 7500.0 | 76.66% | 20654699.0 | routed |
| 10000 | 10000.0 | 77.56% | 20574689.1 | routed |
| 15000 | 15000.0 | 77.91% | 20334953.4 | routed |
| 20000 | 20000.0 | 78.38% | 20302081.7 | routed |
| 25000 | 25000.0 | 79.01% | 20175301.2 | routed |
