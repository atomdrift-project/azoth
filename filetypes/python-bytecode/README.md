# Azoth Filetype `python-bytecode`
Specialist model for `python-bytecode`.
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
- Training rows: 9630 (610 malware, 9020 benign).
- Benchmark rows: 1379 (81 malware, 1298 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.238220 | 8.0 | 100.00% | 770.42 | 0.127975 |
| 1 | 1.0 | 100.00% | 770.42 | 0.127975 | 16.0 | 100.00% | 770.42 | 0.127975 |
| 2 | 2.0 | 100.00% | 770.42 | 0.127975 | 24.0 | 100.00% | 770.42 | 0.127975 |
| 3 | 3.0 | 100.00% | 770.42 | 0.127975 | 32.0 | 100.00% | 770.42 | 0.127975 |
| 4 | 4.0 | 100.00% | 770.42 | 0.127975 | 40.0 | 100.00% | 770.42 | 0.127975 |
| 5 | 5.0 | 100.00% | 770.42 | 0.127975 | 48.0 | 100.00% | 770.42 | 0.127975 |
| 6 | 6.0 | 100.00% | 770.42 | 0.127975 | 56.0 | 100.00% | 770.42 | 0.127975 |
| 7 | 7.0 | 100.00% | 770.42 | 0.127975 | 64.0 | 100.00% | 770.42 | 0.127975 |
| 8 | 8.0 | 100.00% | 770.42 | 0.127975 | 72.0 | 100.00% | 770.42 | 0.127975 |
| 9 | 9.0 | 100.00% | 770.42 | 0.127975 | 80.0 | 100.00% | 770.42 | 0.127975 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 92.86% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.9686558246612549}` |
| 5 | suspicious | filetype_only | 92.86% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.9686558246612549}` |
| 9 | hostile | filetype_only | 92.86% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.9686558246612549}` |
| 9 | suspicious | filetype_only | 92.86% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.9686558246612549}` |
