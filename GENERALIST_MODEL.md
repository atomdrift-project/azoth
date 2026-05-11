# Azoth — Generalist Model

Single LightGBM classifier trained on the full mixed corpus across all supported filetypes. Equivalent to EMBER 2024's "All files" classifier in spirit (Table 5, top section).

**This model alone is not the deployed product.** It is one of the routes the routed ensemble can choose — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Numbers below are reported for transparency and direct EMBER-comparison.

## Per-filetype performance (general model only)

Test-partition only (SHA256-deterministic 12.5% locked holdout, never trained on or calibrated against). EMBER columns reference Joyce et al., *KDD'25*, Table 5 'All files → X' rows.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 408858 | 0.9838 | 0.9737 | 0.9452 | 0.9969 | -0.0131 | 0.9971 | -0.0234 |
| `pe` | 74705 | 0.9942 | 0.9981 | 0.9796 | 0.9982 | -0.0040 | 0.9983 | -0.0002 |
| `elf` | 17668 | 0.9996 | 0.9981 | 0.9752 | 0.9887 | +0.0109 | 0.9902 | +0.0079 |
| `macho` | 949 | 0.9825 | 0.9059 | 0.8466 | — | - | — | - |
| `msi` | 38 | 0.9147 | 0.9773 | 0.9538 | — | - | — | - |
| `pdf` | 358 | 0.3564 | 0.0255 | 0.0592 | 0.9878 | -0.6314 | 0.9901 | -0.9646 |
| `rtf` | 60 | 1.0000 | 1.0000 | 1.0000 | — | - | — | - |
| `javascript` | 57574 | 0.9775 | 0.9621 | 0.9474 | — | - | — | - |
| `python` | 16448 | 0.9908 | 0.9641 | 0.9202 | — | - | — | - |
| `shell` | 5720 | 0.9770 | 0.9198 | 0.8858 | — | - | — | - |
| `powershell` | 323 | 0.9643 | 0.9060 | 0.8382 | — | - | — | - |
| `batch` | 307 | 0.9531 | 0.9166 | 0.8667 | — | - | — | - |
| `package.json` | 3007 | 0.9987 | 0.9994 | 0.9968 | — | - | — | - |
| `jar` | 307 | 0.9806 | 0.9741 | 0.9189 | — | - | — | - |
| `ruby` | 2824 | 1.0000 | 1.0000 | 1.0000 | — | - | — | - |
| `perl` | 3791 | 0.9560 | 0.8665 | 0.8627 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (47621 features)
- Trained on the full mixed corpus across all supported filetypes (75% train / 12.5% dev / 12.5% test, SHA256-deterministic split). Calibrators and L0..L9 thresholds are fit on dev; the metrics in this card are reported on the locked test partition (never seen during training or calibration).

## Hard-pool reference (training-time evaluation)

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029

These are the numbers reported during training on the hard-pool holdout (a curated subset). The per-filetype table above is the better reference for production expectations.
