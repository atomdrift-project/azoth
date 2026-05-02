# Azoth Filegroup `portable`
Specialist model for `dex`, `jar`, `java_class`, `pyc`, `wasm`.
- Inputs: shared general `feature_spec.json` (28960 features); policy `general_shared`.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=25, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 1069 (623 malware, 446 benign).
- Benchmark rows: 1090 (124 malware, 966 benign).
- Benchmark AUC/AP/F1: 0.9816 / 0.9724 / 0.9672.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 60.48% | 0.00 | 0.914178 | 8.0 | 94.35% | 1035.2 | 0.558278 |
| 1 | 1.0 | 94.35% | 1035.2 | 0.558278 | 16.0 | 94.35% | 1035.2 | 0.558278 |
| 2 | 2.0 | 94.35% | 1035.2 | 0.558278 | 24.0 | 94.35% | 1035.2 | 0.558278 |
| 3 | 3.0 | 94.35% | 1035.2 | 0.558278 | 32.0 | 94.35% | 1035.2 | 0.558278 |
| 4 | 4.0 | 94.35% | 1035.2 | 0.558278 | 40.0 | 94.35% | 1035.2 | 0.558278 |
| 5 | 5.0 | 94.35% | 1035.2 | 0.558278 | 48.0 | 94.35% | 1035.2 | 0.558278 |
| 6 | 6.0 | 94.35% | 1035.2 | 0.558278 | 56.0 | 94.35% | 1035.2 | 0.558278 |
| 7 | 7.0 | 94.35% | 1035.2 | 0.558278 | 64.0 | 94.35% | 1035.2 | 0.558278 |
| 8 | 8.0 | 94.35% | 1035.2 | 0.558278 | 72.0 | 94.35% | 1035.2 | 0.558278 |
| 9 | 9.0 | 94.35% | 1035.2 | 0.558278 | 80.0 | 94.35% | 1035.2 | 0.558278 |
