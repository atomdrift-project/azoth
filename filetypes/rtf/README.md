# Azoth Filetype `rtf`
Specialist model for `rtf`.
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
- Training rows: 466 (78 malware, 388 benign).
- Benchmark rows: 56 (11 malware, 45 benign).
- Benchmark AUC/AP/F1: 0.9919 / 0.9485 / 0.9565.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 45.45% | 0.00 | 0.994640 | 8.0 | 100.00% | 22222.2 | 0.818988 |
| 1 | 1.0 | 100.00% | 22222.2 | 0.818988 | 16.0 | 100.00% | 22222.2 | 0.818988 |
| 2 | 2.0 | 100.00% | 22222.2 | 0.818988 | 24.0 | 100.00% | 22222.2 | 0.818988 |
| 3 | 3.0 | 100.00% | 22222.2 | 0.818988 | 32.0 | 100.00% | 22222.2 | 0.818988 |
| 4 | 4.0 | 100.00% | 22222.2 | 0.818988 | 40.0 | 100.00% | 22222.2 | 0.818988 |
| 5 | 5.0 | 100.00% | 22222.2 | 0.818988 | 48.0 | 100.00% | 22222.2 | 0.818988 |
| 6 | 6.0 | 100.00% | 22222.2 | 0.818988 | 56.0 | 100.00% | 22222.2 | 0.818988 |
| 7 | 7.0 | 100.00% | 22222.2 | 0.818988 | 64.0 | 100.00% | 22222.2 | 0.818988 |
| 8 | 8.0 | 100.00% | 22222.2 | 0.818988 | 72.0 | 100.00% | 22222.2 | 0.818988 |
| 9 | 9.0 | 100.00% | 22222.2 | 0.818988 | 80.0 | 100.00% | 22222.2 | 0.818988 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 97.10% | 0 | 0.00 | `{"filetypes/rtf": 0.9513441324234009, "general": 0.826679527759552}` |
| 5 | suspicious | or_general_primary | 97.10% | 0 | 0.00 | `{"filetypes/rtf": 0.9513441324234009, "general": 0.826679527759552}` |
| 9 | hostile | or_general_primary | 97.10% | 0 | 0.00 | `{"filetypes/rtf": 0.9513441324234009, "general": 0.826679527759552}` |
| 9 | suspicious | or_general_primary | 97.10% | 0 | 0.00 | `{"filetypes/rtf": 0.9513441324234009, "general": 0.826679527759552}` |
