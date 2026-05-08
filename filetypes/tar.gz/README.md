# Azoth Filetype `tar.gz`
Specialist model for `tar.gz`.
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
- Training rows: 28291 (17896 malware, 10395 benign).
- Benchmark rows: 2966 (1478 malware, 1488 benign).
- Benchmark AUC/AP/F1: 0.9996 / 0.9996 / 0.9959.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 98.11% | 0.00 | 0.959872 | 8.0 | 98.85% | 672.04 | 0.868223 |
| 1 | 1.0 | 98.85% | 672.04 | 0.868223 | 16.0 | 98.85% | 672.04 | 0.868223 |
| 2 | 2.0 | 98.85% | 672.04 | 0.868223 | 24.0 | 98.85% | 672.04 | 0.868223 |
| 3 | 3.0 | 98.85% | 672.04 | 0.868223 | 32.0 | 98.85% | 672.04 | 0.868223 |
| 4 | 4.0 | 98.85% | 672.04 | 0.868223 | 40.0 | 98.85% | 672.04 | 0.868223 |
| 5 | 5.0 | 98.85% | 672.04 | 0.868223 | 48.0 | 98.85% | 672.04 | 0.868223 |
| 6 | 6.0 | 98.85% | 672.04 | 0.868223 | 56.0 | 98.85% | 672.04 | 0.868223 |
| 7 | 7.0 | 98.85% | 672.04 | 0.868223 | 64.0 | 98.85% | 672.04 | 0.868223 |
| 8 | 8.0 | 98.85% | 672.04 | 0.868223 | 72.0 | 98.85% | 672.04 | 0.868223 |
| 9 | 9.0 | 98.85% | 672.04 | 0.868223 | 80.0 | 98.85% | 672.04 | 0.868223 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 94.30% | 1 | 108.04 | `{"filegroups/archive": 0.8821753859519958, "filetypes/tar.gz": 0.9358141422271729}` |
| 5 | suspicious | group_primary_with_escape | 94.30% | 1 | 108.04 | `{"filegroups/archive": 0.8821753859519958, "filetypes/tar.gz": 0.9358141422271729}` |
| 9 | hostile | group_primary_with_escape | 94.30% | 1 | 108.04 | `{"filegroups/archive": 0.8821753859519958, "filetypes/tar.gz": 0.9358141422271729}` |
| 9 | suspicious | group_primary_with_escape | 94.30% | 1 | 108.04 | `{"filegroups/archive": 0.8821753859519958, "filetypes/tar.gz": 0.9358141422271729}` |
