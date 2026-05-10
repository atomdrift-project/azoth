# Azoth — Generalist Model

Single LightGBM classifier trained on the full mixed corpus across all supported filetypes. Equivalent to EMBER 2024's "All files" classifier in spirit (Table 5, top section).

**This model alone is not the deployed product.** It is one of the routes the routed ensemble can choose — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Numbers below are reported for transparency and direct EMBER-comparison.

## Per-filetype performance (general model only)

Test-partition only (SHA256-deterministic 12.5% locked holdout, never trained on or calibrated against). EMBER columns reference Joyce et al., *KDD'25*, Table 5 'All files → X' rows.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1963 | 0.9942 | 0.9995 | 0.9894 | 0.9969 | -0.0027 | 0.9971 | +0.0024 |
| `pe` | 1253 | 1.0000 | 1.0000 | 1.0000 | 0.9982 | +0.0018 | 0.9983 | +0.0017 |
| `elf` | 14 | 0.0000 | 0.0000 | 0.0000 | 0.9887 | -0.9887 | 0.9902 | -0.9902 |
| `msi` | 2 | 0.0000 | 0.0000 | 0.0000 | — | - | — | - |
| `javascript` | 11 | 1.0000 | 1.0000 | 1.0000 | — | - | — | - |
| `shell` | 21 | 0.0000 | 0.0000 | 0.0000 | — | - | — | - |
| `jar` | 13 | 0.0000 | 0.0000 | 0.0000 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (45503 features)
- Trained on the full mixed corpus across all supported filetypes (75% train / 12.5% dev / 12.5% test, SHA256-deterministic split). Calibrators and L0..L9 thresholds are fit on dev; the metrics in this card are reported on the locked test partition (never seen during training or calibration).

## Hard-pool reference (training-time evaluation)

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029

These are the numbers reported during training on the hard-pool holdout (a curated subset). The per-filetype table above is the better reference for production expectations.
