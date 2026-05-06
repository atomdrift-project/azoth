# Azoth Filetype `shell`
Specialist model for `shell`.
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
- Training rows: 33221 (1491 malware, 31730 benign).
- Benchmark rows: 4802 (306 malware, 4496 benign).
- Benchmark AUC/AP/F1: 0.9911 / 0.9657 / 0.9465.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.64% | 0.00 | 0.992294 | 8.0 | 88.56% | 222.42 | 0.970824 |
| 1 | 1.0 | 88.56% | 222.42 | 0.970824 | 16.0 | 88.56% | 222.42 | 0.970824 |
| 2 | 2.0 | 88.56% | 222.42 | 0.970824 | 24.0 | 88.56% | 222.42 | 0.970824 |
| 3 | 3.0 | 88.56% | 222.42 | 0.970824 | 32.0 | 88.56% | 222.42 | 0.970824 |
| 4 | 4.0 | 88.56% | 222.42 | 0.970824 | 40.0 | 88.56% | 222.42 | 0.970824 |
| 5 | 5.0 | 88.56% | 222.42 | 0.970824 | 48.0 | 88.56% | 222.42 | 0.970824 |
| 6 | 6.0 | 88.56% | 222.42 | 0.970824 | 56.0 | 88.56% | 222.42 | 0.970824 |
| 7 | 7.0 | 88.56% | 222.42 | 0.970824 | 64.0 | 88.56% | 222.42 | 0.970824 |
| 8 | 8.0 | 88.56% | 222.42 | 0.970824 | 72.0 | 88.56% | 222.42 | 0.970824 |
| 9 | 9.0 | 88.56% | 222.42 | 0.970824 | 80.0 | 88.56% | 222.42 | 0.970824 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 69.31% | 1 | 28.11 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9585855007171631, "general": 0.9515489339828491}` |
| 9 | hostile | group_primary_with_escape | 69.31% | 1 | 28.11 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9585855007171631, "general": 0.9515489339828491}` |
| 9 | suspicious | specialist_primary_with_escape | 70.73% | 2 | 56.22 | `{"filegroups/scripts": 0.9822300672531128, "filetypes/shell": 0.9323660731315613, "general": 0.9515489339828491}` |
