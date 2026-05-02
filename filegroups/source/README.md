# Azoth Filegroup `source`
Specialist model for `c`, `cpp`, `csharp`, `go`, `java`, `kotlin`, `makefile`, `rust`, `scala`, `swift`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 10261 (3270 malware, 6991 benign).
- Benchmark rows: 86643 (990 malware, 85653 benign).
- Benchmark AUC/AP/F1: 0.9193 / 0.6586 / 0.6941.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 47.27% | 0.00 | 0.926049 | 8.0 | 49.39% | 11.68 | 0.911312 |
| 1 | 1.0 | 49.39% | 11.68 | 0.911312 | 16.0 | 49.39% | 11.68 | 0.911312 |
| 2 | 2.0 | 49.39% | 11.68 | 0.911312 | 24.0 | 50.20% | 23.35 | 0.899803 |
| 3 | 3.0 | 49.39% | 11.68 | 0.911312 | 32.0 | 50.20% | 23.35 | 0.899803 |
| 4 | 4.0 | 49.39% | 11.68 | 0.911312 | 40.0 | 50.51% | 35.03 | 0.892700 |
| 5 | 5.0 | 49.39% | 11.68 | 0.911312 | 48.0 | 51.62% | 46.70 | 0.875675 |
| 6 | 6.0 | 49.39% | 11.68 | 0.911312 | 56.0 | 51.62% | 46.70 | 0.875675 |
| 7 | 7.0 | 49.39% | 11.68 | 0.911312 | 64.0 | 52.12% | 58.38 | 0.863247 |
| 8 | 8.0 | 49.39% | 11.68 | 0.911312 | 72.0 | 52.12% | 70.05 | 0.858456 |
| 9 | 9.0 | 49.39% | 11.68 | 0.911312 | 80.0 | 52.12% | 70.05 | 0.858456 |
