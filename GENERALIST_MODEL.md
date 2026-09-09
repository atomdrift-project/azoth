# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2285526 | 0.934096 | 0.889691 | 0.8908 | 0.9969 | -0.062804 | 0.9971 | -0.107409 |
| `rtf` | 939 | 0.986374 | 0.998281 | 0.9867 | — | - | — | - |
| `html` | 23,317 | 0.989361 | 0.969819 | 0.9846 | — | - | — | - |
| `ole_doc` | 14,664 | 0.975145 | 0.992033 | 0.9651 | — | - | — | - |
| `elf` | 131,738 | 0.998175 | 0.996144 | 0.9774 | 0.9887 | +0.009475 | 0.9902 | +0.005944 |
| `lnk` | 723 | 0.862188 | 0.970846 | 0.9166 | — | - | — | - |
| `package.json` | 11,568 | 0.978451 | 0.973996 | 0.9522 | — | - | — | - |
| `vbs` | 2,093 | 0.959352 | 0.987283 | 0.9446 | — | - | — | - |
| `perl` | 9,893 | 0.939593 | 0.739167 | 0.7733 | — | - | — | - |
| `registry` | 13,731 | 0.998632 | 0.841748 | 0.8154 | — | - | — | - |
| `npm` | 14,662 | 0.951746 | 0.929189 | 0.8993 | — | - | — | - |
| `tar` | 13,282 | 0.967384 | 0.953750 | 0.9048 | — | - | — | - |
| `macho` | 4,711 | 0.959523 | 0.874135 | 0.8112 | — | - | — | - |
| `pkg_info` | 2,225 | 0.935804 | 0.842006 | 0.8387 | — | - | — | - |
| `pdf` | 26,213 | 0.906126 | 0.984378 | 0.9551 | 0.9878 | -0.081674 | 0.9901 | -0.005722 |
| `pe` | 201,602 | 0.985326 | 0.997420 | 0.9840 | 0.9982 | -0.012874 | 0.9983 | -0.000880 |
| `python_sdist` | 331 | 0.847000 | 0.855990 | 0.7981 | — | - | — | - |
| `jar` | 4,869 | 0.945295 | 0.864828 | 0.8338 | — | - | — | - |
| `powershell` | 1,444 | 0.952089 | 0.965872 | 0.9326 | — | - | — | - |
| `kotlin` | 14,548 | 0.805291 | 0.775018 | 0.7472 | — | - | — | - |
| `shell` | 23,083 | 0.962691 | 0.917881 | 0.8731 | — | - | — | - |
| `java_class` | 220,965 | 0.931427 | 0.792726 | 0.8523 | — | - | — | - |
| `crx` | 1,066 | 0.940271 | 0.904634 | 0.8193 | — | - | — | - |
| `python` | 85,287 | 0.904740 | 0.768938 | 0.7832 | — | - | — | - |
| `whl` | 3,023 | 0.873552 | 0.780063 | 0.7215 | — | - | — | - |
| `javascript` | 232,498 | 0.958005 | 0.898233 | 0.8437 | — | - | — | - |
| `python_bytecode` | 133,396 | 0.820707 | 0.644141 | 0.7510 | — | - | — | - |
| `gem` | 6,094 | 0.501466 | 0.444174 | 0.5850 | — | - | — | - |
| `zip` | 20,385 | 0.743279 | 0.901680 | 0.8158 | — | - | — | - |
| `php` | 77,792 | 0.859644 | 0.671509 | 0.7072 | — | - | — | - |
| `cargo.toml` | 1,197 | 0.745214 | 0.472082 | 0.5294 | — | - | — | - |
| `ooxml` | 9,274 | 0.816297 | 0.982927 | 0.9606 | — | - | — | - |
| `csharp` | 13,267 | 0.677897 | 0.322555 | 0.3864 | — | - | — | - |
| `batch` | 23,177 | 0.418986 | 0.968659 | 0.9829 | — | - | — | - |
| `c` | 216,272 | 0.683467 | 0.244263 | 0.3388 | — | - | — | - |
| `ruby` | 22,810 | 0.796468 | 0.533853 | 0.6429 | — | - | — | - |
| `deb` | 3,539 | 0.401731 | 0.055529 | 0.1481 | — | - | — | - |
| `jpeg` | 5,803 | 0.628004 | 0.161180 | 0.2374 | — | - | — | - |
| `java` | 24,577 | 0.492380 | 0.089422 | 0.1426 | — | - | — | - |
| `png` | 67,844 | 0.663597 | 0.089657 | 0.1016 | — | - | — | - |
| `text` | 41,686 | 0.644656 | 0.060979 | 0.0800 | — | - | — | - |
| `xml` | 58,129 | 0.488476 | 0.081693 | 0.1474 | — | - | — | - |
| `plist` | 12,659 | 0.637374 | 0.043745 | 0.0700 | — | - | — | - |
| `json` | 32,421 | 0.497123 | 0.057076 | 0.0939 | — | - | — | - |
| `makefile` | 7,975 | 0.481845 | 0.025539 | 0.0441 | — | - | — | - |
| `go` | 31,723 | 0.562329 | 0.224073 | 0.2486 | — | - | — | - |
| `rust` | 42,497 | 0.639804 | 0.070474 | 0.1227 | — | - | — | - |
| `7z` | 1,205 | 0.932361 | 0.998014 | 0.9869 | — | - | — | - |
| `apk_android` | 319 | 0.472263 | 0.894536 | 0.9241 | — | - | — | - |
| `yaml` | 1,237 | 0.466908 | 0.080032 | 0.1391 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,194 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
