# Azoth Filetype `batch`
Specialist model for `batch`.
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
- Training rows: 321 (192 malware, 129 benign).
- Benchmark rows: 195 (34 malware, 161 benign).
- Benchmark AUC/AP/F1: 0.9147 / 0.8788 / 0.9032.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 82.35% | 0.00 | 0.680926 | 8.0 | 82.35% | 6211.2 | 0.458324 |
| 1 | 1.0 | 82.35% | 6211.2 | 0.458324 | 16.0 | 82.35% | 6211.2 | 0.458324 |
| 2 | 2.0 | 82.35% | 6211.2 | 0.458324 | 24.0 | 82.35% | 6211.2 | 0.458324 |
| 3 | 3.0 | 82.35% | 6211.2 | 0.458324 | 32.0 | 82.35% | 6211.2 | 0.458324 |
| 4 | 4.0 | 82.35% | 6211.2 | 0.458324 | 40.0 | 82.35% | 6211.2 | 0.458324 |
| 5 | 5.0 | 82.35% | 6211.2 | 0.458324 | 48.0 | 82.35% | 6211.2 | 0.458324 |
| 6 | 6.0 | 82.35% | 6211.2 | 0.458324 | 56.0 | 82.35% | 6211.2 | 0.458324 |
| 7 | 7.0 | 82.35% | 6211.2 | 0.458324 | 64.0 | 82.35% | 6211.2 | 0.458324 |
| 8 | 8.0 | 82.35% | 6211.2 | 0.458324 | 72.0 | 82.35% | 6211.2 | 0.458324 |
| 9 | 9.0 | 82.35% | 6211.2 | 0.458324 | 80.0 | 82.35% | 6211.2 | 0.458324 |
