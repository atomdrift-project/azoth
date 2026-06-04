# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 45 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 6,710,141-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 836,005-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L4 (0.04 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 49 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L4 (0.04 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L4 (0.04 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L4 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 784 / 53 | 0.999933 | 0.999061 | 0.997455 | 98.47% | — |
| [`batch`](filetypes/batch/README.md) | 22,076 / 557 | 0.999890 | 0.997477 | 0.998008 | 97.80% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 354 / 10,701 | 0.980966 | 0.984966 | 0.988604 | 97.74% | — |
| [`xls`](filetypes/xls/README.md) | 4,625 / 2,652 | 0.997915 | 0.996455 | 0.984058 | 93.10% | — |
| [`elf`](filetypes/elf/README.md) | 22,208 / 20,659 | 0.999955 | 0.999952 | 0.997281 | 92.00% | PR +0.006655 / ROC +0.006652 |
| [`package.json`](filetypes/package.json/README.md) | 2,231 / 2,579 | 0.999216 | 0.998998 | 0.996416 | 89.87% | — |
| [`docx`](filetypes/docx/README.md) | 562 / 58 | 0.995047 | 0.961728 | 0.969259 | 88.61% | — |
| [`tar`](filetypes/tar/README.md) | 2,760 / 2,815 | 0.992525 | 0.992578 | 0.953229 | 88.55% | — |
| [`ole`](filetypes/ole/README.md) | 791 / 778 | 0.989440 | 0.986261 | 0.987906 | 84.58% | — |
| [`lnk`](filetypes/lnk/README.md) | 537 / 131 | 0.984087 | 0.948889 | 0.942119 | 83.61% | — |
| [`macho`](filetypes/macho/README.md) | 334 / 1,486 | 0.946065 | 0.970268 | 0.956386 | 83.53% | — |
| [`shell`](filetypes/shell/README.md) | 1,868 / 7,336 | 0.989815 | 0.996508 | 0.955670 | 83.03% | — |
| [`perl`](filetypes/perl/README.md) | 36 / 4,912 | 0.958588 | 0.999067 | 0.957746 | 77.78% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 225 | 0.998913 | 0.996876 | 0.999218 | 76.51% | — |
| [`jar`](filetypes/jar/README.md) | 443 / 451 | 0.988579 | 0.987958 | 0.946408 | 70.65% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,329 / 73,436 | 0.959539 | 0.986645 | 0.896892 | 65.79% | — |
| [`pe`](filetypes/pe/README.md) | 163,397 / 19,933 | 0.999442 | 0.995817 | 0.993475 | 57.37% | PR +0.001142 / ROC -0.002383 |
| [`php`](filetypes/php/README.md) | 566 / 18,259 | 0.878471 | 0.984543 | 0.844221 | 54.42% | — |
| [`python`](filetypes/python/README.md) | 2,362 / 22,592 | 0.958004 | 0.990974 | 0.907305 | 51.95% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,896 / 6,375 | 0.979601 | 0.981061 | 0.943346 | 49.10% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,428 / 426 | 0.994165 | 0.986979 | 0.986072 | 42.30% | — |
| [`powershell`](filetypes/powershell/README.md) | 633 / 306 | 0.985617 | 0.973304 | 0.953271 | 40.60% | — |
| [`java_class`](filetypes/java_class/README.md) | 221 / 88,038 | 0.889600 | 0.960752 | 0.907801 | 39.82% | — |
| [`zip`](filetypes/zip/README.md) | 12,583 / 1,426 | 0.984213 | 0.884591 | 0.970666 | 30.59% | — |
| [`csharp`](filetypes/csharp/README.md) | 242 / 8,141 | 0.541540 | 0.914501 | 0.563591 | 29.34% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,384 / 198 | 0.998081 | 0.953191 | 0.997702 | 20.50% | — |
| [`makefile`](filetypes/makefile/README.md) | 67 / 3,260 | 0.512894 | 0.882955 | 0.563107 | 14.93% | — |
| [`text`](filetypes/text/README.md) | 196 / 10,485 | 0.125968 | 0.563585 | 0.222222 | 12.76% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,499 / 2,922 | 0.999061 | 0.993830 | 0.993202 | 11.17% | PR +0.005761 / ROC +0.002630 |
| [`deb`](filetypes/deb/README.md) | 45 / 874 | 0.095950 | 0.699771 | 0.188235 | 11.11% | — |
| [`c`](filetypes/c/README.md) | 1,781 / 83,259 | 0.314030 | 0.808489 | 0.340576 | 7.13% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 151 / 3,733 | 0.216741 | 0.682526 | 0.333333 | 4.64% | — |
| [`rust`](filetypes/rust/README.md) | 166 / 10,730 | 0.083435 | 0.658620 | 0.141527 | 3.01% | — |
| [`xml`](filetypes/xml/README.md) | 392 / 25,662 | 0.023069 | 0.585518 | 0.041570 | 2.30% | — |
| [`go`](filetypes/go/README.md) | 1,183 / 15,122 | 0.458703 | 0.895488 | 0.486216 | 2.03% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,586 | 0.106145 | 0.566973 | 0.176101 | 1.52% | — |
| [`png`](filetypes/png/README.md) | 682 / 21,152 | 0.141163 | 0.640491 | 0.190955 | 1.32% | — |
| [`json`](filetypes/json/README.md) | 100 / 3,761 | 0.109585 | 0.858648 | 0.173421 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@L4 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L4 (0.04 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. The vertical dashed line marks the L4 deploy operating point.

## Provenance

Calibration snapshot `1658031131`, score-table `4f6c4213bd3d`, model-set `ac3213ebbab1`. 1 general, 7 filegroup, 49 filetype routes.

## Limits

- Strict L0..L4 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
