# Azoth Filetype `rust`
Specialist model for `rust`.
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
- Training rows: 55681 (45 malware, 55636 benign).
- Benchmark rows: 7928 (7 malware, 7921 benign).
- Benchmark AUC/AP/F1: 0.9931 / 0.1496 / 0.2500.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | 14.29% | 126.25 | 1.000000 |
| 1 | 1.0 | 14.29% | 126.25 | 1.000000 | 16.0 | 14.29% | 126.25 | 1.000000 |
| 2 | 2.0 | 14.29% | 126.25 | 1.000000 | 24.0 | 14.29% | 126.25 | 1.000000 |
| 3 | 3.0 | 14.29% | 126.25 | 1.000000 | 32.0 | 14.29% | 126.25 | 1.000000 |
| 4 | 4.0 | 14.29% | 126.25 | 1.000000 | 40.0 | 14.29% | 126.25 | 1.000000 |
| 5 | 5.0 | 14.29% | 126.25 | 1.000000 | 48.0 | 14.29% | 126.25 | 1.000000 |
| 6 | 6.0 | 14.29% | 126.25 | 1.000000 | 56.0 | 14.29% | 126.25 | 1.000000 |
| 7 | 7.0 | 14.29% | 126.25 | 1.000000 | 64.0 | 14.29% | 126.25 | 1.000000 |
| 8 | 8.0 | 14.29% | 126.25 | 1.000000 | 72.0 | 14.29% | 126.25 | 1.000000 |
| 9 | 9.0 | 14.29% | 126.25 | 1.000000 | 80.0 | 14.29% | 126.25 | 1.000000 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 25.00% | 0 | 0.00 | `{"filegroups/source": 0.6817883253097534, "general": 0.09213332086801529}` |
| 5 | suspicious | group_primary_with_escape | 25.00% | 0 | 0.00 | `{"filegroups/source": 0.6817883253097534, "general": 0.09213332086801529}` |
| 9 | hostile | group_primary_with_escape | 25.00% | 0 | 0.00 | `{"filegroups/source": 0.6817883253097534, "general": 0.09213332086801529}` |
| 9 | suspicious | group_primary_with_escape | 26.92% | 4 | 62.94 | `{"filegroups/source": 0.6817883253097534, "filetypes/rust": 5.522569467280327e-24, "general": 0.09213332086801529}` |
