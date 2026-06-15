# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 987410 | 0.959490 | 0.946671 | 0.8979 | 0.9969 | -0.037410 | 0.9971 | -0.050429 |
| `rtf` | 884 | 0.985634 | 0.999082 | 0.9879 | — | - | — | - |
| `package.json` | 5,464 | 0.993649 | 0.995343 | 0.9890 | — | - | — | - |
| `elf` | 47,581 | 0.996835 | 0.997956 | 0.9881 | 0.9887 | +0.008135 | 0.9902 | +0.007756 |
| `pkg-info` | 1,599 | 0.997071 | 0.999253 | 0.9895 | — | - | — | - |
| `xls` | 7,596 | 0.984229 | 0.993037 | 0.9727 | — | - | — | - |
| `macho` | 1,965 | 0.969049 | 0.928723 | 0.8604 | — | - | — | - |
| `ole` | 1,675 | 0.987314 | 0.990897 | 0.9848 | — | - | — | - |
| `tar` | 7,866 | 0.986565 | 0.986364 | 0.9556 | — | - | — | - |
| `vbs` | 1,960 | 0.962891 | 0.988650 | 0.9556 | — | - | — | - |
| `lnk` | 698 | 0.867110 | 0.968139 | 0.9075 | — | - | — | - |
| `shell` | 10,525 | 0.977686 | 0.959264 | 0.9271 | — | - | — | - |
| `perl` | 5,475 | 0.937595 | 0.785930 | 0.8000 | — | - | — | - |
| `docx` | 657 | 0.880726 | 0.982928 | 0.9619 | — | - | — | - |
| `python-bytecode` | 34,432 | 0.914612 | 0.827874 | 0.8742 | — | - | — | - |
| `powershell` | 1,045 | 0.924636 | 0.966339 | 0.9217 | — | - | — | - |
| `jar` | 1,022 | 0.908937 | 0.916599 | 0.8643 | — | - | — | - |
| `whl` | 680 | 0.913319 | 0.758667 | 0.7059 | — | - | — | - |
| `pdf` | 25,606 | 0.957479 | 0.991664 | 0.9776 | 0.9878 | -0.030321 | 0.9901 | +0.001564 |
| `java_class` | 99,575 | 0.964895 | 0.857740 | 0.8876 | — | - | — | - |
| `pe` | 189,387 | 0.990657 | 0.998780 | 0.9910 | 0.9982 | -0.007543 | 0.9983 | +0.000480 |
| `javascript` | 100,680 | 0.969629 | 0.935886 | 0.8892 | — | - | — | - |
| `php` | 21,511 | 0.897567 | 0.745685 | 0.7568 | — | - | — | - |
| `batch` | 22,875 | 0.860359 | 0.994264 | 0.9956 | — | - | — | - |
| `kotlin` | 11,262 | 0.896654 | 0.884815 | 0.8267 | — | - | — | - |
| `zip` | 15,230 | 0.746417 | 0.956754 | 0.9275 | — | - | — | - |
| `ruby` | 3,538 | 0.785574 | 0.457799 | 0.5641 | — | - | — | - |
| `python` | 32,539 | 0.880170 | 0.775694 | 0.7807 | — | - | — | - |
| `xlsx` | 8,069 | 0.598865 | 0.987667 | 0.9872 | — | - | — | - |
| `cargo.toml` | 272 | 0.518320 | 0.435395 | 0.5116 | — | - | — | - |
| `csharp` | 10,272 | 0.721660 | 0.338422 | 0.3720 | — | - | — | - |
| `c` | 106,930 | 0.675480 | 0.256478 | 0.3336 | — | - | — | - |
| `jpeg` | 4,179 | 0.551841 | 0.203955 | 0.2848 | — | - | — | - |
| `deb` | 1,062 | 0.473554 | 0.139560 | 0.1695 | — | - | — | - |
| `go` | 18,140 | 0.602805 | 0.201643 | 0.1980 | — | - | — | - |
| `plist` | 1,720 | 0.578541 | 0.122561 | 0.1957 | — | - | — | - |
| `java` | 10,745 | 0.705748 | 0.168304 | 0.2598 | — | - | — | - |
| `rust` | 12,808 | 0.587108 | 0.071056 | 0.1083 | — | - | — | - |
| `png` | 25,183 | 0.520142 | 0.104333 | 0.1295 | — | - | — | - |
| `xml` | 33,838 | 0.583186 | 0.093035 | 0.1734 | — | - | — | - |
| `text` | 15,869 | 0.686998 | 0.135116 | 0.1681 | — | - | — | - |
| `makefile` | 4,358 | 0.627262 | 0.041990 | 0.1100 | — | - | — | - |
| `gem` | 75 | 0.942901 | 0.946741 | 0.9412 | — | - | — | - |
| `applescript` | 66 | 0.355769 | 0.517093 | 0.5909 | — | - | — | - |
| `json` | 7,948 | 0.699909 | 0.050615 | 0.1252 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (7,705 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
