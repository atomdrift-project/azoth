# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 588274 | 0.984154 | 0.978512 | 0.9505 | 0.9969 | -0.012746 | 0.9971 | -0.018588 |
| `pkg-info` | 1,390 | 0.993414 | 0.999418 | 0.9867 | — | - | — | - |
| `batch` | 21,555 | 0.901819 | 0.996725 | 0.9985 | — | - | — | - |
| `elf` | 26,093 | 0.999238 | 0.998558 | 0.9826 | 0.9887 | +0.010538 | 0.9902 | +0.008358 |
| `python-bytecode` | 4,096 | 0.988649 | 0.979381 | 0.9736 | — | - | — | - |
| `ole` | 885 | 0.978878 | 0.974984 | 0.9722 | — | - | — | - |
| `rtf` | 266 | 0.995531 | 0.998919 | 0.9862 | — | - | — | - |
| `kotlin` | 8,200 | 0.959448 | 0.949491 | 0.8727 | — | - | — | - |
| `pdf` | 23,535 | 0.982474 | 0.997864 | 0.9924 | 0.9878 | -0.005326 | 0.9901 | +0.007764 |
| `package.json` | 3,601 | 0.998601 | 0.999258 | 0.9965 | — | - | — | - |
| `perl` | 3,987 | 0.985196 | 0.811656 | 0.8462 | — | - | — | - |
| `shell` | 6,644 | 0.988136 | 0.965270 | 0.9213 | — | - | — | - |
| `java_class` | 47,550 | 0.933249 | 0.906509 | 0.9254 | — | - | — | - |
| `macho` | 1,645 | 0.919364 | 0.846748 | 0.8482 | — | - | — | - |
| `javascript` | 70,196 | 0.987060 | 0.957879 | 0.9166 | — | - | — | - |
| `pe` | 129,196 | 0.995231 | 0.999148 | 0.9909 | 0.9982 | -0.002969 | 0.9983 | +0.000848 |
| `docx` | 207 | 0.898644 | 0.974060 | 0.9191 | — | - | — | - |
| `jar` | 452 | 0.962388 | 0.962605 | 0.9029 | — | - | — | - |
| `php` | 11,390 | 0.967669 | 0.857125 | 0.8285 | — | - | — | - |
| `vbs` | 885 | 0.963178 | 0.961208 | 0.9339 | — | - | — | - |
| `lnk` | 388 | 0.822035 | 0.895491 | 0.8122 | — | - | — | - |
| `csharp` | 7,806 | 0.768360 | 0.421544 | 0.4903 | — | - | — | - |
| `python` | 18,615 | 0.984627 | 0.929572 | 0.8588 | — | - | — | - |
| `plist` | 1,612 | 0.419718 | 0.093530 | 0.1237 | — | - | — | - |
| `xml` | 18,669 | 0.564779 | 0.097781 | 0.1944 | — | - | — | - |
| `powershell` | 531 | 0.962396 | 0.954361 | 0.9216 | — | - | — | - |
| `text` | 8,152 | 0.693167 | 0.200023 | 0.2618 | — | - | — | - |
| `go` | 13,044 | 0.949551 | 0.592146 | 0.6961 | — | - | — | - |
| `rust` | 9,768 | 0.603679 | 0.053809 | 0.1044 | — | - | — | - |
| `jpeg` | 1,446 | 0.652558 | 0.282968 | 0.3158 | — | - | — | - |
| `c` | 68,413 | 0.582182 | 0.248637 | 0.3339 | — | - | — | - |
| `png` | 15,045 | 0.585970 | 0.141966 | 0.1825 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60,790 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.999889
- Average Precision: 0.999915
- Brier: 0.0029
