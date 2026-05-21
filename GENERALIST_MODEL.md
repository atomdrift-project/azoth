# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 588274 | 0.9842 | 0.9785 | 0.9505 | 0.9969 | -0.0127 | 0.9971 | -0.0186 |
| `pkg-info` | 1,390 | 0.9934 | 0.9994 | 0.9867 | — | - | — | - |
| `batch` | 21,555 | 0.9018 | 0.9967 | 0.9985 | — | - | — | - |
| `elf` | 26,093 | 0.9992 | 0.9986 | 0.9826 | 0.9887 | +0.0105 | 0.9902 | +0.0084 |
| `python-bytecode` | 4,096 | 0.9886 | 0.9794 | 0.9736 | — | - | — | - |
| `ole` | 885 | 0.9789 | 0.9750 | 0.9722 | — | - | — | - |
| `rtf` | 266 | 0.9955 | 0.9989 | 0.9862 | — | - | — | - |
| `kotlin` | 8,200 | 0.9594 | 0.9495 | 0.8727 | — | - | — | - |
| `pdf` | 23,535 | 0.9825 | 0.9979 | 0.9924 | 0.9878 | -0.0053 | 0.9901 | +0.0078 |
| `package.json` | 3,601 | 0.9986 | 0.9993 | 0.9965 | — | - | — | - |
| `perl` | 3,987 | 0.9852 | 0.8117 | 0.8462 | — | - | — | - |
| `shell` | 6,644 | 0.9881 | 0.9653 | 0.9213 | — | - | — | - |
| `java_class` | 47,550 | 0.9332 | 0.9065 | 0.9254 | — | - | — | - |
| `macho` | 1,645 | 0.9194 | 0.8467 | 0.8482 | — | - | — | - |
| `javascript` | 70,196 | 0.9871 | 0.9579 | 0.9166 | — | - | — | - |
| `pe` | 129,196 | 0.9952 | 0.9991 | 0.9909 | 0.9982 | -0.0030 | 0.9983 | +0.0008 |
| `docx` | 207 | 0.8986 | 0.9741 | 0.9191 | — | - | — | - |
| `jar` | 452 | 0.9624 | 0.9626 | 0.9029 | — | - | — | - |
| `php` | 11,390 | 0.9677 | 0.8571 | 0.8285 | — | - | — | - |
| `vbs` | 885 | 0.9632 | 0.9612 | 0.9339 | — | - | — | - |
| `lnk` | 388 | 0.8220 | 0.8955 | 0.8122 | — | - | — | - |
| `csharp` | 7,806 | 0.7684 | 0.4215 | 0.4903 | — | - | — | - |
| `python` | 18,615 | 0.9846 | 0.9296 | 0.8588 | — | - | — | - |
| `plist` | 1,612 | 0.4197 | 0.0935 | 0.1237 | — | - | — | - |
| `xml` | 18,669 | 0.5648 | 0.0978 | 0.1944 | — | - | — | - |
| `powershell` | 531 | 0.9624 | 0.9544 | 0.9216 | — | - | — | - |
| `text` | 8,152 | 0.6932 | 0.2000 | 0.2618 | — | - | — | - |
| `go` | 13,044 | 0.9496 | 0.5921 | 0.6961 | — | - | — | - |
| `rust` | 9,768 | 0.6037 | 0.0538 | 0.1044 | — | - | — | - |
| `jpeg` | 1,446 | 0.6526 | 0.2830 | 0.3158 | — | - | — | - |
| `c` | 68,413 | 0.5822 | 0.2486 | 0.3339 | — | - | — | - |
| `png` | 15,045 | 0.5860 | 0.1420 | 0.1825 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60,790 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.9999
- Average Precision: 0.9999
- Brier: 0.0029
