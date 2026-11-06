# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2653916 | 0.950076 | 0.913633 | 0.4148 | 0.9969 | -0.046824 | 0.9971 | -0.083467 |
| `rtf` | 937 | 0.998833 | 0.999842 | 0.6710 | — | - | — | - |
| `kotlin` | 13,745 | 0.966495 | 0.898793 | 0.0013 | — | - | — | - |
| `pdf` | 26,258 | 0.946889 | 0.990750 | 0.0000 | 0.9878 | -0.040911 | 0.9901 | +0.000650 |
| `batch` | 23,480 | 0.658336 | 0.969290 | 0.0004 | — | - | — | - |
| `elf` | 138,434 | 0.999085 | 0.998778 | 0.8442 | 0.9887 | +0.010385 | 0.9902 | +0.008578 |
| `vbs` | 2,416 | 0.944845 | 0.986355 | 0.0233 | — | - | — | - |
| `apk_android` | 620 | 0.823125 | 0.949295 | 0.0000 | — | - | — | - |
| `ole_doc` | 15,205 | 0.974557 | 0.992208 | 0.6753 | — | - | — | - |
| `html` | 65,798 | 0.995610 | 0.994223 | 0.0080 | — | - | — | - |
| `python_sdist` | 1,945 | 0.926318 | 0.932837 | 0.0684 | — | - | — | - |
| `lnk` | 731 | 0.962755 | 0.989948 | 0.0374 | — | - | — | - |
| `7z` | 1,174 | 0.961168 | 0.998223 | 0.6032 | — | - | — | - |
| `ooxml` | 9,279 | 0.498565 | 0.936957 | 0.4318 | — | - | — | - |
| `static-lib` | 1,822 | 0.889786 | 0.636211 | 0.0000 | — | - | — | - |
| `jar` | 5,735 | 0.994931 | 0.965612 | 0.0448 | — | - | — | - |
| `registry` | 13,739 | 0.999544 | 0.950177 | 0.0000 | — | - | — | - |
| `shell` | 24,056 | 0.992688 | 0.982956 | 0.0268 | — | - | — | - |
| `gem` | 15,099 | 0.975506 | 0.905923 | 0.0000 | — | - | — | - |
| `ruby` | 24,759 | 0.979448 | 0.890992 | 0.0000 | — | - | — | - |
| `macho` | 5,130 | 0.988660 | 0.936334 | 0.0000 | — | - | — | - |
| `pe` | 237,984 | 0.990343 | 0.998488 | 0.4897 | 0.9982 | -0.007857 | 0.9983 | +0.000188 |
| `perl` | 10,246 | 0.988166 | 0.888721 | 0.0000 | — | - | — | - |
| `php` | 79,310 | 0.965169 | 0.910251 | 0.1437 | — | - | — | - |
| `json` | 39,119 | 0.966711 | 0.551394 | 0.0000 | — | - | — | - |
| `java_class` | 229,526 | 0.975547 | 0.886306 | 0.0070 | — | - | — | - |
| `ico` | 135 | 0.937378 | 0.891491 | 0.0000 | — | - | — | - |
| `powershell` | 1,572 | 0.981399 | 0.986818 | 0.1011 | — | - | — | - |
| `python_bytecode` | 154,698 | 0.931281 | 0.776091 | 0.0000 | — | - | — | - |
| `java` | 25,622 | 0.499723 | 0.213064 | 0.0000 | — | - | — | - |
| `npm` | 47,956 | 0.978229 | 0.938451 | 0.3534 | — | - | — | - |
| `package.json` | 12,348 | 0.995509 | 0.992466 | 0.0007 | — | - | — | - |
| `tar` | 15,469 | 0.987304 | 0.951256 | 0.0541 | — | - | — | - |
| `go` | 33,224 | 0.705869 | 0.531835 | 0.0000 | — | - | — | - |
| `gif` | 313 | 0.751905 | 0.463632 | 0.0000 | — | - | — | - |
| `python` | 87,961 | 0.946632 | 0.888181 | 0.0008 | — | - | — | - |
| `zip` | 31,877 | 0.881001 | 0.926093 | 0.2954 | — | - | — | - |
| `javascript` | 245,843 | 0.939691 | 0.918742 | 0.0380 | — | - | — | - |
| `pkg_info` | 2,359 | 0.959940 | 0.867975 | 0.0000 | — | - | — | - |
| `crx` | 1,856 | 0.981532 | 0.906921 | 0.0000 | — | - | — | - |
| `vsix` | 820 | 0.849263 | 0.619673 | 0.0000 | — | - | — | - |
| `png` | 69,442 | 0.942475 | 0.312085 | 0.0000 | — | - | — | - |
| `rust` | 45,765 | 0.861273 | 0.344852 | 0.0000 | — | - | — | - |
| `xml` | 56,087 | 0.943192 | 0.369025 | 0.0000 | — | - | — | - |
| `whl` | 8,923 | 0.977974 | 0.757218 | 0.0062 | — | - | — | - |
| `csharp` | 13,333 | 0.808620 | 0.463556 | 0.0000 | — | - | — | - |
| `c` | 223,937 | 0.770101 | 0.479720 | 0.0047 | — | - | — | - |
| `jpeg` | 5,846 | 0.744812 | 0.224060 | 0.0000 | — | - | — | - |
| `text` | 63,860 | 0.688874 | 0.166894 | 0.0000 | — | - | — | - |

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
