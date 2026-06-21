# Azoth General

General malware detector used for every routed decision.

- Inputs: shared `feature_spec.json` (9,374 features) extracted from cleave reports.
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
- Calibration corpus: 8,168,688 rows (2,620,539 malware, 5,548,149 benign).

| L | Target/100M | Recall | FP/100M | Threshold |
| ---: | ---: | ---: | ---: | ---: |
| 0 | - | 58.03% | 0.00 | routed |
| 1 | 1.0 | 58.16% | 1870335.9 | routed |
| 2 | 2.0 | 58.17% | 1870335.9 | routed |
| 3 | 3.0 | 58.17% | 1870335.9 | routed |
| 4 | 4.0 | 58.17% | 1870335.9 | routed |
| 5 | 5.0 | 58.18% | 1870335.9 | routed |
| 10 | 10.0 | 67.55% | 1875385.0 | routed |
| 20 | 20.0 | 69.76% | 2310762.8 | routed |
| 30 | 30.0 | 70.63% | 2321149.6 | routed |
| 40 | 40.0 | 71.42% | 2617316.2 | routed |
| 50 | 50.0 | 71.67% | 2625827.5 | routed |
| 60 | 60.0 | 71.92% | 2639965.0 | routed |
| 70 | 70.0 | 72.10% | 2648187.9 | routed |
| 80 | 80.0 | 72.33% | 2656410.7 | routed |
| 90 | 90.0 | 72.45% | 2664056.5 | routed |
| 100 | 100.0 | 72.56% | 2671990.8 | routed |
| 200 | 200.0 | 73.65% | 3498314.3 | routed |
| 300 | 300.0 | 75.07% | 3563375.8 | routed |
| 500 | 500.0 | 76.29% | 3723072.0 | routed |
| 1000 | 1000.0 | 77.81% | 4484189.8 | routed |
| 2000 | 2000.0 | 79.37% | 4773864.6 | routed |
| 5000 | 5000.0 | 71.23% | 4328821.3 | routed |
| 7500 | 7500.0 | 72.63% | 3889260.0 | routed |
| 10000 | 10000.0 | 73.55% | 3894020.6 | routed |
| 15000 | 15000.0 | 74.14% | 3126988.1 | routed |
| 20000 | 20000.0 | 74.91% | 3095395.1 | routed |
| 25000 | 25000.0 | 75.81% | 2824474.1 | routed |
