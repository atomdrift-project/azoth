# Azoth Filetype `go`
Specialist model for `go`.
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
- Training rows: 73453 (689 malware, 72764 benign).
- Benchmark rows: 10669 (115 malware, 10554 benign).
- Benchmark AUC/AP/F1: 0.9660 / 0.6863 / 0.6739.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 41.74% | 0.00 | 0.994747 | 8.0 | 41.74% | 94.75 | 0.994196 |
| 1 | 1.0 | 41.74% | 94.75 | 0.994196 | 16.0 | 41.74% | 94.75 | 0.994196 |
| 2 | 2.0 | 41.74% | 94.75 | 0.994196 | 24.0 | 41.74% | 94.75 | 0.994196 |
| 3 | 3.0 | 41.74% | 94.75 | 0.994196 | 32.0 | 41.74% | 94.75 | 0.994196 |
| 4 | 4.0 | 41.74% | 94.75 | 0.994196 | 40.0 | 41.74% | 94.75 | 0.994196 |
| 5 | 5.0 | 41.74% | 94.75 | 0.994196 | 48.0 | 41.74% | 94.75 | 0.994196 |
| 6 | 6.0 | 41.74% | 94.75 | 0.994196 | 56.0 | 41.74% | 94.75 | 0.994196 |
| 7 | 7.0 | 41.74% | 94.75 | 0.994196 | 64.0 | 41.74% | 94.75 | 0.994196 |
| 8 | 8.0 | 41.74% | 94.75 | 0.994196 | 72.0 | 41.74% | 94.75 | 0.994196 |
| 9 | 9.0 | 41.74% | 94.75 | 0.994196 | 80.0 | 41.74% | 94.75 | 0.994196 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 46.89% | 3 | 36.01 | `{"filegroups/source": 0.9598113894462585, "filetypes/go": 0.7352849245071411, "general": 0.9522479176521301}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 47.26% | 6 | 72.01 | `{"filegroups/source": 0.9598113894462585, "filetypes/go": 0.638207197189331}` |
