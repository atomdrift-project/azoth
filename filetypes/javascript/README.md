# Azoth Filetype `javascript`
Specialist model for `javascript`.
- Inputs: shared general `feature_spec.json` (37595 features); policy `general_shared`.
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
- Training rows: 340960 (49381 malware, 291579 benign).
- Benchmark rows: 49195 (7179 malware, 42016 benign).
- Benchmark AUC/AP/F1: 0.9980 / 0.9943 / 0.9778.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 91.99% | 0.00 | 0.997118 | 8.0 | 93.09% | 23.80 | 0.994586 |
| 1 | 1.0 | 93.09% | 23.80 | 0.994586 | 16.0 | 93.09% | 23.80 | 0.994586 |
| 2 | 2.0 | 93.09% | 23.80 | 0.994586 | 24.0 | 93.09% | 23.80 | 0.994586 |
| 3 | 3.0 | 93.09% | 23.80 | 0.994586 | 32.0 | 93.09% | 23.80 | 0.994586 |
| 4 | 4.0 | 93.09% | 23.80 | 0.994586 | 40.0 | 93.09% | 23.80 | 0.994586 |
| 5 | 5.0 | 93.09% | 23.80 | 0.994586 | 48.0 | 94.27% | 47.60 | 0.977869 |
| 6 | 6.0 | 93.09% | 23.80 | 0.994586 | 56.0 | 94.27% | 47.60 | 0.977869 |
| 7 | 7.0 | 93.09% | 23.80 | 0.994586 | 64.0 | 94.27% | 47.60 | 0.977869 |
| 8 | 8.0 | 93.09% | 23.80 | 0.994586 | 72.0 | 94.68% | 71.40 | 0.967413 |
| 9 | 9.0 | 93.09% | 23.80 | 0.994586 | 80.0 | 94.68% | 71.40 | 0.967413 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 87.04% | 1 | 3.00 | `{"filegroups/scripts": 0.9992733001708984, "filetypes/javascript": 0.9957285523414612, "general": 0.9862461090087891}` |
| 5 | suspicious | specialist_primary_with_escape | 90.89% | 15 | 45.03 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9692838788032532, "general": 0.9862461090087891}` |
| 9 | hostile | group_primary_with_escape | 89.07% | 2 | 6.00 | `{"filegroups/scripts": 0.998188853263855, "filetypes/javascript": 0.9908182621002197, "general": 0.9862461090087891}` |
| 9 | suspicious | specialist_primary_with_escape | 91.86% | 26 | 78.05 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9480387568473816, "general": 0.9840287566184998}` |
