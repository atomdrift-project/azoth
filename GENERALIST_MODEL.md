# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2659751 | 0.949854 | 0.914001 | 0.2685 | 0.9969 | -0.047046 | 0.9971 | -0.083099 |
| `rtf` | 937 | 0.998760 | 0.999832 | 0.0000 | — | - | — | - |
| `pdf` | 26,258 | 0.927557 | 0.987698 | 0.0000 | 0.9878 | -0.060243 | 0.9901 | -0.002402 |
| `kotlin` | 13,635 | 0.965832 | 0.898923 | 0.0012 | — | - | — | - |
| `batch` | 23,483 | 0.652198 | 0.968374 | 0.0001 | — | - | — | - |
| `elf` | 138,640 | 0.999138 | 0.998794 | 0.7501 | 0.9887 | +0.010438 | 0.9902 | +0.008594 |
| `vbs` | 2,420 | 0.945124 | 0.986137 | 0.0043 | — | - | — | - |
| `ole_doc` | 15,213 | 0.974549 | 0.992193 | 0.1832 | — | - | — | - |
| `apk_android` | 638 | 0.832840 | 0.951849 | 0.0000 | — | - | — | - |
| `python_sdist` | 1,948 | 0.926683 | 0.933502 | 0.0108 | — | - | — | - |
| `html` | 65,862 | 0.995757 | 0.994403 | 0.0000 | — | - | — | - |
| `lnk` | 731 | 0.950944 | 0.987280 | 0.0000 | — | - | — | - |
| `7z` | 1,174 | 0.959760 | 0.998145 | 0.5132 | — | - | — | - |
| `ooxml` | 9,282 | 0.547730 | 0.943741 | 0.0071 | — | - | — | - |
| `static-lib` | 1,812 | 0.887476 | 0.630078 | 0.0000 | — | - | — | - |
| `jar` | 5,737 | 0.994769 | 0.965620 | 0.0041 | — | - | — | - |
| `gem` | 14,983 | 0.975031 | 0.908537 | 0.0000 | — | - | — | - |
| `registry` | 13,739 | 0.999536 | 0.948961 | 0.0000 | — | - | — | - |
| `shell` | 24,178 | 0.992206 | 0.982186 | 0.0008 | — | - | — | - |
| `macho` | 5,130 | 0.990145 | 0.940607 | 0.0000 | — | - | — | - |
| `json` | 39,146 | 0.943413 | 0.543784 | 0.0000 | — | - | — | - |
| `pe` | 239,683 | 0.990585 | 0.998540 | 0.3148 | 0.9982 | -0.007615 | 0.9983 | +0.000240 |
| `ruby` | 24,764 | 0.999421 | 0.914753 | 0.0000 | — | - | — | - |
| `php` | 79,318 | 0.965622 | 0.910904 | 0.0707 | — | - | — | - |
| `gif` | 319 | 0.871900 | 0.575461 | 0.0000 | — | - | — | - |
| `perl` | 10,244 | 0.987874 | 0.882636 | 0.0000 | — | - | — | - |
| `zip` | 31,661 | 0.883035 | 0.927916 | 0.2087 | — | - | — | - |
| `java_class` | 229,526 | 0.975086 | 0.883865 | 0.0000 | — | - | — | - |
| `ico` | 135 | 0.939980 | 0.875787 | 0.0000 | — | - | — | - |
| `vsix` | 822 | 0.987181 | 0.871159 | 0.0000 | — | - | — | - |
| `powershell` | 1,584 | 0.980654 | 0.985773 | 0.0203 | — | - | — | - |
| `python_bytecode` | 154,704 | 0.929863 | 0.771895 | 0.0000 | — | - | — | - |
| `java` | 25,622 | 0.500834 | 0.211614 | 0.0000 | — | - | — | - |
| `npm` | 49,589 | 0.976894 | 0.933915 | 0.2240 | — | - | — | - |
| `javascript` | 245,789 | 0.939737 | 0.918753 | 0.0045 | — | - | — | - |
| `crx` | 1,963 | 0.980406 | 0.915357 | 0.0000 | — | - | — | - |
| `go` | 33,228 | 0.702937 | 0.532555 | 0.0000 | — | - | — | - |
| `tar` | 15,403 | 0.989180 | 0.957456 | 0.0233 | — | - | — | - |
| `python` | 87,892 | 0.945485 | 0.883500 | 0.0000 | — | - | — | - |
| `package.json` | 12,347 | 0.993566 | 0.991850 | 0.0000 | — | - | — | - |
| `pkg_info` | 2,348 | 0.951542 | 0.834063 | 0.0000 | — | - | — | - |
| `whl` | 9,160 | 0.983575 | 0.799391 | 0.0000 | — | - | — | - |
| `png` | 69,443 | 0.936592 | 0.261554 | 0.0000 | — | - | — | - |
| `xml` | 55,779 | 0.948088 | 0.372990 | 0.0000 | — | - | — | - |
| `csharp` | 13,333 | 0.800010 | 0.472779 | 0.0000 | — | - | — | - |
| `rust` | 45,765 | 0.860424 | 0.372437 | 0.0000 | — | - | — | - |
| `c` | 223,957 | 0.794230 | 0.497250 | 0.0029 | — | - | — | - |
| `jpeg` | 5,847 | 0.781418 | 0.226959 | 0.0000 | — | - | — | - |
| `text` | 64,422 | 0.644808 | 0.167475 | 0.0000 | — | - | — | - |

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
