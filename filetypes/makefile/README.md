# Azoth Filetype `makefile`
Specialist model for `makefile`.
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
- Training rows: 15557 (62 malware, 15495 benign).
- Benchmark rows: 2275 (4 malware, 2271 benign).
- Benchmark AUC/AP/F1: 0.8778 / 0.3366 / 0.4000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 25.00% | 0.00 | 0.997118 | 8.0 | 25.00% | 440.33 | 0.987454 |
| 1 | 1.0 | 25.00% | 440.33 | 0.987454 | 16.0 | 25.00% | 440.33 | 0.987454 |
| 2 | 2.0 | 25.00% | 440.33 | 0.987454 | 24.0 | 25.00% | 440.33 | 0.987454 |
| 3 | 3.0 | 25.00% | 440.33 | 0.987454 | 32.0 | 25.00% | 440.33 | 0.987454 |
| 4 | 4.0 | 25.00% | 440.33 | 0.987454 | 40.0 | 25.00% | 440.33 | 0.987454 |
| 5 | 5.0 | 25.00% | 440.33 | 0.987454 | 48.0 | 25.00% | 440.33 | 0.987454 |
| 6 | 6.0 | 25.00% | 440.33 | 0.987454 | 56.0 | 25.00% | 440.33 | 0.987454 |
| 7 | 7.0 | 25.00% | 440.33 | 0.987454 | 64.0 | 25.00% | 440.33 | 0.987454 |
| 8 | 8.0 | 25.00% | 440.33 | 0.987454 | 72.0 | 25.00% | 440.33 | 0.987454 |
| 9 | 9.0 | 25.00% | 440.33 | 0.987454 | 80.0 | 25.00% | 440.33 | 0.987454 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 5 | suspicious | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 9 | hostile | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
| 9 | suspicious | general_only | 1.54% | 0 | 0.00 | `{"general": 0.8322421908378601}` |
