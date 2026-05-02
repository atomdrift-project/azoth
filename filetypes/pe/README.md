# Azoth Filetype `pe`
Specialist model for `pe`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 338046 (223567 malware, 114479 benign).
- Benchmark rows: 46568 (30313 malware, 16255 benign).
- Benchmark AUC/AP/F1: 0.9998 / 0.9999 / 0.9957.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 85.94% | 0.00 | 0.997808 | 8.0 | 89.91% | 61.52 | 0.996000 |
| 1 | 1.0 | 89.91% | 61.52 | 0.996000 | 16.0 | 89.91% | 61.52 | 0.996000 |
| 2 | 2.0 | 89.91% | 61.52 | 0.996000 | 24.0 | 89.91% | 61.52 | 0.996000 |
| 3 | 3.0 | 89.91% | 61.52 | 0.996000 | 32.0 | 89.91% | 61.52 | 0.996000 |
| 4 | 4.0 | 89.91% | 61.52 | 0.996000 | 40.0 | 89.91% | 61.52 | 0.996000 |
| 5 | 5.0 | 89.91% | 61.52 | 0.996000 | 48.0 | 89.91% | 61.52 | 0.996000 |
| 6 | 6.0 | 89.91% | 61.52 | 0.996000 | 56.0 | 89.91% | 61.52 | 0.996000 |
| 7 | 7.0 | 89.91% | 61.52 | 0.996000 | 64.0 | 89.91% | 61.52 | 0.996000 |
| 8 | 8.0 | 89.91% | 61.52 | 0.996000 | 72.0 | 89.91% | 61.52 | 0.996000 |
| 9 | 9.0 | 89.91% | 61.52 | 0.996000 | 80.0 | 89.91% | 61.52 | 0.996000 |
