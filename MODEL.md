# Azoth Model Card

Azoth is a routed malware detector for broad file scanning. It optimizes for very low false positives first, then maximizes recall within that budget.

## Model

- Task: binary malware classification over cleave reports.
- Inputs: one cleave report per file; routes use the general or route-specific feature spec shipped with the bundle.
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
- Algorithm: LightGBM binary classifier: estimators=600, num_leaves=160, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=60, device=cpu.
- Ensemble: 1 general, 8 filegroup, 40 filetype routes; runtime names are `az`, `az/<filegroup>`, and `az/<filetype>`.
- Decision: a file is flagged when any calibrated route crosses the stored threshold for the chosen level.
- Threshold search: maximize union true positives subject to `FP(union) <= floor(benign * target/1M / 1e6)`.

## Measurement

- Full corpus: 2293938 rows (472475 malware, 1821463 benign).
- Caveat: the general model is trained/evaluated on harder hopper-score-filtered cases; public numbers below use the full corpus, including low-score rows.
- Hard-pool holdout: accuracy=99.28%, F1=0.9938, AUC=0.9996, AP=0.9996.
- Calibration quality on hard-pool holdout: Brier=0.0055, ECE=0.0010.
- Default operating point: L3 hostile; suspicious is a higher-recall companion signal.

## Full-Corpus Policy

| L | H target/1M | H accuracy | H recall | H FP/1M | S target/1M | S accuracy | S recall | S FP/1M |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 92.50% | 63.57% | 0.00 | 8.0 | 94.02% | 70.98% | 7.69 |
| 1 | 1.0 | 88.00% | 41.76% | 0.55 | 16.0 | 94.64% | 73.97% | 15.92 |
| 2 | 2.0 | 91.17% | 57.14% | 1.65 | 24.0 | 95.04% | 75.92% | 23.61 |
| 3 | 3.0 | 92.50% | 63.59% | 2.75 | 32.0 | 95.26% | 77.02% | 31.84 |
| 4 | 4.0 | 93.60% | 68.93% | 3.84 | 40.0 | 95.49% | 78.12% | 39.53 |
| 5 | 5.0 | 93.84% | 70.09% | 4.94 | 48.0 | 95.56% | 78.46% | 46.67 |
| 6 | 6.0 | 93.89% | 70.35% | 5.49 | 56.0 | 95.58% | 78.58% | 52.70 |
| 7 | 7.0 | 93.98% | 70.75% | 6.59 | 64.0 | 95.60% | 78.65% | 62.59 |
| 8 | 8.0 | 94.02% | 70.98% | 7.69 | 72.0 | 95.64% | 78.85% | 69.18 |
| 9 | 9.0 | 94.08% | 71.25% | 8.78 | 80.0 | 95.68% | 79.05% | 74.67 |

## Reproducibility

- Snapshot: `199337321`; score table `a820a15ee99d`; model set `82ca6b97cf0d`.
- Search: `coordinate_descent_v1`; objective `maximize_recall_under_routed_fp_budget`.

## Limits

- Metrics reflect the labeled corpus and its filetype mix; shifts in either can change real-world results.
- The full-corpus recall includes low-score malware that looks weak before ML scoring. This lowers the published recall, but it is the number users should expect when scanning broad, mostly benign corpora.
- The hard-pool holdout shows how well the classifier separates harder cases; the full-corpus table shows the end-to-end tradeoff users care about: detection at a fixed false-positive budget.
