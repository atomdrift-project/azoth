# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2490700 | 0.933796 | 0.889709 | 0.8841 | 0.9969 | -0.063104 | 0.9971 | -0.107391 |
| `ico` | 118 | 0.892870 | 0.829733 | 0.7733 | — | - | — | - |
| `rtf` | 925 | 0.995797 | 0.999440 | 0.9950 | — | - | — | - |
| `gem` | 14,102 | 0.978353 | 0.941226 | 0.9647 | — | - | — | - |
| `html` | 34,592 | 0.991712 | 0.902471 | 0.9429 | — | - | — | - |
| `ole_doc` | 15,179 | 0.964644 | 0.989209 | 0.9567 | — | - | — | - |
| `python_sdist` | 1,473 | 0.914740 | 0.923242 | 0.9099 | — | - | — | - |
| `elf` | 136,779 | 0.997192 | 0.994312 | 0.9782 | 0.9887 | +0.008492 | 0.9902 | +0.004112 |
| `package.json` | 12,264 | 0.967556 | 0.960125 | 0.9475 | — | - | — | - |
| `lnk` | 732 | 0.865889 | 0.970512 | 0.9138 | — | - | — | - |
| `pe` | 236,852 | 0.956355 | 0.993271 | 0.9704 | 0.9982 | -0.041845 | 0.9983 | -0.005029 |
| `pdf` | 26,248 | 0.857753 | 0.977286 | 0.9431 | 0.9878 | -0.130047 | 0.9901 | -0.012814 |
| `registry` | 13,740 | 0.997275 | 0.829807 | 0.7970 | — | - | — | - |
| `macho` | 5,065 | 0.955692 | 0.878681 | 0.8412 | — | - | — | - |
| `npm` | 27,725 | 0.943309 | 0.921758 | 0.8995 | — | - | — | - |
| `perl` | 10,118 | 0.931733 | 0.732692 | 0.7586 | — | - | — | - |
| `ruby` | 24,199 | 0.988715 | 0.730250 | 0.7302 | — | - | — | - |
| `tar` | 12,917 | 0.961602 | 0.920787 | 0.8595 | — | - | — | - |
| `python_bytecode` | 150,007 | 0.794733 | 0.657255 | 0.7547 | — | - | — | - |
| `python` | 87,068 | 0.924893 | 0.802676 | 0.7958 | — | - | — | - |
| `shell` | 23,053 | 0.964008 | 0.915887 | 0.8668 | — | - | — | - |
| `kotlin` | 14,022 | 0.747090 | 0.709851 | 0.7269 | — | - | — | - |
| `pkg_info` | 2,303 | 0.934719 | 0.757103 | 0.7692 | — | - | — | - |
| `powershell` | 1,486 | 0.954142 | 0.963824 | 0.9273 | — | - | — | - |
| `vsix` | 740 | 0.814835 | 0.586871 | 0.6420 | — | - | — | - |
| `zip` | 25,468 | 0.758024 | 0.870320 | 0.8130 | — | - | — | - |
| `php` | 78,662 | 0.908972 | 0.717781 | 0.7253 | — | - | — | - |
| `jar` | 5,623 | 0.983103 | 0.921160 | 0.8584 | — | - | — | - |
| `java_class` | 228,661 | 0.925601 | 0.723731 | 0.7559 | — | - | — | - |
| `crx` | 1,511 | 0.966602 | 0.882687 | 0.8293 | — | - | — | - |
| `apk_android` | 586 | 0.762179 | 0.939566 | 0.9026 | — | - | — | - |
| `ooxml` | 9,151 | 0.807551 | 0.979000 | 0.9532 | — | - | — | - |
| `static-lib` | 1,539 | 0.688701 | 0.356728 | 0.3862 | — | - | — | - |
| `javascript` | 243,687 | 0.922532 | 0.826352 | 0.7999 | — | - | — | - |
| `json` | 33,986 | 0.633122 | 0.357688 | 0.4889 | — | - | — | - |
| `vbs` | 2,335 | 0.942762 | 0.983663 | 0.9373 | — | - | — | - |
| `whl` | 7,111 | 0.932087 | 0.597227 | 0.5629 | — | - | — | - |
| `csharp` | 13,322 | 0.652120 | 0.302591 | 0.3693 | — | - | — | - |
| `batch` | 23,387 | 0.629629 | 0.972948 | 0.9814 | — | - | — | - |
| `deb` | 3,470 | 0.611872 | 0.147866 | 0.2500 | — | - | — | - |
| `c` | 222,183 | 0.680661 | 0.248715 | 0.3471 | — | - | — | - |
| `jpeg` | 5,839 | 0.587438 | 0.168678 | 0.2521 | — | - | — | - |
| `gif` | 279 | 0.216465 | 0.246663 | 0.4670 | — | - | — | - |
| `go` | 32,465 | 0.633506 | 0.321227 | 0.3553 | — | - | — | - |
| `text` | 43,572 | 0.665505 | 0.096964 | 0.1316 | — | - | — | - |
| `xml` | 58,207 | 0.454392 | 0.155638 | 0.2865 | — | - | — | - |
| `png` | 69,064 | 0.669422 | 0.089785 | 0.1010 | — | - | — | - |
| `rust` | 44,210 | 0.820461 | 0.262975 | 0.3333 | — | - | — | - |
| `java` | 25,361 | 0.617471 | 0.078399 | 0.1260 | — | - | — | - |
| `7z` | 1,168 | 0.927895 | 0.996859 | 0.9807 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (6,307 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
