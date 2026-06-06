# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (8,595 features) extracted from cleave reports.
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
- Calibration corpus: 6,720,544 rows (2,496,311 malware, 4,224,233 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 31.89% | 0.00 | routed |
| 1 | 1.0 | 32.25% | 28928.3 | routed |
| 2 | 2.0 | 32.27% | 28928.3 | routed |
| 3 | 3.0 | 32.30% | 28928.3 | routed |
| 4 | 4.0 | 32.33% | 28928.3 | routed |
| 5 | 5.0 | 32.35% | 28928.3 | routed |
| 10 | 10.0 | 32.55% | 28928.3 | routed |
| 20 | 20.0 | 33.15% | 28928.3 | routed |
| 30 | 30.0 | 33.59% | 28952.0 | routed |
| 40 | 40.0 | 33.81% | 28952.0 | routed |
| 50 | 50.0 | 34.09% | 28952.0 | routed |
| 60 | 60.0 | 34.61% | 28952.0 | routed |
| 70 | 70.0 | 35.34% | 28952.0 | routed |
| 80 | 80.0 | 35.71% | 28975.7 | routed |
| 90 | 90.0 | 36.04% | 28975.7 | routed |
| 100 | 100.0 | 36.33% | 29046.7 | routed |
| 200 | 200.0 | 39.03% | 29236.1 | routed |
| 300 | 300.0 | 42.20% | 29425.5 | routed |
| 500 | 500.0 | 44.67% | 29780.6 | routed |
| 1000 | 1000.0 | 49.08% | 30869.5 | routed |
| 2000 | 2000.0 | 53.85% | 33094.8 | routed |
| 5000 | 5000.0 | 61.93% | 44836.5 | routed |
| 7500 | 7500.0 | 65.37% | 50210.3 | routed |
| 10000 | 10000.0 | 67.40% | 56010.2 | routed |
