# Azoth Filetype `ruby`
Specialist model for `ruby`.
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
- Training rows: 20365 (63 malware, 20302 benign).
- Benchmark rows: 2813 (7 malware, 2806 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.975179 | 8.0 | 100.00% | 356.38 | 0.662422 |
| 1 | 1.0 | 100.00% | 356.38 | 0.662422 | 16.0 | 100.00% | 356.38 | 0.662422 |
| 2 | 2.0 | 100.00% | 356.38 | 0.662422 | 24.0 | 100.00% | 356.38 | 0.662422 |
| 3 | 3.0 | 100.00% | 356.38 | 0.662422 | 32.0 | 100.00% | 356.38 | 0.662422 |
| 4 | 4.0 | 100.00% | 356.38 | 0.662422 | 40.0 | 100.00% | 356.38 | 0.662422 |
| 5 | 5.0 | 100.00% | 356.38 | 0.662422 | 48.0 | 100.00% | 356.38 | 0.662422 |
| 6 | 6.0 | 100.00% | 356.38 | 0.662422 | 56.0 | 100.00% | 356.38 | 0.662422 |
| 7 | 7.0 | 100.00% | 356.38 | 0.662422 | 64.0 | 100.00% | 356.38 | 0.662422 |
| 8 | 8.0 | 100.00% | 356.38 | 0.662422 | 72.0 | 100.00% | 356.38 | 0.662422 |
| 9 | 9.0 | 100.00% | 356.38 | 0.662422 | 80.0 | 100.00% | 356.38 | 0.662422 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 95.65% | 1 | 83.72 | `{"filegroups/scripts": 0.9614102840423584, "filetypes/ruby": 0.9984004497528076}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 95.65% | 1 | 83.72 | `{"filegroups/scripts": 0.9614102840423584, "filetypes/ruby": 0.9984004497528076}` |
