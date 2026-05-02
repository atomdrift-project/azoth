# Azoth Filetype `c`
Specialist model for `c`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 6771 (2352 malware, 4419 benign).
- Benchmark rows: 52818 (726 malware, 52092 benign).
- Benchmark AUC/AP/F1: 0.9249 / 0.6158 / 0.6366.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 45.87% | 0.00 | 0.912349 | 8.0 | 46.14% | 19.20 | 0.907551 |
| 1 | 1.0 | 46.14% | 19.20 | 0.907551 | 16.0 | 46.14% | 19.20 | 0.907551 |
| 2 | 2.0 | 46.14% | 19.20 | 0.907551 | 24.0 | 46.14% | 19.20 | 0.907551 |
| 3 | 3.0 | 46.14% | 19.20 | 0.907551 | 32.0 | 46.14% | 19.20 | 0.907551 |
| 4 | 4.0 | 46.14% | 19.20 | 0.907551 | 40.0 | 46.42% | 38.39 | 0.904040 |
| 5 | 5.0 | 46.14% | 19.20 | 0.907551 | 48.0 | 46.42% | 38.39 | 0.904040 |
| 6 | 6.0 | 46.14% | 19.20 | 0.907551 | 56.0 | 46.42% | 38.39 | 0.904040 |
| 7 | 7.0 | 46.14% | 19.20 | 0.907551 | 64.0 | 46.42% | 57.59 | 0.901982 |
| 8 | 8.0 | 46.14% | 19.20 | 0.907551 | 72.0 | 46.42% | 57.59 | 0.901982 |
| 9 | 9.0 | 46.14% | 19.20 | 0.907551 | 80.0 | 46.83% | 76.79 | 0.897997 |
