# Azoth Filetype `python`
Specialist model for `python`.
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
- Training rows: 109753 (11494 malware, 98259 benign).
- Benchmark rows: 15650 (1652 malware, 13998 benign).
- Benchmark AUC/AP/F1: 0.9998 / 0.9986 / 0.9872.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 64.83% | 0.00 | 0.999982 | 8.0 | 94.73% | 71.44 | 0.992613 |
| 1 | 1.0 | 94.73% | 71.44 | 0.992613 | 16.0 | 94.73% | 71.44 | 0.992613 |
| 2 | 2.0 | 94.73% | 71.44 | 0.992613 | 24.0 | 94.73% | 71.44 | 0.992613 |
| 3 | 3.0 | 94.73% | 71.44 | 0.992613 | 32.0 | 94.73% | 71.44 | 0.992613 |
| 4 | 4.0 | 94.73% | 71.44 | 0.992613 | 40.0 | 94.73% | 71.44 | 0.992613 |
| 5 | 5.0 | 94.73% | 71.44 | 0.992613 | 48.0 | 94.73% | 71.44 | 0.992613 |
| 6 | 6.0 | 94.73% | 71.44 | 0.992613 | 56.0 | 94.73% | 71.44 | 0.992613 |
| 7 | 7.0 | 94.73% | 71.44 | 0.992613 | 64.0 | 94.73% | 71.44 | 0.992613 |
| 8 | 8.0 | 94.73% | 71.44 | 0.992613 | 72.0 | 94.73% | 71.44 | 0.992613 |
| 9 | 9.0 | 94.73% | 71.44 | 0.992613 | 80.0 | 94.73% | 71.44 | 0.992613 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 89.87% | 1 | 10.23 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9982598423957825, "general": 0.9818487763404846}` |
| 5 | suspicious | or_general_primary | 92.44% | 4 | 40.91 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9982598423957825, "general": 0.9685817956924438}` |
| 9 | hostile | or_general_primary | 89.87% | 1 | 10.23 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9982598423957825, "general": 0.9818487763404846}` |
| 9 | suspicious | or_general_primary | 92.83% | 7 | 71.59 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9982598423957825, "general": 0.9583919048309326}` |
