# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2198975 | 0.951417 | 0.904380 | 0.8916 | 0.9969 | -0.045483 | 0.9971 | -0.092720 |
| `rtf` | 931 | 0.980854 | 0.997853 | 0.9848 | — | - | — | - |
| `html` | 10,292 | 0.975365 | 0.969816 | 0.9846 | — | - | — | - |
| `pkg_info` | 3,335 | 0.997104 | 0.996351 | 0.9787 | — | - | — | - |
| `gem` | 1,162 | 0.949435 | 0.944281 | 0.9585 | — | - | — | - |
| `ole_doc` | 14,597 | 0.963683 | 0.989276 | 0.9652 | — | - | — | - |
| `elf` | 125,983 | 0.998205 | 0.996135 | 0.9753 | 0.9887 | +0.009505 | 0.9902 | +0.005935 |
| `lnk` | 723 | 0.862260 | 0.971039 | 0.9134 | — | - | — | - |
| `perl` | 9,846 | 0.938518 | 0.748254 | 0.7895 | — | - | — | - |
| `registry` | 13,731 | 0.998692 | 0.841462 | 0.8154 | — | - | — | - |
| `vbs` | 2,074 | 0.951617 | 0.985342 | 0.9485 | — | - | — | - |
| `package.json` | 10,779 | 0.983206 | 0.975735 | 0.9509 | — | - | — | - |
| `pdf` | 26,195 | 0.962923 | 0.993696 | 0.9737 | 0.9878 | -0.024877 | 0.9901 | +0.003596 |
| `macho` | 4,383 | 0.953749 | 0.863447 | 0.8096 | — | - | — | - |
| `tar` | 12,594 | 0.967669 | 0.953726 | 0.9037 | — | - | — | - |
| `pe` | 199,568 | 0.984801 | 0.997464 | 0.9839 | 0.9982 | -0.013399 | 0.9983 | -0.000836 |
| `shell` | 22,538 | 0.963792 | 0.924603 | 0.8774 | — | - | — | - |
| `npm` | 4,996 | 0.912374 | 0.878433 | 0.8375 | — | - | — | - |
| `python_bytecode` | 127,833 | 0.828255 | 0.656363 | 0.7587 | — | - | — | - |
| `powershell` | 1,433 | 0.951985 | 0.967816 | 0.9362 | — | - | — | - |
| `jar` | 4,177 | 0.950776 | 0.879906 | 0.8414 | — | - | — | - |
| `kotlin` | 14,506 | 0.833311 | 0.799969 | 0.7404 | — | - | — | - |
| `ruby` | 22,219 | 0.796563 | 0.559755 | 0.6500 | — | - | — | - |
| `javascript` | 223,957 | 0.957011 | 0.896046 | 0.8431 | — | - | — | - |
| `whl` | 2,562 | 0.872125 | 0.791625 | 0.7320 | — | - | — | - |
| `python` | 82,952 | 0.903182 | 0.769077 | 0.7802 | — | - | — | - |
| `crx` | 1,062 | 0.931148 | 0.893564 | 0.8227 | — | - | — | - |
| `java_class` | 214,746 | 0.934209 | 0.790621 | 0.8425 | — | - | — | - |
| `php` | 77,481 | 0.900866 | 0.709383 | 0.7292 | — | - | — | - |
| `cargo.toml` | 1,152 | 0.820998 | 0.498577 | 0.5278 | — | - | — | - |
| `zip` | 19,087 | 0.750732 | 0.915077 | 0.8437 | — | - | — | - |
| `ooxml` | 8,918 | 0.785886 | 0.989500 | 0.9798 | — | - | — | - |
| `csharp` | 13,154 | 0.599926 | 0.309237 | 0.3869 | — | - | — | - |
| `batch` | 23,146 | 0.706336 | 0.982865 | 0.9873 | — | - | — | - |
| `jpeg` | 5,784 | 0.574219 | 0.162266 | 0.2832 | — | - | — | - |
| `deb` | 3,461 | 0.470363 | 0.067886 | 0.1515 | — | - | — | - |
| `png` | 67,280 | 0.618220 | 0.084086 | 0.1049 | — | - | — | - |
| `text` | 40,862 | 0.610410 | 0.062492 | 0.0912 | — | - | — | - |
| `java` | 23,169 | 0.573221 | 0.097756 | 0.1541 | — | - | — | - |
| `plist` | 12,639 | 0.700090 | 0.049948 | 0.0706 | — | - | — | - |
| `makefile` | 7,965 | 0.419916 | 0.025981 | 0.0531 | — | - | — | - |
| `xml` | 57,520 | 0.430122 | 0.074826 | 0.1438 | — | - | — | - |
| `go` | 31,484 | 0.572145 | 0.228142 | 0.2689 | — | - | — | - |
| `json` | 31,962 | 0.518979 | 0.060355 | 0.0901 | — | - | — | - |
| `rust` | 41,846 | 0.602175 | 0.069062 | 0.1313 | — | - | — | - |
| `c` | 212,246 | 0.662175 | 0.243486 | 0.3386 | — | - | — | - |
| `7z` | 1,196 | 0.938615 | 0.998514 | 0.9903 | — | - | — | - |
| `apk_android` | 316 | 0.472888 | 0.896054 | 0.9336 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,231 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
