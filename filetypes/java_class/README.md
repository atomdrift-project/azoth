# Azoth Filetype `java_class`
Specialist model for `java_class`.
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
- Training rows: 6720 (335 malware, 6385 benign).
- Benchmark rows: 918 (41 malware, 877 benign).
- Benchmark AUC/AP/F1: 0.9991 / 0.9816 / 0.9756.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 60.98% | 0.00 | 0.944740 | 8.0 | 97.56% | 1140.3 | 0.898792 |
| 1 | 1.0 | 97.56% | 1140.3 | 0.898792 | 16.0 | 97.56% | 1140.3 | 0.898792 |
| 2 | 2.0 | 97.56% | 1140.3 | 0.898792 | 24.0 | 97.56% | 1140.3 | 0.898792 |
| 3 | 3.0 | 97.56% | 1140.3 | 0.898792 | 32.0 | 97.56% | 1140.3 | 0.898792 |
| 4 | 4.0 | 97.56% | 1140.3 | 0.898792 | 40.0 | 97.56% | 1140.3 | 0.898792 |
| 5 | 5.0 | 97.56% | 1140.3 | 0.898792 | 48.0 | 97.56% | 1140.3 | 0.898792 |
| 6 | 6.0 | 97.56% | 1140.3 | 0.898792 | 56.0 | 97.56% | 1140.3 | 0.898792 |
| 7 | 7.0 | 97.56% | 1140.3 | 0.898792 | 64.0 | 97.56% | 1140.3 | 0.898792 |
| 8 | 8.0 | 97.56% | 1140.3 | 0.898792 | 72.0 | 97.56% | 1140.3 | 0.898792 |
| 9 | 9.0 | 97.56% | 1140.3 | 0.898792 | 80.0 | 97.56% | 1140.3 | 0.898792 |
## Routed Policy
| L | Severity | Policy | Recall | FP | FP/1M | Thresholds |
| ---: | --- | --- | ---: | ---: | ---: | --- |
| 5 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 5 | suspicious | or_general_primary | 82.42% | 1 | 137.70 | `{"filetypes/java_class": 0.9461427927017212, "general": 0.8206426501274109}` |
| 9 | hostile | group_only | 79.67% | 0 | 0.00 | `{"filegroups/portable": 0.8742847442626953}` |
| 9 | suspicious | or_general_primary | 82.42% | 1 | 137.70 | `{"filetypes/java_class": 0.9461427927017212, "general": 0.8206426501274109}` |
