# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 924,631-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 924,639-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| [`package.json`](filetypes/package.json/README.md) | 2,267 / 2,923 | 0.994611 | 0.993833 | 0.991567 | 98.72% | — |
| [`elf`](filetypes/elf/README.md) | 22,552 / 22,610 | 0.999967 | 0.999967 | 0.998183 | 98.70% | PR +0.006667 / ROC +0.006667 |
| [`rtf`](filetypes/rtf/README.md) | 791 / 55 | 0.999190 | 0.992380 | 0.991714 | 98.61% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 289 | 0.997339 | 0.992042 | 0.984114 | 97.18% | — |
| [`xls`](filetypes/xls/README.md) | 4,697 / 2,652 | 0.996478 | 0.993103 | 0.981650 | 95.74% | — |
| [`ole`](filetypes/ole/README.md) | 813 / 799 | 0.990201 | 0.987403 | 0.964736 | 94.22% | — |
| [`macho`](filetypes/macho/README.md) | 341 / 1,570 | 0.990760 | 0.997086 | 0.958209 | 94.13% | — |
| [`tar`](filetypes/tar/README.md) | 2,803 / 3,396 | 0.990702 | 0.988846 | 0.972610 | 93.04% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,457 / 428 | 0.994072 | 0.979777 | 0.965940 | 88.19% | — |
| [`jar`](filetypes/jar/README.md) | 459 / 489 | 0.976535 | 0.970905 | 0.926554 | 85.40% | — |
| [`shell`](filetypes/shell/README.md) | 1,950 / 8,082 | 0.981518 | 0.992548 | 0.944919 | 84.97% | — |
| [`lnk`](filetypes/lnk/README.md) | 547 / 132 | 0.970041 | 0.910628 | 0.911243 | 84.46% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 415 / 24,307 | 0.860267 | 0.923657 | 0.910995 | 83.86% | — |
| [`docx`](filetypes/docx/README.md) | 569 / 59 | 0.984881 | 0.902818 | 0.950710 | 82.95% | — |
| [`perl`](filetypes/perl/README.md) | 41 / 5,328 | 0.778519 | 0.952405 | 0.857143 | 82.93% | — |
| [`powershell`](filetypes/powershell/README.md) | 677 / 312 | 0.986205 | 0.973639 | 0.947130 | 79.76% | — |
| [`pe`](filetypes/pe/README.md) | 164,925 / 20,260 | 0.999811 | 0.998505 | 0.993660 | 78.56% | PR +0.001511 / ROC +0.000305 |
| [`pdf`](filetypes/pdf/README.md) | 22,502 / 2,976 | 0.997619 | 0.984700 | 0.987153 | 77.61% | PR +0.004319 / ROC -0.006500 |
| [`whl`](filetypes/whl/README.md) | 40 / 113 | 0.880577 | 0.908186 | 0.816901 | 77.50% | — |
| [`java_class`](filetypes/java_class/README.md) | 240 / 98,272 | 0.862492 | 0.970076 | 0.890351 | 72.92% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,888 / 81,081 | 0.949398 | 0.972367 | 0.918019 | 64.27% | — |
| [`php`](filetypes/php/README.md) | 713 / 19,535 | 0.788621 | 0.901515 | 0.799039 | 62.97% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,949 / 6,907 | 0.894704 | 0.892491 | 0.819619 | 59.74% | — |
| [`zip`](filetypes/zip/README.md) | 12,704 / 1,536 | 0.992934 | 0.951935 | 0.974662 | 51.66% | — |
| [`python`](filetypes/python/README.md) | 2,824 / 27,179 | 0.784781 | 0.889486 | 0.807281 | 50.53% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,500 / 201 | 0.989124 | 0.704629 | 0.986777 | 48.71% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 28 / 173 | 0.480521 | 0.723472 | 0.476190 | 39.29% | — |
| [`deb`](filetypes/deb/README.md) | 51 / 965 | 0.156376 | 0.618145 | 0.178571 | 23.53% | — |
| [`batch`](filetypes/batch/README.md) | 22,107 / 689 | 0.993379 | 0.892862 | 0.995555 | 22.07% | — |
| [`csharp`](filetypes/csharp/README.md) | 418 / 9,682 | 0.361684 | 0.796223 | 0.380952 | 20.57% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 176 / 3,849 | 0.195308 | 0.551994 | 0.247191 | 12.50% | — |
| [`java`](filetypes/java/README.md) | 361 / 9,905 | 0.224363 | 0.770404 | 0.271255 | 11.36% | — |
| [`c`](filetypes/c/README.md) | 2,143 / 97,740 | 0.259418 | 0.721339 | 0.336933 | 11.11% | — |
| [`go`](filetypes/go/README.md) | 1,396 / 16,015 | 0.655281 | 0.890141 | 0.673492 | 10.82% | — |
| [`xml`](filetypes/xml/README.md) | 507 / 28,364 | 0.227565 | 0.643907 | 0.320127 | 9.07% | — |
| [`rust`](filetypes/rust/README.md) | 228 / 11,902 | 0.073313 | 0.627739 | 0.107256 | 7.46% | — |
| [`plist`](filetypes/plist/README.md) | 82 / 1,623 | 0.123874 | 0.680244 | 0.187970 | 6.10% | — |
| [`png`](filetypes/png/README.md) | 1,053 / 22,769 | 0.121775 | 0.540747 | 0.184040 | 5.70% | — |
| [`text`](filetypes/text/README.md) | 598 / 13,216 | 0.118292 | 0.574295 | 0.126685 | 5.69% | — |
| [`makefile`](filetypes/makefile/README.md) | 88 / 3,996 | 0.026964 | 0.576065 | 0.054735 | 2.27% | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 36 | 0.629290 | 0.651175 | 0.658228 | — | — |
| [`json`](filetypes/json/README.md) | 134 / 6,384 | 0.020451 | 0.505392 | 0.041825 | 0.00% | — |
| **Weighted avg** (by test pop) | **860,136** | **0.7525** | **0.8903** | **0.7674** | **55.6%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1685037226`, score-table `ac994141c20e`, model-set `1497dc36d07f`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
