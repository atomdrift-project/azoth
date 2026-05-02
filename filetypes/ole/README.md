# Azoth Filetype `ole`
Specialist model for `ole`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 293 (218 malware, 75 benign).
- Benchmark rows: 680 (31 malware, 649 benign).
- Benchmark AUC/AP/F1: 0.9182 / 0.8310 / 0.8525.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 67.74% | 0.00 | 0.787446 | 8.0 | 74.19% | 1540.8 | 0.734624 |
| 1 | 1.0 | 74.19% | 1540.8 | 0.734624 | 16.0 | 74.19% | 1540.8 | 0.734624 |
| 2 | 2.0 | 74.19% | 1540.8 | 0.734624 | 24.0 | 74.19% | 1540.8 | 0.734624 |
| 3 | 3.0 | 74.19% | 1540.8 | 0.734624 | 32.0 | 74.19% | 1540.8 | 0.734624 |
| 4 | 4.0 | 74.19% | 1540.8 | 0.734624 | 40.0 | 74.19% | 1540.8 | 0.734624 |
| 5 | 5.0 | 74.19% | 1540.8 | 0.734624 | 48.0 | 74.19% | 1540.8 | 0.734624 |
| 6 | 6.0 | 74.19% | 1540.8 | 0.734624 | 56.0 | 74.19% | 1540.8 | 0.734624 |
| 7 | 7.0 | 74.19% | 1540.8 | 0.734624 | 64.0 | 74.19% | 1540.8 | 0.734624 |
| 8 | 8.0 | 74.19% | 1540.8 | 0.734624 | 72.0 | 74.19% | 1540.8 | 0.734624 |
| 9 | 9.0 | 74.19% | 1540.8 | 0.734624 | 80.0 | 74.19% | 1540.8 | 0.734624 |
