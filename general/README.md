# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,519 features) extracted from cleave reports.
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
- Technique: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Calibration corpus: 7,416,064 rows (2,543,560 malware, 4,872,504 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 25.48% | 0.00 | routed |
| 1 | 1.0 | 25.63% | 13627.5 | routed |
| 2 | 2.0 | 25.66% | 13627.5 | routed |
| 3 | 3.0 | 25.69% | 13627.5 | routed |
| 4 | 4.0 | 25.71% | 13627.5 | routed |
| 5 | 5.0 | 25.74% | 13627.5 | routed |
| 10 | 10.0 | 27.04% | 14161.1 | routed |
| 20 | 20.0 | 28.10% | 15289.9 | routed |
| 30 | 30.0 | 28.62% | 16110.8 | routed |
| 40 | 40.0 | 29.07% | 480697.4 | routed |
| 50 | 50.0 | 30.43% | 482216.1 | routed |
| 60 | 60.0 | 31.94% | 483283.3 | routed |
| 70 | 70.0 | 34.07% | 484145.3 | routed |
| 80 | 80.0 | 36.84% | 486628.6 | routed |
| 90 | 90.0 | 38.98% | 487388.0 | routed |
| 100 | 100.0 | 39.23% | 488434.7 | routed |
| 200 | 200.0 | 42.42% | 499640.4 | routed |
| 300 | 300.0 | 44.63% | 506700.5 | routed |
| 500 | 500.0 | 47.48% | 546536.2 | routed |
| 1000 | 1000.0 | 54.41% | 738306.2 | routed |
| 2000 | 2000.0 | 60.27% | 899270.7 | routed |
| 5000 | 5000.0 | 62.49% | 486300.3 | routed |
| 7500 | 7500.0 | 65.15% | 325787.3 | routed |
| 10000 | 10000.0 | 65.42% | 244104.5 | routed |
| 15000 | 15000.0 | 67.22% | 188219.4 | routed |
| 20000 | 20000.0 | 68.16% | 118440.1 | routed |
| 25000 | 25000.0 | 69.06% | 123878.8 | routed |
