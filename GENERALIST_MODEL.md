# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2659751 | 0.950146 | 0.914286 | 0.3716 | 0.9969 | -0.046754 | 0.9971 | -0.082814 |
| `rtf` | 937 | 0.998843 | 0.999843 | 0.3551 | — | - | — | - |
| `kotlin` | 13,635 | 0.966433 | 0.900081 | 0.0012 | — | - | — | - |
| `pdf` | 26,258 | 0.938208 | 0.989809 | 0.0000 | 0.9878 | -0.049592 | 0.9901 | -0.000291 |
| `batch` | 23,483 | 0.655363 | 0.968585 | 0.0002 | — | - | — | - |
| `vbs` | 2,420 | 0.945528 | 0.986203 | 0.0117 | — | - | — | - |
| `elf` | 138,640 | 0.999170 | 0.998836 | 0.8140 | 0.9887 | +0.010470 | 0.9902 | +0.008636 |
| `ole_doc` | 15,213 | 0.974841 | 0.992286 | 0.5393 | — | - | — | - |
| `apk_android` | 638 | 0.836046 | 0.953025 | 0.0000 | — | - | — | - |
| `html` | 65,862 | 0.995774 | 0.994294 | 0.0000 | — | - | — | - |
| `python_sdist` | 1,948 | 0.927635 | 0.935093 | 0.0733 | — | - | — | - |
| `lnk` | 731 | 0.957100 | 0.987724 | 0.0206 | — | - | — | - |
| `7z` | 1,174 | 0.960285 | 0.998183 | 0.5700 | — | - | — | - |
| `ooxml` | 9,282 | 0.565330 | 0.943758 | 0.0129 | — | - | — | - |
| `static-lib` | 1,812 | 0.888246 | 0.636021 | 0.0000 | — | - | — | - |
| `jar` | 5,737 | 0.994956 | 0.966647 | 0.0285 | — | - | — | - |
| `gem` | 14,983 | 0.966208 | 0.914566 | 0.0000 | — | - | — | - |
| `registry` | 13,739 | 0.999584 | 0.953665 | 0.0000 | — | - | — | - |
| `shell` | 24,178 | 0.992313 | 0.981761 | 0.0234 | — | - | — | - |
| `macho` | 5,130 | 0.990785 | 0.941347 | 0.0000 | — | - | — | - |
| `perl` | 10,244 | 0.987562 | 0.876953 | 0.0000 | — | - | — | - |
| `json` | 39,146 | 0.944818 | 0.536232 | 0.0000 | — | - | — | - |
| `php` | 79,318 | 0.965162 | 0.911544 | 0.1320 | — | - | — | - |
| `pe` | 239,683 | 0.991478 | 0.998668 | 0.4502 | 0.9982 | -0.006722 | 0.9983 | +0.000368 |
| `zip` | 31,661 | 0.882874 | 0.927668 | 0.2749 | — | - | — | - |
| `java_class` | 229,526 | 0.973567 | 0.881325 | 0.0000 | — | - | — | - |
| `ico` | 135 | 0.939330 | 0.889852 | 0.0000 | — | - | — | - |
| `vsix` | 822 | 0.983762 | 0.901857 | 0.0000 | — | - | — | - |
| `javascript` | 245,789 | 0.939934 | 0.918969 | 0.0122 | — | - | — | - |
| `ruby` | 24,764 | 0.999530 | 0.926405 | 0.0000 | — | - | — | - |
| `powershell` | 1,584 | 0.980626 | 0.985799 | 0.0620 | — | - | — | - |
| `crx` | 1,963 | 0.983873 | 0.921003 | 0.0000 | — | - | — | - |
| `python_bytecode` | 154,704 | 0.929596 | 0.763398 | 0.0000 | — | - | — | - |
| `java` | 25,622 | 0.499389 | 0.214726 | 0.0000 | — | - | — | - |
| `npm` | 49,589 | 0.977605 | 0.937559 | 0.3077 | — | - | — | - |
| `go` | 33,228 | 0.703190 | 0.532304 | 0.0000 | — | - | — | - |
| `tar` | 15,403 | 0.988239 | 0.952565 | 0.0524 | — | - | — | - |
| `python` | 87,892 | 0.945702 | 0.883515 | 0.0031 | — | - | — | - |
| `package.json` | 12,347 | 0.992919 | 0.991720 | 0.0007 | — | - | — | - |
| `pkg_info` | 2,348 | 0.944809 | 0.841962 | 0.0000 | — | - | — | - |
| `whl` | 9,160 | 0.980936 | 0.801918 | 0.0000 | — | - | — | - |
| `png` | 69,443 | 0.938502 | 0.303569 | 0.0000 | — | - | — | - |
| `xml` | 55,779 | 0.958244 | 0.374257 | 0.0000 | — | - | — | - |
| `gif` | 319 | 0.764447 | 0.492660 | 0.0000 | — | - | — | - |
| `csharp` | 13,333 | 0.803799 | 0.471429 | 0.0000 | — | - | — | - |
| `c` | 223,957 | 0.793290 | 0.499274 | 0.0019 | — | - | — | - |
| `rust` | 45,765 | 0.859320 | 0.374001 | 0.0000 | — | - | — | - |
| `jpeg` | 5,847 | 0.770515 | 0.234485 | 0.0000 | — | - | — | - |
| `text` | 64,422 | 0.680517 | 0.167883 | 0.0000 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (128,071 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
