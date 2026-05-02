# Azoth Filegroup `scripts`
Specialist model for `batch`, `javascript`, `lua`, `perl`, `php`, `powershell`, `python`, `ruby`, `shell`, `typescript`, `vbscript`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 99017 (56468 malware, 42549 benign).
- Benchmark rows: 73784 (8649 malware, 65135 benign).
- Benchmark AUC/AP/F1: 0.9867 / 0.9723 / 0.9685.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 84.47% | 0.00 | 0.998958 | 8.0 | 91.50% | 15.35 | 0.984926 |
| 1 | 1.0 | 91.50% | 15.35 | 0.984926 | 16.0 | 91.50% | 15.35 | 0.984926 |
| 2 | 2.0 | 91.50% | 15.35 | 0.984926 | 24.0 | 91.50% | 15.35 | 0.984926 |
| 3 | 3.0 | 91.50% | 15.35 | 0.984926 | 32.0 | 92.20% | 30.71 | 0.972963 |
| 4 | 4.0 | 91.50% | 15.35 | 0.984926 | 40.0 | 92.20% | 30.71 | 0.972963 |
| 5 | 5.0 | 91.50% | 15.35 | 0.984926 | 48.0 | 92.37% | 46.06 | 0.966879 |
| 6 | 6.0 | 91.50% | 15.35 | 0.984926 | 56.0 | 92.37% | 46.06 | 0.966879 |
| 7 | 7.0 | 91.50% | 15.35 | 0.984926 | 64.0 | 92.46% | 61.41 | 0.964678 |
| 8 | 8.0 | 91.50% | 15.35 | 0.984926 | 72.0 | 92.46% | 61.41 | 0.964678 |
| 9 | 9.0 | 91.50% | 15.35 | 0.984926 | 80.0 | 92.66% | 76.76 | 0.954358 |
