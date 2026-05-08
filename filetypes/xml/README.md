# Azoth Filetype `xml`
Specialist model for `xml`.
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
- Training rows: 73866 (895 malware, 72971 benign).
- Benchmark rows: 10593 (144 malware, 10449 benign).
- Benchmark AUC/AP/F1: 0.8995 / 0.1039 / 0.1894.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | - | - | - |
| 1 | 1.0 | - | - | - | 16.0 | - | - | - |
| 2 | 2.0 | - | - | - | 24.0 | - | - | - |
| 3 | 3.0 | - | - | - | 32.0 | - | - | - |
| 4 | 4.0 | - | - | - | 40.0 | - | - | - |
| 5 | 5.0 | - | - | - | 48.0 | - | - | - |
| 6 | 6.0 | - | - | - | 56.0 | - | - | - |
| 7 | 7.0 | - | - | - | 64.0 | - | - | - |
| 8 | 8.0 | - | - | - | 72.0 | - | - | - |
| 9 | 9.0 | - | - | - | 80.0 | - | - | - |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 2.70% | 0 | 0.00 | `{"filegroups/config": 0.5439979434013367, "general": 0.6749266386032104}` |
| 5 | suspicious | or_general_primary | 3.09% | 2 | 23.99 | `{"filegroups/config": 0.05154723674058914, "general": 0.6749266386032104}` |
| 9 | hostile | or_general_primary | 2.70% | 0 | 0.00 | `{"filegroups/config": 0.5439979434013367, "general": 0.6749266386032104}` |
| 9 | suspicious | or_general_primary | 3.19% | 6 | 71.98 | `{"filegroups/config": 0.05154723674058914, "general": 0.10532117635011673}` |
