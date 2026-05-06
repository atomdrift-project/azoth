# Azoth Filetype `vbs`
Specialist model for `vbs`.
- Inputs: shared general `feature_spec.json` (37595 features); policy `general_shared`.
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
- Training rows: 631 (519 malware, 112 benign).
- Benchmark rows: 88 (70 malware, 18 benign).
- Benchmark AUC/AP/F1: 0.9131 / 0.9751 / 0.9296.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 65.71% | 0.00 | 0.848943 | 8.0 | 67.14% | 55555.6 | 0.781721 |
| 1 | 1.0 | 67.14% | 55555.6 | 0.781721 | 16.0 | 67.14% | 55555.6 | 0.781721 |
| 2 | 2.0 | 67.14% | 55555.6 | 0.781721 | 24.0 | 67.14% | 55555.6 | 0.781721 |
| 3 | 3.0 | 67.14% | 55555.6 | 0.781721 | 32.0 | 67.14% | 55555.6 | 0.781721 |
| 4 | 4.0 | 67.14% | 55555.6 | 0.781721 | 40.0 | 67.14% | 55555.6 | 0.781721 |
| 5 | 5.0 | 67.14% | 55555.6 | 0.781721 | 48.0 | 67.14% | 55555.6 | 0.781721 |
| 6 | 6.0 | 67.14% | 55555.6 | 0.781721 | 56.0 | 67.14% | 55555.6 | 0.781721 |
| 7 | 7.0 | 67.14% | 55555.6 | 0.781721 | 64.0 | 67.14% | 55555.6 | 0.781721 |
| 8 | 8.0 | 67.14% | 55555.6 | 0.781721 | 72.0 | 67.14% | 55555.6 | 0.781721 |
| 9 | 9.0 | 67.14% | 55555.6 | 0.781721 | 80.0 | 67.14% | 55555.6 | 0.781721 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 59.00% | 1 | 7692.3 | `{"filetypes/vbs": 0.8690733909606934, "general": 0.9726125597953796}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 59.00% | 1 | 7692.3 | `{"filetypes/vbs": 0.8690733909606934, "general": 0.9726125597953796}` |
