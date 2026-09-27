# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2470304 | 0.921161 | 0.882781 | 0.8757 | 0.9969 | -0.075739 | 0.9971 | -0.114319 |
| `ico` | 114 | 0.923494 | 0.898993 | 0.8889 | — | - | — | - |
| `rtf` | 925 | 0.996194 | 0.999488 | 0.9950 | — | - | — | - |
| `gem` | 13,995 | 0.976252 | 0.945637 | 0.9639 | — | - | — | - |
| `ole_doc` | 15,173 | 0.962593 | 0.988551 | 0.9570 | — | - | — | - |
| `html` | 34,562 | 0.991491 | 0.894686 | 0.9412 | — | - | — | - |
| `python_sdist` | 1,391 | 0.910369 | 0.916913 | 0.9022 | — | - | — | - |
| `elf` | 136,774 | 0.997010 | 0.994234 | 0.9772 | 0.9887 | +0.008310 | 0.9902 | +0.004034 |
| `lnk` | 732 | 0.861909 | 0.970338 | 0.9130 | — | - | — | - |
| `perl` | 10,114 | 0.943546 | 0.751096 | 0.7952 | — | - | — | - |
| `pe` | 236,785 | 0.953386 | 0.992749 | 0.9673 | 0.9982 | -0.044814 | 0.9983 | -0.005551 |
| `package.json` | 12,254 | 0.966494 | 0.959436 | 0.9487 | — | - | — | - |
| `registry` | 13,740 | 0.981234 | 0.820381 | 0.7970 | — | - | — | - |
| `pdf` | 26,248 | 0.948930 | 0.991317 | 0.9704 | 0.9878 | -0.038870 | 0.9901 | +0.001217 |
| `macho` | 5,051 | 0.956700 | 0.884408 | 0.8443 | — | - | — | - |
| `npm` | 27,036 | 0.941201 | 0.918830 | 0.8997 | — | - | — | - |
| `python_bytecode` | 149,777 | 0.849556 | 0.665544 | 0.7609 | — | - | — | - |
| `ruby` | 23,994 | 0.974354 | 0.718082 | 0.7213 | — | - | — | - |
| `python` | 87,012 | 0.910371 | 0.801348 | 0.7961 | — | - | — | - |
| `tar` | 12,745 | 0.964065 | 0.927346 | 0.8657 | — | - | — | - |
| `pkg_info` | 2,287 | 0.955904 | 0.765731 | 0.7843 | — | - | — | - |
| `shell` | 23,086 | 0.964672 | 0.913930 | 0.8666 | — | - | — | - |
| `kotlin` | 13,942 | 0.854960 | 0.797024 | 0.7264 | — | - | — | - |
| `php` | 78,645 | 0.914348 | 0.716281 | 0.7200 | — | - | — | - |
| `java_class` | 228,128 | 0.932043 | 0.711410 | 0.7472 | — | - | — | - |
| `powershell` | 1,475 | 0.952840 | 0.959256 | 0.9272 | — | - | — | - |
| `vbs` | 2,265 | 0.932231 | 0.980567 | 0.9395 | — | - | — | - |
| `jar` | 5,599 | 0.981120 | 0.912596 | 0.8507 | — | - | — | - |
| `zip` | 24,558 | 0.762089 | 0.875829 | 0.8117 | — | - | — | - |
| `vsix` | 665 | 0.803320 | 0.506238 | 0.5753 | — | - | — | - |
| `json` | 33,870 | 0.630031 | 0.404745 | 0.5333 | — | - | — | - |
| `javascript` | 243,085 | 0.910719 | 0.823738 | 0.7956 | — | - | — | - |
| `ooxml` | 9,151 | 0.770117 | 0.974172 | 0.9534 | — | - | — | - |
| `apk_android` | 582 | 0.755255 | 0.939951 | 0.9053 | — | - | — | - |
| `crx` | 1,095 | 0.953530 | 0.889353 | 0.8257 | — | - | — | - |
| `static-lib` | 1,537 | 0.728651 | 0.364128 | 0.3919 | — | - | — | - |
| `whl` | 6,201 | 0.935095 | 0.620216 | 0.5766 | — | - | — | - |
| `csharp` | 13,322 | 0.640290 | 0.294574 | 0.3695 | — | - | — | - |
| `batch` | 23,366 | 0.314894 | 0.953063 | 0.9766 | — | - | — | - |
| `go` | 32,298 | 0.613973 | 0.316785 | 0.3518 | — | - | — | - |
| `deb` | 3,478 | 0.508370 | 0.110371 | 0.1951 | — | - | — | - |
| `jpeg` | 5,838 | 0.631959 | 0.171912 | 0.2363 | — | - | — | - |
| `c` | 221,828 | 0.606223 | 0.244983 | 0.3443 | — | - | — | - |
| `png` | 69,040 | 0.591417 | 0.087648 | 0.1010 | — | - | — | - |
| `xml` | 58,205 | 0.465643 | 0.148621 | 0.2857 | — | - | — | - |
| `text` | 42,523 | 0.612781 | 0.089368 | 0.1315 | — | - | — | - |
| `rust` | 43,854 | 0.834179 | 0.268007 | 0.3590 | — | - | — | - |
| `java` | 25,361 | 0.451856 | 0.071613 | 0.1227 | — | - | — | - |
| `7z` | 1,167 | 0.914758 | 0.996493 | 0.9825 | — | - | — | - |
| `gif` | 269 | 0.260710 | 0.256953 | 0.4802 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (6,388 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
