# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (28960 features) extracted from cleave reports.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=500, num_leaves=96, max_depth=14, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Calibration corpus: 2173639 rows (393489 malware, 1780150 benign).

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 18.18% | 0.00 | 0.999881 | 8.0 | 51.70% | 7.86 | 0.998768 |
| 1 | 1.0 | 22.67% | 0.56 | 0.999827 | 16.0 | 60.29% | 15.73 | 0.997758 |
| 2 | 2.0 | 24.30% | 1.69 | 0.999807 | 24.0 | 62.72% | 23.59 | 0.997233 |
| 3 | 3.0 | 41.61% | 2.81 | 0.999379 | 32.0 | 66.90% | 31.46 | 0.995868 |
| 4 | 4.0 | 46.33% | 3.93 | 0.999157 | 40.0 | 68.39% | 36.51 | 0.995318 |
| 5 | 5.0 | 46.75% | 4.49 | 0.999131 | 48.0 | 68.39% | 36.51 | 0.995318 |
| 6 | 6.0 | 46.79% | 5.62 | 0.999129 | 56.0 | 68.61% | 55.61 | 0.995204 |
| 7 | 7.0 | 49.44% | 6.18 | 0.998958 | 64.0 | 69.73% | 62.35 | 0.994636 |
| 8 | 8.0 | 51.70% | 7.86 | 0.998768 | 72.0 | 70.41% | 70.78 | 0.994191 |
| 9 | 9.0 | 53.17% | 8.99 | 0.998641 | 80.0 | 70.66% | 76.40 | 0.994028 |
