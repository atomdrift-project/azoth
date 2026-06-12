# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 924639 | 0.959871 | 0.949794 | 0.8985 | 0.9969 | -0.037029 | 0.9971 | -0.047306 |
| `pkg-info` | 1,566 | 0.997754 | 0.999475 | 0.9938 | — | - | — | - |
| `batch` | 22,796 | 0.837831 | 0.994142 | 0.9956 | — | - | — | - |
| `rtf` | 846 | 0.993024 | 0.999243 | 0.9924 | — | - | — | - |
| `package.json` | 5,190 | 0.994107 | 0.995724 | 0.9898 | — | - | — | - |
| `elf` | 45,162 | 0.996758 | 0.998039 | 0.9896 | 0.9887 | +0.008058 | 0.9902 | +0.007839 |
| `ole` | 1,612 | 0.989821 | 0.990091 | 0.9640 | — | - | — | - |
| `xls` | 7,349 | 0.971812 | 0.988308 | 0.9733 | — | - | — | - |
| `pdf` | 25,478 | 0.966533 | 0.993737 | 0.9780 | 0.9878 | -0.021267 | 0.9901 | +0.003637 |
| `macho` | 1,911 | 0.969983 | 0.932903 | 0.8590 | — | - | — | - |
| `tar` | 6,202 | 0.982001 | 0.985800 | 0.9543 | — | - | — | - |
| `docx` | 628 | 0.876277 | 0.982369 | 0.9603 | — | - | — | - |
| `vbs` | 1,885 | 0.958033 | 0.986683 | 0.9539 | — | - | — | - |
| `lnk` | 679 | 0.904680 | 0.968057 | 0.9087 | — | - | — | - |
| `shell` | 10,032 | 0.979311 | 0.962156 | 0.9252 | — | - | — | - |
| `powershell` | 989 | 0.937072 | 0.972230 | 0.9325 | — | - | — | - |
| `python-bytecode` | 24,722 | 0.940205 | 0.866776 | 0.9017 | — | - | — | - |
| `jar` | 948 | 0.915895 | 0.933967 | 0.8795 | — | - | — | - |
| `perl` | 5,369 | 0.939379 | 0.789736 | 0.8108 | — | - | — | - |
| `whl` | 138 | 0.833274 | 0.675090 | 0.5946 | — | - | — | - |
| `pe` | 185,185 | 0.989509 | 0.998702 | 0.9908 | 0.9982 | -0.008691 | 0.9983 | +0.000402 |
| `php` | 20,248 | 0.919481 | 0.755324 | 0.7474 | — | - | — | - |
| `javascript` | 95,969 | 0.967487 | 0.941339 | 0.8985 | — | - | — | - |
| `java_class` | 98,512 | 0.971668 | 0.866450 | 0.8967 | — | - | — | - |
| `kotlin` | 10,856 | 0.853500 | 0.859181 | 0.8036 | — | - | — | - |
| `xlsx` | 7,701 | 0.741788 | 0.988691 | 0.9868 | — | - | — | - |
| `zip` | 14,265 | 0.767573 | 0.969475 | 0.9458 | — | - | — | - |
| `python` | 30,003 | 0.893660 | 0.789961 | 0.7878 | — | - | — | - |
| `cargo.toml` | 201 | 0.484930 | 0.428889 | 0.4865 | — | - | — | - |
| `csharp` | 10,100 | 0.780186 | 0.367862 | 0.3933 | — | - | — | - |
| `jpeg` | 4,025 | 0.565159 | 0.206342 | 0.2819 | — | - | — | - |
| `json` | 6,518 | 0.625927 | 0.029217 | 0.0615 | — | - | — | - |
| `plist` | 1,705 | 0.520419 | 0.100623 | 0.1273 | — | - | — | - |
| `deb` | 1,016 | 0.498578 | 0.149013 | 0.1786 | — | - | — | - |
| `java` | 10,266 | 0.657566 | 0.150007 | 0.2249 | — | - | — | - |
| `c` | 99,883 | 0.694846 | 0.253314 | 0.3278 | — | - | — | - |
| `xml` | 28,871 | 0.651742 | 0.109797 | 0.1863 | — | - | — | - |
| `text` | 13,814 | 0.592590 | 0.122078 | 0.1267 | — | - | — | - |
| `go` | 17,411 | 0.612422 | 0.209881 | 0.2176 | — | - | — | - |
| `rust` | 12,130 | 0.643409 | 0.077220 | 0.0957 | — | - | — | - |
| `png` | 23,822 | 0.476210 | 0.106908 | 0.1410 | — | - | — | - |
| `makefile` | 4,084 | 0.623938 | 0.047285 | 0.0958 | — | - | — | - |
| `applescript` | 62 | 0.410256 | 0.535906 | 0.5909 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,519 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
