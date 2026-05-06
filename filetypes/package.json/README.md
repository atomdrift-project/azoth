# Azoth Filetype `package.json`
Specialist model for `package.json`.
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
- Training rows: 19163 (13519 malware, 5644 benign).
- Benchmark rows: 2667 (1844 malware, 823 benign).
- Benchmark AUC/AP/F1: 0.9992 / 0.9996 / 0.9967.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 87.09% | 0.00 | 0.995094 | 8.0 | 90.84% | 1215.1 | 0.992533 |
| 1 | 1.0 | 90.84% | 1215.1 | 0.992533 | 16.0 | 90.84% | 1215.1 | 0.992533 |
| 2 | 2.0 | 90.84% | 1215.1 | 0.992533 | 24.0 | 90.84% | 1215.1 | 0.992533 |
| 3 | 3.0 | 90.84% | 1215.1 | 0.992533 | 32.0 | 90.84% | 1215.1 | 0.992533 |
| 4 | 4.0 | 90.84% | 1215.1 | 0.992533 | 40.0 | 90.84% | 1215.1 | 0.992533 |
| 5 | 5.0 | 90.84% | 1215.1 | 0.992533 | 48.0 | 90.84% | 1215.1 | 0.992533 |
| 6 | 6.0 | 90.84% | 1215.1 | 0.992533 | 56.0 | 90.84% | 1215.1 | 0.992533 |
| 7 | 7.0 | 90.84% | 1215.1 | 0.992533 | 64.0 | 90.84% | 1215.1 | 0.992533 |
| 8 | 8.0 | 90.84% | 1215.1 | 0.992533 | 72.0 | 90.84% | 1215.1 | 0.992533 |
| 9 | 9.0 | 90.84% | 1215.1 | 0.992533 | 80.0 | 90.84% | 1215.1 | 0.992533 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_primary_with_escape | 97.73% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| 5 | suspicious | group_primary_with_escape | 97.73% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| 9 | hostile | group_primary_with_escape | 97.73% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| 9 | suspicious | group_primary_with_escape | 97.73% | 1 | 155.01 | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
