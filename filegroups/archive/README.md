# Azoth Filegroup `archive`
Specialist model for `7z`, `apk`, `cab`, `deb`, `egg`, `gz`, `msi`, `rar`, `rpm`, `tar`, `tar.gz`, `tgz`, `vsix`, `war`, `whl`, `xpi`, `xz`, `zip`, `zst`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families: hopper score, cleave trait taxonomy, element tokens, path/criticality bigrams/trigrams, ATT&CK/MBC n-grams, aggregate finding counts, extended file metrics, soft presence, repetition penalties, severity distribution, hostile density/escalation, structural coverage; clusters disabled; packaged capability mode=paths.
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 76794 (36562 malware, 40232 benign).
- Benchmark rows: 15982 (5789 malware, 10193 benign).
- Benchmark AUC/AP/F1: 0.9630 / 0.9498 / 0.9173.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 79.93% | 0.00 | 0.988925 | 8.0 | 80.43% | 98.11 | 0.984387 |
| 1 | 1.0 | 80.43% | 98.11 | 0.984387 | 16.0 | 80.43% | 98.11 | 0.984387 |
| 2 | 2.0 | 80.43% | 98.11 | 0.984387 | 24.0 | 80.43% | 98.11 | 0.984387 |
| 3 | 3.0 | 80.43% | 98.11 | 0.984387 | 32.0 | 80.43% | 98.11 | 0.984387 |
| 4 | 4.0 | 80.43% | 98.11 | 0.984387 | 40.0 | 80.43% | 98.11 | 0.984387 |
| 5 | 5.0 | 80.43% | 98.11 | 0.984387 | 48.0 | 80.43% | 98.11 | 0.984387 |
| 6 | 6.0 | 80.43% | 98.11 | 0.984387 | 56.0 | 80.43% | 98.11 | 0.984387 |
| 7 | 7.0 | 80.43% | 98.11 | 0.984387 | 64.0 | 80.43% | 98.11 | 0.984387 |
| 8 | 8.0 | 80.43% | 98.11 | 0.984387 | 72.0 | 80.43% | 98.11 | 0.984387 |
| 9 | 9.0 | 80.43% | 98.11 | 0.984387 | 80.0 | 80.43% | 98.11 | 0.984387 |
