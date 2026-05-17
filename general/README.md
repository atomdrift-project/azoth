# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (56209 features) extracted from cleave reports.
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
- Calibration corpus: 4231044 rows (1486369 malware, 2744675 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 30.41% | 0.00 | 0.998565 | 8.0 | 47.06% | 7.65 | 0.995747 |
| 1 | 1.0 | 34.24% | 0.73 | 0.998204 | 16.0 | 53.06% | 15.67 | 0.993773 |
| 2 | 2.0 | 43.05% | 1.82 | 0.996783 | 24.0 | 55.26% | 23.68 | 0.992571 |
| 3 | 3.0 | 45.05% | 2.91 | 0.996355 | 32.0 | 56.99% | 31.70 | 0.991110 |
| 4 | 4.0 | 45.34% | 3.64 | 0.996279 | 40.0 | 58.28% | 39.71 | 0.989600 |
| 5 | 5.0 | 46.03% | 4.74 | 0.996056 | 48.0 | 59.06% | 46.64 | 0.988838 |
| 6 | 6.0 | 46.45% | 5.83 | 0.995910 | 56.0 | 60.11% | 55.74 | 0.987362 |
| 7 | 7.0 | 46.71% | 6.92 | 0.995833 | 64.0 | 60.96% | 63.76 | 0.985821 |
| 8 | 8.0 | 47.06% | 7.65 | 0.995747 | 72.0 | 61.43% | 71.78 | 0.984933 |
| 9 | 9.0 | 48.76% | 8.74 | 0.995274 | 80.0 | 61.85% | 79.79 | 0.983895 |
