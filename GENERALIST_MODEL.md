# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1832567 | 0.925630 | 0.899259 | 0.8956 | 0.9969 | -0.071270 | 0.9971 | -0.097841 |
| `html` | 2,043 | 0.972087 | 0.968306 | 0.9836 | — | - | — | - |
| `rtf` | 925 | 0.991363 | 0.998880 | 0.9897 | — | - | — | - |
| `pkg_info` | 2,987 | 0.996547 | 0.996362 | 0.9800 | — | - | — | - |
| `ole_doc` | 14,530 | 0.980129 | 0.993243 | 0.9643 | — | - | — | - |
| `gem` | 347 | 0.945727 | 0.946790 | 0.9529 | — | - | — | - |
| `elf` | 91,850 | 0.997998 | 0.996824 | 0.9818 | 0.9887 | +0.009298 | 0.9902 | +0.006624 |
| `vbs` | 2,042 | 0.952487 | 0.985722 | 0.9457 | — | - | — | - |
| `lnk` | 706 | 0.909685 | 0.970238 | 0.9084 | — | - | — | - |
| `macho` | 3,317 | 0.956900 | 0.872981 | 0.8094 | — | - | — | - |
| `jar` | 3,383 | 0.933736 | 0.873297 | 0.8474 | — | - | — | - |
| `powershell` | 1,331 | 0.948925 | 0.964499 | 0.9215 | — | - | — | - |
| `perl` | 8,965 | 0.953240 | 0.729653 | 0.7805 | — | - | — | - |
| `registry` | 13,696 | 0.998621 | 0.836238 | 0.8154 | — | - | — | - |
| `tar` | 11,164 | 0.971457 | 0.962908 | 0.9125 | — | - | — | - |
| `pdf` | 26,108 | 0.945729 | 0.990390 | 0.9703 | 0.9878 | -0.042071 | 0.9901 | +0.000290 |
| `shell` | 19,499 | 0.966305 | 0.921578 | 0.8751 | — | - | — | - |
| `npm` | 1,351 | 0.898249 | 0.916627 | 0.8364 | — | - | — | - |
| `crx` | 614 | 0.902652 | 0.898383 | 0.8585 | — | - | — | - |
| `whl` | 1,353 | 0.897872 | 0.875121 | 0.8051 | — | - | — | - |
| `kotlin` | 13,230 | 0.791801 | 0.779769 | 0.7595 | — | - | — | - |
| `pe` | 194,802 | 0.985412 | 0.997883 | 0.9871 | 0.9982 | -0.012788 | 0.9983 | -0.000417 |
| `python_bytecode` | 103,053 | 0.860927 | 0.698478 | 0.7785 | — | - | — | - |
| `zip` | 16,712 | 0.737973 | 0.936438 | 0.8928 | — | - | — | - |
| `python` | 73,414 | 0.922745 | 0.789123 | 0.7840 | — | - | — | - |
| `php` | 73,513 | 0.880401 | 0.699015 | 0.7330 | — | - | — | - |
| `ruby` | 21,762 | 0.781677 | 0.548028 | 0.6279 | — | - | — | - |
| `ooxml` | 8,911 | 0.564237 | 0.977918 | 0.9800 | — | - | — | - |
| `javascript` | 185,883 | 0.964106 | 0.909628 | 0.8606 | — | - | — | - |
| `cargo.toml` | 1,036 | 0.776329 | 0.465519 | 0.5634 | — | - | — | - |
| `batch` | 23,097 | 0.890981 | 0.994653 | 0.9935 | — | - | — | - |
| `csharp` | 12,493 | 0.641469 | 0.301876 | 0.3869 | — | - | — | - |
| `dockerfile` | 592 | 0.684621 | 0.172410 | 0.2532 | — | - | — | - |
| `c` | 186,516 | 0.655293 | 0.231686 | 0.3159 | — | - | — | - |
| `deb` | 2,691 | 0.613945 | 0.079982 | 0.1515 | — | - | — | - |
| `go` | 29,083 | 0.635273 | 0.238051 | 0.2467 | — | - | — | - |
| `text` | 36,191 | 0.612321 | 0.087130 | 0.1238 | — | - | — | - |
| `plist` | 12,090 | 0.530140 | 0.041374 | 0.0690 | — | - | — | - |
| `json` | 27,682 | 0.752468 | 0.073061 | 0.1134 | — | - | — | - |
| `rust` | 40,355 | 0.649287 | 0.075504 | 0.1474 | — | - | — | - |
| `makefile` | 7,566 | 0.489024 | 0.026990 | 0.0480 | — | - | — | - |
| `java` | 22,165 | 0.630393 | 0.063586 | 0.1169 | — | - | — | - |
| `java_class` | 210,759 | 0.921484 | 0.790713 | 0.8362 | — | - | — | - |
| `jpeg` | 5,616 | 0.642338 | 0.173357 | 0.2844 | — | - | — | - |
| `package.json` | 8,767 | 0.980219 | 0.978636 | 0.9616 | — | - | — | - |
| `png` | 49,641 | 0.541566 | 0.083065 | 0.1049 | — | - | — | - |
| `xml` | 46,246 | 0.582664 | 0.114688 | 0.2265 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,310 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
