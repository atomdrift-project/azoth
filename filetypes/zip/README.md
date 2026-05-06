# Azoth Filetype `zip`
Specialist model for `zip`.
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
- Training rows: 30249 (27731 malware, 2518 benign).
- Benchmark rows: 4113 (3790 malware, 323 benign).
- Benchmark AUC/AP/F1: 0.9801 / 0.9977 / 0.9864.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 74.88% | 0.00 | 0.963597 | 8.0 | 79.31% | 3096.0 | 0.829484 |
| 1 | 1.0 | 79.31% | 3096.0 | 0.829484 | 16.0 | 79.31% | 3096.0 | 0.829484 |
| 2 | 2.0 | 79.31% | 3096.0 | 0.829484 | 24.0 | 79.31% | 3096.0 | 0.829484 |
| 3 | 3.0 | 79.31% | 3096.0 | 0.829484 | 32.0 | 79.31% | 3096.0 | 0.829484 |
| 4 | 4.0 | 79.31% | 3096.0 | 0.829484 | 40.0 | 79.31% | 3096.0 | 0.829484 |
| 5 | 5.0 | 79.31% | 3096.0 | 0.829484 | 48.0 | 79.31% | 3096.0 | 0.829484 |
| 6 | 6.0 | 79.31% | 3096.0 | 0.829484 | 56.0 | 79.31% | 3096.0 | 0.829484 |
| 7 | 7.0 | 79.31% | 3096.0 | 0.829484 | 64.0 | 79.31% | 3096.0 | 0.829484 |
| 8 | 8.0 | 79.31% | 3096.0 | 0.829484 | 72.0 | 79.31% | 3096.0 | 0.829484 |
| 9 | 9.0 | 79.31% | 3096.0 | 0.829484 | 80.0 | 79.31% | 3096.0 | 0.829484 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | specialist_primary_with_escape | 74.70% | 1 | 352.73 | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| 5 | suspicious | specialist_primary_with_escape | 74.70% | 1 | 352.73 | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| 9 | hostile | specialist_primary_with_escape | 74.70% | 1 | 352.73 | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| 9 | suspicious | specialist_primary_with_escape | 74.70% | 1 | 352.73 | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
