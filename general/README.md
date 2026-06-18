# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,388 features) extracted from cleave reports.
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
- Calibration corpus: 8,128,149 rows (2,620,313 malware, 5,507,836 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 69.69% | 0.00 | routed |
| 1 | 1.0 | 69.81% | 1874798.4 | routed |
| 2 | 2.0 | 69.81% | 1874798.4 | routed |
| 3 | 3.0 | 69.81% | 1874798.4 | routed |
| 4 | 4.0 | 69.82% | 1874798.4 | routed |
| 5 | 5.0 | 69.82% | 1874798.4 | routed |
| 10 | 10.0 | 70.90% | 1880319.8 | routed |
| 20 | 20.0 | 71.74% | 2322756.5 | routed |
| 30 | 30.0 | 72.00% | 2336559.9 | routed |
| 40 | 40.0 | 72.29% | 2628902.4 | routed |
| 50 | 50.0 | 72.72% | 2641834.0 | routed |
| 60 | 60.0 | 72.93% | 2652150.3 | routed |
| 70 | 70.0 | 73.09% | 2660141.8 | routed |
| 80 | 80.0 | 73.37% | 2668423.8 | routed |
| 90 | 90.0 | 73.60% | 2675979.4 | routed |
| 100 | 100.0 | 73.91% | 2684116.2 | routed |
| 200 | 200.0 | 75.26% | 3517989.5 | routed |
| 300 | 300.0 | 75.90% | 3581340.1 | routed |
| 500 | 500.0 | 76.70% | 3716323.2 | routed |
| 1000 | 1000.0 | 77.90% | 3961298.0 | routed |
| 2000 | 2000.0 | 79.23% | 4362615.0 | routed |
| 5000 | 5000.0 | 73.73% | 4445290.4 | routed |
| 7500 | 7500.0 | 74.28% | 3928315.1 | routed |
| 10000 | 10000.0 | 74.86% | 3932674.1 | routed |
| 15000 | 15000.0 | 75.36% | 3136723.8 | routed |
| 20000 | 20000.0 | 75.92% | 3104612.7 | routed |
| 25000 | 25000.0 | 76.40% | 2866757.5 | routed |
