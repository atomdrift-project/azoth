# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,338 features) extracted from cleave reports.
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
- Calibration corpus: 8,434,434 rows (2,612,902 malware, 5,821,532 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 62.58% | 0.00 | routed |
| 1 | 1.0 | 62.68% | 1744369.9 | routed |
| 2 | 2.0 | 62.69% | 1744369.9 | routed |
| 3 | 3.0 | 62.69% | 1744369.9 | routed |
| 4 | 4.0 | 62.69% | 1744369.9 | routed |
| 5 | 5.0 | 62.69% | 1744369.9 | routed |
| 10 | 10.0 | 64.52% | 1749595.1 | routed |
| 20 | 20.0 | 67.64% | 2164030.7 | routed |
| 30 | 30.0 | 70.98% | 2601567.0 | routed |
| 40 | 40.0 | 71.43% | 2615179.8 | routed |
| 50 | 50.0 | 71.77% | 2623017.5 | routed |
| 60 | 60.0 | 72.32% | 2630855.2 | routed |
| 70 | 70.0 | 72.69% | 2638968.0 | routed |
| 80 | 80.0 | 73.02% | 2647355.7 | routed |
| 90 | 90.0 | 73.31% | 2653955.8 | routed |
| 100 | 100.0 | 73.55% | 2661518.5 | routed |
| 200 | 200.0 | 74.72% | 3512803.0 | routed |
| 300 | 300.0 | 75.78% | 3571792.0 | routed |
| 500 | 500.0 | 76.97% | 3688670.0 | routed |
| 1000 | 1000.0 | 78.27% | 3949514.2 | routed |
| 2000 | 2000.0 | 79.72% | 4201833.2 | routed |
| 5000 | 5000.0 | 70.11% | 4260272.2 | routed |
| 7500 | 7500.0 | 72.06% | 3882687.5 | routed |
| 10000 | 10000.0 | 73.36% | 3887500.1 | routed |
| 15000 | 15000.0 | 74.63% | 3179356.9 | routed |
| 20000 | 20000.0 | 75.87% | 2954813.6 | routed |
| 25000 | 25000.0 | 76.49% | 2630442.7 | routed |
