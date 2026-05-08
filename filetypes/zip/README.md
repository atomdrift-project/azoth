# Azoth Filetype `zip`
Specialist model for `zip`.
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
- Training rows: 33762 (28881 malware, 4881 benign).
- Benchmark rows: 4595 (3926 malware, 669 benign).
- Benchmark AUC/AP/F1: 0.9984 / 0.9997 / 0.9950.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 77.59% | 0.00 | 0.998992 | 8.0 | 90.98% | 1494.8 | 0.985054 |
| 1 | 1.0 | 90.98% | 1494.8 | 0.985054 | 16.0 | 90.98% | 1494.8 | 0.985054 |
| 2 | 2.0 | 90.98% | 1494.8 | 0.985054 | 24.0 | 90.98% | 1494.8 | 0.985054 |
| 3 | 3.0 | 90.98% | 1494.8 | 0.985054 | 32.0 | 90.98% | 1494.8 | 0.985054 |
| 4 | 4.0 | 90.98% | 1494.8 | 0.985054 | 40.0 | 90.98% | 1494.8 | 0.985054 |
| 5 | 5.0 | 90.98% | 1494.8 | 0.985054 | 48.0 | 90.98% | 1494.8 | 0.985054 |
| 6 | 6.0 | 90.98% | 1494.8 | 0.985054 | 56.0 | 90.98% | 1494.8 | 0.985054 |
| 7 | 7.0 | 90.98% | 1494.8 | 0.985054 | 64.0 | 90.98% | 1494.8 | 0.985054 |
| 8 | 8.0 | 90.98% | 1494.8 | 0.985054 | 72.0 | 90.98% | 1494.8 | 0.985054 |
| 9 | 9.0 | 90.98% | 1494.8 | 0.985054 | 80.0 | 90.98% | 1494.8 | 0.985054 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 84.33% | 1 | 352.73 | `{"filegroups/archive": 0.999099612236023, "filetypes/zip": 0.9961474537849426, "general": 0.9974381327629089}` |
| 5 | suspicious | group_primary_with_escape | 84.33% | 1 | 352.73 | `{"filegroups/archive": 0.999099612236023, "filetypes/zip": 0.9961474537849426, "general": 0.9974381327629089}` |
| 9 | hostile | group_primary_with_escape | 84.33% | 1 | 352.73 | `{"filegroups/archive": 0.999099612236023, "filetypes/zip": 0.9961474537849426, "general": 0.9974381327629089}` |
| 9 | suspicious | group_primary_with_escape | 84.33% | 1 | 352.73 | `{"filegroups/archive": 0.999099612236023, "filetypes/zip": 0.9961474537849426, "general": 0.9974381327629089}` |
