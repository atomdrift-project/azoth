# Azoth Filetype `docx`
Specialist model for `docx`.
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
- Training rows: 319 (146 malware, 173 benign).
- Benchmark rows: 43 (17 malware, 26 benign).
- Benchmark AUC/AP/F1: 0.8914 / 0.8348 / 0.8750.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | - | - | - | 8.0 | 82.35% | 38461.5 | 0.711292 |
| 1 | 1.0 | 82.35% | 38461.5 | 0.711292 | 16.0 | 82.35% | 38461.5 | 0.711292 |
| 2 | 2.0 | 82.35% | 38461.5 | 0.711292 | 24.0 | 82.35% | 38461.5 | 0.711292 |
| 3 | 3.0 | 82.35% | 38461.5 | 0.711292 | 32.0 | 82.35% | 38461.5 | 0.711292 |
| 4 | 4.0 | 82.35% | 38461.5 | 0.711292 | 40.0 | 82.35% | 38461.5 | 0.711292 |
| 5 | 5.0 | 82.35% | 38461.5 | 0.711292 | 48.0 | 82.35% | 38461.5 | 0.711292 |
| 6 | 6.0 | 82.35% | 38461.5 | 0.711292 | 56.0 | 82.35% | 38461.5 | 0.711292 |
| 7 | 7.0 | 82.35% | 38461.5 | 0.711292 | 64.0 | 82.35% | 38461.5 | 0.711292 |
| 8 | 8.0 | 82.35% | 38461.5 | 0.711292 | 72.0 | 82.35% | 38461.5 | 0.711292 |
| 9 | 9.0 | 82.35% | 38461.5 | 0.711292 | 80.0 | 82.35% | 38461.5 | 0.711292 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | general_only | 78.12% | 1 | 5025.1 | `{"general": 0.8694261312484741}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | general_only | 78.12% | 1 | 5025.1 | `{"general": 0.8694261312484741}` |
