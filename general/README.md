# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (49112 features) extracted from cleave reports.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Calibration corpus: 2293938 rows (472475 malware, 1821463 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 29.59% | 0.00 | 0.999601 | 8.0 | 54.42% | 7.69 | 0.997852 |
| 1 | 1.0 | 36.96% | 0.55 | 0.999327 | 16.0 | 58.19% | 15.92 | 0.997168 |
| 2 | 2.0 | 38.69% | 1.65 | 0.999235 | 24.0 | 61.96% | 23.61 | 0.996306 |
| 3 | 3.0 | 41.67% | 2.75 | 0.999092 | 32.0 | 62.56% | 31.84 | 0.996114 |
| 4 | 4.0 | 41.80% | 3.29 | 0.999083 | 40.0 | 63.78% | 39.53 | 0.995702 |
| 5 | 5.0 | 47.08% | 4.94 | 0.998714 | 48.0 | 65.51% | 47.76 | 0.995067 |
| 6 | 6.0 | 47.86% | 5.49 | 0.998633 | 56.0 | 67.54% | 56.00 | 0.994147 |
| 7 | 7.0 | 50.53% | 6.59 | 0.998335 | 64.0 | 69.56% | 63.69 | 0.993267 |
| 8 | 8.0 | 54.42% | 7.69 | 0.997852 | 72.0 | 71.00% | 71.92 | 0.992407 |
| 9 | 9.0 | 55.18% | 8.78 | 0.997791 | 80.0 | 71.74% | 79.61 | 0.991815 |
