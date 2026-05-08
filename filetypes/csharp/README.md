# Azoth Filetype `csharp`
Specialist model for `csharp`.
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
- Training rows: 39487 (673 malware, 38814 benign).
- Benchmark rows: 5776 (115 malware, 5661 benign).
- Benchmark AUC/AP/F1: 0.9980 / 0.9519 / 0.9132.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 75.65% | 0.00 | 0.984100 | 8.0 | 82.61% | 176.65 | 0.895422 |
| 1 | 1.0 | 82.61% | 176.65 | 0.895422 | 16.0 | 82.61% | 176.65 | 0.895422 |
| 2 | 2.0 | 82.61% | 176.65 | 0.895422 | 24.0 | 82.61% | 176.65 | 0.895422 |
| 3 | 3.0 | 82.61% | 176.65 | 0.895422 | 32.0 | 82.61% | 176.65 | 0.895422 |
| 4 | 4.0 | 82.61% | 176.65 | 0.895422 | 40.0 | 82.61% | 176.65 | 0.895422 |
| 5 | 5.0 | 82.61% | 176.65 | 0.895422 | 48.0 | 82.61% | 176.65 | 0.895422 |
| 6 | 6.0 | 82.61% | 176.65 | 0.895422 | 56.0 | 82.61% | 176.65 | 0.895422 |
| 7 | 7.0 | 82.61% | 176.65 | 0.895422 | 64.0 | 82.61% | 176.65 | 0.895422 |
| 8 | 8.0 | 82.61% | 176.65 | 0.895422 | 72.0 | 82.61% | 176.65 | 0.895422 |
| 9 | 9.0 | 82.61% | 176.65 | 0.895422 | 80.0 | 82.61% | 176.65 | 0.895422 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 5 | suspicious | or_general_primary | 55.64% | 1 | 29.00 | `{"filegroups/source": 0.9630320072174072, "filetypes/csharp": 0.995499849319458, "general": 0.9332911372184753}` |
| 9 | hostile | no_policy | 0.00% | 0 | 0.00 | `{}` |
| 9 | suspicious | specialist_primary_with_escape | 56.11% | 2 | 57.99 | `{"filegroups/source": 0.9739324450492859, "filetypes/csharp": 0.992536723613739}` |
