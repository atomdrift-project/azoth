# Azoth Filetype `php`
Specialist model for `php`.
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
- Training rows: 17083 (1090 malware, 15993 benign).
- Benchmark rows: 2418 (160 malware, 2258 benign).
- Benchmark AUC/AP/F1: 0.9999 / 0.9986 / 0.9874.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 95.00% | 0.00 | 0.970051 | 8.0 | 98.12% | 442.87 | 0.885103 |
| 1 | 1.0 | 98.12% | 442.87 | 0.885103 | 16.0 | 98.12% | 442.87 | 0.885103 |
| 2 | 2.0 | 98.12% | 442.87 | 0.885103 | 24.0 | 98.12% | 442.87 | 0.885103 |
| 3 | 3.0 | 98.12% | 442.87 | 0.885103 | 32.0 | 98.12% | 442.87 | 0.885103 |
| 4 | 4.0 | 98.12% | 442.87 | 0.885103 | 40.0 | 98.12% | 442.87 | 0.885103 |
| 5 | 5.0 | 98.12% | 442.87 | 0.885103 | 48.0 | 98.12% | 442.87 | 0.885103 |
| 6 | 6.0 | 98.12% | 442.87 | 0.885103 | 56.0 | 98.12% | 442.87 | 0.885103 |
| 7 | 7.0 | 98.12% | 442.87 | 0.885103 | 64.0 | 98.12% | 442.87 | 0.885103 |
| 8 | 8.0 | 98.12% | 442.87 | 0.885103 | 72.0 | 98.12% | 442.87 | 0.885103 |
| 9 | 9.0 | 98.12% | 442.87 | 0.885103 | 80.0 | 98.12% | 442.87 | 0.885103 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 82.36% | 0 | 0.00 | `{"filetypes/php": 0.9792458415031433}` |
| 5 | suspicious | group_primary_with_escape | 85.32% | 1 | 61.07 | `{"filegroups/scripts": 0.944978654384613, "filetypes/php": 0.9792458415031433, "general": 0.92668616771698}` |
| 9 | hostile | filetype_only | 82.36% | 0 | 0.00 | `{"filetypes/php": 0.9792458415031433}` |
| 9 | suspicious | group_primary_with_escape | 85.32% | 1 | 61.07 | `{"filegroups/scripts": 0.944978654384613, "filetypes/php": 0.9792458415031433, "general": 0.92668616771698}` |
