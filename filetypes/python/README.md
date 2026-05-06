# Azoth Filetype `python`
Specialist model for `python`.
- Inputs: shared general `feature_spec.json` (37595 features); policy `general_shared`.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 96088 (10440 malware, 85648 benign).
- Benchmark rows: 13697 (1525 malware, 12172 benign).
- Benchmark AUC/AP/F1: 0.9987 / 0.9958 / 0.9835.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 54.49% | 0.00 | 0.999958 | 8.0 | 87.08% | 82.16 | 0.999632 |
| 1 | 1.0 | 87.08% | 82.16 | 0.999632 | 16.0 | 87.08% | 82.16 | 0.999632 |
| 2 | 2.0 | 87.08% | 82.16 | 0.999632 | 24.0 | 87.08% | 82.16 | 0.999632 |
| 3 | 3.0 | 87.08% | 82.16 | 0.999632 | 32.0 | 87.08% | 82.16 | 0.999632 |
| 4 | 4.0 | 87.08% | 82.16 | 0.999632 | 40.0 | 87.08% | 82.16 | 0.999632 |
| 5 | 5.0 | 87.08% | 82.16 | 0.999632 | 48.0 | 87.08% | 82.16 | 0.999632 |
| 6 | 6.0 | 87.08% | 82.16 | 0.999632 | 56.0 | 87.08% | 82.16 | 0.999632 |
| 7 | 7.0 | 87.08% | 82.16 | 0.999632 | 64.0 | 87.08% | 82.16 | 0.999632 |
| 8 | 8.0 | 87.08% | 82.16 | 0.999632 | 72.0 | 87.08% | 82.16 | 0.999632 |
| 9 | 9.0 | 87.08% | 82.16 | 0.999632 | 80.0 | 87.08% | 82.16 | 0.999632 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 87.78% | 1 | 10.23 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9985394477844238, "general": 0.9818487763404846}` |
| 5 | suspicious | or_general_primary | 90.76% | 4 | 40.91 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9985394477844238, "general": 0.9685817956924438}` |
| 9 | hostile | or_general_primary | 87.78% | 1 | 10.23 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9985394477844238, "general": 0.9818487763404846}` |
| 9 | suspicious | specialist_primary_with_escape | 92.11% | 7 | 71.59 | `{"filegroups/scripts": 0.9941955804824829, "filetypes/python": 0.9817735552787781, "general": 0.9743776917457581}` |
