# Azoth Filetype `python-bytecode`
Specialist model for `python-bytecode`.
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
- Training rows: 7407 (75 malware, 7332 benign).
- Benchmark rows: 1088 (9 malware, 1079 benign).
- Benchmark AUC/AP/F1: 0.9996 / 0.9658 / 0.9412.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 88.89% | 0.00 | 0.996752 | 8.0 | 88.89% | 926.78 | 0.615042 |
| 1 | 1.0 | 88.89% | 926.78 | 0.615042 | 16.0 | 88.89% | 926.78 | 0.615042 |
| 2 | 2.0 | 88.89% | 926.78 | 0.615042 | 24.0 | 88.89% | 926.78 | 0.615042 |
| 3 | 3.0 | 88.89% | 926.78 | 0.615042 | 32.0 | 88.89% | 926.78 | 0.615042 |
| 4 | 4.0 | 88.89% | 926.78 | 0.615042 | 40.0 | 88.89% | 926.78 | 0.615042 |
| 5 | 5.0 | 88.89% | 926.78 | 0.615042 | 48.0 | 88.89% | 926.78 | 0.615042 |
| 6 | 6.0 | 88.89% | 926.78 | 0.615042 | 56.0 | 88.89% | 926.78 | 0.615042 |
| 7 | 7.0 | 88.89% | 926.78 | 0.615042 | 64.0 | 88.89% | 926.78 | 0.615042 |
| 8 | 8.0 | 88.89% | 926.78 | 0.615042 | 72.0 | 88.89% | 926.78 | 0.615042 |
| 9 | 9.0 | 88.89% | 926.78 | 0.615042 | 80.0 | 88.89% | 926.78 | 0.615042 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 91.67% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| 5 | suspicious | filetype_only | 91.67% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| 9 | hostile | filetype_only | 91.67% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| 9 | suspicious | filetype_only | 91.67% | 0 | 0.00 | `{"filetypes/python-bytecode": 0.7946628332138062}` |
