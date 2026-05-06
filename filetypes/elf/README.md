# Azoth Filetype `elf`
Specialist model for `elf`.
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
- Training rows: 98557 (14159 malware, 84398 benign).
- Benchmark rows: 14228 (2009 malware, 12219 benign).
- Benchmark AUC/AP/F1: 1.0000 / 0.9998 / 0.9958.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.47% | 0.00 | 0.998250 | 8.0 | 98.61% | 81.84 | 0.983212 |
| 1 | 1.0 | 98.61% | 81.84 | 0.983212 | 16.0 | 98.61% | 81.84 | 0.983212 |
| 2 | 2.0 | 98.61% | 81.84 | 0.983212 | 24.0 | 98.61% | 81.84 | 0.983212 |
| 3 | 3.0 | 98.61% | 81.84 | 0.983212 | 32.0 | 98.61% | 81.84 | 0.983212 |
| 4 | 4.0 | 98.61% | 81.84 | 0.983212 | 40.0 | 98.61% | 81.84 | 0.983212 |
| 5 | 5.0 | 98.61% | 81.84 | 0.983212 | 48.0 | 98.61% | 81.84 | 0.983212 |
| 6 | 6.0 | 98.61% | 81.84 | 0.983212 | 56.0 | 98.61% | 81.84 | 0.983212 |
| 7 | 7.0 | 98.61% | 81.84 | 0.983212 | 64.0 | 98.61% | 81.84 | 0.983212 |
| 8 | 8.0 | 98.61% | 81.84 | 0.983212 | 72.0 | 98.61% | 81.84 | 0.983212 |
| 9 | 9.0 | 98.61% | 81.84 | 0.983212 | 80.0 | 98.61% | 81.84 | 0.983212 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 98.99% | 1 | 10.49 | `{"filetypes/elf": 0.9951940178871155}` |
| 5 | suspicious | filetype_only | 99.41% | 4 | 41.96 | `{"filetypes/elf": 0.973215639591217}` |
| 9 | hostile | filetype_only | 98.99% | 1 | 10.49 | `{"filetypes/elf": 0.9951940178871155}` |
| 9 | suspicious | filetype_only | 99.58% | 7 | 73.43 | `{"filetypes/elf": 0.9218172430992126}` |
