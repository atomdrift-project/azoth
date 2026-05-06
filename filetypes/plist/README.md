# Azoth Filetype `plist`
Specialist model for `plist`.
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
- Training rows: 8187 (416 malware, 7771 benign).
- Benchmark rows: 1159 (58 malware, 1101 benign).
- Benchmark AUC/AP/F1: 0.9908 / 0.9114 / 0.8522.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 24.14% | 0.00 | 0.993849 | 8.0 | 63.79% | 908.27 | 0.952783 |
| 1 | 1.0 | 63.79% | 908.27 | 0.952783 | 16.0 | 63.79% | 908.27 | 0.952783 |
| 2 | 2.0 | 63.79% | 908.27 | 0.952783 | 24.0 | 63.79% | 908.27 | 0.952783 |
| 3 | 3.0 | 63.79% | 908.27 | 0.952783 | 32.0 | 63.79% | 908.27 | 0.952783 |
| 4 | 4.0 | 63.79% | 908.27 | 0.952783 | 40.0 | 63.79% | 908.27 | 0.952783 |
| 5 | 5.0 | 63.79% | 908.27 | 0.952783 | 48.0 | 63.79% | 908.27 | 0.952783 |
| 6 | 6.0 | 63.79% | 908.27 | 0.952783 | 56.0 | 63.79% | 908.27 | 0.952783 |
| 7 | 7.0 | 63.79% | 908.27 | 0.952783 | 64.0 | 63.79% | 908.27 | 0.952783 |
| 8 | 8.0 | 63.79% | 908.27 | 0.952783 | 72.0 | 63.79% | 908.27 | 0.952783 |
| 9 | 9.0 | 63.79% | 908.27 | 0.952783 | 80.0 | 63.79% | 908.27 | 0.952783 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 8.12% | 1 | 112.83 | `{"filetypes/plist": 0.6069956421852112, "general": 0.16379986703395844}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 8.12% | 1 | 112.83 | `{"filetypes/plist": 0.6069956421852112, "general": 0.16379986703395844}` |
