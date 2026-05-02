# Azoth Filetype `shell`
Specialist model for `shell`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 8376 (1114 malware, 7262 benign).
- Benchmark rows: 4592 (221 malware, 4371 benign).
- Benchmark AUC/AP/F1: 0.9720 / 0.9218 / 0.9151.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 80.54% | 0.00 | 0.988031 | 8.0 | 82.81% | 228.78 | 0.974971 |
| 1 | 1.0 | 82.81% | 228.78 | 0.974971 | 16.0 | 82.81% | 228.78 | 0.974971 |
| 2 | 2.0 | 82.81% | 228.78 | 0.974971 | 24.0 | 82.81% | 228.78 | 0.974971 |
| 3 | 3.0 | 82.81% | 228.78 | 0.974971 | 32.0 | 82.81% | 228.78 | 0.974971 |
| 4 | 4.0 | 82.81% | 228.78 | 0.974971 | 40.0 | 82.81% | 228.78 | 0.974971 |
| 5 | 5.0 | 82.81% | 228.78 | 0.974971 | 48.0 | 82.81% | 228.78 | 0.974971 |
| 6 | 6.0 | 82.81% | 228.78 | 0.974971 | 56.0 | 82.81% | 228.78 | 0.974971 |
| 7 | 7.0 | 82.81% | 228.78 | 0.974971 | 64.0 | 82.81% | 228.78 | 0.974971 |
| 8 | 8.0 | 82.81% | 228.78 | 0.974971 | 72.0 | 82.81% | 228.78 | 0.974971 |
| 9 | 9.0 | 82.81% | 228.78 | 0.974971 | 80.0 | 82.81% | 228.78 | 0.974971 |
