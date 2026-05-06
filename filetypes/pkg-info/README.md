# Azoth Filetype `pkg-info`
Specialist model for `pkg-info`.
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
- Training rows: 3850 (3230 malware, 620 benign).
- Benchmark rows: 524 (441 malware, 83 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.193063 | 8.0 | 100.00% | 12048.2 | 0.095291 |
| 1 | 1.0 | 100.00% | 12048.2 | 0.095291 | 16.0 | 100.00% | 12048.2 | 0.095291 |
| 2 | 2.0 | 100.00% | 12048.2 | 0.095291 | 24.0 | 100.00% | 12048.2 | 0.095291 |
| 3 | 3.0 | 100.00% | 12048.2 | 0.095291 | 32.0 | 100.00% | 12048.2 | 0.095291 |
| 4 | 4.0 | 100.00% | 12048.2 | 0.095291 | 40.0 | 100.00% | 12048.2 | 0.095291 |
| 5 | 5.0 | 100.00% | 12048.2 | 0.095291 | 48.0 | 100.00% | 12048.2 | 0.095291 |
| 6 | 6.0 | 100.00% | 12048.2 | 0.095291 | 56.0 | 100.00% | 12048.2 | 0.095291 |
| 7 | 7.0 | 100.00% | 12048.2 | 0.095291 | 64.0 | 100.00% | 12048.2 | 0.095291 |
| 8 | 8.0 | 100.00% | 12048.2 | 0.095291 | 72.0 | 100.00% | 12048.2 | 0.095291 |
| 9 | 9.0 | 100.00% | 12048.2 | 0.095291 | 80.0 | 100.00% | 12048.2 | 0.095291 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 91.04% | 1 | 1424.5 | `{"filetypes/pkg-info": 0.07038185745477676}` |
| 5 | suspicious | filetype_only | 91.04% | 1 | 1424.5 | `{"filetypes/pkg-info": 0.07038185745477676}` |
| 9 | hostile | filetype_only | 91.04% | 1 | 1424.5 | `{"filetypes/pkg-info": 0.07038185745477676}` |
| 9 | suspicious | filetype_only | 91.04% | 1 | 1424.5 | `{"filetypes/pkg-info": 0.07038185745477676}` |
