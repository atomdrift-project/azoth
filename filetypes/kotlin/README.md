# Azoth Filetype `kotlin`
Specialist model for `kotlin`.
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
- Training rows: 274 (213 malware, 61 benign).
- Benchmark rows: 3397 (53 malware, 3344 benign).
- Benchmark AUC/AP/F1: 0.9196 / 0.8237 / 0.8750.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 54.72% | 0.00 | 0.932684 | 8.0 | 79.25% | 299.04 | 0.796352 |
| 1 | 1.0 | 79.25% | 299.04 | 0.796352 | 16.0 | 79.25% | 299.04 | 0.796352 |
| 2 | 2.0 | 79.25% | 299.04 | 0.796352 | 24.0 | 79.25% | 299.04 | 0.796352 |
| 3 | 3.0 | 79.25% | 299.04 | 0.796352 | 32.0 | 79.25% | 299.04 | 0.796352 |
| 4 | 4.0 | 79.25% | 299.04 | 0.796352 | 40.0 | 79.25% | 299.04 | 0.796352 |
| 5 | 5.0 | 79.25% | 299.04 | 0.796352 | 48.0 | 79.25% | 299.04 | 0.796352 |
| 6 | 6.0 | 79.25% | 299.04 | 0.796352 | 56.0 | 79.25% | 299.04 | 0.796352 |
| 7 | 7.0 | 79.25% | 299.04 | 0.796352 | 64.0 | 79.25% | 299.04 | 0.796352 |
| 8 | 8.0 | 79.25% | 299.04 | 0.796352 | 72.0 | 79.25% | 299.04 | 0.796352 |
| 9 | 9.0 | 79.25% | 299.04 | 0.796352 | 80.0 | 79.25% | 299.04 | 0.796352 |
