# Azoth Filetype `php`
Specialist model for `php`.
- Inputs: shared general `feature_spec.json` (49112 features); policy `general_shared`.
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
- Training rows: 37476 (1214 malware, 36262 benign).
- Benchmark rows: 5303 (178 malware, 5125 benign).
- Benchmark AUC/AP/F1: 1.0000 / 0.9998 / 0.9944.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 98.31% | 0.00 | 0.963190 | 8.0 | 99.44% | 195.12 | 0.920663 |
| 1 | 1.0 | 99.44% | 195.12 | 0.920663 | 16.0 | 99.44% | 195.12 | 0.920663 |
| 2 | 2.0 | 99.44% | 195.12 | 0.920663 | 24.0 | 99.44% | 195.12 | 0.920663 |
| 3 | 3.0 | 99.44% | 195.12 | 0.920663 | 32.0 | 99.44% | 195.12 | 0.920663 |
| 4 | 4.0 | 99.44% | 195.12 | 0.920663 | 40.0 | 99.44% | 195.12 | 0.920663 |
| 5 | 5.0 | 99.44% | 195.12 | 0.920663 | 48.0 | 99.44% | 195.12 | 0.920663 |
| 6 | 6.0 | 99.44% | 195.12 | 0.920663 | 56.0 | 99.44% | 195.12 | 0.920663 |
| 7 | 7.0 | 99.44% | 195.12 | 0.920663 | 64.0 | 99.44% | 195.12 | 0.920663 |
| 8 | 8.0 | 99.44% | 195.12 | 0.920663 | 72.0 | 99.44% | 195.12 | 0.920663 |
| 9 | 9.0 | 99.44% | 195.12 | 0.920663 | 80.0 | 99.44% | 195.12 | 0.920663 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 87.89% | 1 | 61.07 | `{"filegroups/scripts": 0.9553837180137634, "filetypes/php": 0.8189165592193604, "general": 0.92668616771698}` |
| 9 | hostile | specialist_primary_with_escape | 87.89% | 1 | 61.07 | `{"filegroups/scripts": 0.9553837180137634, "filetypes/php": 0.8189165592193604, "general": 0.92668616771698}` |
| 9 | suspicious | specialist_primary_with_escape | 87.89% | 1 | 61.07 | `{"filegroups/scripts": 0.9553837180137634, "filetypes/php": 0.8189165592193604, "general": 0.92668616771698}` |
