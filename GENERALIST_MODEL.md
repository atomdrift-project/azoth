# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2484155 | 0.943374 | 0.895644 | 0.8820 | 0.9969 | -0.053526 | 0.9971 | -0.101456 |
| `ico` | 116 | 0.923147 | 0.890195 | 0.8788 | — | - | — | - |
| `rtf` | 925 | 0.995969 | 0.999465 | 0.9944 | — | - | — | - |
| `gem` | 14,023 | 0.977433 | 0.941692 | 0.9639 | — | - | — | - |
| `ole_doc` | 15,174 | 0.974156 | 0.991365 | 0.9570 | — | - | — | - |
| `html` | 34,582 | 0.990777 | 0.895616 | 0.9412 | — | - | — | - |
| `python_sdist` | 1,419 | 0.911371 | 0.917679 | 0.9118 | — | - | — | - |
| `elf` | 136,777 | 0.997173 | 0.994391 | 0.9786 | 0.9887 | +0.008473 | 0.9902 | +0.004191 |
| `package.json` | 12,254 | 0.965944 | 0.958963 | 0.9454 | — | - | — | - |
| `lnk` | 732 | 0.872096 | 0.971567 | 0.9138 | — | - | — | - |
| `pdf` | 26,248 | 0.862541 | 0.977804 | 0.9396 | 0.9878 | -0.125259 | 0.9901 | -0.012296 |
| `registry` | 13,740 | 0.997370 | 0.831472 | 0.7970 | — | - | — | - |
| `perl` | 10,117 | 0.923893 | 0.737370 | 0.7609 | — | - | — | - |
| `npm` | 27,367 | 0.941865 | 0.919920 | 0.8992 | — | - | — | - |
| `python_bytecode` | 149,777 | 0.806303 | 0.662906 | 0.7602 | — | - | — | - |
| `macho` | 5,057 | 0.956732 | 0.890480 | 0.8616 | — | - | — | - |
| `python` | 87,027 | 0.923023 | 0.804792 | 0.7971 | — | - | — | - |
| `tar` | 12,831 | 0.963871 | 0.929411 | 0.8733 | — | - | — | - |
| `shell` | 23,059 | 0.964045 | 0.913332 | 0.8594 | — | - | — | - |
| `kotlin` | 14,010 | 0.772877 | 0.722735 | 0.7269 | — | - | — | - |
| `pe` | 236,796 | 0.955651 | 0.993160 | 0.9698 | 0.9982 | -0.042549 | 0.9983 | -0.005140 |
| `jar` | 5,616 | 0.980048 | 0.918166 | 0.8605 | — | - | — | - |
| `pkg_info` | 2,288 | 0.926371 | 0.766360 | 0.7778 | — | - | — | - |
| `powershell` | 1,485 | 0.954380 | 0.964376 | 0.9293 | — | - | — | - |
| `zip` | 24,842 | 0.753914 | 0.872595 | 0.8113 | — | - | — | - |
| `php` | 78,654 | 0.906292 | 0.714235 | 0.7209 | — | - | — | - |
| `ruby` | 24,106 | 0.987989 | 0.718159 | 0.7188 | — | - | — | - |
| `vsix` | 685 | 0.807364 | 0.510405 | 0.5672 | — | - | — | - |
| `vbs` | 2,332 | 0.939759 | 0.982478 | 0.9374 | — | - | — | - |
| `crx` | 1,212 | 0.963189 | 0.898437 | 0.8401 | — | - | — | - |
| `ooxml` | 9,151 | 0.800815 | 0.978498 | 0.9533 | — | - | — | - |
| `javascript` | 243,405 | 0.926591 | 0.828083 | 0.7905 | — | - | — | - |
| `json` | 33,900 | 0.692513 | 0.414678 | 0.5532 | — | - | — | - |
| `apk_android` | 582 | 0.785546 | 0.947269 | 0.9063 | — | - | — | - |
| `static-lib` | 1,538 | 0.683237 | 0.351075 | 0.3862 | — | - | — | - |
| `csharp` | 13,322 | 0.639896 | 0.302010 | 0.3691 | — | - | — | - |
| `deb` | 3,466 | 0.593771 | 0.162969 | 0.2581 | — | - | — | - |
| `batch` | 23,387 | 0.665568 | 0.975161 | 0.9854 | — | - | — | - |
| `whl` | 6,419 | 0.932585 | 0.616854 | 0.5705 | — | - | — | - |
| `rust` | 43,919 | 0.830943 | 0.262241 | 0.3294 | — | - | — | - |
| `jpeg` | 5,838 | 0.621929 | 0.165353 | 0.2562 | — | - | — | - |
| `c` | 222,149 | 0.653126 | 0.246184 | 0.3398 | — | - | — | - |
| `go` | 32,320 | 0.627175 | 0.316572 | 0.3513 | — | - | — | - |
| `java_class` | 228,128 | 0.926953 | 0.713461 | 0.7527 | — | - | — | - |
| `png` | 69,040 | 0.590671 | 0.085497 | 0.1008 | — | - | — | - |
| `text` | 42,481 | 0.665385 | 0.095718 | 0.1323 | — | - | — | - |
| `java` | 25,361 | 0.601795 | 0.075342 | 0.1208 | — | - | — | - |
| `gif` | 276 | 0.291500 | 0.277650 | 0.4709 | — | - | — | - |
| `xml` | 58,241 | 0.456762 | 0.149400 | 0.2928 | — | - | — | - |
| `7z` | 1,166 | 0.918228 | 0.996544 | 0.9816 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (6,391 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
