# Azoth Filetype `powershell`
Specialist model for `powershell`.
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
- Training rows: 1051 (291 malware, 760 benign).
- Benchmark rows: 159 (47 malware, 112 benign).
- Benchmark AUC/AP/F1: 0.9953 / 0.9902 / 0.9574.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 89.36% | 0.00 | 0.900818 | 8.0 | 91.49% | 8928.6 | 0.880548 |
| 1 | 1.0 | 91.49% | 8928.6 | 0.880548 | 16.0 | 91.49% | 8928.6 | 0.880548 |
| 2 | 2.0 | 91.49% | 8928.6 | 0.880548 | 24.0 | 91.49% | 8928.6 | 0.880548 |
| 3 | 3.0 | 91.49% | 8928.6 | 0.880548 | 32.0 | 91.49% | 8928.6 | 0.880548 |
| 4 | 4.0 | 91.49% | 8928.6 | 0.880548 | 40.0 | 91.49% | 8928.6 | 0.880548 |
| 5 | 5.0 | 91.49% | 8928.6 | 0.880548 | 48.0 | 91.49% | 8928.6 | 0.880548 |
| 6 | 6.0 | 91.49% | 8928.6 | 0.880548 | 56.0 | 91.49% | 8928.6 | 0.880548 |
| 7 | 7.0 | 91.49% | 8928.6 | 0.880548 | 64.0 | 91.49% | 8928.6 | 0.880548 |
| 8 | 8.0 | 91.49% | 8928.6 | 0.880548 | 72.0 | 91.49% | 8928.6 | 0.880548 |
| 9 | 9.0 | 91.49% | 8928.6 | 0.880548 | 80.0 | 91.49% | 8928.6 | 0.880548 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 65.58% | 1 | 1146.8 | `{"filegroups/scripts": 0.9872816801071167, "filetypes/powershell": 0.9841626286506653}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 65.58% | 1 | 1146.8 | `{"filegroups/scripts": 0.9872816801071167, "filetypes/powershell": 0.9841626286506653}` |
