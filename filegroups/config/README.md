# Azoth Filegroup `config`
Specialist model for `ini`, `json`, `package.json`, `plist`, `toml`, `xml`, `yaml`, `yml`.
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
- Training rows: 19023 (13587 malware, 5436 benign).
- Benchmark rows: 14419 (2046 malware, 12373 benign).
- Benchmark AUC/AP/F1: 0.9670 / 0.9404 / 0.9458.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 72.24% | 0.00 | 0.995805 | 8.0 | 80.01% | 80.82 | 0.992186 |
| 1 | 1.0 | 80.01% | 80.82 | 0.992186 | 16.0 | 80.01% | 80.82 | 0.992186 |
| 2 | 2.0 | 80.01% | 80.82 | 0.992186 | 24.0 | 80.01% | 80.82 | 0.992186 |
| 3 | 3.0 | 80.01% | 80.82 | 0.992186 | 32.0 | 80.01% | 80.82 | 0.992186 |
| 4 | 4.0 | 80.01% | 80.82 | 0.992186 | 40.0 | 80.01% | 80.82 | 0.992186 |
| 5 | 5.0 | 80.01% | 80.82 | 0.992186 | 48.0 | 80.01% | 80.82 | 0.992186 |
| 6 | 6.0 | 80.01% | 80.82 | 0.992186 | 56.0 | 80.01% | 80.82 | 0.992186 |
| 7 | 7.0 | 80.01% | 80.82 | 0.992186 | 64.0 | 80.01% | 80.82 | 0.992186 |
| 8 | 8.0 | 80.01% | 80.82 | 0.992186 | 72.0 | 80.01% | 80.82 | 0.992186 |
| 9 | 9.0 | 80.01% | 80.82 | 0.992186 | 80.0 | 80.01% | 80.82 | 0.992186 |
