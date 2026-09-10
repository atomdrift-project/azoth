# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2301703 | 0.940725 | 0.892387 | 0.8901 | 0.9969 | -0.056175 | 0.9971 | -0.104713 |
| `rtf` | 940 | 0.988009 | 0.998470 | 0.9879 | — | - | — | - |
| `html` | 24,574 | 0.989634 | 0.969816 | 0.9846 | — | - | — | - |
| `ole_doc` | 14,664 | 0.968643 | 0.990235 | 0.9650 | — | - | — | - |
| `elf` | 132,478 | 0.998101 | 0.995858 | 0.9753 | 0.9887 | +0.009401 | 0.9902 | +0.005658 |
| `lnk` | 724 | 0.861384 | 0.970832 | 0.9159 | — | - | — | - |
| `package.json` | 11,674 | 0.979191 | 0.974191 | 0.9511 | — | - | — | - |
| `perl` | 9,898 | 0.941615 | 0.727321 | 0.7692 | — | - | — | - |
| `registry` | 13,731 | 0.998657 | 0.850572 | 0.8154 | — | - | — | - |
| `vbs` | 2,095 | 0.952337 | 0.985900 | 0.9457 | — | - | — | - |
| `python_sdist` | 423 | 0.850500 | 0.843205 | 0.7900 | — | - | — | - |
| `npm` | 15,566 | 0.952171 | 0.928318 | 0.8977 | — | - | — | - |
| `xml` | 58,193 | 0.555415 | 0.083253 | 0.1462 | — | - | — | - |
| `macho` | 4,747 | 0.956442 | 0.855345 | 0.8079 | — | - | — | - |
| `pkg_info` | 2,232 | 0.951442 | 0.833627 | 0.8070 | — | - | — | - |
| `tar` | 13,357 | 0.968364 | 0.954841 | 0.9094 | — | - | — | - |
| `pdf` | 26,218 | 0.954701 | 0.991320 | 0.9703 | 0.9878 | -0.033099 | 0.9901 | +0.001220 |
| `shell` | 23,116 | 0.963095 | 0.920101 | 0.8736 | — | - | — | - |
| `pe` | 201,927 | 0.984998 | 0.997327 | 0.9836 | 0.9982 | -0.013202 | 0.9983 | -0.000973 |
| `kotlin` | 14,536 | 0.846912 | 0.796466 | 0.7474 | — | - | — | - |
| `python_bytecode` | 135,112 | 0.823421 | 0.644749 | 0.7519 | — | - | — | - |
| `php` | 77,927 | 0.872269 | 0.669975 | 0.7066 | — | - | — | - |
| `jar` | 4,926 | 0.949995 | 0.868725 | 0.8340 | — | - | — | - |
| `python` | 85,600 | 0.899017 | 0.767569 | 0.7840 | — | - | — | - |
| `whl` | 3,530 | 0.878200 | 0.771162 | 0.7235 | — | - | — | - |
| `javascript` | 234,127 | 0.956575 | 0.895214 | 0.8414 | — | - | — | - |
| `powershell` | 1,460 | 0.949434 | 0.962339 | 0.9293 | — | - | — | - |
| `crx` | 1,065 | 0.935158 | 0.895482 | 0.8122 | — | - | — | - |
| `gem` | 7,527 | 0.489750 | 0.438056 | 0.5850 | — | - | — | - |
| `zip` | 21,094 | 0.737815 | 0.893473 | 0.7975 | — | - | — | - |
| `cargo.toml` | 1,230 | 0.768678 | 0.494185 | 0.5287 | — | - | — | - |
| `java_class` | 221,159 | 0.945501 | 0.788502 | 0.8381 | — | - | — | - |
| `ooxml` | 9,274 | 0.783206 | 0.979182 | 0.9620 | — | - | — | - |
| `csharp` | 13,269 | 0.682204 | 0.321401 | 0.3855 | — | - | — | - |
| `batch` | 23,179 | 0.399979 | 0.961176 | 0.9794 | — | - | — | - |
| `c` | 216,591 | 0.708093 | 0.244887 | 0.3399 | — | - | — | - |
| `ruby` | 22,899 | 0.798190 | 0.547730 | 0.6341 | — | - | — | - |
| `jpeg` | 5,804 | 0.629748 | 0.164600 | 0.2284 | — | - | — | - |
| `deb` | 3,541 | 0.414212 | 0.075001 | 0.1538 | — | - | — | - |
| `json` | 32,502 | 0.469834 | 0.055103 | 0.0939 | — | - | — | - |
| `png` | 67,904 | 0.551406 | 0.079074 | 0.1070 | — | - | — | - |
| `java` | 24,579 | 0.432290 | 0.084372 | 0.1423 | — | - | — | - |
| `plist` | 12,661 | 0.639800 | 0.044203 | 0.0690 | — | - | — | - |
| `text` | 41,803 | 0.582329 | 0.056400 | 0.0772 | — | - | — | - |
| `makefile` | 7,980 | 0.495524 | 0.025828 | 0.0469 | — | - | — | - |
| `go` | 31,745 | 0.568006 | 0.220091 | 0.2485 | — | - | — | - |
| `rust` | 42,832 | 0.635614 | 0.069268 | 0.1214 | — | - | — | - |
| `yaml` | 1,585 | 0.364533 | 0.063736 | 0.1301 | — | - | — | - |
| `7z` | 1,208 | 0.928245 | 0.997681 | 0.9857 | — | - | — | - |
| `apk_android` | 319 | 0.458394 | 0.889512 | 0.9241 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,177 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
