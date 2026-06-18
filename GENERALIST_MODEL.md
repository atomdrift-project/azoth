# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1012990 | 0.952124 | 0.938330 | 0.8959 | 0.9969 | -0.044776 | 0.9971 | -0.058770 |
| `rtf` | 884 | 0.986577 | 0.998968 | 0.9867 | — | - | — | - |
| `package.json` | 5,502 | 0.993666 | 0.995237 | 0.9888 | — | - | — | - |
| `elf` | 47,954 | 0.996102 | 0.997509 | 0.9866 | 0.9887 | +0.007402 | 0.9902 | +0.007309 |
| `pkg-info` | 1,616 | 0.997063 | 0.999227 | 0.9899 | — | - | — | - |
| `gem` | 126 | 0.947032 | 0.933850 | 0.9455 | — | - | — | - |
| `xls` | 7,597 | 0.976502 | 0.989987 | 0.9741 | — | - | — | - |
| `macho` | 1,986 | 0.964569 | 0.919388 | 0.8595 | — | - | — | - |
| `ole` | 1,680 | 0.991398 | 0.992308 | 0.9726 | — | - | — | - |
| `tar` | 7,993 | 0.987393 | 0.986387 | 0.9563 | — | - | — | - |
| `vbs` | 1,960 | 0.965952 | 0.989399 | 0.9551 | — | - | — | - |
| `shell` | 10,704 | 0.978608 | 0.957798 | 0.9275 | — | - | — | - |
| `powershell` | 1,047 | 0.930165 | 0.969122 | 0.9257 | — | - | — | - |
| `docx` | 657 | 0.883112 | 0.983230 | 0.9628 | — | - | — | - |
| `perl` | 5,577 | 0.959456 | 0.772400 | 0.7848 | — | - | — | - |
| `python-bytecode` | 37,798 | 0.900752 | 0.820559 | 0.8721 | — | - | — | - |
| `jar` | 1,157 | 0.913876 | 0.907310 | 0.8500 | — | - | — | - |
| `lnk` | 698 | 0.960549 | 0.989277 | 0.9729 | — | - | — | - |
| `whl` | 711 | 0.867602 | 0.717796 | 0.7018 | — | - | — | - |
| `pe` | 189,691 | 0.986113 | 0.998282 | 0.9890 | 0.9982 | -0.012087 | 0.9983 | -0.000018 |
| `pdf` | 25,607 | 0.956591 | 0.992004 | 0.9775 | 0.9878 | -0.031209 | 0.9901 | +0.001904 |
| `php` | 21,656 | 0.883220 | 0.748416 | 0.7552 | — | - | — | - |
| `javascript` | 101,494 | 0.968416 | 0.935473 | 0.8856 | — | - | — | - |
| `kotlin` | 11,245 | 0.855848 | 0.850134 | 0.7869 | — | - | — | - |
| `zip` | 15,327 | 0.772487 | 0.959671 | 0.9323 | — | - | — | - |
| `ruby` | 3,561 | 0.934321 | 0.461231 | 0.5641 | — | - | — | - |
| `python` | 32,891 | 0.871151 | 0.773040 | 0.7811 | — | - | — | - |
| `xlsx` | 8,071 | 0.724415 | 0.988134 | 0.9872 | — | - | — | - |
| `cargo.toml` | 274 | 0.475820 | 0.427345 | 0.5116 | — | - | — | - |
| `csharp` | 10,272 | 0.731181 | 0.353018 | 0.3814 | — | - | — | - |
| `deb` | 1,077 | 0.531679 | 0.143536 | 0.1695 | — | - | — | - |
| `batch` | 22,881 | 0.870983 | 0.993784 | 0.9955 | — | - | — | - |
| `xml` | 34,054 | 0.518050 | 0.075310 | 0.1385 | — | - | — | - |
| `plist` | 1,724 | 0.630625 | 0.110188 | 0.1597 | — | - | — | - |
| `go` | 18,520 | 0.547896 | 0.198841 | 0.2111 | — | - | — | - |
| `png` | 25,203 | 0.470165 | 0.096434 | 0.1148 | — | - | — | - |
| `text` | 16,316 | 0.617393 | 0.120075 | 0.1560 | — | - | — | - |
| `java` | 11,873 | 0.756694 | 0.160753 | 0.2251 | — | - | — | - |
| `rust` | 12,863 | 0.568989 | 0.070954 | 0.1100 | — | - | — | - |
| `makefile` | 4,468 | 0.544896 | 0.035141 | 0.0751 | — | - | — | - |
| `json` | 8,233 | 0.518358 | 0.023780 | 0.0495 | — | - | — | - |
| `npm` | 200 | 0.793605 | 0.966729 | 0.9319 | — | - | — | - |
| `applescript` | 66 | 0.569231 | 0.627023 | 0.6000 | — | - | — | - |
| `c` | 107,717 | 0.635221 | 0.249575 | 0.3292 | — | - | — | - |
| `java_class` | 102,110 | 0.913481 | 0.850206 | 0.8862 | — | - | — | - |
| `jpeg` | 4,184 | 0.644397 | 0.218713 | 0.2739 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,388 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
