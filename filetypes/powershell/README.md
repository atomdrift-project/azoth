# Azoth Filetype `powershell`
Specialist model for `powershell`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 463 (237 malware, 226 benign).
- Benchmark rows: 143 (43 malware, 100 benign).
- Benchmark AUC/AP/F1: 0.9923 / 0.9841 / 0.9524.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 76.74% | 0.00 | 0.933927 | 8.0 | 93.02% | 10000.0 | 0.642716 |
| 1 | 1.0 | 93.02% | 10000.0 | 0.642716 | 16.0 | 93.02% | 10000.0 | 0.642716 |
| 2 | 2.0 | 93.02% | 10000.0 | 0.642716 | 24.0 | 93.02% | 10000.0 | 0.642716 |
| 3 | 3.0 | 93.02% | 10000.0 | 0.642716 | 32.0 | 93.02% | 10000.0 | 0.642716 |
| 4 | 4.0 | 93.02% | 10000.0 | 0.642716 | 40.0 | 93.02% | 10000.0 | 0.642716 |
| 5 | 5.0 | 93.02% | 10000.0 | 0.642716 | 48.0 | 93.02% | 10000.0 | 0.642716 |
| 6 | 6.0 | 93.02% | 10000.0 | 0.642716 | 56.0 | 93.02% | 10000.0 | 0.642716 |
| 7 | 7.0 | 93.02% | 10000.0 | 0.642716 | 64.0 | 93.02% | 10000.0 | 0.642716 |
| 8 | 8.0 | 93.02% | 10000.0 | 0.642716 | 72.0 | 93.02% | 10000.0 | 0.642716 |
| 9 | 9.0 | 93.02% | 10000.0 | 0.642716 | 80.0 | 93.02% | 10000.0 | 0.642716 |
