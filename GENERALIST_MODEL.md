# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 817809 | 0.982156 | 0.976093 | 0.9497 | 0.9969 | -0.014744 | 0.9971 | -0.021007 |
| `rtf` | 742 | 0.995928 | 0.999668 | 0.9949 | — | - | — | - |
| `batch` | 22,531 | 0.918880 | 0.996892 | 0.9975 | — | - | — | - |
| `python-bytecode` | 9,576 | 0.989352 | 0.981453 | 0.9838 | — | - | — | - |
| `xls` | 6,727 | 0.973036 | 0.987684 | 0.9779 | — | - | — | - |
| `ole` | 1,437 | 0.992932 | 0.993235 | 0.9677 | — | - | — | - |
| `elf` | 40,926 | 0.998602 | 0.998560 | 0.9824 | 0.9887 | +0.009902 | 0.9902 | +0.008360 |
| `package.json` | 4,358 | 0.997255 | 0.998202 | 0.9928 | — | - | — | - |
| `docx` | 559 | 0.875972 | 0.981183 | 0.9568 | — | - | — | - |
| `shell` | 8,506 | 0.987256 | 0.969866 | 0.9206 | — | - | — | - |
| `lnk` | 628 | 0.934562 | 0.977922 | 0.9408 | — | - | — | - |
| `macho` | 1,788 | 0.915164 | 0.848125 | 0.8459 | — | - | — | - |
| `pdf` | 25,185 | 0.976531 | 0.995232 | 0.9840 | 0.9878 | -0.011269 | 0.9901 | +0.005132 |
| `pkg-info` | 1,449 | 0.996335 | 0.999487 | 0.9942 | — | - | — | - |
| `perl` | 4,225 | 0.993905 | 0.853607 | 0.8571 | — | - | — | - |
| `html` | 3,250 | 0.793005 | 0.568318 | 0.7179 | — | - | — | - |
| `javascript` | 83,044 | 0.983341 | 0.956353 | 0.8977 | — | - | — | - |
| `pe` | 175,597 | 0.986651 | 0.998122 | 0.9905 | 0.9982 | -0.011549 | 0.9983 | -0.000178 |
| `php` | 15,617 | 0.959951 | 0.853258 | 0.8176 | — | - | — | - |
| `vbs` | 1,681 | 0.963440 | 0.987414 | 0.9716 | — | - | — | - |
| `jar` | 830 | 0.951135 | 0.951547 | 0.9014 | — | - | — | - |
| `kotlin` | 10,227 | 0.952813 | 0.952892 | 0.8938 | — | - | — | - |
| `python` | 22,853 | 0.960869 | 0.877521 | 0.8496 | — | - | — | - |
| `tar` | 5,128 | 0.986310 | 0.989330 | 0.9455 | — | - | — | - |
| `java_class` | 84,031 | 0.937471 | 0.900750 | 0.9128 | — | - | — | - |
| `xlsx` | 6,695 | 0.571791 | 0.988058 | 0.9872 | — | - | — | - |
| `powershell` | 877 | 0.966243 | 0.979903 | 0.9508 | — | - | — | - |
| `zip` | 13,371 | 0.809456 | 0.977498 | 0.9542 | — | - | — | - |
| `csharp` | 8,353 | 0.788359 | 0.403025 | 0.4752 | — | - | — | - |
| `text` | 8,943 | 0.780728 | 0.242417 | 0.3014 | — | - | — | - |
| `jpeg` | 3,512 | 0.675284 | 0.226685 | 0.3158 | — | - | — | - |
| `c` | 76,006 | 0.649053 | 0.248367 | 0.3263 | — | - | — | - |
| `deb` | 891 | 0.825243 | 0.277825 | 0.3592 | — | - | — | - |
| `markdown` | 7,698 | 0.555454 | 0.111627 | 0.1818 | — | - | — | - |
| `go` | 14,896 | 0.816287 | 0.312134 | 0.4038 | — | - | — | - |
| `rust` | 10,512 | 0.550017 | 0.061879 | 0.0914 | — | - | — | - |
| `png` | 19,671 | 0.503069 | 0.121953 | 0.1737 | — | - | — | - |
| `xml` | 22,677 | 0.719413 | 0.164016 | 0.2424 | — | - | — | - |
| `plist` | 1,647 | 0.597541 | 0.118217 | 0.1731 | — | - | — | - |
| `json` | 4,028 | 0.523107 | 0.024217 | 0.0476 | — | - | — | - |
| `makefile` | 3,012 | 0.570509 | 0.030597 | 0.0711 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (76,116 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
