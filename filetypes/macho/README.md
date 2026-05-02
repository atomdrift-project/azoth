# Azoth Filetype `macho`
Specialist model for `macho`.
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
- Training rows: 5236 (1137 malware, 4099 benign).
- Benchmark rows: 754 (145 malware, 609 benign).
- Benchmark AUC/AP/F1: 0.9988 / 0.9939 / 0.9730.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 55.17% | 0.00 | 0.993030 | 8.0 | 91.03% | 1642.0 | 0.937062 |
| 1 | 1.0 | 91.03% | 1642.0 | 0.937062 | 16.0 | 91.03% | 1642.0 | 0.937062 |
| 2 | 2.0 | 91.03% | 1642.0 | 0.937062 | 24.0 | 91.03% | 1642.0 | 0.937062 |
| 3 | 3.0 | 91.03% | 1642.0 | 0.937062 | 32.0 | 91.03% | 1642.0 | 0.937062 |
| 4 | 4.0 | 91.03% | 1642.0 | 0.937062 | 40.0 | 91.03% | 1642.0 | 0.937062 |
| 5 | 5.0 | 91.03% | 1642.0 | 0.937062 | 48.0 | 91.03% | 1642.0 | 0.937062 |
| 6 | 6.0 | 91.03% | 1642.0 | 0.937062 | 56.0 | 91.03% | 1642.0 | 0.937062 |
| 7 | 7.0 | 91.03% | 1642.0 | 0.937062 | 64.0 | 91.03% | 1642.0 | 0.937062 |
| 8 | 8.0 | 91.03% | 1642.0 | 0.937062 | 72.0 | 91.03% | 1642.0 | 0.937062 |
| 9 | 9.0 | 91.03% | 1642.0 | 0.937062 | 80.0 | 91.03% | 1642.0 | 0.937062 |
