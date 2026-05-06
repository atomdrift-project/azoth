# Azoth Filegroup `native`
Specialist model for `elf`, `macho`, `pe`.
- Inputs: shared general `feature_spec.json` (39115 features); policy `route_specific`.
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
- Training rows: 541780 (317097 malware, 224683 benign).
- Benchmark rows: 75513 (43284 malware, 32229 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 0.9984.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.96% | 0.00 | 0.999447 | 8.0 | 90.92% | 31.03 | 0.998666 |
| 1 | 1.0 | 90.92% | 31.03 | 0.998666 | 16.0 | 90.92% | 31.03 | 0.998666 |
| 2 | 2.0 | 90.92% | 31.03 | 0.998666 | 24.0 | 90.92% | 31.03 | 0.998666 |
| 3 | 3.0 | 90.92% | 31.03 | 0.998666 | 32.0 | 90.92% | 31.03 | 0.998666 |
| 4 | 4.0 | 90.92% | 31.03 | 0.998666 | 40.0 | 90.92% | 31.03 | 0.998666 |
| 5 | 5.0 | 90.92% | 31.03 | 0.998666 | 48.0 | 90.92% | 31.03 | 0.998666 |
| 6 | 6.0 | 90.92% | 31.03 | 0.998666 | 56.0 | 90.92% | 31.03 | 0.998666 |
| 7 | 7.0 | 90.92% | 31.03 | 0.998666 | 64.0 | 91.03% | 62.06 | 0.998643 |
| 8 | 8.0 | 90.92% | 31.03 | 0.998666 | 72.0 | 91.03% | 62.06 | 0.998643 |
| 9 | 9.0 | 90.92% | 31.03 | 0.998666 | 80.0 | 91.03% | 62.06 | 0.998643 |
