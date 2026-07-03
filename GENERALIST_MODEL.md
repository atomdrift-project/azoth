# Azoth — Generalist Model

One LightGBM classifier trained on the entire labeled corpus, every supported filetype mixed together. The point of having a generalist is that some files don't fit any specialist's domain, and a single model across all of them establishes a floor.

The generalist alone is not what gets deployed. It is one route in the ensemble — see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). The numbers here are reported for transparency, and to line up directly against the "All files" row in EMBER 2024 (Joyce et al., *KDD'25*, Table 5).

## Per-filetype performance

Generalist model scored on each filetype's slice of the locked test partition (12.5% holdout, SHA256-deterministic, disjoint from training and dev calibration). EMBER columns reference Joyce et al.'s "All files → X" rows where they exist.

| File type | Files | ROC AUC | PR AUC | F1 | EMBER ROC (All files → X) | Δ ROC | EMBER PR | Δ PR |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **all files** | 1608866 | 0.921373 | 0.816267 | 0.8405 | 0.9969 | -0.075527 | 0.9971 | -0.180833 |
| `elf` | 72,810 | 0.952186 | 0.821558 | 0.9429 | 0.9887 | -0.036514 | 0.9902 | -0.168642 |
| `pe` | 192,805 | 0.846209 | 0.967021 | 0.9395 | 0.9982 | -0.151991 | 0.9983 | -0.031279 |
| `rtf` | 924 | 0.995335 | 0.999471 | 0.9878 | — | - | — | - |
| `pdf` | 25,938 | 0.921275 | 0.979565 | 0.9782 | 0.9878 | -0.066525 | 0.9901 | -0.010535 |
| `ole_doc` | 14,489 | 0.965500 | 0.986421 | 0.9536 | — | - | — | - |
| `batch` | 23,073 | 0.669701 | 0.982650 | 0.9874 | — | - | — | - |
| `vbs` | 2,018 | 0.907252 | 0.947818 | 0.9436 | — | - | — | - |
| `html` | 2,041 | 0.999326 | 0.976489 | 0.9524 | — | - | — | - |
| `lnk` | 701 | 0.940672 | 0.982588 | 0.9632 | — | - | — | - |
| `zip` | 15,818 | 0.532501 | 0.822843 | 0.9070 | — | - | — | - |
| `package.json` | 7,851 | 0.929179 | 0.808581 | 0.9031 | — | - | — | - |
| `pkg_info` | 2,662 | 0.984270 | 0.985666 | 0.9746 | — | - | — | - |
| `ooxml` | 8,909 | 0.474018 | 0.967060 | 0.9799 | — | - | — | - |
| `tar` | 10,038 | 0.796682 | 0.488707 | 0.7758 | — | - | — | - |
| `gem` | 324 | 0.874412 | 0.700437 | 0.8571 | — | - | — | - |
| `powershell` | 1,291 | 0.916359 | 0.920209 | 0.9100 | — | - | — | - |
| `kotlin` | 12,970 | 0.917360 | 0.860075 | 0.7842 | — | - | — | - |
| `macho` | 3,031 | 0.816506 | 0.314055 | 0.4970 | — | - | — | - |
| `shell` | 18,356 | 0.902861 | 0.597103 | 0.8051 | — | - | — | - |
| `whl` | 1,072 | 0.799075 | 0.624703 | 0.7898 | — | - | — | - |
| `npm` | 932 | 0.771344 | 0.712567 | 0.7705 | — | - | — | - |
| `jar` | 2,129 | 0.761582 | 0.549498 | 0.6900 | — | - | — | - |
| `javascript` | 165,792 | 0.917941 | 0.667488 | 0.8194 | — | - | — | - |
| `java_class` | 188,416 | 0.946997 | 0.444830 | 0.6355 | — | - | — | - |
| `perl` | 8,150 | 0.831200 | 0.217967 | 0.4690 | — | - | — | - |
| `registry` | 9,010 | 0.997504 | 0.749091 | 0.7191 | — | - | — | - |
| `python` | 64,504 | 0.870896 | 0.543100 | 0.7364 | — | - | — | - |
| `php` | 68,154 | 0.866785 | 0.275262 | 0.4919 | — | - | — | - |
| `python_bytecode` | 82,119 | 0.901236 | 0.279793 | 0.6056 | — | - | — | - |
| `cargo.toml` | 873 | 0.662139 | 0.379389 | 0.4375 | — | - | — | - |
| `ruby` | 21,006 | 0.786299 | 0.101135 | 0.2097 | — | - | — | - |
| `csharp` | 11,591 | 0.657178 | 0.166703 | 0.3304 | — | - | — | - |
| `go` | 28,398 | 0.472204 | 0.152931 | 0.2349 | — | - | — | - |
| `jpeg` | 5,571 | 0.583371 | 0.179181 | 0.2379 | — | - | — | - |
| `deb` | 2,393 | 0.425893 | 0.022687 | 0.0547 | — | - | — | - |
| `xml` | 50,166 | 0.690892 | 0.040989 | 0.1245 | — | - | — | - |
| `text` | 32,313 | 0.520828 | 0.047368 | 0.1127 | — | - | — | - |
| `json` | 18,902 | 0.500178 | 0.040995 | 0.1210 | — | - | — | - |
| `png` | 46,448 | 0.583099 | 0.085166 | 0.1269 | — | - | — | - |
| `c` | 170,988 | 0.545082 | 0.074608 | 0.2693 | — | - | — | - |
| `crx` | 404 | 0.898338 | 0.903244 | 0.8814 | — | - | — | - |
| `dockerfile` | 566 | 0.679519 | 0.173144 | 0.2917 | — | - | — | - |
| `java` | 19,730 | 0.442543 | 0.027803 | 0.0754 | — | - | — | - |
| `makefile` | 7,494 | 0.635768 | 0.026559 | 0.0609 | — | - | — | - |
| `plist` | 12,039 | 0.463222 | 0.025431 | 0.0531 | — | - | — | - |
| `rust` | 39,893 | 0.521197 | 0.024405 | 0.1003 | — | - | — | - |

## Training

- Algorithm: LightGBM binary classifier: estimators=?, num_leaves=?, max_depth=?, min_child_samples=?, learning_rate=?, subsample=?, colsample=?, reg_alpha=?, reg_lambda=?, early_stop=?, device=cpu.
- Feature spec: `general/feature_spec.json` (229 features)
- Split: 75% train / 12.5% dev / 12.5% test, SHA256-deterministic. The model is fit on train. Calibrators and L0..L20 thresholds are fit on dev. The numbers above come from test.

## Training-time evaluation

The training pipeline reports metrics on a hard-pool holdout — a curated subset of train, used for early stopping and hyperparameter selection. These numbers run hot because the pool is selected for difficulty during training, not after. The per-filetype table above is the better reference for production expectations.

- Accuracy: -
- F1: -
- ROC AUC: -
- Average Precision: -
- Brier: -
