# Azoth Filetype `elf`
Specialist model for `elf`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 77998 (9455 malware, 68543 benign).
- Benchmark rows: 12184 (1385 malware, 10799 benign).
- Benchmark AUC/AP/F1: 1.0000 / 0.9997 / 0.9935.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 94.51% | 0.00 | 0.998116 | 8.0 | 97.47% | 92.60 | 0.984187 |
| 1 | 1.0 | 97.47% | 92.60 | 0.984187 | 16.0 | 97.47% | 92.60 | 0.984187 |
| 2 | 2.0 | 97.47% | 92.60 | 0.984187 | 24.0 | 97.47% | 92.60 | 0.984187 |
| 3 | 3.0 | 97.47% | 92.60 | 0.984187 | 32.0 | 97.47% | 92.60 | 0.984187 |
| 4 | 4.0 | 97.47% | 92.60 | 0.984187 | 40.0 | 97.47% | 92.60 | 0.984187 |
| 5 | 5.0 | 97.47% | 92.60 | 0.984187 | 48.0 | 97.47% | 92.60 | 0.984187 |
| 6 | 6.0 | 97.47% | 92.60 | 0.984187 | 56.0 | 97.47% | 92.60 | 0.984187 |
| 7 | 7.0 | 97.47% | 92.60 | 0.984187 | 64.0 | 97.47% | 92.60 | 0.984187 |
| 8 | 8.0 | 97.47% | 92.60 | 0.984187 | 72.0 | 97.47% | 92.60 | 0.984187 |
| 9 | 9.0 | 97.47% | 92.60 | 0.984187 | 80.0 | 97.47% | 92.60 | 0.984187 |
