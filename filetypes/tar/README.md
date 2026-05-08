# Azoth Filetype `tar`
Specialist model for `tar`.
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
- Training rows: 1243 (931 malware, 312 benign).
- Benchmark rows: 153 (111 malware, 42 benign).
- Benchmark AUC/AP/F1: 0.9760 / 0.9923 / 0.9817.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 96.40% | 0.00 | 0.268038 | 8.0 | 96.40% | 23809.5 | 0.211336 |
| 1 | 1.0 | 96.40% | 23809.5 | 0.211336 | 16.0 | 96.40% | 23809.5 | 0.211336 |
| 2 | 2.0 | 96.40% | 23809.5 | 0.211336 | 24.0 | 96.40% | 23809.5 | 0.211336 |
| 3 | 3.0 | 96.40% | 23809.5 | 0.211336 | 32.0 | 96.40% | 23809.5 | 0.211336 |
| 4 | 4.0 | 96.40% | 23809.5 | 0.211336 | 40.0 | 96.40% | 23809.5 | 0.211336 |
| 5 | 5.0 | 96.40% | 23809.5 | 0.211336 | 48.0 | 96.40% | 23809.5 | 0.211336 |
| 6 | 6.0 | 96.40% | 23809.5 | 0.211336 | 56.0 | 96.40% | 23809.5 | 0.211336 |
| 7 | 7.0 | 96.40% | 23809.5 | 0.211336 | 64.0 | 96.40% | 23809.5 | 0.211336 |
| 8 | 8.0 | 96.40% | 23809.5 | 0.211336 | 72.0 | 96.40% | 23809.5 | 0.211336 |
| 9 | 9.0 | 96.40% | 23809.5 | 0.211336 | 80.0 | 96.40% | 23809.5 | 0.211336 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_only | 95.77% | 0 | 0.00 | `{"filegroups/archive": 0.7737218737602234}` |
| 5 | suspicious | or_general_primary | 96.83% | 1 | 2958.6 | `{"filegroups/archive": 0.7737218737602234, "general": 0.8572259545326233}` |
| 9 | hostile | group_only | 95.77% | 0 | 0.00 | `{"filegroups/archive": 0.7737218737602234}` |
| 9 | suspicious | or_general_primary | 96.83% | 1 | 2958.6 | `{"filegroups/archive": 0.7737218737602234, "general": 0.8572259545326233}` |
