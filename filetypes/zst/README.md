# Azoth Filetype `zst`
Specialist model for `zst`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 13213 (1895 malware, 11318 benign).
- Benchmark rows: 2384 (307 malware, 2077 benign).
- Benchmark AUC/AP/F1: 0.9996 / 0.9967 / 0.9934.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 98.70% | 0.00 | 0.968706 | 8.0 | 98.70% | 481.46 | 0.830421 |
| 1 | 1.0 | 98.70% | 481.46 | 0.830421 | 16.0 | 98.70% | 481.46 | 0.830421 |
| 2 | 2.0 | 98.70% | 481.46 | 0.830421 | 24.0 | 98.70% | 481.46 | 0.830421 |
| 3 | 3.0 | 98.70% | 481.46 | 0.830421 | 32.0 | 98.70% | 481.46 | 0.830421 |
| 4 | 4.0 | 98.70% | 481.46 | 0.830421 | 40.0 | 98.70% | 481.46 | 0.830421 |
| 5 | 5.0 | 98.70% | 481.46 | 0.830421 | 48.0 | 98.70% | 481.46 | 0.830421 |
| 6 | 6.0 | 98.70% | 481.46 | 0.830421 | 56.0 | 98.70% | 481.46 | 0.830421 |
| 7 | 7.0 | 98.70% | 481.46 | 0.830421 | 64.0 | 98.70% | 481.46 | 0.830421 |
| 8 | 8.0 | 98.70% | 481.46 | 0.830421 | 72.0 | 98.70% | 481.46 | 0.830421 |
| 9 | 9.0 | 98.70% | 481.46 | 0.830421 | 80.0 | 98.70% | 481.46 | 0.830421 |
