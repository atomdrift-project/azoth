# Azoth Filegroup `native`
Specialist model for `elf`, `macho`, `pe`.
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
- Training rows: 474077 (274616 malware, 199461 benign).
- Benchmark rows: 66689 (37306 malware, 29383 benign).
- Benchmark AUC/AP/F1: 0.9997 / 0.9998 / 0.9948.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 76.26% | 0.00 | 0.998652 | 8.0 | 84.43% | 34.03 | 0.996707 |
| 1 | 1.0 | 84.43% | 34.03 | 0.996707 | 16.0 | 84.43% | 34.03 | 0.996707 |
| 2 | 2.0 | 84.43% | 34.03 | 0.996707 | 24.0 | 84.43% | 34.03 | 0.996707 |
| 3 | 3.0 | 84.43% | 34.03 | 0.996707 | 32.0 | 84.43% | 34.03 | 0.996707 |
| 4 | 4.0 | 84.43% | 34.03 | 0.996707 | 40.0 | 84.43% | 34.03 | 0.996707 |
| 5 | 5.0 | 84.43% | 34.03 | 0.996707 | 48.0 | 84.43% | 34.03 | 0.996707 |
| 6 | 6.0 | 84.43% | 34.03 | 0.996707 | 56.0 | 84.43% | 34.03 | 0.996707 |
| 7 | 7.0 | 84.43% | 34.03 | 0.996707 | 64.0 | 84.43% | 34.03 | 0.996707 |
| 8 | 8.0 | 84.43% | 34.03 | 0.996707 | 72.0 | 85.85% | 68.07 | 0.996147 |
| 9 | 9.0 | 84.43% | 34.03 | 0.996707 | 80.0 | 85.85% | 68.07 | 0.996147 |
