# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 585889 | 0.9833 | 0.9782 | 0.9512 | 0.9969 | -0.0136 | 0.9971 | -0.0189 |
| `batch` | 21,520 | 0.9092 | 0.9953 | 0.9986 | — | - | — | - |
| `rtf` | 265 | 0.9955 | 0.9989 | 0.9838 | — | - | — | - |
| `pkg-info` | 1,390 | 0.9956 | 0.9996 | 0.9911 | — | - | — | - |
| `elf` | 25,753 | 0.9993 | 0.9986 | 0.9806 | 0.9887 | +0.0106 | 0.9902 | +0.0084 |
| `package.json` | 3,523 | 0.9991 | 0.9995 | 0.9965 | — | - | — | - |
| `ole` | 885 | 0.9854 | 0.9839 | 0.9724 | — | - | — | - |
| `perl` | 3,984 | 0.9631 | 0.8056 | 0.8302 | — | - | — | - |
| `pe` | 128,908 | 0.9956 | 0.9992 | 0.9908 | 0.9982 | -0.0026 | 0.9983 | +0.0009 |
| `macho` | 1,640 | 0.9283 | 0.8632 | 0.8625 | — | - | — | - |
| `docx` | 204 | 0.8965 | 0.9731 | 0.9178 | — | - | — | - |
| `javascript` | 69,906 | 0.9883 | 0.9617 | 0.9169 | — | - | — | - |
| `jar` | 451 | 0.9681 | 0.9664 | 0.9161 | — | - | — | - |
| `python` | 18,557 | 0.9653 | 0.8906 | 0.8587 | — | - | — | - |
| `php` | 11,325 | 0.9621 | 0.8554 | 0.8280 | — | - | — | - |
| `kotlin` | 8,170 | 0.8714 | 0.8888 | 0.8730 | — | - | — | - |
| `lnk` | 384 | 0.8359 | 0.9171 | 0.8547 | — | - | — | - |
| `shell` | 6,602 | 0.9888 | 0.9648 | 0.9194 | — | - | — | - |
| `java_class` | 47,243 | 0.9309 | 0.9060 | 0.9254 | — | - | — | - |
| `python-bytecode` | 4,074 | 0.9884 | 0.9794 | 0.9736 | — | - | — | - |
| `vbs` | 868 | 0.9351 | 0.9470 | 0.9234 | — | - | — | - |
| `powershell` | 514 | 0.9608 | 0.9495 | 0.9131 | — | - | — | - |
| `csharp` | 7,806 | 0.8135 | 0.4314 | 0.4930 | — | - | — | - |
| `text` | 8,138 | 0.6438 | 0.1987 | 0.2646 | — | - | — | - |
| `jpeg` | 1,444 | 0.5116 | 0.2553 | 0.3095 | — | - | — | - |
| `png` | 14,995 | 0.5497 | 0.1422 | 0.1891 | — | - | — | - |
| `pdf` | 23,511 | 0.9770 | 0.9965 | 0.9934 | 0.9878 | -0.0108 | 0.9901 | +0.0064 |
| `c` | 68,328 | 0.6073 | 0.2548 | 0.3353 | — | - | — | - |
| `xml` | 18,209 | 0.5016 | 0.1028 | 0.2364 | — | - | — | - |
| `plist` | 1,612 | 0.3707 | 0.0866 | 0.1200 | — | - | — | - |
| `rust` | 9,768 | 0.6536 | 0.0608 | 0.0909 | — | - | — | - |
| `go` | 13,035 | 0.9289 | 0.5975 | 0.6959 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60,358 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029
