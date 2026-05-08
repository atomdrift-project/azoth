# Azoth Filetype `docx`
Specialist model for `docx`.
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
- Training rows: 516 (328 malware, 188 benign).
- Benchmark rows: 74 (44 malware, 30 benign).
- Benchmark AUC/AP/F1: 0.9996 / 0.9995 / 0.9888.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 97.73% | 0.00 | 0.807034 | 8.0 | 100.00% | 33333.3 | 0.798073 |
| 1 | 1.0 | 100.00% | 33333.3 | 0.798073 | 16.0 | 100.00% | 33333.3 | 0.798073 |
| 2 | 2.0 | 100.00% | 33333.3 | 0.798073 | 24.0 | 100.00% | 33333.3 | 0.798073 |
| 3 | 3.0 | 100.00% | 33333.3 | 0.798073 | 32.0 | 100.00% | 33333.3 | 0.798073 |
| 4 | 4.0 | 100.00% | 33333.3 | 0.798073 | 40.0 | 100.00% | 33333.3 | 0.798073 |
| 5 | 5.0 | 100.00% | 33333.3 | 0.798073 | 48.0 | 100.00% | 33333.3 | 0.798073 |
| 6 | 6.0 | 100.00% | 33333.3 | 0.798073 | 56.0 | 100.00% | 33333.3 | 0.798073 |
| 7 | 7.0 | 100.00% | 33333.3 | 0.798073 | 64.0 | 100.00% | 33333.3 | 0.798073 |
| 8 | 8.0 | 100.00% | 33333.3 | 0.798073 | 72.0 | 100.00% | 33333.3 | 0.798073 |
| 9 | 9.0 | 100.00% | 33333.3 | 0.798073 | 80.0 | 100.00% | 33333.3 | 0.798073 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 79.38% | 0 | 0.00 | `{"filetypes/docx": 0.7904877066612244, "general": 0.8754796385765076}` |
| 5 | suspicious | specialist_primary_with_escape | 79.38% | 0 | 0.00 | `{"filetypes/docx": 0.7904877066612244, "general": 0.8754796385765076}` |
| 9 | hostile | specialist_primary_with_escape | 79.38% | 0 | 0.00 | `{"filetypes/docx": 0.7904877066612244, "general": 0.8754796385765076}` |
| 9 | suspicious | specialist_primary_with_escape | 79.38% | 0 | 0.00 | `{"filetypes/docx": 0.7904877066612244, "general": 0.8754796385765076}` |
