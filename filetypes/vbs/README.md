# Azoth Filetype `vbs`
Specialist model for `vbs`.
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
- Training rows: 1320 (646 malware, 674 benign).
- Benchmark rows: 184 (86 malware, 98 benign).
- Benchmark AUC/AP/F1: 0.9968 / 0.9972 / 0.9884.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 97.67% | 0.00 | 0.850961 | 8.0 | 98.84% | 10204.1 | 0.780367 |
| 1 | 1.0 | 98.84% | 10204.1 | 0.780367 | 16.0 | 98.84% | 10204.1 | 0.780367 |
| 2 | 2.0 | 98.84% | 10204.1 | 0.780367 | 24.0 | 98.84% | 10204.1 | 0.780367 |
| 3 | 3.0 | 98.84% | 10204.1 | 0.780367 | 32.0 | 98.84% | 10204.1 | 0.780367 |
| 4 | 4.0 | 98.84% | 10204.1 | 0.780367 | 40.0 | 98.84% | 10204.1 | 0.780367 |
| 5 | 5.0 | 98.84% | 10204.1 | 0.780367 | 48.0 | 98.84% | 10204.1 | 0.780367 |
| 6 | 6.0 | 98.84% | 10204.1 | 0.780367 | 56.0 | 98.84% | 10204.1 | 0.780367 |
| 7 | 7.0 | 98.84% | 10204.1 | 0.780367 | 64.0 | 98.84% | 10204.1 | 0.780367 |
| 8 | 8.0 | 98.84% | 10204.1 | 0.780367 | 72.0 | 98.84% | 10204.1 | 0.780367 |
| 9 | 9.0 | 98.84% | 10204.1 | 0.780367 | 80.0 | 98.84% | 10204.1 | 0.780367 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 68.51% | 1 | 7692.3 | `{"filetypes/vbs": 0.9668214321136475, "general": 0.9726125597953796}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 68.51% | 1 | 7692.3 | `{"filetypes/vbs": 0.9668214321136475, "general": 0.9726125597953796}` |
