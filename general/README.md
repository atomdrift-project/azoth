# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (7,740 features) extracted from cleave reports.
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
- Calibration corpus: 7,920,730 rows (2,613,468 malware, 5,307,262 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 5.26% | 0.00 | 0.999775 |
| 1 | 1.0 | 14.80% | 18.84 | 0.999476 |
| 2 | 2.0 | 14.80% | 18.84 | 0.999476 |
| 3 | 3.0 | 14.80% | 18.84 | 0.999476 |
| 4 | 4.0 | 14.80% | 18.84 | 0.999476 |
| 5 | 5.0 | 14.80% | 18.84 | 0.999476 |
| 10 | 10.0 | 14.80% | 18.84 | 0.999476 |
| 20 | 20.0 | 14.80% | 18.84 | 0.999476 |
| 30 | 30.0 | 14.80% | 18.84 | 0.999476 |
| 40 | 40.0 | 15.37% | 37.68 | 0.999442 |
| 50 | 50.0 | 15.37% | 37.68 | 0.999442 |
| 60 | 60.0 | 16.44% | 56.53 | 0.999370 |
| 70 | 70.0 | 16.44% | 56.53 | 0.999370 |
| 80 | 80.0 | 17.56% | 75.37 | 0.999304 |
| 90 | 90.0 | 17.56% | 75.37 | 0.999304 |
| 100 | 100.0 | 21.18% | 94.21 | 0.999127 |
| 200 | 200.0 | 28.66% | 188.42 | 0.998556 |
| 300 | 300.0 | 31.91% | 282.63 | 0.998195 |
| 500 | 500.0 | 35.87% | 489.89 | 0.997664 |
| 1000 | 1000.0 | 42.30% | 998.63 | 0.996519 |
| 2000 | 2000.0 | 49.56% | 1997.3 | 0.993681 |
| 5000 | 5000.0 | 56.76% | 4993.2 | 0.986583 |
| 7500 | 7500.0 | 59.06% | 7499.2 | 0.981277 |
| 10000 | 10000.0 | 60.63% | 9986.3 | 0.975033 |
| 15000 | 15000.0 | 62.38% | 14998.3 | 0.964536 |
| 20000 | 20000.0 | 63.31% | 19991.5 | 0.955639 |
| 25000 | 25000.0 | 63.95% | 24965.8 | 0.947996 |
