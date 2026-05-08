# Azoth Filetype `java_class`
Specialist model for `java_class`.
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
- Training rows: 161127 (528 malware, 160599 benign).
- Benchmark rows: 22784 (75 malware, 22709 benign).
- Benchmark AUC/AP/F1: 0.9927 / 0.9746 / 0.9865.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 97.33% | 0.00 | 0.930347 | 8.0 | 97.33% | 44.04 | 0.620390 |
| 1 | 1.0 | 97.33% | 44.04 | 0.620390 | 16.0 | 97.33% | 44.04 | 0.620390 |
| 2 | 2.0 | 97.33% | 44.04 | 0.620390 | 24.0 | 97.33% | 44.04 | 0.620390 |
| 3 | 3.0 | 97.33% | 44.04 | 0.620390 | 32.0 | 97.33% | 44.04 | 0.620390 |
| 4 | 4.0 | 97.33% | 44.04 | 0.620390 | 40.0 | 97.33% | 44.04 | 0.620390 |
| 5 | 5.0 | 97.33% | 44.04 | 0.620390 | 48.0 | 97.33% | 44.04 | 0.620390 |
| 6 | 6.0 | 97.33% | 44.04 | 0.620390 | 56.0 | 97.33% | 44.04 | 0.620390 |
| 7 | 7.0 | 97.33% | 44.04 | 0.620390 | 64.0 | 97.33% | 44.04 | 0.620390 |
| 8 | 8.0 | 97.33% | 44.04 | 0.620390 | 72.0 | 97.33% | 44.04 | 0.620390 |
| 9 | 9.0 | 97.33% | 44.04 | 0.620390 | 80.0 | 97.33% | 44.04 | 0.620390 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 5 | suspicious | group_primary_with_escape | 96.43% | 1 | 137.70 | `{"filegroups/portable": 0.8742847442626953, "filetypes/java_class": 0.2499084323644638}` |
| 9 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 9 | suspicious | group_primary_with_escape | 96.43% | 1 | 137.70 | `{"filegroups/portable": 0.8742847442626953, "filetypes/java_class": 0.2499084323644638}` |
