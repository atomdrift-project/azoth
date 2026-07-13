# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,307 features) extracted from cleave reports.
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
- Calibration corpus: 13,792,064 rows (2,654,811 malware, 11,137,253 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 66.65% | 0.00 | routed |
| 1 | 1.0 | 66.67% | 2150386.8 | routed |
| 2 | 2.0 | 66.68% | 2150386.8 | routed |
| 3 | 3.0 | 66.70% | 2150386.8 | routed |
| 4 | 4.0 | 66.72% | 2150386.8 | routed |
| 5 | 5.0 | 66.73% | 2150386.8 | routed |
| 10 | 10.0 | 67.06% | 2152976.2 | routed |
| 15 | 15.0 | 67.29% | 2155277.8 | routed |
| 20 | 20.0 | 67.55% | 2157507.5 | routed |
| 25 | 25.0 | 67.87% | 2159881.1 | routed |
| 30 | 30.0 | 68.16% | 2167721.1 | routed |
| 40 | 40.0 | 68.56% | 2173043.7 | routed |
| 50 | 50.0 | 68.85% | 2176999.6 | routed |
| 60 | 60.0 | 69.71% | 2181171.4 | routed |
| 70 | 70.0 | 70.12% | 2185055.4 | routed |
| 80 | 80.0 | 70.58% | 2188795.6 | routed |
| 90 | 90.0 | 70.82% | 2192391.9 | routed |
| 100 | 100.0 | 71.65% | 2336316.8 | routed |
| 125 | 125.0 | 72.22% | 2346746.2 | routed |
| 150 | 150.0 | 72.65% | 2353866.9 | routed |
| 175 | 175.0 | 73.15% | 2360052.6 | routed |
| 200 | 200.0 | 73.43% | 2365878.6 | routed |
| 250 | 250.0 | 74.65% | 2377530.7 | routed |
| 300 | 300.0 | 75.26% | 2403136.6 | routed |
| 500 | 500.0 | 77.32% | 2451974.7 | routed |
| 750 | 750.0 | 78.36% | 2678255.5 | routed |
| 1000 | 1000.0 | 79.68% | 2727237.4 | routed |
| 1250 | 1250.0 | 80.12% | 2759388.6 | routed |
| 1500 | 1500.0 | 80.46% | 2797078.1 | routed |
| 1750 | 1750.0 | 80.66% | 2818656.0 | routed |
| 2000 | 2000.0 | 80.85% | 2837716.5 | routed |
| 2250 | 2250.0 | 81.02% | 2858503.3 | routed |
| 2500 | 2500.0 | 81.23% | 2876916.5 | routed |
| 3000 | 3000.0 | 81.52% | 2904895.9 | routed |
| 4000 | 4000.0 | 81.98% | 2950209.6 | routed |
| 5000 | 5000.0 | 76.76% | 2842391.8 | routed |
| 6000 | 6000.0 | 77.18% | 2843686.4 | routed |
| 7500 | 7500.0 | 77.57% | 2596403.1 | routed |
| 10000 | 10000.0 | 78.00% | 2558425.9 | routed |
| 15000 | 15000.0 | 77.92% | 2463195.2 | routed |
| 20000 | 20000.0 | 78.48% | 2433777.3 | routed |
| 25000 | 25000.0 | 78.96% | 2442768.1 | routed |
