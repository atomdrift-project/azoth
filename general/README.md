# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,310 features) extracted from cleave reports.
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
- Calibration corpus: 14,692,357 rows (2,661,661 malware, 12,030,696 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 35.42% | 0.00 | routed |
| 1 | 1.0 | 35.54% | 29275.1 | routed |
| 2 | 2.0 | 35.63% | 29275.1 | routed |
| 3 | 3.0 | 35.73% | 29275.1 | routed |
| 4 | 4.0 | 35.81% | 29275.1 | routed |
| 5 | 5.0 | 35.91% | 29275.1 | routed |
| 10 | 10.0 | 36.50% | 29516.2 | routed |
| 15 | 15.0 | 37.16% | 29765.5 | routed |
| 20 | 20.0 | 37.44% | 29973.3 | routed |
| 25 | 25.0 | 37.71% | 30147.9 | routed |
| 30 | 30.0 | 38.04% | 30413.9 | routed |
| 40 | 40.0 | 38.65% | 30854.4 | routed |
| 50 | 50.0 | 39.62% | 31278.3 | routed |
| 60 | 60.0 | 40.05% | 31768.7 | routed |
| 70 | 70.0 | 40.64% | 32342.3 | routed |
| 80 | 80.0 | 41.38% | 34412.0 | routed |
| 90 | 90.0 | 42.00% | 34761.1 | routed |
| 100 | 100.0 | 42.61% | 35135.1 | routed |
| 125 | 125.0 | 43.57% | 36307.1 | routed |
| 150 | 150.0 | 44.11% | 37445.9 | routed |
| 175 | 175.0 | 44.56% | 38385.1 | routed |
| 200 | 200.0 | 45.38% | 39366.0 | routed |
| 250 | 250.0 | 47.11% | 46015.6 | routed |
| 300 | 300.0 | 48.05% | 85971.8 | routed |
| 500 | 500.0 | 52.54% | 92405.3 | routed |
| 750 | 750.0 | 56.14% | 99138.1 | routed |
| 1000 | 1000.0 | 57.62% | 104025.6 | routed |
| 1250 | 1250.0 | 60.41% | 2313623.4 | routed |
| 1500 | 1500.0 | 61.61% | 2317696.3 | routed |
| 1750 | 1750.0 | 62.50% | 2324021.8 | routed |
| 2000 | 2000.0 | 63.41% | 2330355.6 | routed |
| 2250 | 2250.0 | 63.98% | 2332275.7 | routed |
| 2500 | 2500.0 | 64.49% | 2336232.3 | routed |
| 3000 | 3000.0 | 65.70% | 2339665.1 | routed |
| 4000 | 4000.0 | 67.15% | 2457854.5 | routed |
| 5000 | 5000.0 | 68.12% | 2452709.3 | routed |
| 6000 | 6000.0 | 68.77% | 2381449.9 | routed |
| 7500 | 7500.0 | 69.54% | 2328610.1 | routed |
| 10000 | 10000.0 | 70.60% | 2294480.7 | routed |
| 15000 | 15000.0 | 72.02% | 2285079.8 | routed |
| 20000 | 20000.0 | 73.47% | 7792483.5 | routed |
| 25000 | 25000.0 | 74.35% | 7798385.1 | routed |
