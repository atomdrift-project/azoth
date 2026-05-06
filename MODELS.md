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
- Base technique: LightGBM binary classifier: estimators=600, num_leaves=160, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=60, device=cpu.
- Decision rule: route-level OR ensemble calibrated against the full score-cache corpus.
- Runtime route: score `az`, plus `az/<filegroup>` and `az/<filetype>` when calibrated.
- At level L, a file is flagged when any routed score crosses its stored threshold.
- Threshold search maximizes `TP(union)` subject to `FP(union) <= floor(benign * target_L / 1e6)`.
- A specialist is kept only when it adds marginal true positives without breaking that union FP cap.
- Calibration snapshot: `199337321`.
- Calibration rows: 2293938 (472475 malware, 1821463 benign).
- Models: 49 routes.

## Effective Global Policy

| L | H recall | H FP/1M | S recall | S FP/1M |
| ---: | ---: | ---: | ---: | ---: |
| 0 | 63.61% | 0.00 | 70.88% | 7.69 |
| 5 | 69.99% | 4.94 | 78.26% | 46.67 |
| 9 | 71.12% | 8.78 | 78.87% | 74.67 |

| L | H target/1M | H recall | H FP/1M | H threshold | S target/1M | S recall | S FP/1M | S threshold |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | - | 62.73% | 0.00 | routed | 8.0 | 71.97% | 7.69 | routed |
| 1 | 1.0 | 63.77% | 0.55 | routed | 16.0 | 73.24% | 15.92 | routed |
| 2 | 2.0 | 64.05% | 1.65 | routed | 24.0 | 74.47% | 23.61 | routed |
| 3 | 3.0 | 69.35% | 2.75 | routed | 32.0 | 74.64% | 31.84 | routed |
| 4 | 4.0 | 72.61% | 3.84 | routed | 40.0 | 75.04% | 39.53 | routed |
| 5 | 5.0 | 70.05% | 4.94 | routed | 48.0 | 75.91% | 47.76 | routed |
| 6 | 6.0 | 70.20% | 5.49 | routed | 56.0 | 76.69% | 56.00 | routed |
| 7 | 7.0 | 70.75% | 6.59 | routed | 64.0 | 77.53% | 63.69 | routed |
| 8 | 8.0 | 71.97% | 7.69 | routed | 72.0 | 78.18% | 71.92 | routed |
| 9 | 9.0 | 72.08% | 8.78 | routed | 80.0 | 78.54% | 79.61 | routed |
