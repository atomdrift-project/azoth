# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,308 features) extracted from cleave reports.
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
- Calibration corpus: 14,395,301 rows (2,659,504 malware, 11,735,797 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 64.79% | 0.00 | routed |
| 1 | 1.0 | 64.82% | 22108.5 | routed |
| 2 | 2.0 | 64.83% | 22108.5 | routed |
| 3 | 3.0 | 64.83% | 22108.5 | routed |
| 4 | 4.0 | 64.84% | 22108.5 | routed |
| 5 | 5.0 | 64.84% | 22108.5 | routed |
| 10 | 10.0 | 65.22% | 24838.0 | routed |
| 15 | 15.0 | 65.37% | 26680.4 | routed |
| 20 | 20.0 | 65.47% | 28727.5 | routed |
| 25 | 25.0 | 65.59% | 30638.1 | routed |
| 30 | 30.0 | 65.65% | 39850.0 | routed |
| 40 | 40.0 | 65.77% | 44626.5 | routed |
| 50 | 50.0 | 65.86% | 48584.2 | routed |
| 60 | 60.0 | 66.00% | 52132.5 | routed |
| 70 | 70.0 | 66.15% | 55612.5 | routed |
| 80 | 80.0 | 66.31% | 59160.8 | routed |
| 90 | 90.0 | 66.45% | 61958.5 | routed |
| 100 | 100.0 | 66.58% | 64960.9 | routed |
| 125 | 125.0 | 67.37% | 206005.2 | routed |
| 150 | 150.0 | 67.59% | 213442.9 | routed |
| 175 | 175.0 | 67.76% | 218901.8 | routed |
| 200 | 200.0 | 67.86% | 224565.5 | routed |
| 250 | 250.0 | 68.11% | 237735.0 | routed |
| 300 | 300.0 | 68.36% | 246537.5 | routed |
| 500 | 500.0 | 69.76% | 288229.9 | routed |
| 750 | 750.0 | 71.07% | 338247.0 | routed |
| 1000 | 1000.0 | 71.85% | 363835.6 | routed |
| 1250 | 1250.0 | 72.52% | 389083.0 | routed |
| 1500 | 1500.0 | 73.13% | 407575.0 | routed |
| 1750 | 1750.0 | 73.80% | 444354.4 | routed |
| 2000 | 2000.0 | 74.25% | 458342.8 | routed |
| 2250 | 2250.0 | 74.64% | 471512.4 | routed |
| 2500 | 2500.0 | 74.93% | 480656.1 | routed |
| 3000 | 3000.0 | 75.47% | 494849.2 | routed |
| 4000 | 4000.0 | 76.49% | 509724.7 | routed |
| 5000 | 5000.0 | 77.17% | 515183.6 | routed |
| 6000 | 6000.0 | 77.31% | 458888.7 | routed |
| 7500 | 7500.0 | 78.01% | 461277.0 | routed |
| 10000 | 10000.0 | 79.04% | 424838.8 | routed |
| 15000 | 15000.0 | 79.73% | 321188.0 | routed |
| 20000 | 20000.0 | 80.29% | 308086.6 | routed |
| 25000 | 25000.0 | 80.85% | 315660.8 | routed |
