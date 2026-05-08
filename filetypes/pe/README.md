# Azoth Filetype `pe`
Specialist model for `pe`.
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
- Training rows: 476539 (353276 malware, 123263 benign).
- Benchmark rows: 66060 (48516 malware, 17544 benign).
- Benchmark AUC/AP/F1: 0.9999 / 1.0000 / 0.9990.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 67.20% | 0.00 | 0.999878 | 8.0 | 83.18% | 57.00 | 0.999598 |
| 1 | 1.0 | 83.18% | 57.00 | 0.999598 | 16.0 | 83.18% | 57.00 | 0.999598 |
| 2 | 2.0 | 83.18% | 57.00 | 0.999598 | 24.0 | 83.18% | 57.00 | 0.999598 |
| 3 | 3.0 | 83.18% | 57.00 | 0.999598 | 32.0 | 83.18% | 57.00 | 0.999598 |
| 4 | 4.0 | 83.18% | 57.00 | 0.999598 | 40.0 | 83.18% | 57.00 | 0.999598 |
| 5 | 5.0 | 83.18% | 57.00 | 0.999598 | 48.0 | 83.18% | 57.00 | 0.999598 |
| 6 | 6.0 | 83.18% | 57.00 | 0.999598 | 56.0 | 83.18% | 57.00 | 0.999598 |
| 7 | 7.0 | 83.18% | 57.00 | 0.999598 | 64.0 | 83.18% | 57.00 | 0.999598 |
| 8 | 8.0 | 83.18% | 57.00 | 0.999598 | 72.0 | 83.18% | 57.00 | 0.999598 |
| 9 | 9.0 | 83.18% | 57.00 | 0.999598 | 80.0 | 83.18% | 57.00 | 0.999598 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 63.70% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9997933506965637, "general": 0.9993268251419067}` |
| 5 | suspicious | specialist_primary_with_escape | 79.11% | 6 | 45.10 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.99945068359375, "general": 0.9996013045310974}` |
| 9 | hostile | or_general_primary | 63.70% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9997933506965637, "general": 0.9993268251419067}` |
| 9 | suspicious | specialist_primary_with_escape | 84.41% | 10 | 75.17 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9992316961288452, "general": 0.9993268251419067}` |
