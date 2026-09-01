# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,232 features) extracted from cleave reports.
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
- Calibration corpus: 17,535,482 rows (2,678,703 malware, 14,856,779 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 36.11% | 0.00 | routed |
| 1 | 1.0 | 36.30% | 2349.1 | routed |
| 2 | 2.0 | 36.32% | 2349.1 | routed |
| 3 | 3.0 | 36.34% | 2349.1 | routed |
| 4 | 4.0 | 36.36% | 2349.1 | routed |
| 5 | 5.0 | 36.38% | 2349.1 | routed |
| 10 | 10.0 | 36.93% | 2355.8 | routed |
| 15 | 15.0 | 37.73% | 2362.6 | routed |
| 20 | 20.0 | 38.58% | 2362.6 | routed |
| 25 | 25.0 | 38.81% | 2369.3 | routed |
| 30 | 30.0 | 38.96% | 2376.0 | routed |
| 40 | 40.0 | 39.19% | 2396.2 | routed |
| 50 | 50.0 | 39.61% | 2402.9 | routed |
| 60 | 60.0 | 40.10% | 2409.7 | routed |
| 70 | 70.0 | 40.80% | 2436.6 | routed |
| 80 | 80.0 | 41.48% | 2456.8 | routed |
| 90 | 90.0 | 42.16% | 2463.5 | routed |
| 100 | 100.0 | 42.89% | 2483.7 | routed |
| 125 | 125.0 | 43.99% | 2551.0 | routed |
| 150 | 150.0 | 44.95% | 2584.7 | routed |
| 175 | 175.0 | 45.58% | 2631.8 | routed |
| 200 | 200.0 | 46.20% | 2665.4 | routed |
| 250 | 250.0 | 47.12% | 2759.7 | routed |
| 300 | 300.0 | 47.88% | 2853.9 | routed |
| 500 | 500.0 | 50.97% | 3210.7 | routed |
| 750 | 750.0 | 54.45% | 3722.2 | routed |
| 1000 | 1000.0 | 56.94% | 4146.3 | routed |
| 1250 | 1250.0 | 58.94% | 4617.4 | routed |
| 1500 | 1500.0 | 60.44% | 5068.4 | routed |
| 1750 | 1750.0 | 61.50% | 5492.4 | routed |
| 2000 | 2000.0 | 62.32% | 6010.7 | routed |
| 2250 | 2250.0 | 63.02% | 6488.6 | routed |
| 2500 | 2500.0 | 63.65% | 6912.7 | routed |
| 3000 | 3000.0 | 64.66% | 7868.5 | routed |
| 4000 | 4000.0 | 66.19% | 9692.5 | routed |
| 5000 | 5000.0 | 67.26% | 11395.5 | routed |
| 6000 | 6000.0 | 68.13% | 13132.1 | routed |
| 7500 | 7500.0 | 69.24% | 15568.7 | routed |
| 10000 | 10000.0 | 70.35% | 19842.8 | routed |
| 15000 | 15000.0 | 71.85% | 28357.4 | routed |
| 20000 | 20000.0 | 73.34% | 37067.3 | routed |
| 25000 | 25000.0 | 75.69% | 43724.1 | routed |
