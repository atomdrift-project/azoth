# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 905194 | 0.954014 | 0.942127 | 0.8994 | 0.9969 | -0.042886 | 0.9971 | -0.054973 |
| `rtf` | 844 | 0.991690 | 0.999269 | 0.9924 | — | - | — | - |
| `pkg-info` | 1,567 | 0.997732 | 0.999464 | 0.9930 | — | - | — | - |
| `batch` | 22,808 | 0.734654 | 0.988999 | 0.9943 | — | - | — | - |
| `elf` | 44,674 | 0.996595 | 0.997874 | 0.9877 | 0.9887 | +0.007895 | 0.9902 | +0.007674 |
| `package.json` | 5,204 | 0.994691 | 0.996050 | 0.9893 | — | - | — | - |
| `ole` | 1,601 | 0.989511 | 0.990784 | 0.9653 | — | - | — | - |
| `xls` | 7,323 | 0.982388 | 0.991857 | 0.9739 | — | - | — | - |
| `pdf` | 25,449 | 0.965878 | 0.993558 | 0.9783 | 0.9878 | -0.021922 | 0.9901 | +0.003458 |
| `macho` | 1,914 | 0.976002 | 0.939158 | 0.8562 | — | - | — | - |
| `tar` | 6,155 | 0.981546 | 0.985418 | 0.9480 | — | - | — | - |
| `shell` | 9,862 | 0.979913 | 0.961674 | 0.9261 | — | - | — | - |
| `vbs` | 1,878 | 0.951464 | 0.984625 | 0.9561 | — | - | — | - |
| `docx` | 626 | 0.874803 | 0.982416 | 0.9628 | — | - | — | - |
| `python-bytecode` | 24,036 | 0.943443 | 0.886150 | 0.9144 | — | - | — | - |
| `lnk` | 675 | 0.900685 | 0.966956 | 0.9058 | — | - | — | - |
| `perl` | 5,442 | 0.948886 | 0.832383 | 0.8333 | — | - | — | - |
| `jar` | 939 | 0.915873 | 0.930721 | 0.8825 | — | - | — | - |
| `powershell` | 982 | 0.939602 | 0.973321 | 0.9342 | — | - | — | - |
| `pe` | 184,648 | 0.984549 | 0.998027 | 0.9908 | 0.9982 | -0.013651 | 0.9983 | -0.000273 |
| `php` | 20,117 | 0.894944 | 0.750341 | 0.7493 | — | - | — | - |
| `javascript` | 94,539 | 0.964588 | 0.939754 | 0.8922 | — | - | — | - |
| `kotlin` | 10,785 | 0.918215 | 0.907562 | 0.8563 | — | - | — | - |
| `java_class` | 93,928 | 0.977809 | 0.875323 | 0.8958 | — | - | — | - |
| `zip` | 14,198 | 0.751872 | 0.967660 | 0.9474 | — | - | — | - |
| `xlsx` | 7,673 | 0.741921 | 0.988604 | 0.9868 | — | - | — | - |
| `cargo.toml` | 235 | 0.424190 | 0.398202 | 0.4848 | — | - | — | - |
| `python` | 29,620 | 0.888549 | 0.791350 | 0.7892 | — | - | — | - |
| `json` | 5,550 | 0.701522 | 0.056786 | 0.1253 | — | - | — | - |
| `csharp` | 8,765 | 0.711857 | 0.362646 | 0.3815 | — | - | — | - |
| `jpeg` | 3,971 | 0.627104 | 0.218317 | 0.2986 | — | - | — | - |
| `c` | 97,988 | 0.679908 | 0.254399 | 0.3257 | — | - | — | - |
| `deb` | 997 | 0.478279 | 0.146860 | 0.1818 | — | - | — | - |
| `text` | 13,515 | 0.585610 | 0.137106 | 0.1801 | — | - | — | - |
| `java` | 7,453 | 0.681649 | 0.169920 | 0.2374 | — | - | — | - |
| `go` | 17,086 | 0.588976 | 0.209398 | 0.2216 | — | - | — | - |
| `plist` | 1,687 | 0.485432 | 0.085885 | 0.1096 | — | - | — | - |
| `png` | 23,262 | 0.535099 | 0.102239 | 0.1201 | — | - | — | - |
| `rust` | 12,825 | 0.600011 | 0.071388 | 0.1014 | — | - | — | - |
| `makefile` | 3,919 | 0.516185 | 0.037502 | 0.0882 | — | - | — | - |
| `xml` | 27,600 | 0.696893 | 0.140957 | 0.2425 | — | - | — | - |
| `applescript` | 62 | 0.331197 | 0.550764 | 0.6047 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,527 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
