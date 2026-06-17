# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1000673 | 0.957048 | 0.944934 | 0.8952 | 0.9969 | -0.039852 | 0.9971 | -0.052166 |
| `package.json` | 5,464 | 0.993649 | 0.995343 | 0.9890 | — | - | — | - |
| `elf` | 47,581 | 0.996835 | 0.997956 | 0.9881 | 0.9887 | +0.008135 | 0.9902 | +0.007756 |
| `rtf` | 884 | 0.985634 | 0.999082 | 0.9879 | — | - | — | - |
| `pkg-info` | 1,599 | 0.997071 | 0.999253 | 0.9895 | — | - | — | - |
| `xls` | 7,596 | 0.984229 | 0.993037 | 0.9727 | — | - | — | - |
| `ole` | 1,675 | 0.987314 | 0.990897 | 0.9848 | — | - | — | - |
| `macho` | 1,965 | 0.969049 | 0.928723 | 0.8604 | — | - | — | - |
| `vbs` | 1,960 | 0.962891 | 0.988650 | 0.9556 | — | - | — | - |
| `tar` | 7,864 | 0.986748 | 0.986552 | 0.9559 | — | - | — | - |
| `lnk` | 698 | 0.867110 | 0.968139 | 0.9075 | — | - | — | - |
| `shell` | 10,525 | 0.977686 | 0.959264 | 0.9271 | — | - | — | - |
| `docx` | 657 | 0.880726 | 0.982928 | 0.9619 | — | - | — | - |
| `powershell` | 1,045 | 0.924636 | 0.966339 | 0.9217 | — | - | — | - |
| `perl` | 5,475 | 0.937595 | 0.785930 | 0.8000 | — | - | — | - |
| `python-bytecode` | 34,432 | 0.914612 | 0.827874 | 0.8742 | — | - | — | - |
| `jar` | 1,022 | 0.908937 | 0.916599 | 0.8643 | — | - | — | - |
| `whl` | 684 | 0.894756 | 0.742446 | 0.6943 | — | - | — | - |
| `pe` | 189,388 | 0.990652 | 0.998779 | 0.9910 | 0.9982 | -0.007548 | 0.9983 | +0.000479 |
| `pdf` | 25,606 | 0.957479 | 0.991664 | 0.9776 | 0.9878 | -0.030321 | 0.9901 | +0.001564 |
| `java_class` | 99,575 | 0.964895 | 0.857740 | 0.8876 | — | - | — | - |
| `kotlin` | 11,252 | 0.896923 | 0.885121 | 0.8275 | — | - | — | - |
| `php` | 21,511 | 0.897567 | 0.745685 | 0.7568 | — | - | — | - |
| `javascript` | 100,913 | 0.965168 | 0.927530 | 0.8825 | — | - | — | - |
| `zip` | 15,218 | 0.746638 | 0.956882 | 0.9277 | — | - | — | - |
| `python` | 32,539 | 0.880170 | 0.775694 | 0.7807 | — | - | — | - |
| `ruby` | 3,538 | 0.785574 | 0.457799 | 0.5641 | — | - | — | - |
| `xlsx` | 8,070 | 0.598911 | 0.987670 | 0.9872 | — | - | — | - |
| `batch` | 22,875 | 0.860359 | 0.994264 | 0.9956 | — | - | — | - |
| `cargo.toml` | 272 | 0.518320 | 0.435395 | 0.5116 | — | - | — | - |
| `csharp` | 10,273 | 0.722192 | 0.338650 | 0.3732 | — | - | — | - |
| `go` | 18,140 | 0.602805 | 0.201643 | 0.1980 | — | - | — | - |
| `deb` | 1,062 | 0.473554 | 0.139560 | 0.1695 | — | - | — | - |
| `xml` | 33,838 | 0.583186 | 0.093035 | 0.1734 | — | - | — | - |
| `plist` | 1,720 | 0.578541 | 0.122561 | 0.1957 | — | - | — | - |
| `png` | 25,183 | 0.520142 | 0.104333 | 0.1295 | — | - | — | - |
| `java` | 10,745 | 0.705748 | 0.168304 | 0.2598 | — | - | — | - |
| `text` | 15,869 | 0.686998 | 0.135116 | 0.1681 | — | - | — | - |
| `rust` | 12,808 | 0.587108 | 0.071056 | 0.1083 | — | - | — | - |
| `gem` | 75 | 0.942901 | 0.946741 | 0.9412 | — | - | — | - |
| `applescript` | 66 | 0.355769 | 0.517093 | 0.5909 | — | - | — | - |
| `json` | 7,948 | 0.699909 | 0.050615 | 0.1252 | — | - | — | - |
| `makefile` | 4,358 | 0.627262 | 0.041990 | 0.1100 | — | - | — | - |
| `c` | 106,930 | 0.675480 | 0.256478 | 0.3336 | — | - | — | - |
| `jpeg` | 4,179 | 0.551841 | 0.203955 | 0.2848 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,413 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
