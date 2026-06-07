# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 860189 | 0.953839 | 0.946171 | 0.9011 | 0.9969 | -0.043061 | 0.9971 | -0.050929 |
| `rtf` | 839 | 0.994244 | 0.999495 | 0.9924 | — | - | — | - |
| `batch` | 22,685 | 0.788616 | 0.991793 | 0.9957 | — | - | — | - |
| `package.json` | 4,974 | 0.994882 | 0.996338 | 0.9908 | — | - | — | - |
| `elf` | 43,836 | 0.996627 | 0.997925 | 0.9884 | 0.9887 | +0.007927 | 0.9902 | +0.007725 |
| `ole` | 1,583 | 0.911332 | 0.950938 | 0.9278 | — | - | — | - |
| `pdf` | 25,435 | 0.970295 | 0.993969 | 0.9808 | 0.9878 | -0.017505 | 0.9901 | +0.003869 |
| `pkg-info` | 1,520 | 0.996848 | 0.999386 | 0.9918 | — | - | — | - |
| `xls` | 7,299 | 0.980150 | 0.991354 | 0.9739 | — | - | — | - |
| `macho` | 1,842 | 0.974656 | 0.939746 | 0.8664 | — | - | — | - |
| `lnk` | 673 | 0.901137 | 0.967335 | 0.9069 | — | - | — | - |
| `tar` | 5,789 | 0.981021 | 0.985748 | 0.9489 | — | - | — | - |
| `python-bytecode` | 15,662 | 0.950476 | 0.922635 | 0.9381 | — | - | — | - |
| `vbs` | 1,862 | 0.968051 | 0.989949 | 0.9615 | — | - | — | - |
| `perl` | 5,014 | 0.968865 | 0.822871 | 0.8333 | — | - | — | - |
| `shell` | 9,390 | 0.982970 | 0.967647 | 0.9355 | — | - | — | - |
| `docx` | 621 | 0.869373 | 0.981886 | 0.9560 | — | - | — | - |
| `powershell` | 958 | 0.953234 | 0.977137 | 0.9440 | — | - | — | - |
| `jar` | 910 | 0.927644 | 0.939044 | 0.8866 | — | - | — | - |
| `rust` | 11,211 | 0.521441 | 0.082824 | 0.1143 | — | - | — | - |
| `pe` | 183,846 | 0.987765 | 0.998492 | 0.9904 | 0.9982 | -0.010435 | 0.9983 | +0.000192 |
| `python` | 27,530 | 0.901253 | 0.811463 | 0.8136 | — | - | — | - |
| `kotlin` | 10,379 | 0.933471 | 0.928242 | 0.8722 | — | - | — | - |
| `javascript` | 90,995 | 0.971178 | 0.945941 | 0.9044 | — | - | — | - |
| `php` | 19,112 | 0.885444 | 0.756586 | 0.7630 | — | - | — | - |
| `zip` | 14,085 | 0.770747 | 0.970216 | 0.9497 | — | - | — | - |
| `xlsx` | 7,623 | 0.605702 | 0.982941 | 0.9872 | — | - | — | - |
| `java_class` | 88,336 | 0.978616 | 0.887190 | 0.9091 | — | - | — | - |
| `csharp` | 8,683 | 0.705983 | 0.378892 | 0.4270 | — | - | — | - |
| `jpeg` | 3,897 | 0.720412 | 0.237975 | 0.3028 | — | - | — | - |
| `json` | 4,617 | 0.670668 | 0.049697 | 0.1059 | — | - | — | - |
| `java` | 5,364 | 0.752047 | 0.164335 | 0.2323 | — | - | — | - |
| `c` | 90,433 | 0.692744 | 0.251962 | 0.3267 | — | - | — | - |
| `text` | 11,381 | 0.631256 | 0.162178 | 0.2077 | — | - | — | - |
| `deb` | 953 | 0.513068 | 0.150838 | 0.1818 | — | - | — | - |
| `go` | 16,537 | 0.551129 | 0.198033 | 0.2154 | — | - | — | - |
| `plist` | 1,675 | 0.496771 | 0.089523 | 0.1176 | — | - | — | - |
| `png` | 22,614 | 0.531381 | 0.111803 | 0.1511 | — | - | — | - |
| `makefile` | 3,509 | 0.544461 | 0.039570 | 0.0855 | — | - | — | - |
| `xml` | 26,444 | 0.678835 | 0.149626 | 0.3071 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (80,203 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
