# Azoth Filetype `ole`
Specialist model for `ole`.
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
- Training rows: 5056 (375 malware, 4681 benign).
- Benchmark rows: 702 (47 malware, 655 benign).
- Benchmark AUC/AP/F1: 0.9787 / 0.9603 / 0.9783.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 95.74% | 0.00 | 0.938259 | 8.0 | 95.74% | 1526.7 | 0.915004 |
| 1 | 1.0 | 95.74% | 1526.7 | 0.915004 | 16.0 | 95.74% | 1526.7 | 0.915004 |
| 2 | 2.0 | 95.74% | 1526.7 | 0.915004 | 24.0 | 95.74% | 1526.7 | 0.915004 |
| 3 | 3.0 | 95.74% | 1526.7 | 0.915004 | 32.0 | 95.74% | 1526.7 | 0.915004 |
| 4 | 4.0 | 95.74% | 1526.7 | 0.915004 | 40.0 | 95.74% | 1526.7 | 0.915004 |
| 5 | 5.0 | 95.74% | 1526.7 | 0.915004 | 48.0 | 95.74% | 1526.7 | 0.915004 |
| 6 | 6.0 | 95.74% | 1526.7 | 0.915004 | 56.0 | 95.74% | 1526.7 | 0.915004 |
| 7 | 7.0 | 95.74% | 1526.7 | 0.915004 | 64.0 | 95.74% | 1526.7 | 0.915004 |
| 8 | 8.0 | 95.74% | 1526.7 | 0.915004 | 72.0 | 95.74% | 1526.7 | 0.915004 |
| 9 | 9.0 | 95.74% | 1526.7 | 0.915004 | 80.0 | 95.74% | 1526.7 | 0.915004 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 88.93% | 1 | 188.43 | `{"filetypes/ole": 0.9899150729179382, "general": 0.9884464740753174}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 88.93% | 1 | 188.43 | `{"filetypes/ole": 0.9899150729179382, "general": 0.9884464740753174}` |
