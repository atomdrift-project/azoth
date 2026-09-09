# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2263083 | 0.949335 | 0.898640 | 0.8903 | 0.9969 | -0.047565 | 0.9971 | -0.098460 |
| `rtf` | 931 | 0.989164 | 0.998728 | 0.9885 | — | - | — | - |
| `html` | 22,222 | 0.991432 | 0.969856 | 0.9846 | — | - | — | - |
| `ole_doc` | 14,604 | 0.971287 | 0.990844 | 0.9650 | — | - | — | - |
| `elf` | 130,381 | 0.998199 | 0.996255 | 0.9788 | 0.9887 | +0.009499 | 0.9902 | +0.006055 |
| `package.json` | 11,540 | 0.978411 | 0.974223 | 0.9542 | — | - | — | - |
| `lnk` | 723 | 0.858388 | 0.970398 | 0.9160 | — | - | — | - |
| `perl` | 9,884 | 0.933191 | 0.749528 | 0.7848 | — | - | — | - |
| `registry` | 13,731 | 0.998641 | 0.846157 | 0.8154 | — | - | — | - |
| `vbs` | 2,086 | 0.943587 | 0.984294 | 0.9450 | — | - | — | - |
| `npm` | 13,819 | 0.947728 | 0.924788 | 0.8954 | — | - | — | - |
| `macho` | 4,639 | 0.954652 | 0.859307 | 0.8186 | — | - | — | - |
| `python_sdist` | 233 | 0.856262 | 0.903448 | 0.8517 | — | - | — | - |
| `tar` | 13,233 | 0.968201 | 0.954670 | 0.9061 | — | - | — | - |
| `pdf` | 26,202 | 0.955447 | 0.992193 | 0.9788 | 0.9878 | -0.032353 | 0.9901 | +0.002093 |
| `pe` | 201,296 | 0.984427 | 0.997261 | 0.9831 | 0.9982 | -0.013773 | 0.9983 | -0.001039 |
| `jar` | 4,778 | 0.954963 | 0.876719 | 0.8477 | — | - | — | - |
| `kotlin` | 14,534 | 0.826870 | 0.785654 | 0.7500 | — | - | — | - |
| `pkg_info` | 2,219 | 0.945545 | 0.844610 | 0.8276 | — | - | — | - |
| `shell` | 23,034 | 0.964057 | 0.918982 | 0.8721 | — | - | — | - |
| `powershell` | 1,443 | 0.947177 | 0.963943 | 0.9341 | — | - | — | - |
| `whl` | 2,672 | 0.873707 | 0.786558 | 0.7315 | — | - | — | - |
| `crx` | 1,066 | 0.943052 | 0.908788 | 0.8257 | — | - | — | - |
| `python` | 83,860 | 0.905001 | 0.771498 | 0.7850 | — | - | — | - |
| `javascript` | 231,382 | 0.959478 | 0.900261 | 0.8461 | — | - | — | - |
| `gem` | 5,185 | 0.496263 | 0.448556 | 0.5850 | — | - | — | - |
| `php` | 77,759 | 0.887472 | 0.672355 | 0.7040 | — | - | — | - |
| `java_class` | 219,609 | 0.941814 | 0.791005 | 0.8501 | — | - | — | - |
| `python_bytecode` | 129,538 | 0.825306 | 0.647189 | 0.7487 | — | - | — | - |
| `cargo.toml` | 1,191 | 0.780710 | 0.487475 | 0.5352 | — | - | — | - |
| `ooxml` | 8,918 | 0.719649 | 0.985469 | 0.9798 | — | - | — | - |
| `zip` | 19,496 | 0.751094 | 0.911883 | 0.8363 | — | - | — | - |
| `csharp` | 13,267 | 0.665520 | 0.316899 | 0.3902 | — | - | — | - |
| `batch` | 23,174 | 0.665129 | 0.980923 | 0.9865 | — | - | — | - |
| `c` | 215,185 | 0.688246 | 0.245624 | 0.3409 | — | - | — | - |
| `jpeg` | 5,803 | 0.651692 | 0.170229 | 0.2540 | — | - | — | - |
| `deb` | 3,535 | 0.422018 | 0.055974 | 0.1481 | — | - | — | - |
| `ruby` | 22,787 | 0.809335 | 0.559753 | 0.6500 | — | - | — | - |
| `json` | 32,276 | 0.680014 | 0.062949 | 0.0930 | — | - | — | - |
| `png` | 67,776 | 0.547482 | 0.081048 | 0.1106 | — | - | — | - |
| `java` | 24,138 | 0.469936 | 0.090090 | 0.1454 | — | - | — | - |
| `text` | 41,529 | 0.578485 | 0.055412 | 0.0824 | — | - | — | - |
| `plist` | 12,656 | 0.610257 | 0.044406 | 0.0690 | — | - | — | - |
| `xml` | 58,081 | 0.548011 | 0.098319 | 0.1767 | — | - | — | - |
| `makefile` | 7,974 | 0.357098 | 0.022667 | 0.0443 | — | - | — | - |
| `go` | 31,638 | 0.590488 | 0.221214 | 0.2449 | — | - | — | - |
| `rust` | 42,428 | 0.695962 | 0.078679 | 0.1390 | — | - | — | - |
| `7z` | 1,202 | 0.928527 | 0.998068 | 0.9886 | — | - | — | - |
| `apk_android` | 319 | 0.454582 | 0.887745 | 0.9241 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,195 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
