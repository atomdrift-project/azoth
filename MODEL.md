# Azoth Bundle

Routed ensemble of the general model plus eligible filegroup and filetype specialists.

- Inputs: one cleave report vectorized with the shared general feature spec.
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
- Base technique: LightGBM binary classifier: estimators=500, num_leaves=96, max_depth=14, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Decision rule: route-level OR ensemble calibrated against the full score-cache corpus.
- Runtime route: score `az`, plus `az/<filegroup>` and `az/<filetype>` when calibrated.
- At level L, a file is flagged when any routed score crosses its stored threshold.
- Threshold search maximizes `TP(union)` subject to `FP(union) <= floor(benign * target_L / 1e6)`.
- A specialist is kept only when it adds marginal true positives without breaking that union FP cap.
- Calibration snapshot: `51198735`.
- Calibration rows: 2173639 (393489 malware, 1780150 benign).
- Models: 34 routes.

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 60.05% | 0.00 | routed | 8.0 | 65.95% | 7.86 | routed |
| 1 | 1.0 | 60.47% | 0.56 | routed | 16.0 | 69.53% | 15.73 | routed |
| 2 | 2.0 | 60.53% | 1.69 | routed | 24.0 | 71.00% | 23.59 | routed |
| 3 | 3.0 | 62.91% | 2.81 | routed | 32.0 | 73.31% | 31.46 | routed |
| 4 | 4.0 | 64.08% | 3.93 | routed | 40.0 | 75.07% | 39.88 | routed |
| 5 | 5.0 | 64.20% | 4.49 | routed | 48.0 | 75.26% | 47.75 | routed |
| 6 | 6.0 | 64.22% | 5.62 | routed | 56.0 | 74.29% | 55.61 | routed |
| 7 | 7.0 | 66.34% | 6.74 | routed | 64.0 | 75.77% | 63.48 | routed |
| 8 | 8.0 | 65.95% | 7.86 | routed | 72.0 | 76.16% | 71.90 | routed |
| 9 | 9.0 | 66.44% | 8.99 | routed | 80.0 | 76.38% | 79.77 | routed |
