# Azoth Filetype `jar`
Specialist model for `jar`.
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
- Training rows: 1423 (483 malware, 940 benign).
- Benchmark rows: 222 (101 malware, 121 benign).
- Benchmark AUC/AP/F1: 0.9959 / 0.9953 / 0.9800.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 78.22% | 0.00 | 0.941950 | 8.0 | 97.03% | 8264.5 | 0.602814 |
| 1 | 1.0 | 97.03% | 8264.5 | 0.602814 | 16.0 | 97.03% | 8264.5 | 0.602814 |
| 2 | 2.0 | 97.03% | 8264.5 | 0.602814 | 24.0 | 97.03% | 8264.5 | 0.602814 |
| 3 | 3.0 | 97.03% | 8264.5 | 0.602814 | 32.0 | 97.03% | 8264.5 | 0.602814 |
| 4 | 4.0 | 97.03% | 8264.5 | 0.602814 | 40.0 | 97.03% | 8264.5 | 0.602814 |
| 5 | 5.0 | 97.03% | 8264.5 | 0.602814 | 48.0 | 97.03% | 8264.5 | 0.602814 |
| 6 | 6.0 | 97.03% | 8264.5 | 0.602814 | 56.0 | 97.03% | 8264.5 | 0.602814 |
| 7 | 7.0 | 97.03% | 8264.5 | 0.602814 | 64.0 | 97.03% | 8264.5 | 0.602814 |
| 8 | 8.0 | 97.03% | 8264.5 | 0.602814 | 72.0 | 97.03% | 8264.5 | 0.602814 |
| 9 | 9.0 | 97.03% | 8264.5 | 0.602814 | 80.0 | 97.03% | 8264.5 | 0.602814 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 88.36% | 1 | 942.51 | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
| 9 | hostile | or_general_primary | 88.36% | 1 | 942.51 | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
| 9 | suspicious | or_general_primary | 88.36% | 1 | 942.51 | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
