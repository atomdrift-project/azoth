# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 588814 | 0.984797 | 0.979698 | 0.9516 | 0.9969 | -0.012103 | 0.9971 | -0.017402 |
| `batch` | 21,556 | 0.911976 | 0.997755 | 0.9985 | — | - | — | - |
| `python-bytecode` | 4,143 | 0.990715 | 0.981668 | 0.9713 | — | - | — | - |
| `rtf` | 266 | 0.996443 | 0.999138 | 0.9860 | — | - | — | - |
| `pkg-info` | 1,390 | 0.995123 | 0.999568 | 0.9915 | — | - | — | - |
| `package.json` | 3,602 | 0.998978 | 0.999427 | 0.9965 | — | - | — | - |
| `xls` | 1,345 | 0.980074 | 0.999211 | 0.9857 | — | - | — | - |
| `elf` | 26,196 | 0.999410 | 0.998874 | 0.9843 | 0.9887 | +0.010710 | 0.9902 | +0.008674 |
| `ole` | 886 | 0.987545 | 0.980880 | 0.9724 | — | - | — | - |
| `macho` | 1,645 | 0.924895 | 0.851016 | 0.8441 | — | - | — | - |
| `shell` | 6,647 | 0.988466 | 0.966632 | 0.9210 | — | - | — | - |
| `perl` | 3,987 | 0.984416 | 0.830477 | 0.8462 | — | - | — | - |
| `docx` | 207 | 0.899560 | 0.974247 | 0.9191 | — | - | — | - |
| `php` | 11,391 | 0.962304 | 0.858545 | 0.8226 | — | - | — | - |
| `java_class` | 47,567 | 0.932806 | 0.906483 | 0.9254 | — | - | — | - |
| `javascript` | 70,257 | 0.989377 | 0.964529 | 0.9174 | — | - | — | - |
| `jar` | 452 | 0.969375 | 0.966439 | 0.9138 | — | - | — | - |
| `pe` | 129,216 | 0.995997 | 0.999287 | 0.9911 | 0.9982 | -0.002203 | 0.9983 | +0.000987 |
| `python` | 18,616 | 0.970912 | 0.896386 | 0.8588 | — | - | — | - |
| `lnk` | 388 | 0.880547 | 0.927303 | 0.8752 | — | - | — | - |
| `kotlin` | 8,216 | 0.887336 | 0.894732 | 0.8684 | — | - | — | - |
| `powershell` | 533 | 0.963095 | 0.954062 | 0.9213 | — | - | — | - |
| `csharp` | 7,806 | 0.769536 | 0.423210 | 0.4917 | — | - | — | - |
| `vbs` | 886 | 0.947378 | 0.953360 | 0.9313 | — | - | — | - |
| `c` | 68,416 | 0.633988 | 0.259473 | 0.3344 | — | - | — | - |
| `text` | 8,153 | 0.672112 | 0.203982 | 0.2636 | — | - | — | - |
| `png` | 15,050 | 0.557941 | 0.140881 | 0.1873 | — | - | — | - |
| `pdf` | 23,538 | 0.982355 | 0.997996 | 0.9941 | 0.9878 | -0.005445 | 0.9901 | +0.007896 |
| `jpeg` | 1,447 | 0.535900 | 0.262703 | 0.3158 | — | - | — | - |
| `go` | 13,044 | 0.926361 | 0.576056 | 0.6575 | — | - | — | - |
| `rust` | 9,768 | 0.546863 | 0.055883 | 0.0954 | — | - | — | - |
| `xml` | 18,689 | 0.634239 | 0.128552 | 0.2447 | — | - | — | - |
| `plist` | 1,612 | 0.419813 | 0.097115 | 0.1364 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (60,810 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.999889
- Average Precision: 0.999915
- Brier: 0.0029
