# Azoth Filetype `jpeg`
Specialist model for `jpeg`.
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
- Training rows: 7071 (618 malware, 6453 benign).
- Benchmark rows: 969 (90 malware, 879 benign).
- Benchmark AUC/AP/F1: 0.9937 / 0.9446 / 0.8649.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 44.44% | 0.00 | 0.992693 | 8.0 | 63.33% | 1137.7 | 0.984403 |
| 1 | 1.0 | 63.33% | 1137.7 | 0.984403 | 16.0 | 63.33% | 1137.7 | 0.984403 |
| 2 | 2.0 | 63.33% | 1137.7 | 0.984403 | 24.0 | 63.33% | 1137.7 | 0.984403 |
| 3 | 3.0 | 63.33% | 1137.7 | 0.984403 | 32.0 | 63.33% | 1137.7 | 0.984403 |
| 4 | 4.0 | 63.33% | 1137.7 | 0.984403 | 40.0 | 63.33% | 1137.7 | 0.984403 |
| 5 | 5.0 | 63.33% | 1137.7 | 0.984403 | 48.0 | 63.33% | 1137.7 | 0.984403 |
| 6 | 6.0 | 63.33% | 1137.7 | 0.984403 | 56.0 | 63.33% | 1137.7 | 0.984403 |
| 7 | 7.0 | 63.33% | 1137.7 | 0.984403 | 64.0 | 63.33% | 1137.7 | 0.984403 |
| 8 | 8.0 | 63.33% | 1137.7 | 0.984403 | 72.0 | 63.33% | 1137.7 | 0.984403 |
| 9 | 9.0 | 63.33% | 1137.7 | 0.984403 | 80.0 | 63.33% | 1137.7 | 0.984403 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 5 | suspicious | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 9 | hostile | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
| 9 | suspicious | or_general_primary | 2.92% | 0 | 0.00 | `{"filetypes/jpeg": 0.1325506567955017, "general": 0.2928639054298401}` |
