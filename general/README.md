# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,245 features) extracted from cleave reports.
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
- Calibration corpus: 17,074,459 rows (2,672,405 malware, 14,402,054 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 36.85% | 0.00 | routed |
| 1 | 1.0 | 37.06% | 3728.6 | routed |
| 2 | 2.0 | 37.11% | 3728.6 | routed |
| 3 | 3.0 | 37.19% | 3728.6 | routed |
| 4 | 4.0 | 37.42% | 3728.6 | routed |
| 5 | 5.0 | 37.49% | 3728.6 | routed |
| 10 | 10.0 | 37.79% | 3735.6 | routed |
| 15 | 15.0 | 38.22% | 3742.5 | routed |
| 20 | 20.0 | 38.73% | 3742.5 | routed |
| 25 | 25.0 | 39.37% | 3749.5 | routed |
| 30 | 30.0 | 40.09% | 3756.4 | routed |
| 40 | 40.0 | 41.27% | 3784.2 | routed |
| 50 | 50.0 | 41.73% | 3791.1 | routed |
| 60 | 60.0 | 42.32% | 3798.1 | routed |
| 70 | 70.0 | 42.88% | 3825.8 | routed |
| 80 | 80.0 | 43.33% | 3846.7 | routed |
| 90 | 90.0 | 43.73% | 3853.6 | routed |
| 100 | 100.0 | 44.17% | 3874.4 | routed |
| 125 | 125.0 | 45.66% | 3923.1 | routed |
| 150 | 150.0 | 46.66% | 3985.5 | routed |
| 175 | 175.0 | 47.34% | 4027.2 | routed |
| 200 | 200.0 | 47.97% | 4068.9 | routed |
| 250 | 250.0 | 49.15% | 4152.2 | routed |
| 300 | 300.0 | 50.34% | 4221.6 | routed |
| 500 | 500.0 | 54.69% | 4610.5 | routed |
| 750 | 750.0 | 57.84% | 4999.3 | routed |
| 1000 | 1000.0 | 60.19% | 5506.2 | routed |
| 1250 | 1250.0 | 62.28% | 5957.5 | routed |
| 1500 | 1500.0 | 63.92% | 6415.8 | routed |
| 1750 | 1750.0 | 65.02% | 6860.1 | routed |
| 2000 | 2000.0 | 65.91% | 7311.5 | routed |
| 2250 | 2250.0 | 66.56% | 7818.3 | routed |
| 2500 | 2500.0 | 67.23% | 8241.9 | routed |
| 3000 | 3000.0 | 68.30% | 9241.7 | routed |
| 4000 | 4000.0 | 69.94% | 12109.4 | routed |
| 5000 | 5000.0 | 71.10% | 13970.2 | routed |
| 6000 | 6000.0 | 71.93% | 15935.2 | routed |
| 7500 | 7500.0 | 72.80% | 18525.1 | routed |
| 10000 | 10000.0 | 73.93% | 23309.2 | routed |
| 15000 | 15000.0 | 75.31% | 32231.5 | routed |
| 20000 | 20000.0 | 76.18% | 38182.1 | routed |
| 25000 | 25000.0 | 76.82% | 48062.6 | routed |
