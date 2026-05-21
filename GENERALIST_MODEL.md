# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 588243 | 0.9841 | 0.9780 | 0.9487 | 0.9969 | -0.0128 | 0.9971 | -0.0191 |
| `batch` | 21,555 | 0.9120 | 0.9965 | 0.9987 | — | - | — | - |
| `pe` | 129,185 | 0.9955 | 0.9992 | 0.9905 | 0.9982 | -0.0027 | 0.9983 | +0.0009 |
| `pkg-info` | 1,390 | 0.9956 | 0.9996 | 0.9918 | — | - | — | - |
| `elf` | 26,083 | 0.9993 | 0.9987 | 0.9813 | 0.9887 | +0.0106 | 0.9902 | +0.0085 |
| `rtf` | 266 | 0.9964 | 0.9991 | 0.9860 | — | - | — | - |
| `package.json` | 3,601 | 0.9988 | 0.9994 | 0.9965 | — | - | — | - |
| `pdf` | 23,535 | 0.9758 | 0.9965 | 0.9926 | 0.9878 | -0.0120 | 0.9901 | +0.0064 |
| `kotlin` | 8,198 | 0.9001 | 0.8992 | 0.8715 | — | - | — | - |
| `javascript` | 70,194 | 0.9895 | 0.9635 | 0.9169 | — | - | — | - |
| `macho` | 1,645 | 0.9251 | 0.8548 | 0.8439 | — | - | — | - |
| `python` | 18,615 | 0.9810 | 0.9189 | 0.8588 | — | - | — | - |
| `python-bytecode` | 4,095 | 0.9888 | 0.9793 | 0.9714 | — | - | — | - |
| `ole` | 885 | 0.9788 | 0.9747 | 0.9700 | — | - | — | - |
| `jar` | 452 | 0.9698 | 0.9641 | 0.9066 | — | - | — | - |
| `shell` | 6,642 | 0.9902 | 0.9677 | 0.9208 | — | - | — | - |
| `vbs` | 885 | 0.9424 | 0.9519 | 0.9291 | — | - | — | - |
| `docx` | 207 | 0.8997 | 0.9744 | 0.9191 | — | - | — | - |
| `powershell` | 530 | 0.9642 | 0.9572 | 0.9231 | — | - | — | - |
| `perl` | 3,987 | 0.9838 | 0.8171 | 0.8462 | — | - | — | - |
| `php` | 11,390 | 0.9603 | 0.8555 | 0.8233 | — | - | — | - |
| `lnk` | 388 | 0.8843 | 0.9282 | 0.8782 | — | - | — | - |
| `java_class` | 47,550 | 0.9321 | 0.9046 | 0.9226 | — | - | — | - |
| `go` | 13,044 | 0.9372 | 0.5779 | 0.6978 | — | - | — | - |
| `csharp` | 7,806 | 0.7899 | 0.4311 | 0.4914 | — | - | — | - |
| `c` | 68,413 | 0.6309 | 0.2569 | 0.3364 | — | - | — | - |
| `xml` | 18,669 | 0.6349 | 0.1048 | 0.2120 | — | - | — | - |
| `text` | 8,152 | 0.5825 | 0.1922 | 0.2632 | — | - | — | - |
| `jpeg` | 1,446 | 0.5299 | 0.2646 | 0.3158 | — | - | — | - |
| `png` | 15,045 | 0.5942 | 0.1406 | 0.1838 | — | - | — | - |
| `rust` | 9,768 | 0.5127 | 0.0516 | 0.1043 | — | - | — | - |
| `plist` | 1,612 | 0.5191 | 0.1029 | 0.1509 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60,778 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029
