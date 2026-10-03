# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2503210 | 0.942705 | 0.893598 | 0.8733 | 0.9969 | -0.054195 | 0.9971 | -0.103502 |
| `rtf` | 928 | 0.995497 | 0.999394 | 0.9938 | — | - | — | - |
| `gem` | 14,154 | 0.976324 | 0.941089 | 0.9535 | — | - | — | - |
| `ole_doc` | 15,179 | 0.955888 | 0.986824 | 0.9572 | — | - | — | - |
| `html` | 37,250 | 0.991378 | 0.897900 | 0.9429 | — | - | — | - |
| `elf` | 137,576 | 0.997014 | 0.994194 | 0.9778 | 0.9887 | +0.008314 | 0.9902 | +0.003994 |
| `python_sdist` | 1,486 | 0.917429 | 0.922721 | 0.9058 | — | - | — | - |
| `lnk` | 732 | 0.870303 | 0.970924 | 0.9138 | — | - | — | - |
| `package.json` | 12,269 | 0.966266 | 0.959387 | 0.9455 | — | - | — | - |
| `batch` | 23,409 | 0.726419 | 0.982145 | 0.9808 | — | - | — | - |
| `pdf` | 26,251 | 0.776941 | 0.966054 | 0.9271 | 0.9878 | -0.210859 | 0.9901 | -0.024046 |
| `registry` | 13,740 | 0.996519 | 0.853455 | 0.7970 | — | - | — | - |
| `macho` | 5,073 | 0.953411 | 0.880306 | 0.8526 | — | - | — | - |
| `npm` | 28,099 | 0.941177 | 0.916411 | 0.8948 | — | - | — | - |
| `pkg_info` | 2,322 | 0.926801 | 0.760286 | 0.7660 | — | - | — | - |
| `python_bytecode` | 153,289 | 0.844462 | 0.655775 | 0.7576 | — | - | — | - |
| `perl` | 10,131 | 0.943609 | 0.724523 | 0.7609 | — | - | — | - |
| `ico` | 119 | 0.914553 | 0.871477 | 0.8571 | — | - | — | - |
| `python` | 87,207 | 0.921958 | 0.803451 | 0.7966 | — | - | — | - |
| `java_class` | 228,931 | 0.927410 | 0.719065 | 0.7519 | — | - | — | - |
| `tar` | 12,616 | 0.959942 | 0.914106 | 0.8518 | — | - | — | - |
| `kotlin` | 13,885 | 0.780217 | 0.730777 | 0.7268 | — | - | — | - |
| `ruby` | 24,289 | 0.985769 | 0.741157 | 0.7541 | — | - | — | - |
| `shell` | 23,076 | 0.964504 | 0.915955 | 0.8653 | — | - | — | - |
| `powershell` | 1,487 | 0.952690 | 0.962093 | 0.9272 | — | - | — | - |
| `pe` | 236,968 | 0.954548 | 0.992942 | 0.9683 | 0.9982 | -0.043652 | 0.9983 | -0.005358 |
| `jar` | 5,655 | 0.981719 | 0.912789 | 0.8605 | — | - | — | - |
| `zip` | 25,944 | 0.760386 | 0.867029 | 0.8077 | — | - | — | - |
| `php` | 78,663 | 0.916551 | 0.713486 | 0.7248 | — | - | — | - |
| `vsix` | 794 | 0.806102 | 0.571266 | 0.6136 | — | - | — | - |
| `crx` | 1,781 | 0.967711 | 0.884920 | 0.8177 | — | - | — | - |
| `ooxml` | 9,151 | 0.811095 | 0.978897 | 0.9553 | — | - | — | - |
| `json` | 34,568 | 0.642740 | 0.351820 | 0.4783 | — | - | — | - |
| `static-lib` | 1,553 | 0.692102 | 0.346213 | 0.3836 | — | - | — | - |
| `apk_android` | 588 | 0.752163 | 0.940085 | 0.9026 | — | - | — | - |
| `javascript` | 243,542 | 0.927182 | 0.823976 | 0.7869 | — | - | — | - |
| `deb` | 3,472 | 0.608412 | 0.188381 | 0.3077 | — | - | — | - |
| `vbs` | 2,333 | 0.933409 | 0.981304 | 0.9279 | — | - | — | - |
| `whl` | 7,632 | 0.929255 | 0.573303 | 0.5546 | — | - | — | - |
| `csharp` | 13,323 | 0.683698 | 0.303595 | 0.3645 | — | - | — | - |
| `go` | 32,483 | 0.643438 | 0.313589 | 0.3511 | — | - | — | - |
| `jpeg` | 5,839 | 0.545683 | 0.167825 | 0.2627 | — | - | — | - |
| `c` | 222,386 | 0.702383 | 0.247906 | 0.3462 | — | - | — | - |
| `rust` | 44,290 | 0.843941 | 0.265045 | 0.3415 | — | - | — | - |
| `xml` | 58,202 | 0.454062 | 0.172407 | 0.2898 | — | - | — | - |
| `text` | 44,683 | 0.664124 | 0.095156 | 0.1316 | — | - | — | - |
| `png` | 69,064 | 0.675361 | 0.093669 | 0.1023 | — | - | — | - |
| `java` | 25,361 | 0.589347 | 0.069476 | 0.1207 | — | - | — | - |
| `7z` | 1,168 | 0.914486 | 0.996205 | 0.9807 | — | - | — | - |
| `gif` | 287 | 0.260076 | 0.253623 | 0.4570 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (6,212 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
