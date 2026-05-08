# Azoth Filetype `package.json`
Specialist model for `package.json`.
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
- Training rows: 19983 (13777 malware, 6206 benign).
- Benchmark rows: 2775 (1875 malware, 900 benign).
- Benchmark AUC/AP/F1: 0.9998 / 0.9999 / 0.9981.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 88.00% | 0.00 | 0.998667 | 8.0 | 93.01% | 1111.1 | 0.996908 |
| 1 | 1.0 | 93.01% | 1111.1 | 0.996908 | 16.0 | 93.01% | 1111.1 | 0.996908 |
| 2 | 2.0 | 93.01% | 1111.1 | 0.996908 | 24.0 | 93.01% | 1111.1 | 0.996908 |
| 3 | 3.0 | 93.01% | 1111.1 | 0.996908 | 32.0 | 93.01% | 1111.1 | 0.996908 |
| 4 | 4.0 | 93.01% | 1111.1 | 0.996908 | 40.0 | 93.01% | 1111.1 | 0.996908 |
| 5 | 5.0 | 93.01% | 1111.1 | 0.996908 | 48.0 | 93.01% | 1111.1 | 0.996908 |
| 6 | 6.0 | 93.01% | 1111.1 | 0.996908 | 56.0 | 93.01% | 1111.1 | 0.996908 |
| 7 | 7.0 | 93.01% | 1111.1 | 0.996908 | 64.0 | 93.01% | 1111.1 | 0.996908 |
| 8 | 8.0 | 93.01% | 1111.1 | 0.996908 | 72.0 | 93.01% | 1111.1 | 0.996908 |
| 9 | 9.0 | 93.01% | 1111.1 | 0.996908 | 80.0 | 93.01% | 1111.1 | 0.996908 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 98.38% | 1 | 155.01 | `{"filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 5 | suspicious | specialist_primary_with_escape | 98.38% | 1 | 155.01 | `{"filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 9 | hostile | specialist_primary_with_escape | 98.38% | 1 | 155.01 | `{"filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
| 9 | suspicious | specialist_primary_with_escape | 98.38% | 1 | 155.01 | `{"filetypes/package.json": 0.9742239713668823, "general": 0.9896659851074219}` |
