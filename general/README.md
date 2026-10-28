# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (127,227 features) extracted from cleave reports.
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
- Calibration corpus: 21,220,121 rows (3,066,848 malware, 18,153,273 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 40.05% | 0.00 | routed |
| 1 | 1.0 | 40.17% | 11310.8 | routed |
| 2 | 2.0 | 40.18% | 11310.8 | routed |
| 3 | 3.0 | 40.19% | 11310.8 | routed |
| 4 | 4.0 | 40.19% | 11310.8 | routed |
| 5 | 5.0 | 40.21% | 11310.8 | routed |
| 10 | 10.0 | 40.25% | 11310.8 | routed |
| 15 | 15.0 | 40.29% | 11310.8 | routed |
| 20 | 20.0 | 40.35% | 11310.8 | routed |
| 25 | 25.0 | 40.39% | 11310.8 | routed |
| 30 | 30.0 | 40.44% | 11310.8 | routed |
| 40 | 40.0 | 40.52% | 11310.8 | routed |
| 50 | 50.0 | 40.63% | 11310.8 | routed |
| 60 | 60.0 | 40.88% | 11310.8 | routed |
| 70 | 70.0 | 41.36% | 11310.8 | routed |
| 80 | 80.0 | 42.06% | 11310.8 | routed |
| 90 | 90.0 | 42.74% | 11310.8 | routed |
| 100 | 100.0 | 42.96% | 11310.8 | routed |
| 125 | 125.0 | 43.67% | 11310.8 | routed |
| 150 | 150.0 | 44.15% | 11355.0 | routed |
| 175 | 175.0 | 44.97% | 11355.0 | routed |
| 200 | 200.0 | 45.23% | 11399.1 | routed |
| 250 | 250.0 | 45.93% | 11443.3 | routed |
| 300 | 300.0 | 46.35% | 11487.5 | routed |
| 500 | 500.0 | 47.94% | 11664.2 | routed |
| 750 | 750.0 | 50.14% | 12061.9 | routed |
| 1000 | 1000.0 | 51.20% | 12415.4 | routed |
| 1250 | 1250.0 | 55.24% | 12768.8 | routed |
| 1500 | 1500.0 | 56.41% | 13210.6 | routed |
| 1750 | 1750.0 | 57.49% | 13740.8 | routed |
| 2000 | 2000.0 | 58.21% | 14359.4 | routed |
| 2250 | 2250.0 | 58.77% | 14757.0 | routed |
| 2500 | 2500.0 | 59.45% | 15154.7 | routed |
| 3000 | 3000.0 | 60.49% | 15950.0 | routed |
| 4000 | 4000.0 | 62.05% | 18424.2 | routed |
| 5000 | 5000.0 | 63.24% | 20103.1 | routed |
| 6000 | 6000.0 | 64.14% | 22047.2 | routed |
| 7500 | 7500.0 | 65.12% | 24963.3 | routed |
| 10000 | 10000.0 | 66.06% | 30441.9 | routed |
| 15000 | 15000.0 | 67.18% | 41045.8 | routed |
| 20000 | 20000.0 | 67.93% | 50589.2 | routed |
| 25000 | 25000.0 | 68.54% | 60839.6 | routed |
