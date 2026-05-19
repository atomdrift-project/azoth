# Azoth — Generalist Model

Single LightGBM classifier trained on the full mixed corpus across all supported filetypes. Equivalent to EMBER 2024's "All files" classifier in spirit (Table 5, top section).

**This model alone is not the deployed product.** It is one of the routes the routed ensemble can choose — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Numbers below are reported for transparency and direct EMBER-comparison.

## Per-filetype performance (general model only)

Test-partition only (SHA256-deterministic 12.5% locked holdout, never trained on or calibrated against). EMBER columns reference Joyce et al., *KDD'25*, Table 5 'All files → X' rows.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 585889 | 0.9833 | 0.9782 | 0.9512 | 0.9969 | -0.0136 | 0.9971 | -0.0189 |
| `pe` | 128908 | 0.9956 | 0.9992 | 0.9908 | 0.9982 | -0.0026 | 0.9983 | +0.0009 |
| `elf` | 25753 | 0.9993 | 0.9986 | 0.9806 | 0.9887 | +0.0106 | 0.9902 | +0.0084 |
| `macho` | 1640 | 0.9283 | 0.8632 | 0.8625 | — | - | — | - |
| `msi` | 223 | 0.8064 | 0.9919 | 0.9840 | — | - | — | - |
| `pdf` | 23511 | 0.9770 | 0.9965 | 0.9934 | 0.9878 | -0.0108 | 0.9901 | +0.0064 |
| `rtf` | 265 | 0.9955 | 0.9989 | 0.9838 | — | - | — | - |
| `javascript` | 69906 | 0.9883 | 0.9617 | 0.9169 | — | - | — | - |
| `python` | 18557 | 0.9653 | 0.8906 | 0.8587 | — | - | — | - |
| `shell` | 6602 | 0.9888 | 0.9648 | 0.9194 | — | - | — | - |
| `powershell` | 514 | 0.9608 | 0.9495 | 0.9131 | — | - | — | - |
| `batch` | 21520 | 0.9092 | 0.9953 | 0.9986 | — | - | — | - |
| `package.json` | 3523 | 0.9991 | 0.9995 | 0.9965 | — | - | — | - |
| `jar` | 451 | 0.9681 | 0.9664 | 0.9161 | — | - | — | - |
| `ruby` | 2950 | 0.9998 | 0.9240 | 0.8750 | — | - | — | - |
| `perl` | 3984 | 0.9631 | 0.8056 | 0.8302 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60358 features)
- Trained on the full mixed corpus across all supported filetypes (75% train / 12.5% dev / 12.5% test, SHA256-deterministic split). Calibrators and L0..L9 thresholds are fit on dev; the metrics in this card are reported on the locked test partition (never seen during training or calibration).

## Hard-pool reference (training-time evaluation)

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029

These are the numbers reported during training on the hard-pool holdout (a curated subset). The per-filetype table above is the better reference for production expectations.
