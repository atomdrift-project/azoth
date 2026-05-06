# Azoth Filetype `perl`
Specialist model for `perl`.
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
- Training rows: 19168 (131 malware, 19037 benign).
- Benchmark rows: 2744 (18 malware, 2726 benign).
- Benchmark AUC/AP/F1: 0.9999 / 0.9899 / 0.9714.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.44% | 0.00 | 0.993226 | 8.0 | 94.44% | 366.84 | 0.700704 |
| 1 | 1.0 | 94.44% | 366.84 | 0.700704 | 16.0 | 94.44% | 366.84 | 0.700704 |
| 2 | 2.0 | 94.44% | 366.84 | 0.700704 | 24.0 | 94.44% | 366.84 | 0.700704 |
| 3 | 3.0 | 94.44% | 366.84 | 0.700704 | 32.0 | 94.44% | 366.84 | 0.700704 |
| 4 | 4.0 | 94.44% | 366.84 | 0.700704 | 40.0 | 94.44% | 366.84 | 0.700704 |
| 5 | 5.0 | 94.44% | 366.84 | 0.700704 | 48.0 | 94.44% | 366.84 | 0.700704 |
| 6 | 6.0 | 94.44% | 366.84 | 0.700704 | 56.0 | 94.44% | 366.84 | 0.700704 |
| 7 | 7.0 | 94.44% | 366.84 | 0.700704 | 64.0 | 94.44% | 366.84 | 0.700704 |
| 8 | 8.0 | 94.44% | 366.84 | 0.700704 | 72.0 | 94.44% | 366.84 | 0.700704 |
| 9 | 9.0 | 94.44% | 366.84 | 0.700704 | 80.0 | 94.44% | 366.84 | 0.700704 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | group_primary_with_escape | 82.55% | 1 | 45.63 | `{"filegroups/scripts": 0.7477678060531616, "filetypes/perl": 0.9500136375427246}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | group_primary_with_escape | 82.55% | 1 | 45.63 | `{"filegroups/scripts": 0.7477678060531616, "filetypes/perl": 0.9500136375427246}` |
