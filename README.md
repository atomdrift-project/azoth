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
| [`rtf`](filetypes/rtf/README.md) | 790 / 54 | 0.998918 | 0.991045 | 0.990440 | 100.00% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 290 | 0.998881 | 0.997251 | 0.996873 | 99.84% | — |
| [`batch`](filetypes/batch/README.md) | 22,100 / 708 | 0.999953 | 0.998584 | 0.996553 | 99.25% | — |
| [`elf`](filetypes/elf/README.md) | 22,443 / 22,231 | 0.999410 | 0.999521 | 0.995857 | 98.80% | PR +0.006110 / ROC +0.006221 |
| [`package.json`](filetypes/package.json/README.md) | 2,265 / 2,939 | 0.996038 | 0.994621 | 0.991351 | 98.68% | — |
| [`ole`](filetypes/ole/README.md) | 809 / 792 | 0.993639 | 0.990718 | 0.985723 | 98.15% | — |
| [`xls`](filetypes/xls/README.md) | 4,671 / 2,652 | 0.996209 | 0.992593 | 0.981157 | 95.80% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,502 / 2,947 | 0.999294 | 0.994837 | 0.990941 | 95.56% | PR +0.005994 / ROC +0.003637 |
| [`macho`](filetypes/macho/README.md) | 339 / 1,575 | 0.980041 | 0.990382 | 0.961424 | 94.69% | — |
| [`tar`](filetypes/tar/README.md) | 2,823 / 3,332 | 0.992959 | 0.993144 | 0.970919 | 94.05% | — |
| [`shell`](filetypes/shell/README.md) | 1,937 / 7,925 | 0.971878 | 0.985079 | 0.946720 | 88.13% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,450 / 428 | 0.990760 | 0.969214 | 0.954019 | 87.10% | — |
| [`docx`](filetypes/docx/README.md) | 568 / 58 | 0.987472 | 0.932734 | 0.964413 | 86.62% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 401 / 23,635 | 0.888578 | 0.943650 | 0.925134 | 86.53% | — |
| [`lnk`](filetypes/lnk/README.md) | 543 / 132 | 0.986677 | 0.947828 | 0.941071 | 86.00% | — |
| [`perl`](filetypes/perl/README.md) | 39 / 5,403 | 0.838257 | 0.944233 | 0.868421 | 84.62% | — |
| [`jar`](filetypes/jar/README.md) | 458 / 481 | 0.957082 | 0.949764 | 0.894063 | 81.22% | — |
| [`powershell`](filetypes/powershell/README.md) | 670 / 312 | 0.985446 | 0.970121 | 0.950301 | 80.90% | — |
| [`pe`](filetypes/pe/README.md) | 164,518 / 20,130 | 0.999545 | 0.996569 | 0.991709 | 78.85% | PR +0.001245 / ROC -0.001631 |
| [`php`](filetypes/php/README.md) | 708 / 19,409 | 0.744384 | 0.896034 | 0.773698 | 63.98% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,813 / 79,726 | 0.937615 | 0.964016 | 0.897870 | 62.30% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,937 / 6,848 | 0.958998 | 0.966111 | 0.898506 | 62.08% | — |
| [`java_class`](filetypes/java_class/README.md) | 238 / 93,690 | 0.875538 | 0.959819 | 0.894382 | 56.72% | — |
| [`zip`](filetypes/zip/README.md) | 12,698 / 1,500 | 0.994492 | 0.962798 | 0.972960 | 56.62% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,472 / 201 | 0.997355 | 0.933198 | 0.996199 | 52.45% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 25 / 210 | 0.550891 | 0.899143 | 0.607595 | 48.00% | — |
| [`python`](filetypes/python/README.md) | 2,760 / 26,860 | 0.781372 | 0.886889 | 0.793487 | 44.49% | — |
| [`json`](filetypes/json/README.md) | 129 / 5,421 | 0.022211 | 0.477137 | 0.045623 | 37.21% | — |
| [`csharp`](filetypes/csharp/README.md) | 392 / 8,373 | 0.426004 | 0.854818 | 0.403194 | 25.77% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 168 / 3,803 | 0.234056 | 0.619184 | 0.271028 | 16.07% | — |
| [`c`](filetypes/c/README.md) | 2,106 / 95,882 | 0.241588 | 0.675896 | 0.333088 | 10.40% | — |
| [`deb`](filetypes/deb/README.md) | 50 / 947 | 0.154787 | 0.590665 | 0.181818 | 10.00% | — |
| [`text`](filetypes/text/README.md) | 381 / 13,134 | 0.125632 | 0.583393 | 0.160377 | 8.92% | — |
| [`java`](filetypes/java/README.md) | 307 / 7,146 | 0.165212 | 0.698217 | 0.206186 | 8.79% | — |
| [`go`](filetypes/go/README.md) | 1,377 / 15,709 | 0.358152 | 0.796953 | 0.376669 | 8.28% | — |
| [`plist`](filetypes/plist/README.md) | 77 / 1,610 | 0.076549 | 0.519811 | 0.115418 | 7.79% | — |
| [`png`](filetypes/png/README.md) | 1,023 / 22,239 | 0.185242 | 0.659876 | 0.232246 | 6.45% | — |
| [`rust`](filetypes/rust/README.md) | 213 / 12,612 | 0.094939 | 0.711864 | 0.153034 | 5.16% | — |
| [`makefile`](filetypes/makefile/README.md) | 85 / 3,834 | 0.098032 | 0.766731 | 0.215768 | 4.71% | — |
| [`xml`](filetypes/xml/README.md) | 491 / 27,109 | 0.135591 | 0.690276 | 0.178899 | 2.85% | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 36 | 0.621083 | 0.695513 | 0.650000 | — | — |
| **Weighted avg** (by test pop) | **842,402** | **0.7492** | **0.8954** | **0.7612** | **56.7%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1679491877`, score-table `e5c2398d107a`, model-set `784dd0c8b6c5`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
