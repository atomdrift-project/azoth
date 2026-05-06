# Azoth Filegroup `scripts`
Specialist model for `batch`, `javascript`, `lua`, `perl`, `php`, `powershell`, `python`, `ruby`, `shell`, `typescript`, `vbscript`.
- Inputs: shared general `feature_spec.json` (45160 features); policy `general_shared`.
- Feature families:
  - aggregate finding counts
  - ATT&CK/MBC n-grams
  - cleave trait taxonomy
  - element tokens
  - extended file metrics
  - format-group hints
  - hopper score
  - hostile density/escalation
  - packaged capability mode=paths
  - path/criticality bigrams/trigrams
  - repetition penalties
  - severity distribution
  - soft presence
  - structural coverage
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Training rows: 605458 (66428 malware, 539030 benign).
- Benchmark rows: 87084 (9808 malware, 77276 benign).
- Benchmark AUC/AP/F1: 0.9992 / 0.9970 / 0.9849.
| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 80.70% | 0.00 | 0.999570 | 8.0 | 92.43% | 12.94 | 0.994739 |
| 1 | 1.0 | 92.43% | 12.94 | 0.994739 | 16.0 | 92.43% | 12.94 | 0.994739 |
| 2 | 2.0 | 92.43% | 12.94 | 0.994739 | 24.0 | 92.43% | 12.94 | 0.994739 |
| 3 | 3.0 | 92.43% | 12.94 | 0.994739 | 32.0 | 93.73% | 25.88 | 0.990744 |
| 4 | 4.0 | 92.43% | 12.94 | 0.994739 | 40.0 | 94.52% | 38.82 | 0.985312 |
| 5 | 5.0 | 92.43% | 12.94 | 0.994739 | 48.0 | 94.52% | 38.82 | 0.985312 |
| 6 | 6.0 | 92.43% | 12.94 | 0.994739 | 56.0 | 94.58% | 51.76 | 0.984939 |
| 7 | 7.0 | 92.43% | 12.94 | 0.994739 | 64.0 | 94.58% | 51.76 | 0.984939 |
| 8 | 8.0 | 92.43% | 12.94 | 0.994739 | 72.0 | 94.86% | 64.70 | 0.982325 |
| 9 | 9.0 | 92.43% | 12.94 | 0.994739 | 80.0 | 94.88% | 77.64 | 0.982238 |
