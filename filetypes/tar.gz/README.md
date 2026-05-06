# Azoth Filetype `tar.gz`
Specialist model for `tar.gz`.
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
- Training rows: 22783 (14636 malware, 8147 benign).
- Benchmark rows: 2608 (1419 malware, 1189 benign).
- Benchmark AUC/AP/F1: 0.9990 / 0.9993 / 0.9926.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.05% | 0.00 | 0.942051 | 8.0 | 96.90% | 841.04 | 0.895715 |
| 1 | 1.0 | 96.90% | 841.04 | 0.895715 | 16.0 | 96.90% | 841.04 | 0.895715 |
| 2 | 2.0 | 96.90% | 841.04 | 0.895715 | 24.0 | 96.90% | 841.04 | 0.895715 |
| 3 | 3.0 | 96.90% | 841.04 | 0.895715 | 32.0 | 96.90% | 841.04 | 0.895715 |
| 4 | 4.0 | 96.90% | 841.04 | 0.895715 | 40.0 | 96.90% | 841.04 | 0.895715 |
| 5 | 5.0 | 96.90% | 841.04 | 0.895715 | 48.0 | 96.90% | 841.04 | 0.895715 |
| 6 | 6.0 | 96.90% | 841.04 | 0.895715 | 56.0 | 96.90% | 841.04 | 0.895715 |
| 7 | 7.0 | 96.90% | 841.04 | 0.895715 | 64.0 | 96.90% | 841.04 | 0.895715 |
| 8 | 8.0 | 96.90% | 841.04 | 0.895715 | 72.0 | 96.90% | 841.04 | 0.895715 |
| 9 | 9.0 | 96.90% | 841.04 | 0.895715 | 80.0 | 96.90% | 841.04 | 0.895715 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 93.92% | 1 | 108.04 | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| 5 | suspicious | or_general_primary | 93.92% | 1 | 108.04 | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| 9 | hostile | or_general_primary | 93.92% | 1 | 108.04 | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| 9 | suspicious | or_general_primary | 93.92% | 1 | 108.04 | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
