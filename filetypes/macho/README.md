# Azoth Filetype `macho`
Specialist model for `macho`.
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
- Training rows: 5398 (1159 malware, 4239 benign).
- Benchmark rows: 771 (145 malware, 626 benign).
- Benchmark AUC/AP/F1: 0.9991 / 0.9953 / 0.9831.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 60.69% | 0.00 | 0.995418 | 8.0 | 93.10% | 1597.4 | 0.931796 |
| 1 | 1.0 | 93.10% | 1597.4 | 0.931796 | 16.0 | 93.10% | 1597.4 | 0.931796 |
| 2 | 2.0 | 93.10% | 1597.4 | 0.931796 | 24.0 | 93.10% | 1597.4 | 0.931796 |
| 3 | 3.0 | 93.10% | 1597.4 | 0.931796 | 32.0 | 93.10% | 1597.4 | 0.931796 |
| 4 | 4.0 | 93.10% | 1597.4 | 0.931796 | 40.0 | 93.10% | 1597.4 | 0.931796 |
| 5 | 5.0 | 93.10% | 1597.4 | 0.931796 | 48.0 | 93.10% | 1597.4 | 0.931796 |
| 6 | 6.0 | 93.10% | 1597.4 | 0.931796 | 56.0 | 93.10% | 1597.4 | 0.931796 |
| 7 | 7.0 | 93.10% | 1597.4 | 0.931796 | 64.0 | 93.10% | 1597.4 | 0.931796 |
| 8 | 8.0 | 93.10% | 1597.4 | 0.931796 | 72.0 | 93.10% | 1597.4 | 0.931796 |
| 9 | 9.0 | 93.10% | 1597.4 | 0.931796 | 80.0 | 93.10% | 1597.4 | 0.931796 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 60.03% | 1 | 206.02 | `{"filegroups/native": 0.9966633915901184, "filetypes/macho": 0.9784113764762878, "general": 0.9814670085906982}` |
| 9 | hostile | group_primary_with_escape | 60.03% | 1 | 206.02 | `{"filegroups/native": 0.9966633915901184, "filetypes/macho": 0.9784113764762878, "general": 0.9814670085906982}` |
| 9 | suspicious | group_primary_with_escape | 60.03% | 1 | 206.02 | `{"filegroups/native": 0.9966633915901184, "filetypes/macho": 0.9784113764762878, "general": 0.9814670085906982}` |
