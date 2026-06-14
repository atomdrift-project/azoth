# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,519 features) extracted from cleave reports.
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
- Calibration corpus: 7,416,064 rows (2,543,560 malware, 4,872,504 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 65.90% | 0.00 | routed |
| 1 | 1.0 | 65.92% | 503182.7 | routed |
| 2 | 2.0 | 65.92% | 503182.7 | routed |
| 3 | 3.0 | 65.92% | 503182.7 | routed |
| 4 | 4.0 | 65.92% | 503182.7 | routed |
| 5 | 5.0 | 65.92% | 503182.7 | routed |
| 10 | 10.0 | 67.24% | 657224.9 | routed |
| 20 | 20.0 | 68.30% | 671183.9 | routed |
| 30 | 30.0 | 68.68% | 681530.0 | routed |
| 40 | 40.0 | 69.57% | 698609.4 | routed |
| 50 | 50.0 | 69.97% | 1028371.4 | routed |
| 60 | 60.0 | 70.78% | 1038060.6 | routed |
| 70 | 70.0 | 71.43% | 1047421.4 | routed |
| 80 | 80.0 | 71.75% | 1056125.2 | routed |
| 90 | 90.0 | 72.21% | 1064993.3 | routed |
| 100 | 100.0 | 73.55% | 1074846.8 | routed |
| 200 | 200.0 | 76.84% | 1473090.2 | routed |
| 300 | 300.0 | 78.85% | 1558815.2 | routed |
| 500 | 500.0 | 80.49% | 2368275.8 | routed |
| 1000 | 1000.0 | 81.93% | 2568957.7 | routed |
| 2000 | 2000.0 | 83.30% | 5413811.9 | routed |
| 5000 | 5000.0 | 76.53% | 4370988.8 | routed |
| 7500 | 7500.0 | 77.33% | 4082282.8 | routed |
| 10000 | 10000.0 | 77.91% | 2468945.2 | routed |
| 15000 | 15000.0 | 77.63% | 2173670.3 | routed |
| 20000 | 20000.0 | 78.66% | 2140332.8 | routed |
| 25000 | 25000.0 | 79.45% | 2149693.6 | routed |
