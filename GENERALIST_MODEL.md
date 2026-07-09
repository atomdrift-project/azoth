# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1688448 | 0.956029 | 0.918951 | 0.8951 | 0.9969 | -0.040871 | 0.9971 | -0.078149 |
| `html` | 2,041 | 0.974418 | 0.968357 | 0.9836 | — | - | — | - |
| `rtf` | 924 | 0.988958 | 0.998830 | 0.9897 | — | - | — | - |
| `pkg_info` | 2,728 | 0.997453 | 0.997215 | 0.9796 | — | - | — | - |
| `package.json` | 7,918 | 0.991976 | 0.991530 | 0.9735 | — | - | — | - |
| `ole_doc` | 14,494 | 0.974600 | 0.992229 | 0.9646 | — | - | — | - |
| `gem` | 325 | 0.946779 | 0.948958 | 0.9581 | — | - | — | - |
| `elf` | 75,152 | 0.997608 | 0.997018 | 0.9838 | 0.9887 | +0.008908 | 0.9902 | +0.006818 |
| `vbs` | 2,019 | 0.951443 | 0.985717 | 0.9497 | — | - | — | - |
| `macho` | 3,045 | 0.958469 | 0.879590 | 0.8058 | — | - | — | - |
| `lnk` | 701 | 0.941824 | 0.986041 | 0.9623 | — | - | — | - |
| `perl` | 8,234 | 0.941554 | 0.774576 | 0.7901 | — | - | — | - |
| `tar` | 10,737 | 0.971275 | 0.962001 | 0.9124 | — | - | — | - |
| `registry` | 10,159 | 0.998682 | 0.874969 | 0.8160 | — | - | — | - |
| `shell` | 18,542 | 0.969060 | 0.929054 | 0.8770 | — | - | — | - |
| `npm` | 1,025 | 0.878357 | 0.901780 | 0.8168 | — | - | — | - |
| `whl` | 1,195 | 0.898919 | 0.884847 | 0.8214 | — | - | — | - |
| `crx` | 569 | 0.908103 | 0.906072 | 0.8661 | — | - | — | - |
| `powershell` | 1,305 | 0.941693 | 0.963244 | 0.9187 | — | - | — | - |
| `pe` | 193,228 | 0.986868 | 0.998219 | 0.9860 | 0.9982 | -0.011332 | 0.9983 | -0.000081 |
| `jar` | 2,217 | 0.943637 | 0.892021 | 0.8454 | — | - | — | - |
| `kotlin` | 12,954 | 0.922156 | 0.897250 | 0.8307 | — | - | — | - |
| `php` | 68,372 | 0.889616 | 0.689787 | 0.7237 | — | - | — | - |
| `python` | 66,514 | 0.926353 | 0.801488 | 0.7822 | — | - | — | - |
| `zip` | 16,434 | 0.749853 | 0.942117 | 0.9014 | — | - | — | - |
| `javascript` | 167,320 | 0.966594 | 0.913617 | 0.8565 | — | - | — | - |
| `cargo.toml` | 909 | 0.729278 | 0.464690 | 0.5634 | — | - | — | - |
| `python_bytecode` | 85,817 | 0.841167 | 0.691627 | 0.7806 | — | - | — | - |
| `ooxml` | 8,909 | 0.727635 | 0.985108 | 0.9800 | — | - | — | - |
| `batch` | 23,073 | 0.407265 | 0.971495 | 0.9835 | — | - | — | - |
| `ruby` | 21,035 | 0.805957 | 0.335844 | 0.4286 | — | - | — | - |
| `csharp` | 11,591 | 0.678636 | 0.311607 | 0.3813 | — | - | — | - |
| `jpeg` | 5,572 | 0.570848 | 0.170518 | 0.2743 | — | - | — | - |
| `dockerfile` | 570 | 0.665798 | 0.208651 | 0.2609 | — | - | — | - |
| `deb` | 2,444 | 0.492340 | 0.072692 | 0.1515 | — | - | — | - |
| `c` | 171,343 | 0.640502 | 0.231321 | 0.3172 | — | - | — | - |
| `json` | 19,509 | 0.409396 | 0.064768 | 0.1288 | — | - | — | - |
| `go` | 28,588 | 0.638617 | 0.233469 | 0.2460 | — | - | — | - |
| `text` | 32,870 | 0.592624 | 0.095370 | 0.1337 | — | - | — | - |
| `plist` | 12,039 | 0.513544 | 0.043372 | 0.0682 | — | - | — | - |
| `xml` | 49,860 | 0.679542 | 0.117637 | 0.2149 | — | - | — | - |
| `makefile` | 7,497 | 0.543880 | 0.030030 | 0.0571 | — | - | — | - |
| `java` | 19,736 | 0.751101 | 0.080727 | 0.1140 | — | - | — | - |
| `java_class` | 190,384 | 0.921268 | 0.787465 | 0.8333 | — | - | — | - |
| `pdf` | 25,942 | 0.968826 | 0.993151 | 0.9746 | 0.9878 | -0.018974 | 0.9901 | +0.003051 |
| `png` | 46,568 | 0.608681 | 0.087949 | 0.1086 | — | - | — | - |
| `rust` | 39,931 | 0.626165 | 0.071935 | 0.1398 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,309 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
