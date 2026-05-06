# Azoth Filetype `zst`
Specialist model for `zst`.
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
- Training rows: 16031 (1975 malware, 14056 benign).
- Benchmark rows: 2384 (307 malware, 2077 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.951767 | 8.0 | 100.00% | 481.46 | 0.072760 |
| 1 | 1.0 | 100.00% | 481.46 | 0.072760 | 16.0 | 100.00% | 481.46 | 0.072760 |
| 2 | 2.0 | 100.00% | 481.46 | 0.072760 | 24.0 | 100.00% | 481.46 | 0.072760 |
| 3 | 3.0 | 100.00% | 481.46 | 0.072760 | 32.0 | 100.00% | 481.46 | 0.072760 |
| 4 | 4.0 | 100.00% | 481.46 | 0.072760 | 40.0 | 100.00% | 481.46 | 0.072760 |
| 5 | 5.0 | 100.00% | 481.46 | 0.072760 | 48.0 | 100.00% | 481.46 | 0.072760 |
| 6 | 6.0 | 100.00% | 481.46 | 0.072760 | 56.0 | 100.00% | 481.46 | 0.072760 |
| 7 | 7.0 | 100.00% | 481.46 | 0.072760 | 64.0 | 100.00% | 481.46 | 0.072760 |
| 8 | 8.0 | 100.00% | 481.46 | 0.072760 | 72.0 | 100.00% | 481.46 | 0.072760 |
| 9 | 9.0 | 100.00% | 481.46 | 0.072760 | 80.0 | 100.00% | 481.46 | 0.072760 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | or_general_primary | 98.20% | 0 | 0.00 | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| 5 | suspicious | or_general_primary | 98.20% | 0 | 0.00 | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| 9 | hostile | or_general_primary | 98.20% | 0 | 0.00 | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| 9 | suspicious | or_general_primary | 98.20% | 0 | 0.00 | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
