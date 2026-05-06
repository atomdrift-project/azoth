# Azoth Filetype `data`
Specialist model for `data`.
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
- Training rows: 7718 (256 malware, 7462 benign).
- Benchmark rows: 1151 (43 malware, 1108 benign).
- Benchmark AUC/AP/F1: 0.9981 / 0.9744 / 0.9512.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 90.70% | 0.00 | 0.809101 | 8.0 | 90.70% | 902.53 | 0.559438 |
| 1 | 1.0 | 90.70% | 902.53 | 0.559438 | 16.0 | 90.70% | 902.53 | 0.559438 |
| 2 | 2.0 | 90.70% | 902.53 | 0.559438 | 24.0 | 90.70% | 902.53 | 0.559438 |
| 3 | 3.0 | 90.70% | 902.53 | 0.559438 | 32.0 | 90.70% | 902.53 | 0.559438 |
| 4 | 4.0 | 90.70% | 902.53 | 0.559438 | 40.0 | 90.70% | 902.53 | 0.559438 |
| 5 | 5.0 | 90.70% | 902.53 | 0.559438 | 48.0 | 90.70% | 902.53 | 0.559438 |
| 6 | 6.0 | 90.70% | 902.53 | 0.559438 | 56.0 | 90.70% | 902.53 | 0.559438 |
| 7 | 7.0 | 90.70% | 902.53 | 0.559438 | 64.0 | 90.70% | 902.53 | 0.559438 |
| 8 | 8.0 | 90.70% | 902.53 | 0.559438 | 72.0 | 90.70% | 902.53 | 0.559438 |
| 9 | 9.0 | 90.70% | 902.53 | 0.559438 | 80.0 | 90.70% | 902.53 | 0.559438 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 85.95% | 0 | 0.00 | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| 5 | suspicious | or_general_primary | 85.95% | 0 | 0.00 | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| 9 | hostile | or_general_primary | 85.95% | 0 | 0.00 | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| 9 | suspicious | or_general_primary | 85.95% | 0 | 0.00 | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
