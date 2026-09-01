# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2187006 | 0.959605 | 0.909103 | 0.8943 | 0.9969 | -0.037295 | 0.9971 | -0.087997 |
| `rtf` | 929 | 0.989311 | 0.998705 | 0.9897 | — | - | — | - |
| `html` | 8,508 | 0.967750 | 0.967859 | 0.9836 | — | - | — | - |
| `pkg_info` | 3,379 | 0.997563 | 0.996811 | 0.9812 | — | - | — | - |
| `gem` | 484 | 0.947521 | 0.945957 | 0.9574 | — | - | — | - |
| `ole_doc` | 14,590 | 0.969056 | 0.990596 | 0.9658 | — | - | — | - |
| `elf` | 122,255 | 0.998131 | 0.996259 | 0.9773 | 0.9887 | +0.009431 | 0.9902 | +0.006059 |
| `package.json` | 10,331 | 0.979290 | 0.976991 | 0.9624 | — | - | — | - |
| `lnk` | 716 | 0.857763 | 0.969743 | 0.9108 | — | - | — | - |
| `perl` | 9,572 | 0.943146 | 0.736550 | 0.7949 | — | - | — | - |
| `registry` | 13,731 | 0.998919 | 0.875846 | 0.8154 | — | - | — | - |
| `macho` | 4,275 | 0.955376 | 0.865451 | 0.8152 | — | - | — | - |
| `vbs` | 2,066 | 0.945709 | 0.984651 | 0.9456 | — | - | — | - |
| `tar` | 12,263 | 0.970678 | 0.958985 | 0.9075 | — | - | — | - |
| `npm` | 1,711 | 0.885827 | 0.908273 | 0.8311 | — | - | — | - |
| `pdf` | 26,189 | 0.962411 | 0.993394 | 0.9736 | 0.9878 | -0.025389 | 0.9901 | +0.003294 |
| `pe` | 198,342 | 0.985509 | 0.997661 | 0.9861 | 0.9982 | -0.012691 | 0.9983 | -0.000639 |
| `jar` | 4,090 | 0.951067 | 0.880184 | 0.8486 | — | - | — | - |
| `kotlin` | 14,451 | 0.832545 | 0.812034 | 0.7766 | — | - | — | - |
| `ruby` | 22,198 | 0.823478 | 0.553000 | 0.6190 | — | - | — | - |
| `python_bytecode` | 126,803 | 0.850890 | 0.679785 | 0.7769 | — | - | — | - |
| `shell` | 22,187 | 0.964534 | 0.922523 | 0.8800 | — | - | — | - |
| `javascript` | 219,505 | 0.966383 | 0.905999 | 0.8540 | — | - | — | - |
| `whl` | 2,196 | 0.877576 | 0.818662 | 0.7578 | — | - | — | - |
| `powershell` | 1,402 | 0.945409 | 0.965721 | 0.9317 | — | - | — | - |
| `java_class` | 214,653 | 0.937658 | 0.799069 | 0.8512 | — | - | — | - |
| `python` | 82,121 | 0.911263 | 0.777134 | 0.7839 | — | - | — | - |
| `crx` | 1,000 | 0.912652 | 0.872755 | 0.8243 | — | - | — | - |
| `php` | 77,260 | 0.909854 | 0.705356 | 0.7275 | — | - | — | - |
| `cargo.toml` | 1,121 | 0.686620 | 0.450773 | 0.5217 | — | - | — | - |
| `ooxml` | 8,916 | 0.744244 | 0.986387 | 0.9809 | — | - | — | - |
| `zip` | 18,015 | 0.740650 | 0.920680 | 0.8599 | — | - | — | - |
| `csharp` | 12,928 | 0.637174 | 0.312530 | 0.3910 | — | - | — | - |
| `batch` | 23,143 | 0.796930 | 0.986093 | 0.9925 | — | - | — | - |
| `jpeg` | 5,759 | 0.649221 | 0.188708 | 0.2768 | — | - | — | - |
| `deb` | 3,361 | 0.466895 | 0.112444 | 0.1587 | — | - | — | - |
| `c` | 211,283 | 0.643127 | 0.226006 | 0.3195 | — | - | — | - |
| `dockerfile` | 605 | 0.560069 | 0.136083 | 0.2041 | — | - | — | - |
| `png` | 65,656 | 0.589410 | 0.085198 | 0.1132 | — | - | — | - |
| `go` | 30,721 | 0.593911 | 0.226531 | 0.2443 | — | - | — | - |
| `json` | 31,372 | 0.701082 | 0.063441 | 0.0841 | — | - | — | - |
| `plist` | 12,601 | 0.664785 | 0.040442 | 0.0667 | — | - | — | - |
| `xml` | 56,527 | 0.552215 | 0.114444 | 0.2383 | — | - | — | - |
| `java` | 23,126 | 0.484989 | 0.089342 | 0.1519 | — | - | — | - |
| `makefile` | 7,936 | 0.488286 | 0.025519 | 0.0585 | — | - | — | - |
| `text` | 40,395 | 0.624779 | 0.060819 | 0.0906 | — | - | — | - |
| `rust` | 41,681 | 0.637181 | 0.067246 | 0.1358 | — | - | — | - |
| `7z` | 1,194 | 0.941715 | 0.998587 | 0.9894 | — | - | — | - |
| `apk_android` | 316 | 0.466154 | 0.893606 | 0.9336 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,232 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
