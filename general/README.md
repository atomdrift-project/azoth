# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (73,750 features) extracted from cleave reports.
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
- Calibration corpus: 6,488,381 rows (2,337,508 malware, 4,150,873 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 13.46% | 0.00 | 0.999337 |
| 1 | 1.0 | 19.66% | 24.09 | 0.998954 |
| 2 | 2.0 | 19.66% | 24.09 | 0.998954 |
| 3 | 3.0 | 19.66% | 24.09 | 0.998954 |
| 5 | 5.0 | 19.66% | 24.09 | 0.998954 |
| 10 | 10.0 | 19.66% | 24.09 | 0.998954 |
| 20 | 20.0 | 19.66% | 24.09 | 0.998954 |
| 30 | 30.0 | 19.66% | 24.09 | 0.998954 |
| 40 | 40.0 | 19.66% | 24.09 | 0.998954 |
| 50 | 50.0 | 22.21% | 48.18 | 0.998841 |
| 60 | 60.0 | 22.21% | 48.18 | 0.998841 |
| 70 | 70.0 | 22.21% | 48.18 | 0.998841 |
| 80 | 80.0 | 22.40% | 72.27 | 0.998827 |
| 90 | 90.0 | 22.40% | 72.27 | 0.998827 |
| 100 | 100.0 | 25.93% | 96.37 | 0.998546 |
