# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1608866 | 0.921373 | 0.816267 | 0.8405 | 0.9969 | -0.075527 | 0.9971 | -0.180833 |
| `html` | 2,024 | 1.000000 | 1.000000 | 1.0000 | — | - | — | - |
| `rtf` | 885 | 0.984567 | 0.998876 | 0.9860 | — | - | — | - |
| `pkg_info` | 1,748 | 0.997451 | 0.999011 | 0.9871 | — | - | — | - |
| `package.json` | 5,891 | 0.993930 | 0.994883 | 0.9840 | — | - | — | - |
| `registry` | 4,202 | 0.997490 | 0.771163 | 0.7304 | — | - | — | - |
| `gem` | 199 | 0.958270 | 0.963545 | 0.9577 | — | - | — | - |
| `macho` | 2,140 | 0.957641 | 0.903879 | 0.8404 | — | - | — | - |
| `elf` | 59,215 | 0.997131 | 0.997350 | 0.9835 | 0.9887 | +0.008431 | 0.9902 | +0.007150 |
| `tar` | 8,809 | 0.985732 | 0.982373 | 0.9470 | — | - | — | - |
| `ole_doc` | 14,106 | 0.978449 | 0.993221 | 0.9644 | — | - | — | - |
| `npm` | 419 | 0.861254 | 0.931080 | 0.8594 | — | - | — | - |
| `vbs` | 1,987 | 0.954442 | 0.986959 | 0.9518 | — | - | — | - |
| `jar` | 1,640 | 0.928539 | 0.894627 | 0.8550 | — | - | — | - |
| `whl` | 991 | 0.910057 | 0.899861 | 0.8462 | — | - | — | - |
| `shell` | 11,649 | 0.973953 | 0.952748 | 0.9222 | — | - | — | - |
| `powershell` | 1,050 | 0.922795 | 0.967479 | 0.9174 | — | - | — | - |
| `perl` | 5,734 | 0.937517 | 0.797828 | 0.8205 | — | - | — | - |
| `pe` | 191,146 | 0.986255 | 0.998254 | 0.9881 | 0.9982 | -0.011945 | 0.9983 | -0.000046 |
| `pdf` | 25,619 | 0.956014 | 0.991519 | 0.9743 | 0.9878 | -0.031786 | 0.9901 | +0.001419 |
| `lnk` | 699 | 0.906626 | 0.969680 | 0.9041 | — | - | — | - |
| `java_class` | 104,711 | 0.954161 | 0.831099 | 0.8629 | — | - | — | - |
| `python_bytecode` | 56,791 | 0.884652 | 0.774532 | 0.8384 | — | - | — | - |
| `php` | 22,791 | 0.865610 | 0.733434 | 0.7386 | — | - | — | - |
| `kotlin` | 10,816 | 0.891490 | 0.896425 | 0.8399 | — | - | — | - |
| `javascript` | 108,797 | 0.969776 | 0.934794 | 0.8824 | — | - | — | - |
| `python` | 36,140 | 0.916801 | 0.816281 | 0.8079 | — | - | — | - |
| `zip` | 15,070 | 0.728691 | 0.954675 | 0.9256 | — | - | — | - |
| `ooxml` | 8,836 | 0.725040 | 0.985366 | 0.9830 | — | - | — | - |
| `ruby` | 4,795 | 0.614743 | 0.356606 | 0.4242 | — | - | — | - |
| `csharp` | 10,285 | 0.647329 | 0.333066 | 0.3910 | — | - | — | - |
| `jpeg` | 4,302 | 0.654881 | 0.190633 | 0.2679 | — | - | — | - |
| `deb` | 1,519 | 0.420881 | 0.142700 | 0.2083 | — | - | — | - |
| `batch` | 22,888 | 0.766067 | 0.989137 | 0.9940 | — | - | — | - |
| `go` | 20,064 | 0.629170 | 0.204821 | 0.2261 | — | - | — | - |
| `text` | 19,418 | 0.493624 | 0.085134 | 0.1095 | — | - | — | - |
| `png` | 25,622 | 0.488023 | 0.093675 | 0.1030 | — | - | — | - |
| `java` | 16,330 | 0.663923 | 0.083575 | 0.1282 | — | - | — | - |
| `xml` | 31,621 | 0.404157 | 0.087591 | 0.1589 | — | - | — | - |
| `plist` | 1,761 | 0.450620 | 0.078464 | 0.1017 | — | - | — | - |
| `rust` | 12,979 | 0.574291 | 0.073756 | 0.1006 | — | - | — | - |
| `makefile` | 4,687 | 0.453806 | 0.039551 | 0.0899 | — | - | — | - |
| `json` | 11,054 | 0.605984 | 0.033787 | 0.0503 | — | - | — | - |
| `crx` | 227 | 0.989052 | 0.998352 | 0.9925 | — | - | — | - |
| `c` | 111,548 | 0.671785 | 0.248283 | 0.3248 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (229 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
