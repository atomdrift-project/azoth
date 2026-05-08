# Azoth Filetype `perl`
Specialist model for `perl`.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=48, max_depth=12, min_child_samples=140, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.5, reg_lambda=4.0, early_stop=50, device=cpu.
- Training rows: 25798 (133 malware, 25665 benign).
- Benchmark rows: 3721 (18 malware, 3703 benign).
- Benchmark AUC/AP/F1: 0.9994 / 0.9608 / 0.9714.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.44% | 0.00 | 0.992144 | 8.0 | 94.44% | 270.05 | 0.910061 |
| 1 | 1.0 | 94.44% | 270.05 | 0.910061 | 16.0 | 94.44% | 270.05 | 0.910061 |
| 2 | 2.0 | 94.44% | 270.05 | 0.910061 | 24.0 | 94.44% | 270.05 | 0.910061 |
| 3 | 3.0 | 94.44% | 270.05 | 0.910061 | 32.0 | 94.44% | 270.05 | 0.910061 |
| 4 | 4.0 | 94.44% | 270.05 | 0.910061 | 40.0 | 94.44% | 270.05 | 0.910061 |
| 5 | 5.0 | 94.44% | 270.05 | 0.910061 | 48.0 | 94.44% | 270.05 | 0.910061 |
| 6 | 6.0 | 94.44% | 270.05 | 0.910061 | 56.0 | 94.44% | 270.05 | 0.910061 |
| 7 | 7.0 | 94.44% | 270.05 | 0.910061 | 64.0 | 94.44% | 270.05 | 0.910061 |
| 8 | 8.0 | 94.44% | 270.05 | 0.910061 | 72.0 | 94.44% | 270.05 | 0.910061 |
| 9 | 9.0 | 94.44% | 270.05 | 0.910061 | 80.0 | 94.44% | 270.05 | 0.910061 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 5 | suspicious | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 9 | hostile | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
| 9 | suspicious | specialist_primary_with_escape | 85.23% | 0 | 0.00 | `{"filegroups/scripts": 0.8397799730300903, "filetypes/perl": 0.6115842461585999}` |
