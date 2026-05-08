# Azoth Filetype `batch`
Specialist model for `batch`.
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
- Training rows: 2167 (333 malware, 1834 benign).
- Benchmark rows: 290 (60 malware, 230 benign).
- Benchmark AUC/AP/F1: 0.9951 / 0.9836 / 0.9492.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 70.00% | 0.00 | 0.994239 | 8.0 | 88.33% | 4347.8 | 0.936692 |
| 1 | 1.0 | 88.33% | 4347.8 | 0.936692 | 16.0 | 88.33% | 4347.8 | 0.936692 |
| 2 | 2.0 | 88.33% | 4347.8 | 0.936692 | 24.0 | 88.33% | 4347.8 | 0.936692 |
| 3 | 3.0 | 88.33% | 4347.8 | 0.936692 | 32.0 | 88.33% | 4347.8 | 0.936692 |
| 4 | 4.0 | 88.33% | 4347.8 | 0.936692 | 40.0 | 88.33% | 4347.8 | 0.936692 |
| 5 | 5.0 | 88.33% | 4347.8 | 0.936692 | 48.0 | 88.33% | 4347.8 | 0.936692 |
| 6 | 6.0 | 88.33% | 4347.8 | 0.936692 | 56.0 | 88.33% | 4347.8 | 0.936692 |
| 7 | 7.0 | 88.33% | 4347.8 | 0.936692 | 64.0 | 88.33% | 4347.8 | 0.936692 |
| 8 | 8.0 | 88.33% | 4347.8 | 0.936692 | 72.0 | 88.33% | 4347.8 | 0.936692 |
| 9 | 9.0 | 88.33% | 4347.8 | 0.936692 | 80.0 | 88.33% | 4347.8 | 0.936692 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 79.22% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9955556988716125, "general": 0.8541349172592163}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 79.22% | 1 | 674.31 | `{"filegroups/scripts": 0.9398530125617981, "filetypes/batch": 0.9955556988716125, "general": 0.8541349172592163}` |
