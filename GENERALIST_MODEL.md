# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2653951 | 0.950569 | 0.914331 | 0.3082 | 0.9969 | -0.046331 | 0.9971 | -0.082769 |
| `rtf` | 937 | 0.998876 | 0.999847 | 0.2788 | — | - | — | - |
| `kotlin` | 13,771 | 0.964591 | 0.894522 | 0.0013 | — | - | — | - |
| `pdf` | 26,258 | 0.919052 | 0.986216 | 0.0000 | 0.9878 | -0.068748 | 0.9901 | -0.003884 |
| `batch` | 23,483 | 0.657830 | 0.969055 | 0.0000 | — | - | — | - |
| `elf` | 138,437 | 0.999032 | 0.998665 | 0.7631 | 0.9887 | +0.010332 | 0.9902 | +0.008465 |
| `python_sdist` | 1,943 | 0.926910 | 0.933331 | 0.0108 | — | - | — | - |
| `apk_android` | 628 | 0.839693 | 0.956502 | 0.0000 | — | - | — | - |
| `vbs` | 2,415 | 0.943997 | 0.985596 | 0.0053 | — | - | — | - |
| `ole_doc` | 15,206 | 0.974933 | 0.992300 | 0.2601 | — | - | — | - |
| `html` | 65,788 | 0.995576 | 0.994094 | 0.0003 | — | - | — | - |
| `7z` | 1,176 | 0.965790 | 0.998492 | 0.5310 | — | - | — | - |
| `lnk` | 738 | 0.962181 | 0.989994 | 0.0000 | — | - | — | - |
| `ooxml` | 9,279 | 0.804838 | 0.974639 | 0.1462 | — | - | — | - |
| `static-lib` | 1,686 | 0.907704 | 0.649430 | 0.0000 | — | - | — | - |
| `jar` | 5,736 | 0.994835 | 0.965252 | 0.0083 | — | - | — | - |
| `gem` | 15,079 | 0.975494 | 0.902798 | 0.0000 | — | - | — | - |
| `registry` | 13,739 | 0.999671 | 0.961065 | 0.0000 | — | - | — | - |
| `shell` | 24,057 | 0.991900 | 0.982209 | 0.0155 | — | - | — | - |
| `macho` | 5,131 | 0.988430 | 0.933685 | 0.0000 | — | - | — | - |
| `pe` | 237,988 | 0.992564 | 0.998822 | 0.3712 | 0.9982 | -0.005636 | 0.9983 | +0.000522 |
| `php` | 79,310 | 0.962946 | 0.902215 | 0.0583 | — | - | — | - |
| `json` | 39,117 | 0.962092 | 0.520130 | 0.0000 | — | - | — | - |
| `perl` | 10,245 | 0.988810 | 0.885908 | 0.0000 | — | - | — | - |
| `java_class` | 229,530 | 0.970457 | 0.864652 | 0.0000 | — | - | — | - |
| `powershell` | 1,573 | 0.976456 | 0.983499 | 0.0428 | — | - | — | - |
| `python_bytecode` | 154,698 | 0.928784 | 0.767184 | 0.0000 | — | - | — | - |
| `rust` | 45,764 | 0.859647 | 0.350598 | 0.0000 | — | - | — | - |
| `zip` | 32,266 | 0.882516 | 0.926354 | 0.2307 | — | - | — | - |
| `npm` | 47,956 | 0.975428 | 0.934952 | 0.2412 | — | - | — | - |
| `ico` | 134 | 0.913441 | 0.839507 | 0.0000 | — | - | — | - |
| `java` | 25,622 | 0.492182 | 0.209446 | 0.0000 | — | - | — | - |
| `tar` | 15,444 | 0.985802 | 0.948416 | 0.0052 | — | - | — | - |
| `package.json` | 12,348 | 0.994724 | 0.991852 | 0.0052 | — | - | — | - |
| `javascript` | 245,942 | 0.938702 | 0.918367 | 0.0105 | — | - | — | - |
| `python` | 87,972 | 0.946053 | 0.886006 | 0.0000 | — | - | — | - |
| `pkg_info` | 2,368 | 0.947804 | 0.875845 | 0.0000 | — | - | — | - |
| `go` | 33,225 | 0.705278 | 0.526092 | 0.0000 | — | - | — | - |
| `gif` | 313 | 0.872138 | 0.567669 | 0.0000 | — | - | — | - |
| `crx` | 1,860 | 0.972291 | 0.889324 | 0.0000 | — | - | — | - |
| `ruby` | 24,755 | 0.981536 | 0.896290 | 0.0000 | — | - | — | - |
| `png` | 69,442 | 0.919578 | 0.455684 | 0.0000 | — | - | — | - |
| `csharp` | 13,333 | 0.798233 | 0.450339 | 0.0000 | — | - | — | - |
| `xml` | 56,182 | 0.950001 | 0.360386 | 0.0000 | — | - | — | - |
| `whl` | 8,919 | 0.974537 | 0.737421 | 0.0000 | — | - | — | - |
| `jpeg` | 5,846 | 0.793183 | 0.230854 | 0.0000 | — | - | — | - |
| `vsix` | 818 | 0.870461 | 0.592949 | 0.0000 | — | - | — | - |
| `c` | 223,946 | 0.765842 | 0.468998 | 0.0028 | — | - | — | - |
| `text` | 63,158 | 0.694720 | 0.162862 | 0.0000 | — | - | — | - |

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
