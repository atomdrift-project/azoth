# Azoth Filetype `kotlin`
Specialist model for `kotlin`.
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
- Training rows: 31329 (786 malware, 30543 benign).
- Benchmark rows: 4486 (121 malware, 4365 benign).
- Benchmark AUC/AP/F1: 0.9990 / 0.9825 / 0.9664.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 92.56% | 0.00 | 0.959495 | 8.0 | 94.21% | 229.10 | 0.860931 |
| 1 | 1.0 | 94.21% | 229.10 | 0.860931 | 16.0 | 94.21% | 229.10 | 0.860931 |
| 2 | 2.0 | 94.21% | 229.10 | 0.860931 | 24.0 | 94.21% | 229.10 | 0.860931 |
| 3 | 3.0 | 94.21% | 229.10 | 0.860931 | 32.0 | 94.21% | 229.10 | 0.860931 |
| 4 | 4.0 | 94.21% | 229.10 | 0.860931 | 40.0 | 94.21% | 229.10 | 0.860931 |
| 5 | 5.0 | 94.21% | 229.10 | 0.860931 | 48.0 | 94.21% | 229.10 | 0.860931 |
| 6 | 6.0 | 94.21% | 229.10 | 0.860931 | 56.0 | 94.21% | 229.10 | 0.860931 |
| 7 | 7.0 | 94.21% | 229.10 | 0.860931 | 64.0 | 94.21% | 229.10 | 0.860931 |
| 8 | 8.0 | 94.21% | 229.10 | 0.860931 | 72.0 | 94.21% | 229.10 | 0.860931 |
| 9 | 9.0 | 94.21% | 229.10 | 0.860931 | 80.0 | 94.21% | 229.10 | 0.860931 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 5 | suspicious | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 9 | hostile | group_primary_with_escape | 61.12% | 0 | 0.00 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.07098760455846786, "general": 0.8890419602394104}` |
| 9 | suspicious | group_primary_with_escape | 63.68% | 2 | 69.28 | `{"filegroups/source": 0.8013638854026794, "filetypes/kotlin": 0.015584520995616913, "general": 0.8890419602394104}` |
