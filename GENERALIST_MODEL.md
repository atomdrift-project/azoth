# Azoth — Generalist Model

Single LightGBM classifier trained on the full mixed corpus across all supported filetypes. Equivalent to EMBER 2024's "All files" classifier in spirit (Table 5, top section).

**This model alone is not the deployed product.** It is one of the routes the routed ensemble can choose — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Numbers below are reported for transparency and direct EMBER-comparison.

## Per-filetype performance (general model only)

Test-partition only (SHA256-deterministic 12.5% locked holdout, never trained on or calibrated against). EMBER columns reference Joyce et al., *KDD'25*, Table 5 'All files → X' rows.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 526207 | 0.9821 | 0.9748 | 0.9414 | 0.9969 | -0.0148 | 0.9971 | -0.0223 |
| `pe` | 117645 | 0.9933 | 0.9987 | 0.9860 | 0.9982 | -0.0049 | 0.9983 | +0.0004 |
| `elf` | 20007 | 0.9991 | 0.9968 | 0.9692 | 0.9887 | +0.0104 | 0.9902 | +0.0066 |
| `macho` | 1292 | 0.8987 | 0.7373 | 0.6879 | — | - | — | - |
| `msi` | 108 | 0.9066 | 0.9933 | 0.9806 | — | - | — | - |
| `pdf` | 19920 | 0.9721 | 0.9962 | 0.9933 | 0.9878 | -0.0157 | 0.9901 | +0.0061 |
| `rtf` | 246 | 0.9788 | 0.9954 | 0.9796 | — | - | — | - |
| `javascript` | 64604 | 0.9906 | 0.9662 | 0.9286 | — | - | — | - |
| `python` | 17692 | 0.9847 | 0.9307 | 0.8585 | — | - | — | - |
| `shell` | 5939 | 0.9869 | 0.9433 | 0.9069 | — | - | — | - |
| `powershell` | 380 | 0.9716 | 0.9437 | 0.8755 | — | - | — | - |
| `batch` | 17608 | 0.8873 | 0.9948 | 0.9987 | — | - | — | - |
| `package.json` | 3341 | 0.9992 | 0.9996 | 0.9967 | — | - | — | - |
| `jar` | 394 | 0.9778 | 0.9752 | 0.9147 | — | - | — | - |
| `ruby` | 2828 | 0.9999 | 0.9821 | 0.9333 | — | - | — | - |
| `perl` | 3807 | 0.9840 | 0.8260 | 0.8400 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (56209 features)
- Trained on the full mixed corpus across all supported filetypes (75% train / 12.5% dev / 12.5% test, SHA256-deterministic split). Calibrators and L0..L9 thresholds are fit on dev; the metrics in this card are reported on the locked test partition (never seen during training or calibration).

## Hard-pool reference (training-time evaluation)

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029

These are the numbers reported during training on the hard-pool holdout (a curated subset). The per-filetype table above is the better reference for production expectations.
