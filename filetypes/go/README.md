# Azoth Filetype `go`
Specialist model for `go`.
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
- Training rows: 2440 (357 malware, 2083 benign).
- Benchmark rows: 10630 (115 malware, 10515 benign).
- Benchmark AUC/AP/F1: 0.8814 / 0.4875 / 0.6071.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 43.48% | 0.00 | 0.467413 | 8.0 | 43.48% | 95.10 | 0.403596 |
| 1 | 1.0 | 43.48% | 95.10 | 0.403596 | 16.0 | 43.48% | 95.10 | 0.403596 |
| 2 | 2.0 | 43.48% | 95.10 | 0.403596 | 24.0 | 43.48% | 95.10 | 0.403596 |
| 3 | 3.0 | 43.48% | 95.10 | 0.403596 | 32.0 | 43.48% | 95.10 | 0.403596 |
| 4 | 4.0 | 43.48% | 95.10 | 0.403596 | 40.0 | 43.48% | 95.10 | 0.403596 |
| 5 | 5.0 | 43.48% | 95.10 | 0.403596 | 48.0 | 43.48% | 95.10 | 0.403596 |
| 6 | 6.0 | 43.48% | 95.10 | 0.403596 | 56.0 | 43.48% | 95.10 | 0.403596 |
| 7 | 7.0 | 43.48% | 95.10 | 0.403596 | 64.0 | 43.48% | 95.10 | 0.403596 |
| 8 | 8.0 | 43.48% | 95.10 | 0.403596 | 72.0 | 43.48% | 95.10 | 0.403596 |
| 9 | 9.0 | 43.48% | 95.10 | 0.403596 | 80.0 | 43.48% | 95.10 | 0.403596 |
