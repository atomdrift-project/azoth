# Azoth Filetype `csharp`
Specialist model for `csharp`.
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
- Training rows: 30631 (559 malware, 30072 benign).
- Benchmark rows: 4503 (88 malware, 4415 benign).
- Benchmark AUC/AP/F1: 0.9881 / 0.8856 / 0.8727.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 65.91% | 0.00 | 0.968676 | 8.0 | 73.86% | 226.50 | 0.835367 |
| 1 | 1.0 | 73.86% | 226.50 | 0.835367 | 16.0 | 73.86% | 226.50 | 0.835367 |
| 2 | 2.0 | 73.86% | 226.50 | 0.835367 | 24.0 | 73.86% | 226.50 | 0.835367 |
| 3 | 3.0 | 73.86% | 226.50 | 0.835367 | 32.0 | 73.86% | 226.50 | 0.835367 |
| 4 | 4.0 | 73.86% | 226.50 | 0.835367 | 40.0 | 73.86% | 226.50 | 0.835367 |
| 5 | 5.0 | 73.86% | 226.50 | 0.835367 | 48.0 | 73.86% | 226.50 | 0.835367 |
| 6 | 6.0 | 73.86% | 226.50 | 0.835367 | 56.0 | 73.86% | 226.50 | 0.835367 |
| 7 | 7.0 | 73.86% | 226.50 | 0.835367 | 64.0 | 73.86% | 226.50 | 0.835367 |
| 8 | 8.0 | 73.86% | 226.50 | 0.835367 | 72.0 | 73.86% | 226.50 | 0.835367 |
| 9 | 9.0 | 73.86% | 226.50 | 0.835367 | 80.0 | 73.86% | 226.50 | 0.835367 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | specialist_primary_with_escape | 54.87% | 1 | 29.00 | `{"filegroups/source": 0.9739324450492859, "filetypes/csharp": 0.9970453977584839, "general": 0.9349995851516724}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 57.65% | 2 | 57.99 | `{"filetypes/csharp": 0.9886995553970337, "general": 0.9349995851516724}` |
