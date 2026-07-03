# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (229 features) extracted from cleave reports.
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
- Calibration corpus: 12,910,342 rows (2,642,872 malware, 10,267,470 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 56.59% | 0.00 | routed |
| 1 | 1.0 | 56.63% | 7410.8 | routed |
| 2 | 2.0 | 56.64% | 7410.8 | routed |
| 3 | 3.0 | 56.65% | 7410.8 | routed |
| 4 | 4.0 | 56.66% | 7410.8 | routed |
| 5 | 5.0 | 56.67% | 7410.8 | routed |
| 10 | 10.0 | 60.76% | 10063.1 | routed |
| 15 | 15.0 | 61.67% | 12715.4 | routed |
| 20 | 20.0 | 61.85% | 18878.1 | routed |
| 25 | 25.0 | 63.64% | 21374.4 | routed |
| 30 | 30.0 | 64.25% | 56322.3 | routed |
| 40 | 40.0 | 64.57% | 217176.4 | routed |
| 50 | 50.0 | 65.11% | 221388.9 | routed |
| 60 | 60.0 | 67.50% | 226381.5 | routed |
| 70 | 70.0 | 68.11% | 230515.9 | routed |
| 80 | 80.0 | 68.38% | 234572.4 | routed |
| 90 | 90.0 | 69.00% | 248145.9 | routed |
| 100 | 100.0 | 69.52% | 252514.4 | routed |
| 125 | 125.0 | 70.28% | 261173.4 | routed |
| 150 | 150.0 | 70.82% | 270924.5 | routed |
| 175 | 175.0 | 71.39% | 278101.3 | routed |
| 200 | 200.0 | 71.93% | 286448.2 | routed |
| 250 | 250.0 | 72.71% | 340274.3 | routed |
| 300 | 300.0 | 73.55% | 354003.8 | routed |
| 500 | 500.0 | 75.95% | 410326.2 | routed |
| 750 | 750.0 | 77.52% | 461421.9 | routed |
| 1000 | 1000.0 | 78.36% | 502766.6 | routed |
| 1250 | 1250.0 | 78.86% | 539118.7 | routed |
| 1500 | 1500.0 | 79.30% | 570946.3 | routed |
| 1750 | 1750.0 | 79.75% | 596767.2 | routed |
| 2000 | 2000.0 | 80.16% | 623758.2 | routed |
| 2250 | 2250.0 | 80.51% | 647784.9 | routed |
| 2500 | 2500.0 | 80.74% | 666039.0 | routed |
| 3000 | 3000.0 | 81.12% | 701064.9 | routed |
| 4000 | 4000.0 | 81.67% | 773223.0 | routed |
| 5000 | 5000.0 | 73.49% | 654181.6 | routed |
| 6000 | 6000.0 | 74.49% | 582491.6 | routed |
| 7500 | 7500.0 | 74.96% | 522892.8 | routed |
| 10000 | 10000.0 | 76.08% | 484902.6 | routed |
| 15000 | 15000.0 | 77.28% | 410794.2 | routed |
| 20000 | 20000.0 | 78.16% | 357280.2 | routed |
| 25000 | 25000.0 | 78.90% | 367187.3 | routed |
