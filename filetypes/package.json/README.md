# Azoth Filetype `package.json`
Specialist model for `package.json`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 17644 (13379 malware, 4265 benign).
- Benchmark rows: 2641 (1825 malware, 816 benign).
- Benchmark AUC/AP/F1: 0.9992 / 0.9997 / 0.9967.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 89.15% | 0.00 | 0.993347 | 8.0 | 91.73% | 1225.5 | 0.988742 |
| 1 | 1.0 | 91.73% | 1225.5 | 0.988742 | 16.0 | 91.73% | 1225.5 | 0.988742 |
| 2 | 2.0 | 91.73% | 1225.5 | 0.988742 | 24.0 | 91.73% | 1225.5 | 0.988742 |
| 3 | 3.0 | 91.73% | 1225.5 | 0.988742 | 32.0 | 91.73% | 1225.5 | 0.988742 |
| 4 | 4.0 | 91.73% | 1225.5 | 0.988742 | 40.0 | 91.73% | 1225.5 | 0.988742 |
| 5 | 5.0 | 91.73% | 1225.5 | 0.988742 | 48.0 | 91.73% | 1225.5 | 0.988742 |
| 6 | 6.0 | 91.73% | 1225.5 | 0.988742 | 56.0 | 91.73% | 1225.5 | 0.988742 |
| 7 | 7.0 | 91.73% | 1225.5 | 0.988742 | 64.0 | 91.73% | 1225.5 | 0.988742 |
| 8 | 8.0 | 91.73% | 1225.5 | 0.988742 | 72.0 | 91.73% | 1225.5 | 0.988742 |
| 9 | 9.0 | 91.73% | 1225.5 | 0.988742 | 80.0 | 91.73% | 1225.5 | 0.988742 |
