# Azoth Filetype `tar.gz`
Specialist model for `tar.gz`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 15791 (9466 malware, 6325 benign).
- Benchmark rows: 2420 (1331 malware, 1089 benign).
- Benchmark AUC/AP/F1: 0.9959 / 0.9975 / 0.9860.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.67% | 0.00 | 0.958090 | 8.0 | 96.92% | 918.27 | 0.887483 |
| 1 | 1.0 | 96.92% | 918.27 | 0.887483 | 16.0 | 96.92% | 918.27 | 0.887483 |
| 2 | 2.0 | 96.92% | 918.27 | 0.887483 | 24.0 | 96.92% | 918.27 | 0.887483 |
| 3 | 3.0 | 96.92% | 918.27 | 0.887483 | 32.0 | 96.92% | 918.27 | 0.887483 |
| 4 | 4.0 | 96.92% | 918.27 | 0.887483 | 40.0 | 96.92% | 918.27 | 0.887483 |
| 5 | 5.0 | 96.92% | 918.27 | 0.887483 | 48.0 | 96.92% | 918.27 | 0.887483 |
| 6 | 6.0 | 96.92% | 918.27 | 0.887483 | 56.0 | 96.92% | 918.27 | 0.887483 |
| 7 | 7.0 | 96.92% | 918.27 | 0.887483 | 64.0 | 96.92% | 918.27 | 0.887483 |
| 8 | 8.0 | 96.92% | 918.27 | 0.887483 | 72.0 | 96.92% | 918.27 | 0.887483 |
| 9 | 9.0 | 96.92% | 918.27 | 0.887483 | 80.0 | 96.92% | 918.27 | 0.887483 |
