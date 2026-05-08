# Azoth Model Card

Azoth is a routed malware detector for broad file scanning. It spends a fixed false-positive budget first, then maximizes recall inside that budget.

## Summary

- Corpus: 2293938 rows (472475 malware, 1821463 benign).
- Routes: 1 general, 8 filegroup, 41 filetype; runtime names are `az`, `az/<filegroup>`, and `az/<filetype>`.
- Inputs: one cleave report per file, vectorized by the feature spec shipped with the selected route.
- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Main feature families: ATT&CK/MBC paths, cleave taxonomy, severity distributions, density/escalation, metrics, symbols, KV shape/vocab, text encodings, and format hints.
- Decision rule: calibrated route policy chooses the strongest available general/filegroup/filetype route for the file.
- Threshold search: maximize true positives subject to `FP(union) <= floor(benign * target/1M / 1e6)`.

## Measurement

- Hard-pool holdout: accuracy=99.64%, F1=0.9971, AUC=0.9999, AP=0.9999.
- Calibration quality on hard-pool holdout: Brier=0.0029, ECE=0.0007.
- Public policy metrics use the full corpus, including low-score rows the trainer may filter from hard-pool learning.
- Default operating point: L3 hostile; suspicious is a higher-recall companion signal.

## Full-Corpus Policy Metrics

| L | H target/1M | H accuracy | H recall | H FP/1M | S target/1M | S accuracy | S recall | S FP/1M |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0 | 93.43% | 68.11% | 0.00 | 8.0 | 94.02% | 70.97% | 7.69 |
| 1 | 1.0 | 87.94% | 41.43% | 0.55 | 16.0 | 94.64% | 73.97% | 15.92 |
| 2 | 2.0 | 91.31% | 57.81% | 1.65 | 24.0 | 94.89% | 75.21% | 23.61 |
| 3 | 3.0 | 92.61% | 64.14% | 2.75 | 32.0 | 95.27% | 77.04% | 31.84 |
| 4 | 4.0 | 93.70% | 69.43% | 3.84 | 40.0 | 96.16% | 81.35% | 39.53 |
| 5 | 5.0 | 93.89% | 70.33% | 4.94 | 48.0 | 96.21% | 81.63% | 44.47 |
| 6 | 6.0 | 93.94% | 70.56% | 5.49 | 56.0 | 96.64% | 83.69% | 51.06 |
| 7 | 7.0 | 93.97% | 70.74% | 6.59 | 64.0 | 96.65% | 83.76% | 58.19 |
| 8 | 8.0 | 94.02% | 70.97% | 7.69 | 72.0 | 96.87% | 84.84% | 65.33 |
| 9 | 9.0 | 94.08% | 71.24% | 8.78 | 80.0 | 96.90% | 84.99% | 70.82 |

## Reproducibility

- Snapshot: `199337321`; score table `557a01fb1348`; model set `b36bba51fb86`.
- Search: `coordinate_descent_v1`; objective `maximize_recall_under_routed_fp_budget`.

## Limits

- Metrics reflect the labeled corpus and its filetype mix; deployment shifts can change real-world results.
- Full-corpus recall is lower than hard-pool holdout recall because it includes weak low-score malware; this is the practical broad-scan expectation.
