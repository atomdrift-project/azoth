# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1794413 | 0.966542 | 0.927842 | 0.8955 | 0.9969 | -0.030358 | 0.9971 | -0.069258 |
| `html` | 2,042 | 0.999567 | 0.984983 | 0.9836 | — | - | — | - |
| `rtf` | 925 | 0.993291 | 0.999150 | 0.9903 | — | - | — | - |
| `pkg_info` | 2,984 | 0.997531 | 0.997510 | 0.9802 | — | - | — | - |
| `package.json` | 8,744 | 0.982681 | 0.979707 | 0.9595 | — | - | — | - |
| `ole_doc` | 14,530 | 0.976838 | 0.992532 | 0.9642 | — | - | — | - |
| `gem` | 348 | 0.939816 | 0.945796 | 0.9524 | — | - | — | - |
| `elf` | 90,996 | 0.998027 | 0.996869 | 0.9817 | 0.9887 | +0.009327 | 0.9902 | +0.006669 |
| `macho` | 3,311 | 0.952839 | 0.871301 | 0.8051 | — | - | — | - |
| `vbs` | 2,042 | 0.941435 | 0.983420 | 0.9490 | — | - | — | - |
| `lnk` | 706 | 0.856076 | 0.970522 | 0.9099 | — | - | — | - |
| `powershell` | 1,330 | 0.943876 | 0.963292 | 0.9228 | — | - | — | - |
| `perl` | 8,938 | 0.935521 | 0.752735 | 0.7765 | — | - | — | - |
| `registry` | 26,386 | 0.999549 | 0.892915 | 0.8209 | — | - | — | - |
| `tar` | 11,174 | 0.971103 | 0.963118 | 0.9097 | — | - | — | - |
| `pdf` | 26,108 | 0.976807 | 0.995383 | 0.9802 | 0.9878 | -0.010993 | 0.9901 | +0.005283 |
| `npm` | 1,448 | 0.900914 | 0.913524 | 0.8361 | — | - | — | - |
| `crx` | 611 | 0.902408 | 0.898136 | 0.8466 | — | - | — | - |
| `shell` | 19,458 | 0.965790 | 0.923001 | 0.8789 | — | - | — | - |
| `whl` | 1,348 | 0.898086 | 0.873817 | 0.8042 | — | - | — | - |
| `kotlin` | 13,246 | 0.912285 | 0.890415 | 0.8098 | — | - | — | - |
| `jar` | 3,383 | 0.941272 | 0.877951 | 0.8510 | — | - | — | - |
| `pe` | 194,788 | 0.986132 | 0.998009 | 0.9858 | 0.9982 | -0.012068 | 0.9983 | -0.000291 |
| `python_bytecode` | 102,934 | 0.863402 | 0.701844 | 0.7812 | — | - | — | - |
| `zip` | 16,707 | 0.751899 | 0.939198 | 0.8952 | — | - | — | - |
| `python` | 73,463 | 0.927532 | 0.791343 | 0.7819 | — | - | — | - |
| `javascript` | 185,085 | 0.965485 | 0.910518 | 0.8549 | — | - | — | - |
| `php` | 73,493 | 0.888962 | 0.697495 | 0.7306 | — | - | — | - |
| `ooxml` | 8,910 | 0.544192 | 0.976908 | 0.9800 | — | - | — | - |
| `ruby` | 21,758 | 0.826883 | 0.551525 | 0.6429 | — | - | — | - |
| `java_class` | 210,759 | 0.952307 | 0.789454 | 0.8311 | — | - | — | - |
| `cargo.toml` | 1,032 | 0.727831 | 0.467049 | 0.5634 | — | - | — | - |
| `batch` | 23,097 | 0.774491 | 0.986898 | 0.9910 | — | - | — | - |
| `csharp` | 12,493 | 0.656768 | 0.299156 | 0.3760 | — | - | — | - |
| `dockerfile` | 591 | 0.738869 | 0.172798 | 0.2308 | — | - | — | - |
| `jpeg` | 5,616 | 0.641179 | 0.176650 | 0.2844 | — | - | — | - |
| `deb` | 2,697 | 0.673861 | 0.084339 | 0.1515 | — | - | — | - |
| `c` | 186,507 | 0.650027 | 0.231588 | 0.3160 | — | - | — | - |
| `text` | 36,086 | 0.648690 | 0.088970 | 0.1187 | — | - | — | - |
| `plist` | 12,085 | 0.574017 | 0.042691 | 0.0659 | — | - | — | - |
| `makefile` | 7,565 | 0.471200 | 0.028847 | 0.0488 | — | - | — | - |
| `json` | 27,563 | 0.769448 | 0.090401 | 0.1591 | — | - | — | - |
| `go` | 29,078 | 0.656141 | 0.242991 | 0.2460 | — | - | — | - |
| `rust` | 40,344 | 0.634970 | 0.070772 | 0.1336 | — | - | — | - |
| `java` | 22,165 | 0.672894 | 0.068196 | 0.1178 | — | - | — | - |
| `png` | 49,623 | 0.612985 | 0.087860 | 0.1047 | — | - | — | - |
| `xml` | 46,515 | 0.677748 | 0.127138 | 0.2106 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,308 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
