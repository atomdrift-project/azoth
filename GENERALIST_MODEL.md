# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1694890 | 0.956190 | 0.919423 | 0.8956 | 0.9969 | -0.040710 | 0.9971 | -0.077677 |
| `html` | 2,041 | 0.996951 | 0.972267 | 0.9836 | — | - | — | - |
| `rtf` | 924 | 0.989093 | 0.998829 | 0.9897 | — | - | — | - |
| `pkg_info` | 2,894 | 0.996847 | 0.996623 | 0.9808 | — | - | — | - |
| `package.json` | 8,349 | 0.983662 | 0.983516 | 0.9659 | — | - | — | - |
| `ole_doc` | 14,501 | 0.970420 | 0.990811 | 0.9643 | — | - | — | - |
| `gem` | 342 | 0.943385 | 0.945914 | 0.9518 | — | - | — | - |
| `elf` | 79,574 | 0.997609 | 0.996752 | 0.9799 | 0.9887 | +0.008909 | 0.9902 | +0.006552 |
| `java` | 21,646 | 0.646223 | 0.070312 | 0.1194 | — | - | — | - |
| `macho` | 3,070 | 0.955379 | 0.872902 | 0.8185 | — | - | — | - |
| `lnk` | 701 | 0.956736 | 0.988754 | 0.9741 | — | - | — | - |
| `vbs` | 2,020 | 0.937432 | 0.982584 | 0.9469 | — | - | — | - |
| `perl` | 8,470 | 0.938536 | 0.750182 | 0.7765 | — | - | — | - |
| `tar` | 10,905 | 0.970433 | 0.962337 | 0.9120 | — | - | — | - |
| `jar` | 2,713 | 0.946071 | 0.888591 | 0.8411 | — | - | — | - |
| `pdf` | 25,945 | 0.935974 | 0.988107 | 0.9736 | 0.9878 | -0.051826 | 0.9901 | -0.001993 |
| `crx` | 580 | 0.897365 | 0.889323 | 0.8447 | — | - | — | - |
| `registry` | 12,686 | 0.998530 | 0.827794 | 0.8065 | — | - | — | - |
| `npm` | 1,094 | 0.878247 | 0.900958 | 0.8116 | — | - | — | - |
| `shell` | 18,760 | 0.969046 | 0.924957 | 0.8759 | — | - | — | - |
| `powershell` | 1,312 | 0.937176 | 0.960305 | 0.9211 | — | - | — | - |
| `pe` | 193,458 | 0.985314 | 0.997964 | 0.9858 | 0.9982 | -0.012886 | 0.9983 | -0.000336 |
| `whl` | 1,230 | 0.895983 | 0.871965 | 0.8005 | — | - | — | - |
| `kotlin` | 13,123 | 0.825101 | 0.828427 | 0.7844 | — | - | — | - |
| `python` | 69,632 | 0.924421 | 0.796774 | 0.7844 | — | - | — | - |
| `zip` | 16,517 | 0.750273 | 0.941190 | 0.8954 | — | - | — | - |
| `ooxml` | 8,910 | 0.772515 | 0.987147 | 0.9896 | — | - | — | - |
| `python_bytecode` | 93,039 | 0.877517 | 0.703774 | 0.7806 | — | - | — | - |
| `php` | 69,446 | 0.872363 | 0.689956 | 0.7227 | — | - | — | - |
| `cargo.toml` | 911 | 0.715749 | 0.463807 | 0.5634 | — | - | — | - |
| `javascript` | 174,944 | 0.967147 | 0.910880 | 0.8520 | — | - | — | - |
| `batch` | 23,087 | 0.791851 | 0.985621 | 0.9929 | — | - | — | - |
| `ruby` | 21,349 | 0.770802 | 0.359254 | 0.4400 | — | - | — | - |
| `csharp` | 11,689 | 0.690809 | 0.312020 | 0.3712 | — | - | — | - |
| `json` | 25,161 | 0.468813 | 0.063072 | 0.1277 | — | - | — | - |
| `java_class` | 203,568 | 0.946720 | 0.789799 | 0.8263 | — | - | — | - |
| `dockerfile` | 572 | 0.743473 | 0.187829 | 0.2727 | — | - | — | - |
| `rust` | 39,931 | 0.640829 | 0.073209 | 0.1327 | — | - | — | - |
| `jpeg` | 5,575 | 0.630871 | 0.181539 | 0.2832 | — | - | — | - |
| `c` | 171,868 | 0.734549 | 0.232257 | 0.3151 | — | - | — | - |
| `deb` | 2,507 | 0.516590 | 0.114558 | 0.1587 | — | - | — | - |
| `png` | 47,685 | 0.530475 | 0.082872 | 0.1052 | — | - | — | - |
| `plist` | 12,042 | 0.514862 | 0.040477 | 0.0659 | — | - | — | - |
| `makefile` | 7,510 | 0.407463 | 0.026652 | 0.0612 | — | - | — | - |
| `go` | 28,640 | 0.624296 | 0.226088 | 0.2485 | — | - | — | - |
| `text` | 33,966 | 0.631547 | 0.093372 | 0.1293 | — | - | — | - |
| `xml` | 50,071 | 0.633339 | 0.128244 | 0.2556 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (9,307 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
