# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2129518 | 0.961545 | 0.918573 | 0.8946 | 0.9969 | -0.035355 | 0.9971 | -0.078527 |
| `rtf` | 929 | 0.985824 | 0.998346 | 0.9891 | — | - | — | - |
| `html` | 7,997 | 0.996032 | 0.968731 | 0.9836 | — | - | — | - |
| `gem` | 397 | 0.942071 | 0.944806 | 0.9492 | — | - | — | - |
| `ole_doc` | 14,569 | 0.965576 | 0.989498 | 0.9638 | — | - | — | - |
| `elf` | 114,221 | 0.998312 | 0.996634 | 0.9801 | 0.9887 | +0.009612 | 0.9902 | +0.006434 |
| `package.json` | 9,062 | 0.982768 | 0.979894 | 0.9610 | — | - | — | - |
| `vbs` | 2,056 | 0.943052 | 0.983365 | 0.9452 | — | - | — | - |
| `lnk` | 713 | 0.912453 | 0.971781 | 0.9096 | — | - | — | - |
| `registry` | 13,731 | 0.998641 | 0.817115 | 0.8154 | — | - | — | - |
| `pdf` | 26,168 | 0.882481 | 0.981111 | 0.9498 | 0.9878 | -0.105319 | 0.9901 | -0.008989 |
| `tar` | 11,786 | 0.969830 | 0.959638 | 0.9079 | — | - | — | - |
| `macho` | 3,833 | 0.953682 | 0.866672 | 0.8105 | — | - | — | - |
| `perl` | 9,472 | 0.959660 | 0.723957 | 0.7632 | — | - | — | - |
| `npm` | 1,489 | 0.895609 | 0.914438 | 0.8417 | — | - | — | - |
| `pe` | 196,004 | 0.984821 | 0.997700 | 0.9862 | 0.9982 | -0.013379 | 0.9983 | -0.000600 |
| `powershell` | 1,365 | 0.946187 | 0.964484 | 0.9289 | — | - | — | - |
| `shell` | 21,548 | 0.966794 | 0.917063 | 0.8592 | — | - | — | - |
| `kotlin` | 14,390 | 0.786884 | 0.778889 | 0.7512 | — | - | — | - |
| `python` | 79,201 | 0.928045 | 0.786113 | 0.7810 | — | - | — | - |
| `whl` | 1,663 | 0.885509 | 0.841992 | 0.7652 | — | - | — | - |
| `jar` | 3,704 | 0.937976 | 0.871497 | 0.8421 | — | - | — | - |
| `pkg_info` | 3,297 | 0.997437 | 0.996796 | 0.9808 | — | - | — | - |
| `javascript` | 198,851 | 0.967514 | 0.908723 | 0.8494 | — | - | — | - |
| `crx` | 781 | 0.899835 | 0.873327 | 0.8241 | — | - | — | - |
| `php` | 75,412 | 0.885744 | 0.694017 | 0.7270 | — | - | — | - |
| `python_bytecode` | 111,637 | 0.858390 | 0.692207 | 0.7765 | — | - | — | - |
| `ruby` | 21,974 | 0.821277 | 0.551549 | 0.6429 | — | - | — | - |
| `cargo.toml` | 1,083 | 0.763814 | 0.488792 | 0.5217 | — | - | — | - |
| `ooxml` | 8,913 | 0.579834 | 0.979069 | 0.9808 | — | - | — | - |
| `java_class` | 213,227 | 0.947675 | 0.795525 | 0.8398 | — | - | — | - |
| `zip` | 17,240 | 0.754447 | 0.933047 | 0.8771 | — | - | — | - |
| `csharp` | 12,501 | 0.627763 | 0.307327 | 0.3863 | — | - | — | - |
| `batch` | 23,124 | 0.847639 | 0.991447 | 0.9931 | — | - | — | - |
| `jpeg` | 5,731 | 0.567542 | 0.167124 | 0.2715 | — | - | — | - |
| `deb` | 3,166 | 0.602300 | 0.073470 | 0.1667 | — | - | — | - |
| `c` | 208,289 | 0.638389 | 0.225559 | 0.3144 | — | - | — | - |
| `dockerfile` | 610 | 0.651453 | 0.152991 | 0.2353 | — | - | — | - |
| `java` | 22,696 | 0.722295 | 0.104797 | 0.1507 | — | - | — | - |
| `json` | 29,153 | 0.722261 | 0.059301 | 0.0817 | — | - | — | - |
| `go` | 29,327 | 0.622627 | 0.228549 | 0.2467 | — | - | — | - |
| `xml` | 55,216 | 0.553480 | 0.112510 | 0.2354 | — | - | — | - |
| `text` | 39,284 | 0.580105 | 0.075501 | 0.1157 | — | - | — | - |
| `plist` | 12,382 | 0.659612 | 0.043770 | 0.0659 | — | - | — | - |
| `png` | 63,793 | 0.669976 | 0.092570 | 0.1139 | — | - | — | - |
| `rust` | 40,705 | 0.652842 | 0.073163 | 0.1385 | — | - | — | - |
| `makefile` | 7,902 | 0.363063 | 0.024593 | 0.0506 | — | - | — | - |
| `apk_android` | 297 | 0.425343 | 0.914693 | 0.9468 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,245 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
