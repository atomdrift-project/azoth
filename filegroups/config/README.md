# Azoth Filegroup `config`
Specialist model for `ini`, `json`, `package.json`, `plist`, `toml`, `xml`, `yaml`, `yml`.
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
- Training rows: 18831 (13457 malware, 5374 benign).
- Benchmark rows: 14124 (2021 malware, 12103 benign).
- Benchmark AUC/AP/F1: 0.9656 / 0.9413 / 0.9470.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 81.05% | 0.00 | 0.998184 | 8.0 | 82.88% | 82.62 | 0.997104 |
| 1 | 1.0 | 82.88% | 82.62 | 0.997104 | 16.0 | 82.88% | 82.62 | 0.997104 |
| 2 | 2.0 | 82.88% | 82.62 | 0.997104 | 24.0 | 82.88% | 82.62 | 0.997104 |
| 3 | 3.0 | 82.88% | 82.62 | 0.997104 | 32.0 | 82.88% | 82.62 | 0.997104 |
| 4 | 4.0 | 82.88% | 82.62 | 0.997104 | 40.0 | 82.88% | 82.62 | 0.997104 |
| 5 | 5.0 | 82.88% | 82.62 | 0.997104 | 48.0 | 82.88% | 82.62 | 0.997104 |
| 6 | 6.0 | 82.88% | 82.62 | 0.997104 | 56.0 | 82.88% | 82.62 | 0.997104 |
| 7 | 7.0 | 82.88% | 82.62 | 0.997104 | 64.0 | 82.88% | 82.62 | 0.997104 |
| 8 | 8.0 | 82.88% | 82.62 | 0.997104 | 72.0 | 82.88% | 82.62 | 0.997104 |
| 9 | 9.0 | 82.88% | 82.62 | 0.997104 | 80.0 | 82.88% | 82.62 | 0.997104 |
