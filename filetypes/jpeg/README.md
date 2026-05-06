# Azoth Filetype `jpeg`
Specialist model for `jpeg`.
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
- Training rows: 6207 (462 malware, 5745 benign).
- Benchmark rows: 839 (65 malware, 774 benign).
- Benchmark AUC/AP/F1: 0.9333 / 0.6416 / 0.5714.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | 23.08% | 1292.0 | 0.262993 |
| 1 | 1.0 | 23.08% | 1292.0 | 0.262993 | 16.0 | 23.08% | 1292.0 | 0.262993 |
| 2 | 2.0 | 23.08% | 1292.0 | 0.262993 | 24.0 | 23.08% | 1292.0 | 0.262993 |
| 3 | 3.0 | 23.08% | 1292.0 | 0.262993 | 32.0 | 23.08% | 1292.0 | 0.262993 |
| 4 | 4.0 | 23.08% | 1292.0 | 0.262993 | 40.0 | 23.08% | 1292.0 | 0.262993 |
| 5 | 5.0 | 23.08% | 1292.0 | 0.262993 | 48.0 | 23.08% | 1292.0 | 0.262993 |
| 6 | 6.0 | 23.08% | 1292.0 | 0.262993 | 56.0 | 23.08% | 1292.0 | 0.262993 |
| 7 | 7.0 | 23.08% | 1292.0 | 0.262993 | 64.0 | 23.08% | 1292.0 | 0.262993 |
| 8 | 8.0 | 23.08% | 1292.0 | 0.262993 | 72.0 | 23.08% | 1292.0 | 0.262993 |
| 9 | 9.0 | 23.08% | 1292.0 | 0.262993 | 80.0 | 23.08% | 1292.0 | 0.262993 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | general_only | 2.14% | 0 | 0.00 | `{"general": 0.2928639054298401}` |
| 5 | suspicious | general_only | 2.14% | 0 | 0.00 | `{"general": 0.2928639054298401}` |
| 9 | hostile | general_only | 2.14% | 0 | 0.00 | `{"general": 0.2928639054298401}` |
| 9 | suspicious | general_only | 2.14% | 0 | 0.00 | `{"general": 0.2928639054298401}` |
