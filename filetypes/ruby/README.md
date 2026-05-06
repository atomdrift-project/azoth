# Azoth Filetype `ruby`
Specialist model for `ruby`.
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
- Training rows: 10547 (62 malware, 10485 benign).
- Benchmark rows: 1466 (7 malware, 1459 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.954146 | 8.0 | 100.00% | 685.40 | 0.783041 |
| 1 | 1.0 | 100.00% | 685.40 | 0.783041 | 16.0 | 100.00% | 685.40 | 0.783041 |
| 2 | 2.0 | 100.00% | 685.40 | 0.783041 | 24.0 | 100.00% | 685.40 | 0.783041 |
| 3 | 3.0 | 100.00% | 685.40 | 0.783041 | 32.0 | 100.00% | 685.40 | 0.783041 |
| 4 | 4.0 | 100.00% | 685.40 | 0.783041 | 40.0 | 100.00% | 685.40 | 0.783041 |
| 5 | 5.0 | 100.00% | 685.40 | 0.783041 | 48.0 | 100.00% | 685.40 | 0.783041 |
| 6 | 6.0 | 100.00% | 685.40 | 0.783041 | 56.0 | 100.00% | 685.40 | 0.783041 |
| 7 | 7.0 | 100.00% | 685.40 | 0.783041 | 64.0 | 100.00% | 685.40 | 0.783041 |
| 8 | 8.0 | 100.00% | 685.40 | 0.783041 | 72.0 | 100.00% | 685.40 | 0.783041 |
| 9 | 9.0 | 100.00% | 685.40 | 0.783041 | 80.0 | 100.00% | 685.40 | 0.783041 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 98.55% | 1 | 83.72 | `{"filetypes/ruby": 0.995830237865448, "general": 0.8743661046028137}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 98.55% | 1 | 83.72 | `{"filetypes/ruby": 0.995830237865448, "general": 0.8743661046028137}` |
