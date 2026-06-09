# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 905,238-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 905,195-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 51 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`package.json`](filetypes/package.json/README.md) | 2,265 / 2,939 | 0.996038 | 0.994621 | 0.991351 | 98.68% | — |
| [`elf`](filetypes/elf/README.md) | 22,443 / 22,231 | 0.999959 | 0.999958 | 0.997816 | 98.61% | PR +0.006659 / ROC +0.006658 |
| [`rtf`](filetypes/rtf/README.md) | 790 / 54 | 0.999028 | 0.990811 | 0.990440 | 98.35% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 290 | 0.997379 | 0.990438 | 0.984505 | 97.34% | — |
| [`xls`](filetypes/xls/README.md) | 4,671 / 2,652 | 0.997489 | 0.994983 | 0.983843 | 96.75% | — |
| [`ole`](filetypes/ole/README.md) | 809 / 792 | 0.991560 | 0.990686 | 0.971928 | 95.06% | — |
| [`macho`](filetypes/macho/README.md) | 339 / 1,575 | 0.989074 | 0.995414 | 0.960486 | 93.51% | — |
| [`tar`](filetypes/tar/README.md) | 2,802 / 3,332 | 0.991980 | 0.990758 | 0.972122 | 91.65% | — |
| [`perl`](filetypes/perl/README.md) | 39 / 5,403 | 0.780660 | 0.938491 | 0.833333 | 87.18% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 401 / 23,635 | 0.881610 | 0.933825 | 0.926372 | 86.28% | — |
| [`shell`](filetypes/shell/README.md) | 1,937 / 7,925 | 0.981003 | 0.991566 | 0.948758 | 85.70% | — |
| [`lnk`](filetypes/lnk/README.md) | 543 / 132 | 0.974909 | 0.924194 | 0.912525 | 84.53% | — |
| [`powershell`](filetypes/powershell/README.md) | 670 / 312 | 0.989650 | 0.981262 | 0.956329 | 84.48% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,450 / 428 | 0.990742 | 0.971461 | 0.957193 | 84.00% | — |
| [`docx`](filetypes/docx/README.md) | 568 / 58 | 0.985098 | 0.902623 | 0.951424 | 82.92% | — |
| [`jar`](filetypes/jar/README.md) | 458 / 481 | 0.957082 | 0.949764 | 0.894063 | 81.22% | — |
| [`pe`](filetypes/pe/README.md) | 164,518 / 20,130 | 0.999732 | 0.997979 | 0.992642 | 80.18% | PR +0.001432 / ROC -0.000221 |
| [`whl`](filetypes/whl/README.md) | 25 / 109 | 0.827203 | 0.859450 | 0.863636 | 80.00% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,502 / 2,947 | 0.994101 | 0.959645 | 0.980548 | 75.08% | PR +0.000801 / ROC -0.031555 |
| [`java_class`](filetypes/java_class/README.md) | 238 / 93,690 | 0.867556 | 0.976400 | 0.896104 | 71.85% | — |
| [`makefile`](filetypes/makefile/README.md) | 85 / 3,834 | 0.063499 | 0.724748 | 0.116923 | 67.06% | — |
| [`php`](filetypes/php/README.md) | 708 / 19,409 | 0.787665 | 0.896228 | 0.811641 | 65.54% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,813 / 79,726 | 0.952145 | 0.970806 | 0.913010 | 63.80% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,937 / 6,848 | 0.952628 | 0.953752 | 0.907835 | 53.44% | — |
| [`zip`](filetypes/zip/README.md) | 12,676 / 1,500 | 0.995341 | 0.965585 | 0.978018 | 52.64% | — |
| [`python`](filetypes/python/README.md) | 2,760 / 26,860 | 0.811413 | 0.898790 | 0.816367 | 48.59% | — |
| [`batch`](filetypes/batch/README.md) | 22,100 / 708 | 0.999008 | 0.985415 | 0.997197 | 40.72% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,472 / 201 | 0.989237 | 0.715955 | 0.986728 | 40.28% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 25 / 210 | 0.452268 | 0.806286 | 0.432432 | 32.00% | — |
| [`csharp`](filetypes/csharp/README.md) | 392 / 8,373 | 0.426004 | 0.854818 | 0.403194 | 25.77% | — |
| [`deb`](filetypes/deb/README.md) | 50 / 947 | 0.151786 | 0.565723 | 0.181818 | 22.00% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 168 / 3,803 | 0.234056 | 0.619184 | 0.271028 | 16.07% | — |
| [`go`](filetypes/go/README.md) | 1,377 / 15,709 | 0.651638 | 0.913686 | 0.650451 | 11.55% | — |
| [`c`](filetypes/c/README.md) | 2,106 / 95,882 | 0.241599 | 0.678211 | 0.332842 | 11.40% | — |
| [`java`](filetypes/java/README.md) | 307 / 7,146 | 0.223605 | 0.703803 | 0.310777 | 10.75% | — |
| [`text`](filetypes/text/README.md) | 381 / 13,134 | 0.125632 | 0.583393 | 0.160377 | 8.92% | — |
| [`plist`](filetypes/plist/README.md) | 77 / 1,610 | 0.137455 | 0.690453 | 0.231760 | 6.49% | — |
| [`png`](filetypes/png/README.md) | 1,023 / 22,239 | 0.114131 | 0.534153 | 0.132901 | 5.96% | — |
| [`rust`](filetypes/rust/README.md) | 213 / 12,612 | 0.080521 | 0.597279 | 0.105727 | 5.63% | — |
| [`xml`](filetypes/xml/README.md) | 491 / 27,109 | 0.236301 | 0.696699 | 0.337043 | 2.65% | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 36 | 0.621083 | 0.695513 | 0.650000 | — | — |
| [`json`](filetypes/json/README.md) | 129 / 5,421 | 0.050291 | 0.692587 | 0.125330 | 0.00% | — |
| **Weighted avg** (by test pop) | **842,493** | **0.7591** | **0.8941** | **0.7732** | **56.7%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1679491877`, score-table `e1c363b3c523`, model-set `282016a8ca91`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
