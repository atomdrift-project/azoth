# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 17,755,836-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,214,568-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 52 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 99 | 0.998795 | 0.989432 | 0.986731 | 97.24% | — |
| [`html`](filetypes/html/README.md) | 33 / 14,234 | 0.971096 | 0.998548 | 0.984615 | 96.97% | — |
| `pkg_info` | 1,326 / 2,167 | 0.986187 | 0.983964 | 0.982027 | 96.30% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,634 / 3,964 | 0.995169 | 0.986446 | 0.966296 | 87.67% | — |
| [`elf`](filetypes/elf/README.md) | 24,391 / 102,450 | 0.998302 | 0.999290 | 0.994796 | 85.63% | PR +0.005002 / ROC +0.005990 |
| [`lnk`](filetypes/lnk/README.md) | 578 / 145 | 0.998173 | 0.992895 | 0.988803 | 82.53% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,806 | 0.813703 | 0.918337 | 0.888889 | 80.00% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,602 / 472 | 0.993161 | 0.978380 | 0.960845 | 73.78% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,635 / 8,273 | 0.975759 | 0.981671 | 0.971926 | 73.21% | — |
| [`npm`](filetypes/npm/README.md) | 1,320 / 4,625 | 0.950248 | 0.969267 | 0.915836 | 71.97% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,514 / 3,685 | 0.992102 | 0.955713 | 0.954227 | 71.38% | PR -0.001198 / ROC -0.035487 |
| [`tar`](filetypes/tar/README.md) | 3,171 / 9,491 | 0.962778 | 0.974519 | 0.922802 | 69.00% | — |
| [`macho`](filetypes/macho/README.md) | 367 / 4,045 | 0.964608 | 0.986403 | 0.943978 | 65.40% | — |
| [`pe`](filetypes/pe/README.md) | 170,064 / 29,615 | 0.999160 | 0.995243 | 0.988357 | 60.89% | PR +0.000860 / ROC -0.002957 |
| [`shell`](filetypes/shell/README.md) | 2,410 / 20,186 | 0.928366 | 0.962798 | 0.896611 | 60.83% | — |
| [`jar`](filetypes/jar/README.md) | 510 / 3,755 | 0.908096 | 0.957338 | 0.885417 | 59.80% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 86 / 108 | 0.975623 | 0.977498 | 0.918605 | 55.81% | — |
| `python_bytecode` | 465 / 127,818 | 0.647748 | 0.829607 | 0.752604 | 55.70% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,888 / 10,626 | 0.940041 | 0.963984 | 0.887391 | 54.94% | — |
| [`powershell`](filetypes/powershell/README.md) | 732 / 703 | 0.969876 | 0.955494 | 0.945889 | 54.51% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 769 | 0.945050 | 0.964131 | 0.885077 | 54.27% | — |
| [`python`](filetypes/python/README.md) | 2,916 / 80,277 | 0.765238 | 0.897311 | 0.790797 | 50.79% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,507 / 208,370 | 0.898030 | 0.954199 | 0.874528 | 50.04% | — |
| [`php`](filetypes/php/README.md) | 853 / 76,665 | 0.719948 | 0.914451 | 0.746556 | 43.73% | — |
| [`whl`](filetypes/whl/README.md) | 531 / 2,085 | 0.844974 | 0.903001 | 0.790099 | 43.69% | — |
| `gem` | 252 / 1,167 | 0.513402 | 0.479003 | 0.586592 | 41.27% | — |
| `java_class` | 290 / 216,435 | 0.786342 | 0.945110 | 0.844697 | 39.31% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,118 | 0.537495 | 0.817844 | 0.589744 | 36.00% | — |
| [`zip`](filetypes/zip/README.md) | 13,815 / 5,470 | 0.936013 | 0.834188 | 0.845653 | 33.40% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,190 | 0.564469 | 0.797513 | 0.682353 | 30.77% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 354 | 0.993797 | 0.893250 | 0.989936 | 30.15% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,688 | 0.336966 | 0.687067 | 0.398671 | 23.18% | — |
| [`batch`](filetypes/batch/README.md) | 22,140 / 1,009 | 0.993855 | 0.921087 | 0.993050 | 15.47% | — |
| `c` | 2,291 / 210,576 | 0.245003 | 0.656718 | 0.349833 | 13.14% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 180 / 5,606 | 0.216413 | 0.620118 | 0.287037 | 10.56% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 3,422 | 0.136081 | 0.516140 | 0.194444 | 10.34% | — |
| `png` | 1,087 / 66,319 | 0.055128 | 0.423021 | 0.104452 | 5.61% | — |
| [`xml`](filetypes/xml/README.md) | 499 / 57,301 | 0.089662 | 0.490208 | 0.158621 | 4.81% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,729 | 0.137042 | 0.711800 | 0.160000 | 4.56% | — |
| `plist` | 80 / 12,563 | 0.009802 | 0.595535 | 0.030356 | 3.75% | — |
| `makefile` | 102 / 7,867 | 0.013536 | 0.391194 | 0.042254 | 2.94% | — |
| [`text`](filetypes/text/README.md) | 490 / 40,554 | 0.058548 | 0.619777 | 0.089347 | 1.84% | — |
| [`json`](filetypes/json/README.md) | 304 / 31,764 | 0.066359 | 0.627456 | 0.099762 | 1.64% | — |
| [`go`](filetypes/go/README.md) | 2,087 / 29,402 | 0.252209 | 0.641372 | 0.265702 | 1.39% | — |
| `rust` | 259 / 41,732 | 0.076613 | 0.624072 | 0.136126 | 1.16% | — |
| [`7z`](filetypes/7z/README.md) | 1,170 / 28 | 0.998791 | 0.952442 | 0.989429 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 42 | 0.983590 | 0.933264 | 0.955437 | — | — |
| **Weighted avg** (by test pop) | **1,853,174** | **0.6539** | **0.8394** | **0.6845** | **41.0%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `3998018903`, score-table `db64f7c9c981`, model-set `fb945c77c4d8`. 1 general, 6 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
