# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2138249 | 0.961909 | 0.914132 | 0.8947 | 0.9969 | -0.034991 | 0.9971 | -0.082968 |
| `rtf` | 929 | 0.986609 | 0.998429 | 0.9897 | — | - | — | - |
| `html` | 8,499 | 0.967849 | 0.967860 | 0.9836 | — | - | — | - |
| `pkg_info` | 3,378 | 0.996759 | 0.996377 | 0.9800 | — | - | — | - |
| `gem` | 479 | 0.947833 | 0.947141 | 0.9574 | — | - | — | - |
| `ole_doc` | 14,587 | 0.967204 | 0.989811 | 0.9642 | — | - | — | - |
| `elf` | 122,160 | 0.998045 | 0.995979 | 0.9749 | 0.9887 | +0.009345 | 0.9902 | +0.005779 |
| `package.json` | 10,309 | 0.978395 | 0.976271 | 0.9602 | — | - | — | - |
| `lnk` | 716 | 0.852418 | 0.969299 | 0.9108 | — | - | — | - |
| `macho` | 4,269 | 0.953180 | 0.856648 | 0.8141 | — | - | — | - |
| `registry` | 13,731 | 0.998621 | 0.840185 | 0.8154 | — | - | — | - |
| `tar` | 12,260 | 0.970371 | 0.958831 | 0.9081 | — | - | — | - |
| `vbs` | 2,064 | 0.944948 | 0.983440 | 0.9467 | — | - | — | - |
| `pdf` | 26,189 | 0.944011 | 0.990680 | 0.9697 | 0.9878 | -0.043789 | 0.9901 | +0.000580 |
| `perl` | 9,570 | 0.937739 | 0.739027 | 0.8101 | — | - | — | - |
| `npm` | 1,706 | 0.885987 | 0.908063 | 0.8300 | — | - | — | - |
| `powershell` | 1,401 | 0.944233 | 0.964428 | 0.9283 | — | - | — | - |
| `python_bytecode` | 126,797 | 0.847629 | 0.679398 | 0.7781 | — | - | — | - |
| `shell` | 22,177 | 0.964057 | 0.921562 | 0.8781 | — | - | — | - |
| `pe` | 198,304 | 0.984607 | 0.997502 | 0.9852 | 0.9982 | -0.013593 | 0.9983 | -0.000798 |
| `kotlin` | 14,428 | 0.857680 | 0.809581 | 0.7510 | — | - | — | - |
| `python` | 81,875 | 0.909810 | 0.776463 | 0.7827 | — | - | — | - |
| `javascript` | 219,136 | 0.964413 | 0.904360 | 0.8537 | — | - | — | - |
| `whl` | 2,186 | 0.874796 | 0.813736 | 0.7468 | — | - | — | - |
| `php` | 77,260 | 0.906997 | 0.703952 | 0.7290 | — | - | — | - |
| `crx` | 999 | 0.917014 | 0.889511 | 0.8325 | — | - | — | - |
| `ruby` | 22,171 | 0.842944 | 0.538559 | 0.6265 | — | - | — | - |
| `cargo.toml` | 1,120 | 0.709720 | 0.468787 | 0.5294 | — | - | — | - |
| `jar` | 4,088 | 0.954024 | 0.875485 | 0.8421 | — | - | — | - |
| `java_class` | 214,646 | 0.956000 | 0.797751 | 0.8479 | — | - | — | - |
| `ooxml` | 8,915 | 0.806822 | 0.989788 | 0.9815 | — | - | — | - |
| `zip` | 18,007 | 0.740445 | 0.918991 | 0.8632 | — | - | — | - |
| `csharp` | 12,928 | 0.698432 | 0.325852 | 0.3874 | — | - | — | - |
| `batch` | 23,143 | 0.578658 | 0.975145 | 0.9842 | — | - | — | - |
| `jpeg` | 5,759 | 0.656033 | 0.183407 | 0.2807 | — | - | — | - |
| `c` | 210,345 | 0.642874 | 0.222739 | 0.3150 | — | - | — | - |
| `png` | 65,643 | 0.569485 | 0.083605 | 0.1117 | — | - | — | - |
| `dockerfile` | 604 | 0.640104 | 0.138315 | 0.1895 | — | - | — | - |
| `go` | 30,640 | 0.610486 | 0.228714 | 0.2458 | — | - | — | - |
| `json` | 31,321 | 0.414731 | 0.050434 | 0.0807 | — | - | — | - |
| `deb` | 3,360 | 0.513341 | 0.080118 | 0.1519 | — | - | — | - |
| `plist` | 12,601 | 0.629278 | 0.033095 | 0.0638 | — | - | — | - |
| `xml` | 56,518 | 0.568879 | 0.103987 | 0.2059 | — | - | — | - |
| `java` | 23,126 | 0.746696 | 0.102127 | 0.1493 | — | - | — | - |
| `rust` | 41,680 | 0.648527 | 0.068342 | 0.1337 | — | - | — | - |
| `text` | 40,354 | 0.563145 | 0.059930 | 0.0903 | — | - | — | - |
| `makefile` | 7,936 | 0.413278 | 0.026412 | 0.0513 | — | - | — | - |
| `7z` | 1,194 | 0.928989 | 0.998249 | 0.9886 | — | - | — | - |
| `apk_android` | 316 | 0.460245 | 0.891318 | 0.9320 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,072 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
