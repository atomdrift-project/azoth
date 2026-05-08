# Azoth Filetype `javascript`
Specialist model for `javascript`.
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
- Training rows: 377820 (50138 malware, 327682 benign).
- Benchmark rows: 54591 (7288 malware, 47303 benign).
- Benchmark AUC/AP/F1: 0.9999 / 0.9996 / 0.9936.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.98% | 0.00 | 0.995460 | 8.0 | 94.99% | 21.14 | 0.995389 |
| 1 | 1.0 | 94.99% | 21.14 | 0.995389 | 16.0 | 94.99% | 21.14 | 0.995389 |
| 2 | 2.0 | 94.99% | 21.14 | 0.995389 | 24.0 | 94.99% | 21.14 | 0.995389 |
| 3 | 3.0 | 94.99% | 21.14 | 0.995389 | 32.0 | 94.99% | 21.14 | 0.995389 |
| 4 | 4.0 | 94.99% | 21.14 | 0.995389 | 40.0 | 94.99% | 21.14 | 0.995389 |
| 5 | 5.0 | 94.99% | 21.14 | 0.995389 | 48.0 | 95.64% | 42.28 | 0.993515 |
| 6 | 6.0 | 94.99% | 21.14 | 0.995389 | 56.0 | 95.64% | 42.28 | 0.993515 |
| 7 | 7.0 | 94.99% | 21.14 | 0.995389 | 64.0 | 96.21% | 63.42 | 0.989387 |
| 8 | 8.0 | 94.99% | 21.14 | 0.995389 | 72.0 | 96.21% | 63.42 | 0.989387 |
| 9 | 9.0 | 94.99% | 21.14 | 0.995389 | 80.0 | 96.21% | 63.42 | 0.989387 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 90.04% | 1 | 3.00 | `{"filetypes/javascript": 0.9970327615737915, "general": 0.9862461090087891}` |
| 5 | suspicious | specialist_primary_with_escape | 91.70% | 15 | 45.03 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9896018505096436, "general": 0.9840287566184998}` |
| 9 | hostile | or_general_primary | 90.13% | 2 | 6.00 | `{"filetypes/javascript": 0.9970327615737915, "general": 0.9840287566184998}` |
| 9 | suspicious | specialist_primary_with_escape | 92.19% | 26 | 78.05 | `{"filegroups/scripts": 0.9973033666610718, "filetypes/javascript": 0.9832349419593811, "general": 0.9824105501174927}` |
