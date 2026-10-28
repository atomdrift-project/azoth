# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 2646643 | 0.935165 | 0.889369 | 0.1065 | 0.9969 | -0.061735 | 0.9971 | -0.107731 |
| `rtf` | 925 | 0.999946 | 0.999992 | 0.0000 | — | - | — | - |
| `ole_doc` | 15,191 | 0.982126 | 0.993789 | 0.0630 | — | - | — | - |
| `python_sdist` | 1,897 | 0.921213 | 0.921222 | 0.0108 | — | - | — | - |
| `gem` | 14,943 | 0.980763 | 0.911801 | 0.0000 | — | - | — | - |
| `elf` | 138,421 | 0.996658 | 0.992249 | 0.2159 | 0.9887 | +0.007958 | 0.9902 | +0.002049 |
| `7z` | 1,174 | 0.939810 | 0.997293 | 0.4715 | — | - | — | - |
| `registry` | 13,739 | 0.999420 | 0.942272 | 0.0000 | — | - | — | - |
| `jar` | 5,717 | 0.990180 | 0.927788 | 0.0000 | — | - | — | - |
| `pdf` | 26,253 | 0.966522 | 0.993691 | 0.0000 | 0.9878 | -0.021278 | 0.9901 | +0.003591 |
| `perl` | 10,234 | 0.992384 | 0.840513 | 0.0000 | — | - | — | - |
| `apk_android` | 624 | 0.757924 | 0.927422 | 0.0000 | — | - | — | - |
| `macho` | 5,117 | 0.963959 | 0.874744 | 0.0122 | — | - | — | - |
| `package.json` | 12,336 | 0.976426 | 0.972784 | 0.0000 | — | - | — | - |
| `php` | 79,304 | 0.961474 | 0.819721 | 0.0000 | — | - | — | - |
| `html` | 65,753 | 0.990603 | 0.975931 | 0.0000 | — | - | — | - |
| `lnk` | 738 | 0.871996 | 0.970220 | 0.0034 | — | - | — | - |
| `python_bytecode` | 154,698 | 0.875786 | 0.679687 | 0.0000 | — | - | — | - |
| `tar` | 14,978 | 0.960209 | 0.909218 | 0.0207 | — | - | — | - |
| `ruby` | 24,757 | 0.987062 | 0.809184 | 0.0000 | — | - | — | - |
| `powershell` | 1,568 | 0.963512 | 0.972577 | 0.0077 | — | - | — | - |
| `ico` | 132 | 0.941690 | 0.898351 | 0.0000 | — | - | — | - |
| `kotlin` | 13,808 | 0.976883 | 0.942073 | 0.0000 | — | - | — | - |
| `pkg_info` | 2,385 | 0.961161 | 0.848254 | 0.0000 | — | - | — | - |
| `python` | 87,546 | 0.934089 | 0.805012 | 0.0000 | — | - | — | - |
| `shell` | 24,045 | 0.971312 | 0.934421 | 0.0008 | — | - | — | - |
| `zip` | 32,193 | 0.747416 | 0.833171 | 0.1536 | — | - | — | - |
| `javascript` | 245,496 | 0.949492 | 0.846326 | 0.0000 | — | - | — | - |
| `vbs` | 2,404 | 0.940094 | 0.981399 | 0.0000 | — | - | — | - |
| `json` | 39,097 | 0.903369 | 0.532436 | 0.0000 | — | - | — | - |
| `static-lib` | 1,685 | 0.843662 | 0.477873 | 0.0000 | — | - | — | - |
| `pe` | 237,959 | 0.943391 | 0.990847 | 0.1388 | 0.9982 | -0.054809 | 0.9983 | -0.007453 |
| `ooxml` | 9,156 | 0.854123 | 0.983122 | 0.0000 | — | - | — | - |
| `crx` | 1,851 | 0.967291 | 0.881384 | 0.0000 | — | - | — | - |
| `java_class` | 229,533 | 0.964868 | 0.754175 | 0.0000 | — | - | — | - |
| `rust` | 45,755 | 0.943130 | 0.331698 | 0.0000 | — | - | — | - |
| `go` | 32,960 | 0.689467 | 0.366877 | 0.0000 | — | - | — | - |
| `vsix` | 817 | 0.841627 | 0.548662 | 0.0000 | — | - | — | - |
| `npm` | 45,936 | 0.944934 | 0.894519 | 0.0779 | — | - | — | - |
| `csharp` | 13,331 | 0.797349 | 0.331132 | 0.0000 | — | - | — | - |
| `batch` | 23,467 | 0.278626 | 0.948793 | 0.0000 | — | - | — | - |
| `xml` | 56,461 | 0.736958 | 0.244502 | 0.0000 | — | - | — | - |
| `whl` | 8,821 | 0.932994 | 0.636819 | 0.0000 | — | - | — | - |
| `java` | 25,622 | 0.755517 | 0.090394 | 0.0000 | — | - | — | - |
| `jpeg` | 5,844 | 0.736375 | 0.206318 | 0.0000 | — | - | — | - |
| `c` | 223,911 | 0.746271 | 0.267899 | 0.0000 | — | - | — | - |
| `png` | 69,289 | 0.878910 | 0.209472 | 0.0000 | — | - | — | - |
| `text` | 62,381 | 0.879047 | 0.180319 | 0.0000 | — | - | — | - |
| `gif` | 307 | 0.841256 | 0.614615 | 0.0000 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (127,227 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
