# Azoth Filetype `pkg-info`
Specialist model for `pkg-info`.
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
- Training rows: 3947 (3240 malware, 707 benign).
- Benchmark rows: 535 (441 malware, 94 benign).
- Benchmark AUC/AP/F1: 1.0000 / 1.0000 / 1.0000.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 100.00% | 0.00 | 0.608399 | 8.0 | 100.00% | 10638.3 | 0.076727 |
| 1 | 1.0 | 100.00% | 10638.3 | 0.076727 | 16.0 | 100.00% | 10638.3 | 0.076727 |
| 2 | 2.0 | 100.00% | 10638.3 | 0.076727 | 24.0 | 100.00% | 10638.3 | 0.076727 |
| 3 | 3.0 | 100.00% | 10638.3 | 0.076727 | 32.0 | 100.00% | 10638.3 | 0.076727 |
| 4 | 4.0 | 100.00% | 10638.3 | 0.076727 | 40.0 | 100.00% | 10638.3 | 0.076727 |
| 5 | 5.0 | 100.00% | 10638.3 | 0.076727 | 48.0 | 100.00% | 10638.3 | 0.076727 |
| 6 | 6.0 | 100.00% | 10638.3 | 0.076727 | 56.0 | 100.00% | 10638.3 | 0.076727 |
| 7 | 7.0 | 100.00% | 10638.3 | 0.076727 | 64.0 | 100.00% | 10638.3 | 0.076727 |
| 8 | 8.0 | 100.00% | 10638.3 | 0.076727 | 72.0 | 100.00% | 10638.3 | 0.076727 |
| 9 | 9.0 | 100.00% | 10638.3 | 0.076727 | 80.0 | 100.00% | 10638.3 | 0.076727 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 5 | suspicious | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 9 | hostile | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
| 9 | suspicious | filetype_only | 94.77% | 0 | 0.00 | `{"filetypes/pkg-info": 0.44328248500823975}` |
