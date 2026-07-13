# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1719221 | 0.961617 | 0.923851 | 0.8953 | 0.9969 | -0.035283 | 0.9971 | -0.073249 |
| `html` | 2,041 | 0.999888 | 0.994058 | 0.9836 | — | - | — | - |
| `rtf` | 925 | 0.992162 | 0.998843 | 0.9897 | — | - | — | - |
| `pkg_info` | 2,925 | 0.997303 | 0.997103 | 0.9808 | — | - | — | - |
| `package.json` | 8,489 | 0.977326 | 0.978451 | 0.9622 | — | - | — | - |
| `ole_doc` | 14,508 | 0.969899 | 0.990481 | 0.9644 | — | - | — | - |
| `gem` | 344 | 0.942516 | 0.946465 | 0.9529 | — | - | — | - |
| `elf` | 82,412 | 0.997732 | 0.996775 | 0.9815 | 0.9887 | +0.009032 | 0.9902 | +0.006575 |
| `vbs` | 2,029 | 0.942914 | 0.983945 | 0.9486 | — | - | — | - |
| `macho` | 3,102 | 0.954916 | 0.876681 | 0.8127 | — | - | — | - |
| `lnk` | 701 | 0.876931 | 0.970140 | 0.9057 | — | - | — | - |
| `powershell` | 1,320 | 0.938130 | 0.960838 | 0.9190 | — | - | — | - |
| `registry` | 15,819 | 0.999086 | 0.871529 | 0.8209 | — | - | — | - |
| `perl` | 8,684 | 0.930381 | 0.747354 | 0.7805 | — | - | — | - |
| `pdf` | 26,092 | 0.967271 | 0.992842 | 0.9746 | 0.9878 | -0.020529 | 0.9901 | +0.002742 |
| `crx` | 584 | 0.900444 | 0.891400 | 0.8511 | — | - | — | - |
| `tar` | 10,979 | 0.969808 | 0.960860 | 0.9102 | — | - | — | - |
| `shell` | 18,953 | 0.967179 | 0.923207 | 0.8781 | — | - | — | - |
| `npm` | 1,203 | 0.882985 | 0.903229 | 0.8140 | — | - | — | - |
| `whl` | 1,246 | 0.896908 | 0.875533 | 0.8029 | — | - | — | - |
| `pe` | 193,760 | 0.985522 | 0.997977 | 0.9858 | 0.9982 | -0.012678 | 0.9983 | -0.000323 |
| `python_bytecode` | 95,772 | 0.870250 | 0.697216 | 0.7822 | — | - | — | - |
| `kotlin` | 13,081 | 0.887817 | 0.869107 | 0.7867 | — | - | — | - |
| `python` | 70,451 | 0.924818 | 0.795645 | 0.7852 | — | - | — | - |
| `zip` | 16,570 | 0.751335 | 0.940606 | 0.8946 | — | - | — | - |
| `php` | 70,763 | 0.876575 | 0.688749 | 0.7222 | — | - | — | - |
| `ruby` | 21,433 | 0.839352 | 0.580248 | 0.6341 | — | - | — | - |
| `ooxml` | 8,910 | 0.668012 | 0.980033 | 0.9807 | — | - | — | - |
| `jar` | 2,869 | 0.946874 | 0.883759 | 0.8458 | — | - | — | - |
| `cargo.toml` | 968 | 0.716699 | 0.469180 | 0.5634 | — | - | — | - |
| `csharp` | 12,476 | 0.641541 | 0.302013 | 0.3758 | — | - | — | - |
| `jpeg` | 5,594 | 0.621124 | 0.177823 | 0.2756 | — | - | — | - |
| `dockerfile` | 579 | 0.775018 | 0.201291 | 0.2667 | — | - | — | - |
| `deb` | 2,519 | 0.573715 | 0.094586 | 0.1515 | — | - | — | - |
| `xml` | 47,282 | 0.586387 | 0.095767 | 0.1649 | — | - | — | - |
| `text` | 35,089 | 0.617808 | 0.090030 | 0.1357 | — | - | — | - |
| `go` | 28,825 | 0.583710 | 0.222667 | 0.2492 | — | - | — | - |
| `rust` | 40,195 | 0.577305 | 0.068617 | 0.1216 | — | - | — | - |
| `java` | 21,943 | 0.668630 | 0.065868 | 0.1176 | — | - | — | - |
| `makefile` | 7,530 | 0.382391 | 0.028243 | 0.0573 | — | - | — | - |
| `batch` | 23,092 | 0.787566 | 0.989941 | 0.9919 | — | - | — | - |
| `c` | 172,924 | 0.655830 | 0.227739 | 0.3154 | — | - | — | - |
| `java_class` | 207,214 | 0.937378 | 0.789129 | 0.8247 | — | - | — | - |
| `javascript` | 179,250 | 0.964721 | 0.910747 | 0.8560 | — | - | — | - |
| `json` | 26,307 | 0.768760 | 0.085965 | 0.1306 | — | - | — | - |
| `plist` | 12,062 | 0.597784 | 0.042616 | 0.0667 | — | - | — | - |
| `png` | 49,357 | 0.603197 | 0.086367 | 0.1067 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,307 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
