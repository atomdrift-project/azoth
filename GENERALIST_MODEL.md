# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 628939 | 0.984028 | 0.977156 | 0.9493 | 0.9969 | -0.012872 | 0.9971 | -0.019944 |
| `batch` | 22,152 | 0.913165 | 0.997657 | 0.9984 | — | - | — | - |
| `rtf` | 267 | 0.985476 | 0.997036 | 0.9816 | — | - | — | - |
| `python-bytecode` | 7,009 | 0.987606 | 0.981546 | 0.9883 | — | - | — | - |
| `pkg-info` | 1,409 | 0.996453 | 0.999632 | 0.9918 | — | - | — | - |
| `xls` | 3,948 | 0.985427 | 0.988363 | 0.9827 | — | - | — | - |
| `ole` | 923 | 0.984656 | 0.974287 | 0.9531 | — | - | — | - |
| `perl` | 4,030 | 0.996971 | 0.842274 | 0.8519 | — | - | — | - |
| `package.json` | 3,763 | 0.998784 | 0.999273 | 0.9959 | — | - | — | - |
| `elf` | 29,068 | 0.998937 | 0.998081 | 0.9749 | 0.9887 | +0.010237 | 0.9902 | +0.007881 |
| `shell` | 7,051 | 0.989760 | 0.967872 | 0.9191 | — | - | — | - |
| `macho` | 1,677 | 0.928500 | 0.870757 | 0.8589 | — | - | — | - |
| `lnk` | 428 | 0.811949 | 0.923024 | 0.8302 | — | - | — | - |
| `javascript` | 76,643 | 0.987382 | 0.958010 | 0.8987 | — | - | — | - |
| `docx` | 214 | 0.900405 | 0.975376 | 0.9219 | — | - | — | - |
| `php` | 13,887 | 0.951508 | 0.845050 | 0.8264 | — | - | — | - |
| `java_class` | 55,564 | 0.938880 | 0.912213 | 0.9249 | — | - | — | - |
| `pe` | 131,646 | 0.994718 | 0.999062 | 0.9908 | 0.9982 | -0.003482 | 0.9983 | +0.000762 |
| `jar` | 524 | 0.962534 | 0.958936 | 0.8950 | — | - | — | - |
| `kotlin` | 9,498 | 0.948099 | 0.950396 | 0.9115 | — | - | — | - |
| `python` | 19,287 | 0.955722 | 0.878556 | 0.8533 | — | - | — | - |
| `xml` | 20,052 | 0.639282 | 0.142254 | 0.2769 | — | - | — | - |
| `csharp` | 7,849 | 0.776137 | 0.416903 | 0.4770 | — | - | — | - |
| `powershell` | 656 | 0.966644 | 0.970578 | 0.9412 | — | - | — | - |
| `vbs` | 981 | 0.946443 | 0.961506 | 0.9368 | — | - | — | - |
| `c` | 70,039 | 0.635065 | 0.247191 | 0.3361 | — | - | — | - |
| `text` | 8,307 | 0.526121 | 0.195520 | 0.2816 | — | - | — | - |
| `pdf` | 24,053 | 0.973283 | 0.996161 | 0.9917 | 0.9878 | -0.014517 | 0.9901 | +0.006061 |
| `go` | 13,279 | 0.920853 | 0.513970 | 0.6185 | — | - | — | - |
| `jpeg` | 1,475 | 0.456558 | 0.269360 | 0.3204 | — | - | — | - |
| `plist` | 1,623 | 0.623818 | 0.112776 | 0.1250 | — | - | — | - |
| `rust` | 10,373 | 0.424072 | 0.059634 | 0.1043 | — | - | — | - |
| `png` | 15,651 | 0.478360 | 0.134827 | 0.1900 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=50, device=cpu.
- Feature spec: `general/feature_spec.json` (62,607 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: 99.64%
- F1: 0.9971
- ROC AUC: 0.999889
- Average Precision: 0.999915
- Brier: 0.0029
