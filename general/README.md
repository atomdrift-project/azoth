# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (6,212 features) extracted from cleave reports.
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
- Calibration corpus: 20,074,839 rows (2,965,462 malware, 17,109,377 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 24.18% | 0.00 | routed |
| 1 | 1.0 | 24.43% | 1671.6 | routed |
| 2 | 2.0 | 24.49% | 1671.6 | routed |
| 3 | 3.0 | 24.55% | 1671.6 | routed |
| 4 | 4.0 | 24.59% | 1671.6 | routed |
| 5 | 5.0 | 24.64% | 1671.6 | routed |
| 10 | 10.0 | 26.07% | 1677.4 | routed |
| 15 | 15.0 | 26.98% | 1683.3 | routed |
| 20 | 20.0 | 27.77% | 1683.3 | routed |
| 25 | 25.0 | 28.52% | 1689.1 | routed |
| 30 | 30.0 | 29.03% | 1695.0 | routed |
| 40 | 40.0 | 29.55% | 1712.5 | routed |
| 50 | 50.0 | 29.90% | 1724.2 | routed |
| 60 | 60.0 | 30.51% | 1753.4 | routed |
| 70 | 70.0 | 31.22% | 1765.1 | routed |
| 80 | 80.0 | 31.80% | 1771.0 | routed |
| 90 | 90.0 | 32.36% | 1817.7 | routed |
| 100 | 100.0 | 32.91% | 1823.6 | routed |
| 125 | 125.0 | 34.22% | 1870.3 | routed |
| 150 | 150.0 | 35.60% | 1922.9 | routed |
| 175 | 175.0 | 36.86% | 1975.5 | routed |
| 200 | 200.0 | 37.76% | 2004.7 | routed |
| 250 | 250.0 | 39.43% | 2092.4 | routed |
| 300 | 300.0 | 40.96% | 2168.4 | routed |
| 500 | 500.0 | 45.26% | 2630.1 | routed |
| 750 | 750.0 | 49.32% | 3115.3 | routed |
| 1000 | 1000.0 | 51.69% | 3612.1 | routed |
| 1250 | 1250.0 | 53.38% | 4149.8 | routed |
| 1500 | 1500.0 | 54.64% | 4576.4 | routed |
| 1750 | 1750.0 | 55.56% | 5044.0 | routed |
| 2000 | 2000.0 | 56.64% | 5529.1 | routed |
| 2250 | 2250.0 | 57.42% | 5996.7 | routed |
| 2500 | 2500.0 | 58.06% | 6417.5 | routed |
| 3000 | 3000.0 | 59.16% | 7224.1 | routed |
| 4000 | 4000.0 | 60.85% | 9193.8 | routed |
| 5000 | 5000.0 | 62.14% | 11952.5 | routed |
| 6000 | 6000.0 | 63.09% | 13144.8 | routed |
| 7500 | 7500.0 | 64.34% | 15798.4 | routed |
| 10000 | 10000.0 | 65.50% | 20684.6 | routed |
| 15000 | 15000.0 | 66.92% | 29656.3 | routed |
| 20000 | 20000.0 | 67.77% | 37570.0 | routed |
| 25000 | 25000.0 | 68.43% | 45694.2 | routed |
