# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 836005 | 0.982193 | 0.978776 | 0.9495 | 0.9969 | -0.014707 | 0.9971 | -0.018324 |
| `rtf` | 837 | 0.999073 | 0.999937 | 0.9968 | — | - | — | - |
| `batch` | 22,633 | 0.979900 | 0.999117 | 0.9980 | — | - | — | - |
| `python-bytecode` | 11,055 | 0.991373 | 0.978134 | 0.9771 | — | - | — | - |
| `xls` | 7,277 | 0.995696 | 0.997555 | 0.9803 | — | - | — | - |
| `elf` | 42,867 | 0.998788 | 0.998864 | 0.9847 | 0.9887 | +0.010088 | 0.9902 | +0.008664 |
| `package.json` | 4,810 | 0.997270 | 0.998013 | 0.9933 | — | - | — | - |
| `docx` | 620 | 0.857697 | 0.980138 | 0.9572 | — | - | — | - |
| `tar` | 5,575 | 0.989618 | 0.990967 | 0.9455 | — | - | — | - |
| `ole` | 1,569 | 0.996176 | 0.996432 | 0.9788 | — | - | — | - |
| `lnk` | 668 | 0.907835 | 0.974816 | 0.9219 | — | - | — | - |
| `macho` | 1,820 | 0.931982 | 0.876279 | 0.8567 | — | - | — | - |
| `shell` | 9,204 | 0.992955 | 0.978105 | 0.9375 | — | - | — | - |
| `perl` | 4,948 | 0.991042 | 0.887115 | 0.8857 | — | - | — | - |
| `pkg-info` | 1,502 | 0.997960 | 0.999619 | 0.9961 | — | - | — | - |
| `jar` | 894 | 0.966198 | 0.963393 | 0.9165 | — | - | — | - |
| `javascript` | 87,765 | 0.984709 | 0.954798 | 0.8965 | — | - | — | - |
| `pe` | 183,330 | 0.985715 | 0.998078 | 0.9912 | 0.9982 | -0.012485 | 0.9983 | -0.000222 |
| `php` | 18,825 | 0.975739 | 0.857467 | 0.8231 | — | - | — | - |
| `python` | 24,954 | 0.988496 | 0.952334 | 0.9144 | — | - | — | - |
| `kotlin` | 10,271 | 0.945468 | 0.948126 | 0.9117 | — | - | — | - |
| `vbs` | 1,854 | 0.962995 | 0.987615 | 0.9762 | — | - | — | - |
| `powershell` | 939 | 0.961192 | 0.981141 | 0.9497 | — | - | — | - |
| `java_class` | 88,259 | 0.963765 | 0.911677 | 0.9078 | — | - | — | - |
| `zip` | 14,009 | 0.787256 | 0.971094 | 0.9487 | — | - | — | - |
| `csharp` | 8,383 | 0.854090 | 0.434023 | 0.4890 | — | - | — | - |
| `xlsx` | 7,582 | 0.947119 | 0.997953 | 0.9977 | — | - | — | - |
| `makefile` | 3,327 | 0.781991 | 0.146921 | 0.3452 | — | - | — | - |
| `text` | 10,681 | 0.641706 | 0.210772 | 0.2747 | — | - | — | - |
| `pdf` | 25,421 | 0.977053 | 0.994808 | 0.9906 | 0.9878 | -0.010747 | 0.9901 | +0.004708 |
| `deb` | 919 | 0.557107 | 0.162406 | 0.2000 | — | - | — | - |
| `c` | 85,040 | 0.815557 | 0.305526 | 0.3498 | — | - | — | - |
| `jpeg` | 3,884 | 0.660702 | 0.246002 | 0.3482 | — | - | — | - |
| `rust` | 10,896 | 0.647184 | 0.095728 | 0.1392 | — | - | — | - |
| `xml` | 26,054 | 0.663858 | 0.217722 | 0.3369 | — | - | — | - |
| `go` | 16,305 | 0.928352 | 0.670530 | 0.7023 | — | - | — | - |
| `plist` | 1,652 | 0.609977 | 0.147364 | 0.2500 | — | - | — | - |
| `png` | 21,834 | 0.554201 | 0.127454 | 0.1773 | — | - | — | - |
| `json` | 3,861 | 0.209632 | 0.024055 | 0.0522 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (21,496 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
