# Azoth Filetype `ole`
Specialist model for `ole`.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=50, device=cpu.
- Training rows: 4918 (229 malware, 4689 benign).
- Benchmark rows: 688 (30 malware, 658 benign).
- Benchmark AUC/AP/F1: 0.9999 / 0.9979 / 0.9831.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.67% | 0.00 | 0.831924 | 8.0 | 96.67% | 1519.8 | 0.775652 |
| 1 | 1.0 | 96.67% | 1519.8 | 0.775652 | 16.0 | 96.67% | 1519.8 | 0.775652 |
| 2 | 2.0 | 96.67% | 1519.8 | 0.775652 | 24.0 | 96.67% | 1519.8 | 0.775652 |
| 3 | 3.0 | 96.67% | 1519.8 | 0.775652 | 32.0 | 96.67% | 1519.8 | 0.775652 |
| 4 | 4.0 | 96.67% | 1519.8 | 0.775652 | 40.0 | 96.67% | 1519.8 | 0.775652 |
| 5 | 5.0 | 96.67% | 1519.8 | 0.775652 | 48.0 | 96.67% | 1519.8 | 0.775652 |
| 6 | 6.0 | 96.67% | 1519.8 | 0.775652 | 56.0 | 96.67% | 1519.8 | 0.775652 |
| 7 | 7.0 | 96.67% | 1519.8 | 0.775652 | 64.0 | 96.67% | 1519.8 | 0.775652 |
| 8 | 8.0 | 96.67% | 1519.8 | 0.775652 | 72.0 | 96.67% | 1519.8 | 0.775652 |
| 9 | 9.0 | 96.67% | 1519.8 | 0.775652 | 80.0 | 96.67% | 1519.8 | 0.775652 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 82.77% | 1 | 188.61 | `{"filetypes/ole": 0.9965583682060242, "general": 0.9733341336250305}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | or_general_primary | 82.77% | 1 | 188.61 | `{"filetypes/ole": 0.9965583682060242, "general": 0.9733341336250305}` |
