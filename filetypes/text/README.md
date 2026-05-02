# Azoth Filetype `text`
Specialist model for `text`.
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
- Training rows: 356 (121 malware, 235 benign).
- Benchmark rows: 5938 (80 malware, 5858 benign).
- Benchmark AUC/AP/F1: 0.7236 / 0.3060 / 0.3966.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 22.50% | 0.00 | 0.912330 | 8.0 | 25.00% | 170.71 | 0.476686 |
| 1 | 1.0 | 25.00% | 170.71 | 0.476686 | 16.0 | 25.00% | 170.71 | 0.476686 |
| 2 | 2.0 | 25.00% | 170.71 | 0.476686 | 24.0 | 25.00% | 170.71 | 0.476686 |
| 3 | 3.0 | 25.00% | 170.71 | 0.476686 | 32.0 | 25.00% | 170.71 | 0.476686 |
| 4 | 4.0 | 25.00% | 170.71 | 0.476686 | 40.0 | 25.00% | 170.71 | 0.476686 |
| 5 | 5.0 | 25.00% | 170.71 | 0.476686 | 48.0 | 25.00% | 170.71 | 0.476686 |
| 6 | 6.0 | 25.00% | 170.71 | 0.476686 | 56.0 | 25.00% | 170.71 | 0.476686 |
| 7 | 7.0 | 25.00% | 170.71 | 0.476686 | 64.0 | 25.00% | 170.71 | 0.476686 |
| 8 | 8.0 | 25.00% | 170.71 | 0.476686 | 72.0 | 25.00% | 170.71 | 0.476686 |
| 9 | 9.0 | 25.00% | 170.71 | 0.476686 | 80.0 | 25.00% | 170.71 | 0.476686 |
