# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2001402 | 0.956447 | 0.918202 | 0.8948 | 0.9969 | -0.040453 | 0.9971 | -0.078898 |
| `rtf` | 926 | 0.990569 | 0.998821 | 0.9891 | — | - | — | - |
| `html` | 7,437 | 0.995692 | 0.968722 | 0.9836 | — | - | — | - |
| `ole_doc` | 14,567 | 0.969829 | 0.990509 | 0.9641 | — | - | — | - |
| `elf` | 111,276 | 0.998208 | 0.996563 | 0.9795 | 0.9887 | +0.009508 | 0.9902 | +0.006363 |
| `gem` | 373 | 0.941320 | 0.946757 | 0.9551 | — | - | — | - |
| `perl` | 9,439 | 0.944844 | 0.742770 | 0.7848 | — | - | — | - |
| `powershell` | 1,354 | 0.946494 | 0.965088 | 0.9279 | — | - | — | - |
| `macho` | 3,668 | 0.944914 | 0.852085 | 0.8066 | — | - | — | - |
| `vbs` | 2,054 | 0.940455 | 0.983176 | 0.9440 | — | - | — | - |
| `pkg_info` | 3,292 | 0.997366 | 0.996617 | 0.9800 | — | - | — | - |
| `registry` | 13,731 | 0.998709 | 0.838507 | 0.8154 | — | - | — | - |
| `lnk` | 711 | 0.859762 | 0.970745 | 0.9101 | — | - | — | - |
| `pe` | 195,474 | 0.983895 | 0.997594 | 0.9853 | 0.9982 | -0.014305 | 0.9983 | -0.000706 |
| `npm` | 1,444 | 0.890663 | 0.913244 | 0.8374 | — | - | — | - |
| `python_bytecode` | 107,995 | 0.868309 | 0.688815 | 0.7759 | — | - | — | - |
| `shell` | 21,386 | 0.963724 | 0.916271 | 0.8628 | — | - | — | - |
| `whl` | 1,539 | 0.889989 | 0.857311 | 0.7835 | — | - | — | - |
| `javascript` | 191,236 | 0.964099 | 0.905447 | 0.8519 | — | - | — | - |
| `python` | 77,714 | 0.922665 | 0.783042 | 0.7794 | — | - | — | - |
| `php` | 75,338 | 0.891639 | 0.705788 | 0.7399 | — | - | — | - |
| `kotlin` | 14,351 | 0.817663 | 0.803609 | 0.7766 | — | - | — | - |
| `tar` | 11,646 | 0.969697 | 0.959301 | 0.9069 | — | - | — | - |
| `cargo.toml` | 1,051 | 0.770639 | 0.498530 | 0.5352 | — | - | — | - |
| `zip` | 17,004 | 0.747389 | 0.934059 | 0.8857 | — | - | — | - |
| `ooxml` | 8,913 | 0.543870 | 0.976998 | 0.9800 | — | - | — | - |
| `jar` | 3,682 | 0.942598 | 0.875926 | 0.8431 | — | - | — | - |
| `csharp` | 12,501 | 0.688829 | 0.320441 | 0.3876 | — | - | — | - |
| `pdf` | 26,164 | 0.969342 | 0.993956 | 0.9745 | 0.9878 | -0.018458 | 0.9901 | +0.003856 |
| `batch` | 23,126 | 0.845231 | 0.988465 | 0.9940 | — | - | — | - |
| `ruby` | 21,967 | 0.834657 | 0.546807 | 0.6429 | — | - | — | - |
| `dockerfile` | 606 | 0.667805 | 0.165331 | 0.2308 | — | - | — | - |
| `java` | 22,512 | 0.565390 | 0.091586 | 0.1487 | — | - | — | - |
| `text` | 38,632 | 0.615890 | 0.082077 | 0.1205 | — | - | — | - |
| `json` | 28,970 | 0.754084 | 0.076581 | 0.1453 | — | - | — | - |
| `plist` | 12,355 | 0.625049 | 0.042187 | 0.0645 | — | - | — | - |
| `crx` | 704 | 0.892772 | 0.884258 | 0.8257 | — | - | — | - |
| `rust` | 40,494 | 0.604677 | 0.070047 | 0.1386 | — | - | — | - |
| `deb` | 3,141 | 0.636242 | 0.078418 | 0.1519 | — | - | — | - |
| `go` | 29,384 | 0.594470 | 0.228548 | 0.2390 | — | - | — | - |
| `makefile` | 7,861 | 0.415397 | 0.024001 | 0.0560 | — | - | — | - |
| `apk_android` | 297 | 0.465543 | 0.921066 | 0.9468 | — | - | — | - |
| `c` | 205,783 | 0.678782 | 0.230750 | 0.3161 | — | - | — | - |
| `java_class` | 213,071 | 0.954759 | 0.799256 | 0.8500 | — | - | — | - |
| `jpeg` | 5,698 | 0.641569 | 0.184579 | 0.2844 | — | - | — | - |
| `package.json` | 9,013 | 0.977248 | 0.977727 | 0.9623 | — | - | — | - |
| `png` | 62,695 | 0.544142 | 0.082058 | 0.1078 | — | - | — | - |
| `xml` | 54,816 | 0.621027 | 0.115995 | 0.1971 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,276 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
