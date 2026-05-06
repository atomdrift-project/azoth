# Azoth Filetype `pe`
Specialist model for `pe`.
- Inputs: shared general `feature_spec.json` (49964 features); policy `general_shared`.
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
- Training rows: 411043 (292601 malware, 118442 benign).
- Benchmark rows: 56559 (39743 malware, 16816 benign).
- Benchmark AUC/AP/F1: 0.9994 / 0.9998 / 0.9948.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 62.84% | 0.00 | 0.999348 | 8.0 | 71.05% | 59.47 | 0.998583 |
| 1 | 1.0 | 71.05% | 59.47 | 0.998583 | 16.0 | 71.05% | 59.47 | 0.998583 |
| 2 | 2.0 | 71.05% | 59.47 | 0.998583 | 24.0 | 71.05% | 59.47 | 0.998583 |
| 3 | 3.0 | 71.05% | 59.47 | 0.998583 | 32.0 | 71.05% | 59.47 | 0.998583 |
| 4 | 4.0 | 71.05% | 59.47 | 0.998583 | 40.0 | 71.05% | 59.47 | 0.998583 |
| 5 | 5.0 | 71.05% | 59.47 | 0.998583 | 48.0 | 71.05% | 59.47 | 0.998583 |
| 6 | 6.0 | 71.05% | 59.47 | 0.998583 | 56.0 | 71.05% | 59.47 | 0.998583 |
| 7 | 7.0 | 71.05% | 59.47 | 0.998583 | 64.0 | 71.05% | 59.47 | 0.998583 |
| 8 | 8.0 | 71.05% | 59.47 | 0.998583 | 72.0 | 71.05% | 59.47 | 0.998583 |
| 9 | 9.0 | 71.05% | 59.47 | 0.998583 | 80.0 | 71.05% | 59.47 | 0.998583 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 65.14% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9995437860488892, "general": 0.9996013045310974}` |
| 5 | suspicious | specialist_primary_with_escape | 75.43% | 6 | 45.10 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9987611770629883, "general": 0.9993268251419067}` |
| 9 | hostile | specialist_primary_with_escape | 65.14% | 1 | 7.52 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9995437860488892, "general": 0.9996013045310974}` |
| 9 | suspicious | specialist_primary_with_escape | 76.13% | 10 | 75.17 | `{"filegroups/native": 0.9999709725379944, "filetypes/pe": 0.9986722469329834, "general": 0.9993268251419067}` |
