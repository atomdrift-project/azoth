# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 837332 | 0.950074 | 0.943479 | 0.9027 | 0.9969 | -0.046826 | 0.9971 | -0.053621 |
| `makefile` | 3,331 | 0.464479 | 0.038667 | 0.0674 | — | - | — | - |
| `rtf` | 837 | 0.992576 | 0.999332 | 0.9923 | — | - | — | - |
| `python-bytecode` | 11,212 | 0.988199 | 0.980007 | 0.9729 | — | - | — | - |
| `pkg-info` | 1,507 | 0.996720 | 0.999386 | 0.9922 | — | - | — | - |
| `xls` | 7,281 | 0.980045 | 0.990525 | 0.9734 | — | - | — | - |
| `elf` | 42,886 | 0.996613 | 0.997982 | 0.9885 | 0.9887 | +0.007913 | 0.9902 | +0.007782 |
| `package.json` | 4,825 | 0.995158 | 0.996629 | 0.9913 | — | - | — | - |
| `shell` | 9,216 | 0.983685 | 0.968360 | 0.9288 | — | - | — | - |
| `tar` | 5,597 | 0.981022 | 0.986495 | 0.9490 | — | - | — | - |
| `ole` | 1,570 | 0.964038 | 0.976693 | 0.9536 | — | - | — | - |
| `lnk` | 669 | 0.899011 | 0.966381 | 0.9038 | — | - | — | - |
| `docx` | 620 | 0.868373 | 0.981509 | 0.9534 | — | - | — | - |
| `macho` | 1,820 | 0.983291 | 0.953987 | 0.8740 | — | - | — | - |
| `perl` | 4,949 | 0.985305 | 0.884537 | 0.8696 | — | - | — | - |
| `java_class` | 88,268 | 0.983873 | 0.913528 | 0.9281 | — | - | — | - |
| `javascript` | 87,924 | 0.975366 | 0.950318 | 0.9029 | — | - | — | - |
| `pe` | 183,388 | 0.984598 | 0.998038 | 0.9914 | 0.9982 | -0.013602 | 0.9983 | -0.000262 |
| `jar` | 897 | 0.927595 | 0.938295 | 0.8878 | — | - | — | - |
| `kotlin` | 10,265 | 0.925361 | 0.904939 | 0.8306 | — | - | — | - |
| `python` | 25,186 | 0.903254 | 0.828507 | 0.8412 | — | - | — | - |
| `php` | 18,871 | 0.889476 | 0.757157 | 0.7672 | — | - | — | - |
| `powershell` | 942 | 0.962310 | 0.980932 | 0.9493 | — | - | — | - |
| `vbs` | 1,854 | 0.964988 | 0.988830 | 0.9617 | — | - | — | - |
| `zip` | 14,015 | 0.779949 | 0.971632 | 0.9579 | — | - | — | - |
| `xlsx` | 7,592 | 0.714451 | 0.987716 | 0.9869 | — | - | — | - |
| `csharp` | 8,383 | 0.715028 | 0.422743 | 0.4853 | — | - | — | - |
| `pdf` | 25,422 | 0.965984 | 0.993758 | 0.9763 | 0.9878 | -0.021816 | 0.9901 | +0.003658 |
| `jpeg` | 3,871 | 0.613756 | 0.227572 | 0.3070 | — | - | — | - |
| `c` | 85,046 | 0.621754 | 0.248793 | 0.3356 | — | - | — | - |
| `text` | 10,697 | 0.575857 | 0.188136 | 0.2619 | — | - | — | - |
| `deb` | 917 | 0.513417 | 0.159409 | 0.2000 | — | - | — | - |
| `go` | 16,414 | 0.543957 | 0.179008 | 0.2007 | — | - | — | - |
| `png` | 21,917 | 0.555629 | 0.120667 | 0.1621 | — | - | — | - |
| `rust` | 11,048 | 0.508465 | 0.070303 | 0.1020 | — | - | — | - |
| `plist` | 1,650 | 0.531508 | 0.101038 | 0.1429 | — | - | — | - |
| `xml` | 26,027 | 0.692025 | 0.165913 | 0.3172 | — | - | — | - |
| `batch` | 22,635 | 0.708162 | 0.992000 | 0.9953 | — | - | — | - |
| `json` | 3,962 | 0.667489 | 0.049435 | 0.1020 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (8,595 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
