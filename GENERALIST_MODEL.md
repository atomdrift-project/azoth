# Azoth — Generalist Model

Single LightGBM classifier trained on the full mixed corpus across all supported filetypes. Equivalent to EMBER 2024's "All files" classifier in spirit (Table 5, top section).

**This model alone is not the deployed product.** It is one of the routes the routed ensemble can choose — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Numbers below are reported for transparency and direct EMBER-comparison.

## Per-filetype performance (general model only)

Test-partition only (SHA256-deterministic 12.5% locked holdout, never trained on or calibrated against). EMBER columns reference Joyce et al., *KDD'25*, Table 5 'All files → X' rows.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 372198 | 0.9879 | 0.9800 | 0.9631 | 0.9969 | -0.0090 | 0.9971 | -0.0171 |
| `pe` | 67133 | 0.9970 | 0.9989 | 0.9872 | 0.9982 | -0.0012 | 0.9983 | +0.0006 |
| `elf` | 16886 | 0.9998 | 0.9989 | 0.9844 | 0.9887 | +0.0111 | 0.9902 | +0.0087 |
| `macho` | 921 | 0.9716 | 0.9060 | 0.8571 | — | - | — | - |
| `msi` | 37 | 0.7043 | 0.9420 | 0.9118 | — | - | — | - |
| `pdf` | 352 | 0.8252 | 0.1085 | 0.2000 | 0.9878 | -0.1626 | 0.9901 | -0.8816 |
| `rtf` | 56 | 1.0000 | 1.0000 | 1.0000 | — | - | — | - |
| `javascript` | 54690 | 0.9857 | 0.9707 | 0.9551 | — | - | — | - |
| `python` | 15704 | 0.9918 | 0.9801 | 0.9608 | — | - | — | - |
| `shell` | 5455 | 0.9715 | 0.9353 | 0.9105 | — | - | — | - |
| `powershell` | 241 | 0.9812 | 0.9641 | 0.9027 | — | - | — | - |
| `batch` | 291 | 0.9562 | 0.9207 | 0.8704 | — | - | — | - |
| `package.json` | 2782 | 0.9991 | 0.9996 | 0.9971 | — | - | — | - |
| `jar` | 289 | 0.9935 | 0.9890 | 0.9626 | — | - | — | - |
| `ruby` | 2813 | 1.0000 | 1.0000 | 1.0000 | — | - | — | - |
| `perl` | 3721 | 0.9988 | 0.9052 | 0.8750 | — | - | — | - |

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
