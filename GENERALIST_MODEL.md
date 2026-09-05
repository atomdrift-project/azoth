# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2214571 | 0.954590 | 0.906677 | 0.8931 | 0.9969 | -0.042310 | 0.9971 | -0.090423 |
| `rtf` | 931 | 0.983112 | 0.997982 | 0.9854 | — | - | — | - |
| `html` | 14,267 | 0.987567 | 0.969867 | 0.9846 | — | - | — | - |
| `pkg_info` | 3,493 | 0.995695 | 0.994658 | 0.9812 | — | - | — | - |
| `ole_doc` | 14,598 | 0.968402 | 0.990411 | 0.9652 | — | - | — | - |
| `elf` | 126,841 | 0.998172 | 0.996374 | 0.9803 | 0.9887 | +0.009472 | 0.9902 | +0.006174 |
| `lnk` | 723 | 0.867945 | 0.971277 | 0.9160 | — | - | — | - |
| `perl` | 9,851 | 0.943473 | 0.763832 | 0.7952 | — | - | — | - |
| `registry` | 13,731 | 0.998698 | 0.850231 | 0.8154 | — | - | — | - |
| `vbs` | 2,074 | 0.951492 | 0.985697 | 0.9463 | — | - | — | - |
| `package.json` | 10,908 | 0.979267 | 0.974810 | 0.9565 | — | - | — | - |
| `npm` | 5,945 | 0.939530 | 0.922851 | 0.8760 | — | - | — | - |
| `pdf` | 26,199 | 0.956895 | 0.992915 | 0.9724 | 0.9878 | -0.030905 | 0.9901 | +0.002815 |
| `tar` | 12,662 | 0.969667 | 0.957344 | 0.9044 | — | - | — | - |
| `macho` | 4,412 | 0.959447 | 0.873053 | 0.8094 | — | - | — | - |
| `pe` | 199,679 | 0.985666 | 0.997612 | 0.9843 | 0.9982 | -0.012534 | 0.9983 | -0.000688 |
| `shell` | 22,596 | 0.963168 | 0.925464 | 0.8834 | — | - | — | - |
| `jar` | 4,265 | 0.952926 | 0.881893 | 0.8551 | — | - | — | - |
| `python_sdist` | 194 | 0.815515 | 0.862649 | 0.7763 | — | - | — | - |
| `python_bytecode` | 128,283 | 0.830589 | 0.654995 | 0.7529 | — | - | — | - |
| `kotlin` | 14,514 | 0.850885 | 0.823816 | 0.7643 | — | - | — | - |
| `powershell` | 1,435 | 0.952552 | 0.967471 | 0.9380 | — | - | — | - |
| `crx` | 1,062 | 0.939175 | 0.889478 | 0.8439 | — | - | — | - |
| `python` | 83,193 | 0.905799 | 0.773461 | 0.7856 | — | - | — | - |
| `javascript` | 225,877 | 0.957292 | 0.900553 | 0.8523 | — | - | — | - |
| `php` | 77,518 | 0.890177 | 0.708849 | 0.7323 | — | - | — | - |
| `whl` | 2,616 | 0.875762 | 0.799694 | 0.7308 | — | - | — | - |
| `gem` | 1,419 | 0.494182 | 0.523803 | 0.5850 | — | - | — | - |
| `java_class` | 216,725 | 0.950031 | 0.795017 | 0.8496 | — | - | — | - |
| `cargo.toml` | 1,168 | 0.739839 | 0.485816 | 0.5429 | — | - | — | - |
| `zip` | 19,285 | 0.750627 | 0.914728 | 0.8402 | — | - | — | - |
| `ruby` | 22,242 | 0.797334 | 0.560277 | 0.6500 | — | - | — | - |
| `ooxml` | 8,918 | 0.665558 | 0.980870 | 0.9798 | — | - | — | - |
| `csharp` | 13,154 | 0.638570 | 0.313886 | 0.3908 | — | - | — | - |
| `batch` | 23,149 | 0.691162 | 0.981753 | 0.9903 | — | - | — | - |
| `c` | 212,867 | 0.660209 | 0.245266 | 0.3426 | — | - | — | - |
| `jpeg` | 5,786 | 0.639519 | 0.160005 | 0.2362 | — | - | — | - |
| `deb` | 3,480 | 0.466255 | 0.085293 | 0.1622 | — | - | — | - |
| `png` | 67,406 | 0.552545 | 0.077606 | 0.1051 | — | - | — | - |
| `xml` | 57,800 | 0.477966 | 0.084174 | 0.1533 | — | - | — | - |
| `java` | 23,190 | 0.557151 | 0.099204 | 0.1570 | — | - | — | - |
| `plist` | 12,643 | 0.601172 | 0.044225 | 0.0706 | — | - | — | - |
| `makefile` | 7,969 | 0.433613 | 0.024979 | 0.0583 | — | - | — | - |
| `text` | 41,044 | 0.606412 | 0.062745 | 0.0904 | — | - | — | - |
| `json` | 32,068 | 0.688444 | 0.064766 | 0.0904 | — | - | — | - |
| `go` | 31,489 | 0.586056 | 0.231724 | 0.2663 | — | - | — | - |
| `rust` | 41,991 | 0.634801 | 0.071584 | 0.1377 | — | - | — | - |
| `7z` | 1,198 | 0.936661 | 0.998396 | 0.9890 | — | - | — | - |
| `apk_android` | 316 | 0.466893 | 0.897024 | 0.9320 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,230 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
