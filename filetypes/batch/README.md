# Azoth Filetype `batch`
Specialist model for `batch`.
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
- Training rows: 1591 (270 malware, 1321 benign).
- Benchmark rows: 206 (44 malware, 162 benign).
- Benchmark AUC/AP/F1: 0.9579 / 0.9429 / 0.9286.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.09% | 0.00 | 0.784957 | 8.0 | 88.64% | 6172.8 | 0.619279 |
| 1 | 1.0 | 88.64% | 6172.8 | 0.619279 | 16.0 | 88.64% | 6172.8 | 0.619279 |
| 2 | 2.0 | 88.64% | 6172.8 | 0.619279 | 24.0 | 88.64% | 6172.8 | 0.619279 |
| 3 | 3.0 | 88.64% | 6172.8 | 0.619279 | 32.0 | 88.64% | 6172.8 | 0.619279 |
| 4 | 4.0 | 88.64% | 6172.8 | 0.619279 | 40.0 | 88.64% | 6172.8 | 0.619279 |
| 5 | 5.0 | 88.64% | 6172.8 | 0.619279 | 48.0 | 88.64% | 6172.8 | 0.619279 |
| 6 | 6.0 | 88.64% | 6172.8 | 0.619279 | 56.0 | 88.64% | 6172.8 | 0.619279 |
| 7 | 7.0 | 88.64% | 6172.8 | 0.619279 | 64.0 | 88.64% | 6172.8 | 0.619279 |
| 8 | 8.0 | 88.64% | 6172.8 | 0.619279 | 72.0 | 88.64% | 6172.8 | 0.619279 |
| 9 | 9.0 | 88.64% | 6172.8 | 0.619279 | 80.0 | 88.64% | 6172.8 | 0.619279 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 68.18% | 0 | 0.00 | `{"filetypes/batch": 0.9842783212661743}` |
| 5 | suspicious | or_general_primary | 78.25% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9842783212661743, "general": 0.8541349172592163}` |
| 9 | hostile | filetype_only | 68.18% | 0 | 0.00 | `{"filetypes/batch": 0.9842783212661743}` |
| 9 | suspicious | or_general_primary | 78.25% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9842783212661743, "general": 0.8541349172592163}` |
