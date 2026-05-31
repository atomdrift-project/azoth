# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 808366 | 0.983707 | 0.977178 | 0.9487 | 0.9969 | -0.013193 | 0.9971 | -0.019922 |
| `rtf` | 719 | 0.992720 | 0.999467 | 0.9933 | — | - | — | - |
| `batch` | 22,513 | 0.922093 | 0.996383 | 0.9975 | — | - | — | - |
| `python-bytecode` | 9,489 | 0.985899 | 0.980088 | 0.9835 | — | - | — | - |
| `xls` | 6,562 | 0.987013 | 0.993741 | 0.9762 | — | - | — | - |
| `ole` | 1,400 | 0.992640 | 0.992813 | 0.9717 | — | - | — | - |
| `package.json` | 4,277 | 0.997270 | 0.998267 | 0.9932 | — | - | — | - |
| `elf` | 40,196 | 0.998609 | 0.998545 | 0.9815 | 0.9887 | +0.009909 | 0.9902 | +0.008345 |
| `docx` | 539 | 0.874627 | 0.981019 | 0.9485 | — | - | — | - |
| `lnk` | 616 | 0.932919 | 0.976839 | 0.9393 | — | - | — | - |
| `shell` | 8,342 | 0.988615 | 0.970984 | 0.9213 | — | - | — | - |
| `perl` | 4,205 | 0.996626 | 0.857787 | 0.8571 | — | - | — | - |
| `pkg-info` | 1,446 | 0.996502 | 0.999525 | 0.9942 | — | - | — | - |
| `java_class` | 83,356 | 0.937128 | 0.898371 | 0.9184 | — | - | — | - |
| `html` | 3,250 | 0.818847 | 0.594888 | 0.7179 | — | - | — | - |
| `macho` | 1,772 | 0.922476 | 0.860746 | 0.8470 | — | - | — | - |
| `jar` | 804 | 0.953474 | 0.951742 | 0.8995 | — | - | — | - |
| `javascript` | 82,183 | 0.984588 | 0.957876 | 0.9007 | — | - | — | - |
| `php` | 15,327 | 0.957877 | 0.853899 | 0.8151 | — | - | — | - |
| `xlsx` | 6,443 | 0.503906 | 0.984661 | 0.9871 | — | - | — | - |
| `vbs` | 1,631 | 0.971300 | 0.989150 | 0.9711 | — | - | — | - |
| `python` | 22,527 | 0.933093 | 0.861521 | 0.8506 | — | - | — | - |
| `kotlin` | 10,201 | 0.974319 | 0.969280 | 0.9154 | — | - | — | - |
| `powershell` | 858 | 0.968012 | 0.982001 | 0.9481 | — | - | — | - |
| `pe` | 172,990 | 0.985887 | 0.997973 | 0.9892 | 0.9982 | -0.012313 | 0.9983 | -0.000327 |
| `csharp` | 8,353 | 0.805290 | 0.421667 | 0.4818 | — | - | — | - |
| `xml` | 22,537 | 0.738954 | 0.157524 | 0.2447 | — | - | — | - |
| `text` | 8,875 | 0.823061 | 0.255453 | 0.3128 | — | - | — | - |
| `go` | 14,492 | 0.930140 | 0.562434 | 0.6253 | — | - | — | - |
| `deb` | 887 | 0.872837 | 0.281712 | 0.3628 | — | - | — | - |
| `pdf` | 25,137 | 0.974439 | 0.995123 | 0.9860 | 0.9878 | -0.013361 | 0.9901 | +0.005023 |
| `c` | 75,069 | 0.688495 | 0.258273 | 0.3395 | — | - | — | - |
| `jpeg` | 3,432 | 0.546218 | 0.226446 | 0.2879 | — | - | — | - |
| `rust` | 10,505 | 0.569699 | 0.062845 | 0.0966 | — | - | — | - |
| `plist` | 1,642 | 0.563341 | 0.131869 | 0.1760 | — | - | — | - |
| `png` | 19,369 | 0.630178 | 0.131814 | 0.1702 | — | - | — | - |
| `makefile` | 2,972 | 0.449571 | 0.026736 | 0.0588 | — | - | — | - |
| `json` | 3,957 | 0.507817 | 0.023920 | 0.0467 | — | - | — | - |
| `markdown` | 7,548 | 0.544573 | 0.114937 | 0.1961 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0, reg_lambda=1, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (73,750 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
