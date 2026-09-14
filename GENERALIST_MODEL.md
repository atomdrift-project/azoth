# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2422030 | 0.936510 | 0.892661 | 0.8852 | 0.9969 | -0.060390 | 0.9971 | -0.104439 |
| `rtf` | 940 | 0.985237 | 0.998127 | 0.9848 | — | - | — | - |
| `html` | 32,814 | 0.989257 | 0.969783 | 0.9846 | — | - | — | - |
| `ole_doc` | 15,156 | 0.963128 | 0.989039 | 0.9590 | — | - | — | - |
| `elf` | 136,222 | 0.997923 | 0.995620 | 0.9762 | 0.9887 | +0.009223 | 0.9902 | +0.005420 |
| `lnk` | 729 | 0.857440 | 0.969938 | 0.9159 | — | - | — | - |
| `package.json` | 12,190 | 0.980055 | 0.974228 | 0.9556 | — | - | — | - |
| `python_sdist` | 1,119 | 0.870375 | 0.769105 | 0.7429 | — | - | — | - |
| `registry` | 13,731 | 0.998738 | 0.859955 | 0.8154 | — | - | — | - |
| `pdf` | 26,275 | 0.958202 | 0.992315 | 0.9721 | 0.9878 | -0.029598 | 0.9901 | +0.002215 |
| `macho` | 5,034 | 0.954234 | 0.860216 | 0.8037 | — | - | — | - |
| `tar` | 13,751 | 0.966859 | 0.951104 | 0.9009 | — | - | — | - |
| `npm` | 21,919 | 0.957341 | 0.926706 | 0.8943 | — | - | — | - |
| `vbs` | 2,236 | 0.949351 | 0.986937 | 0.9469 | — | - | — | - |
| `pkg_info` | 2,250 | 0.952463 | 0.830151 | 0.7931 | — | - | — | - |
| `perl` | 10,049 | 0.882893 | 0.607329 | 0.6804 | — | - | — | - |
| `pe` | 235,884 | 0.965936 | 0.994764 | 0.9745 | 0.9982 | -0.032264 | 0.9983 | -0.003536 |
| `python_bytecode` | 148,373 | 0.804827 | 0.636014 | 0.7506 | — | - | — | - |
| `kotlin` | 14,486 | 0.881154 | 0.818463 | 0.7418 | — | - | — | - |
| `jar` | 5,563 | 0.946100 | 0.861798 | 0.8240 | — | - | — | - |
| `shell` | 23,444 | 0.960778 | 0.918230 | 0.8764 | — | - | — | - |
| `powershell` | 1,467 | 0.946551 | 0.962324 | 0.9331 | — | - | — | - |
| `crx` | 1,067 | 0.944497 | 0.909457 | 0.8243 | — | - | — | - |
| `javascript` | 241,177 | 0.953633 | 0.892587 | 0.8409 | — | - | — | - |
| `php` | 78,287 | 0.885504 | 0.678256 | 0.7100 | — | - | — | - |
| `java_class` | 226,226 | 0.932476 | 0.757310 | 0.8125 | — | - | — | - |
| `gem` | 14,009 | 0.464397 | 0.428764 | 0.5808 | — | - | — | - |
| `apk_android` | 336 | 0.450563 | 0.872061 | 0.9173 | — | - | — | - |
| `python` | 86,755 | 0.893063 | 0.763857 | 0.7807 | — | - | — | - |
| `whl` | 6,012 | 0.890778 | 0.722539 | 0.6917 | — | - | — | - |
| `ruby` | 23,186 | 0.809423 | 0.558454 | 0.6250 | — | - | — | - |
| `cargo.toml` | 1,269 | 0.762445 | 0.478293 | 0.5278 | — | - | — | - |
| `zip` | 22,007 | 0.746760 | 0.887806 | 0.7865 | — | - | — | - |
| `ooxml` | 9,274 | 0.773991 | 0.979266 | 0.9606 | — | - | — | - |
| `csharp` | 13,313 | 0.670585 | 0.317564 | 0.3922 | — | - | — | - |
| `static-lib` | 1,576 | 0.723626 | 0.362574 | 0.4597 | — | - | — | - |
| `batch` | 23,364 | 0.415126 | 0.957910 | 0.9810 | — | - | — | - |
| `rust` | 43,153 | 0.622457 | 0.069907 | 0.1214 | — | - | — | - |
| `c` | 220,944 | 0.644711 | 0.234012 | 0.3324 | — | - | — | - |
| `jpeg` | 5,810 | 0.619085 | 0.149901 | 0.2573 | — | - | — | - |
| `deb` | 3,533 | 0.449933 | 0.070576 | 0.1653 | — | - | — | - |
| `png` | 68,488 | 0.621432 | 0.088903 | 0.1072 | — | - | — | - |
| `java` | 25,368 | 0.411887 | 0.082496 | 0.1467 | — | - | — | - |
| `json` | 32,874 | 0.693100 | 0.074081 | 0.1038 | — | - | — | - |
| `plist` | 12,674 | 0.617007 | 0.049034 | 0.0721 | — | - | — | - |
| `go` | 31,939 | 0.584171 | 0.248532 | 0.2651 | — | - | — | - |
| `makefile` | 8,038 | 0.312673 | 0.024236 | 0.0588 | — | - | — | - |
| `xml` | 58,275 | 0.532223 | 0.082198 | 0.1448 | — | - | — | - |
| `yaml` | 2,164 | 0.466883 | 0.066005 | 0.1186 | — | - | — | - |
| `text` | 42,256 | 0.622200 | 0.057128 | 0.0764 | — | - | — | - |
| `7z` | 1,213 | 0.914983 | 0.996952 | 0.9841 | — | - | — | - |
| `font` | 102 | 0.641818 | 0.399622 | 0.5672 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,164 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
