# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (76,116 features) extracted from cleave reports.
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
- Technique: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Calibration corpus: 6,563,647 rows (2,373,669 malware, 4,189,978 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 17.48% | 0.00 | 0.999148 |
| 1 | 1.0 | 23.22% | 23.87 | 0.998711 |
| 2 | 2.0 | 23.22% | 23.87 | 0.998711 |
| 3 | 3.0 | 23.22% | 23.87 | 0.998711 |
| 5 | 5.0 | 23.22% | 23.87 | 0.998711 |
| 10 | 10.0 | 23.22% | 23.87 | 0.998711 |
| 20 | 20.0 | 23.22% | 23.87 | 0.998711 |
| 30 | 30.0 | 23.22% | 23.87 | 0.998711 |
| 40 | 40.0 | 23.22% | 23.87 | 0.998711 |
| 50 | 50.0 | 23.73% | 47.73 | 0.998663 |
| 60 | 60.0 | 23.73% | 47.73 | 0.998663 |
| 70 | 70.0 | 23.73% | 47.73 | 0.998663 |
| 80 | 80.0 | 24.15% | 71.60 | 0.998638 |
| 90 | 90.0 | 24.15% | 71.60 | 0.998638 |
| 100 | 100.0 | 24.55% | 95.47 | 0.998599 |
| 200 | 200.0 | 29.06% | 190.93 | 0.998277 |
| 300 | 300.0 | 30.47% | 286.40 | 0.998129 |
| 500 | 500.0 | 35.73% | 477.33 | 0.997579 |
| 1000 | 1000.0 | 41.18% | 978.53 | 0.996607 |
