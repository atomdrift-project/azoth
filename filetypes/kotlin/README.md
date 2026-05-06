# Azoth Filetype `kotlin`
Specialist model for `kotlin`.
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
- Training rows: 25837 (553 malware, 25284 benign).
- Benchmark rows: 3673 (77 malware, 3596 benign).
- Benchmark AUC/AP/F1: 0.9970 / 0.9681 / 0.9530.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 89.61% | 0.00 | 0.996817 | 8.0 | 92.21% | 278.09 | 0.990411 |
| 1 | 1.0 | 92.21% | 278.09 | 0.990411 | 16.0 | 92.21% | 278.09 | 0.990411 |
| 2 | 2.0 | 92.21% | 278.09 | 0.990411 | 24.0 | 92.21% | 278.09 | 0.990411 |
| 3 | 3.0 | 92.21% | 278.09 | 0.990411 | 32.0 | 92.21% | 278.09 | 0.990411 |
| 4 | 4.0 | 92.21% | 278.09 | 0.990411 | 40.0 | 92.21% | 278.09 | 0.990411 |
| 5 | 5.0 | 92.21% | 278.09 | 0.990411 | 48.0 | 92.21% | 278.09 | 0.990411 |
| 6 | 6.0 | 92.21% | 278.09 | 0.990411 | 56.0 | 92.21% | 278.09 | 0.990411 |
| 7 | 7.0 | 92.21% | 278.09 | 0.990411 | 64.0 | 92.21% | 278.09 | 0.990411 |
| 8 | 8.0 | 92.21% | 278.09 | 0.990411 | 72.0 | 92.21% | 278.09 | 0.990411 |
| 9 | 9.0 | 92.21% | 278.09 | 0.990411 | 80.0 | 92.21% | 278.09 | 0.990411 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 57.83% | 0 | 0.00 | `{"filegroups/source": 0.5903330445289612, "filetypes/kotlin": 0.06616190075874329}` |
| 5 | suspicious | group_primary_with_escape | 57.83% | 0 | 0.00 | `{"filegroups/source": 0.5903330445289612, "filetypes/kotlin": 0.06616190075874329}` |
| 9 | hostile | group_primary_with_escape | 57.83% | 0 | 0.00 | `{"filegroups/source": 0.5903330445289612, "filetypes/kotlin": 0.06616190075874329}` |
| 9 | suspicious | or_general_primary | 59.90% | 2 | 69.28 | `{"filetypes/kotlin": 0.06616190075874329, "general": 0.13608065247535706}` |
