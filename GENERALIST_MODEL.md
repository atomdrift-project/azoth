# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 695967 | 0.983706 | 0.976312 | 0.9480 | 0.9969 | -0.013194 | 0.9971 | -0.020788 |
| `pkg-info` | 1,415 | 0.997226 | 0.999698 | 0.9949 | — | - | — | - |
| `batch` | 22,190 | 0.916354 | 0.996423 | 0.9983 | — | - | — | - |
| `python-bytecode` | 8,014 | 0.985125 | 0.977780 | 0.9847 | — | - | — | - |
| `rtf` | 314 | 0.986729 | 0.997700 | 0.9848 | — | - | — | - |
| `xls` | 4,286 | 0.992158 | 0.993367 | 0.9810 | — | - | — | - |
| `package.json` | 3,834 | 0.997476 | 0.998680 | 0.9946 | — | - | — | - |
| `elf` | 30,382 | 0.999074 | 0.998415 | 0.9774 | 0.9887 | +0.010374 | 0.9902 | +0.008215 |
| `ole` | 1,000 | 0.988548 | 0.982414 | 0.9619 | — | - | — | - |
| `macho` | 1,685 | 0.928585 | 0.868150 | 0.8504 | — | - | — | - |
| `shell` | 7,287 | 0.984743 | 0.963453 | 0.9196 | — | - | — | - |
| `xlsx` | 2,780 | 0.836649 | 0.995654 | 0.9885 | — | - | — | - |
| `deb` | 812 | 0.391217 | 0.145147 | 0.2381 | — | - | — | - |
| `lnk` | 440 | 0.807690 | 0.925768 | 0.8370 | — | - | — | - |
| `perl` | 4,068 | 0.990868 | 0.825783 | 0.8462 | — | - | — | - |
| `pe` | 136,120 | 0.994681 | 0.999085 | 0.9913 | 0.9982 | -0.003519 | 0.9983 | +0.000785 |
| `java_class` | 57,728 | 0.936871 | 0.905727 | 0.9167 | — | - | — | - |
| `javascript` | 79,155 | 0.984981 | 0.957755 | 0.9008 | — | - | — | - |
| `docx` | 246 | 0.869106 | 0.966507 | 0.9109 | — | - | — | - |
| `jar` | 589 | 0.969404 | 0.962813 | 0.9049 | — | - | — | - |
| `python` | 20,476 | 0.970911 | 0.897095 | 0.8520 | — | - | — | - |
| `php` | 14,161 | 0.952558 | 0.851169 | 0.8244 | — | - | — | - |
| `powershell` | 673 | 0.964191 | 0.973026 | 0.9416 | — | - | — | - |
| `kotlin` | 9,863 | 0.938952 | 0.940284 | 0.9083 | — | - | — | - |
| `vbs` | 1,037 | 0.945053 | 0.965601 | 0.9423 | — | - | — | - |
| `csharp` | 8,336 | 0.808482 | 0.419560 | 0.4915 | — | - | — | - |
| `makefile` | 2,836 | 0.342082 | 0.019940 | 0.1000 | — | - | — | - |
| `pdf` | 24,418 | 0.979393 | 0.997031 | 0.9924 | 0.9878 | -0.008407 | 0.9901 | +0.006931 |
| `jpeg` | 2,391 | 0.472874 | 0.233844 | 0.3086 | — | - | — | - |
| `c` | 71,812 | 0.633236 | 0.254519 | 0.3366 | — | - | — | - |
| `text` | 8,359 | 0.656956 | 0.205862 | 0.2816 | — | - | — | - |
| `png` | 18,053 | 0.574610 | 0.126153 | 0.1682 | — | - | — | - |
| `rust` | 10,429 | 0.595750 | 0.063058 | 0.0948 | — | - | — | - |
| `xml` | 20,281 | 0.658727 | 0.124549 | 0.2024 | — | - | — | - |
| `go` | 13,298 | 0.929598 | 0.562747 | 0.6437 | — | - | — | - |
| `plist` | 1,633 | 0.593708 | 0.143087 | 0.2171 | — | - | — | - |
| `json` | 3,177 | 0.459379 | 0.014329 | 0.0305 | — | - | — | - |
| `markdown` | 6,680 | 0.540355 | 0.119145 | 0.2041 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (63,983 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.999889
- Average Precision: 0.999915
- Brier: 0.0029
