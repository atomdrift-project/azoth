# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2593965 | 0.921236 | 0.882743 | 0.8740 | 0.9969 | -0.075664 | 0.9971 | -0.114357 |
| `rtf` | 925 | 0.999860 | 0.999980 | 0.9982 | — | - | — | - |
| `ole_doc` | 15,184 | 0.976862 | 0.992241 | 0.9566 | — | - | — | - |
| `python_sdist` | 1,543 | 0.915801 | 0.926000 | 0.9253 | — | - | — | - |
| `gem` | 14,298 | 0.969666 | 0.898620 | 0.9263 | — | - | — | - |
| `elf` | 138,130 | 0.997061 | 0.994149 | 0.9795 | 0.9887 | +0.008361 | 0.9902 | +0.003949 |
| `package.json` | 12,328 | 0.967706 | 0.962062 | 0.9453 | — | - | — | - |
| `lnk` | 737 | 0.875481 | 0.971817 | 0.9099 | — | - | — | - |
| `html` | 65,141 | 0.984301 | 0.966048 | 0.9546 | — | - | — | - |
| `batch` | 23,435 | 0.339878 | 0.963727 | 0.9766 | — | - | — | - |
| `npm` | 32,282 | 0.943592 | 0.917014 | 0.8919 | — | - | — | - |
| `registry` | 13,738 | 0.998986 | 0.878029 | 0.8154 | — | - | — | - |
| `perl` | 10,230 | 0.970783 | 0.817519 | 0.8043 | — | - | — | - |
| `macho` | 5,091 | 0.963578 | 0.879035 | 0.8517 | — | - | — | - |
| `python_bytecode` | 153,486 | 0.854657 | 0.668012 | 0.7590 | — | - | — | - |
| `powershell` | 1,537 | 0.955169 | 0.966626 | 0.9246 | — | - | — | - |
| `ico` | 123 | 0.934175 | 0.883114 | 0.8485 | — | - | — | - |
| `php` | 79,005 | 0.892103 | 0.726106 | 0.7303 | — | - | — | - |
| `pe` | 237,326 | 0.954469 | 0.992894 | 0.9674 | 0.9982 | -0.043731 | 0.9983 | -0.005406 |
| `python` | 87,480 | 0.917184 | 0.795709 | 0.7898 | — | - | — | - |
| `shell` | 23,532 | 0.967351 | 0.922337 | 0.8763 | — | - | — | - |
| `tar` | 12,860 | 0.966214 | 0.925505 | 0.8617 | — | - | — | - |
| `kotlin` | 13,946 | 0.854247 | 0.792470 | 0.7268 | — | - | — | - |
| `zip` | 27,313 | 0.750170 | 0.858417 | 0.8113 | — | - | — | - |
| `jar` | 5,699 | 0.989614 | 0.931247 | 0.8680 | — | - | — | - |
| `pkg_info` | 2,355 | 0.961857 | 0.830514 | 0.8000 | — | - | — | - |
| `java_class` | 229,386 | 0.938492 | 0.740250 | 0.7706 | — | - | — | - |
| `vsix` | 813 | 0.836981 | 0.577203 | 0.6047 | — | - | — | - |
| `crx` | 1,837 | 0.968965 | 0.885764 | 0.8247 | — | - | — | - |
| `static-lib` | 1,705 | 0.693866 | 0.359324 | 0.4242 | — | - | — | - |
| `ruby` | 24,553 | 0.983614 | 0.732246 | 0.7188 | — | - | — | - |
| `ooxml` | 9,150 | 0.773475 | 0.974239 | 0.9539 | — | - | — | - |
| `apk_android` | 596 | 0.782288 | 0.935606 | 0.8981 | — | - | — | - |
| `vbs` | 2,383 | 0.944212 | 0.983656 | 0.9378 | — | - | — | - |
| `javascript` | 245,276 | 0.922568 | 0.832570 | 0.8123 | — | - | — | - |
| `whl` | 8,033 | 0.931550 | 0.601388 | 0.5706 | — | - | — | - |
| `csharp` | 13,320 | 0.666735 | 0.306647 | 0.3796 | — | - | — | - |
| `pdf` | 26,252 | 0.825499 | 0.972481 | 0.9389 | 0.9878 | -0.162301 | 0.9901 | -0.017619 |
| `jpeg` | 5,842 | 0.634189 | 0.190753 | 0.2797 | — | - | — | - |
| `go` | 32,602 | 0.624879 | 0.240049 | 0.2696 | — | - | — | - |
| `rust` | 44,649 | 0.829219 | 0.269422 | 0.3614 | — | - | — | - |
| `gif` | 292 | 0.511310 | 0.384401 | 0.4785 | — | - | — | - |
| `xml` | 57,317 | 0.464888 | 0.192222 | 0.3158 | — | - | — | - |
| `text` | 54,396 | 0.652395 | 0.086085 | 0.1093 | — | - | — | - |
| `java` | 25,585 | 0.564921 | 0.073146 | 0.1252 | — | - | — | - |
| `png` | 69,183 | 0.417326 | 0.066779 | 0.1017 | — | - | — | - |
| `7z` | 1,166 | 0.940125 | 0.997399 | 0.9807 | — | - | — | - |
| `json` | 35,004 | 0.739288 | 0.585964 | 0.6939 | — | - | — | - |
| `c` | 223,643 | 0.670113 | 0.248962 | 0.3440 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (6,260 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
