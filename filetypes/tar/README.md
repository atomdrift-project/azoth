# Azoth Filetype `tar`
Specialist model for `tar`.
- Inputs: shared general `feature_spec.json` (37595 features); policy `general_shared`.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 1227 (932 malware, 295 benign).
- Benchmark rows: 152 (109 malware, 43 benign).
- Benchmark AUC/AP/F1: 0.9888 / 0.9957 / 0.9860.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 97.25% | 0.00 | 0.343225 | 8.0 | 97.25% | 0.00 | 0.343225 |
| 1 | 1.0 | 97.25% | 0.00 | 0.343225 | 16.0 | 97.25% | 0.00 | 0.343225 |
| 2 | 2.0 | 97.25% | 0.00 | 0.343225 | 24.0 | 97.25% | 0.00 | 0.343225 |
| 3 | 3.0 | 97.25% | 0.00 | 0.343225 | 32.0 | 97.25% | 0.00 | 0.343225 |
| 4 | 4.0 | 97.25% | 0.00 | 0.343225 | 40.0 | 97.25% | 0.00 | 0.343225 |
| 5 | 5.0 | 97.25% | 0.00 | 0.343225 | 48.0 | 97.25% | 0.00 | 0.343225 |
| 6 | 6.0 | 97.25% | 0.00 | 0.343225 | 56.0 | 97.25% | 0.00 | 0.343225 |
| 7 | 7.0 | 97.25% | 0.00 | 0.343225 | 64.0 | 97.25% | 0.00 | 0.343225 |
| 8 | 8.0 | 97.25% | 0.00 | 0.343225 | 72.0 | 97.25% | 0.00 | 0.343225 |
| 9 | 9.0 | 97.25% | 0.00 | 0.343225 | 80.0 | 97.25% | 0.00 | 0.343225 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 90.87% | 0 | 0.00 | `{"filetypes/tar": 0.5931394696235657}` |
| 5 | suspicious | or_general_primary | 97.12% | 1 | 2958.6 | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5931394696235657, "general": 0.8572259545326233}` |
| 9 | hostile | filetype_only | 90.87% | 0 | 0.00 | `{"filetypes/tar": 0.5931394696235657}` |
| 9 | suspicious | or_general_primary | 97.12% | 1 | 2958.6 | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5931394696235657, "general": 0.8572259545326233}` |
