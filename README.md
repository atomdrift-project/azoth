# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 822,241-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 821,686-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can derive a suspicious band as crit/4 if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 51 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 691 / 51 | 0.995017 | 0.962217 | 0.991292 | 98.55% | — |
| [`batch`](filetypes/batch/README.md) | 22,011 / 520 | 0.999940 | 0.998434 | 0.998184 | 98.51% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 343 / 9,233 | 0.982285 | 0.987253 | 0.989691 | 97.67% | — |
| [`xls`](filetypes/xls/README.md) | 4,076 / 2,651 | 0.997862 | 0.996402 | 0.983313 | 94.23% | — |
| [`ole`](filetypes/ole/README.md) | 700 / 737 | 0.991028 | 0.987145 | 0.966596 | 92.86% | — |
| [`elf`](filetypes/elf/README.md) | 20,227 / 20,699 | 0.999294 | 0.999353 | 0.987453 | 91.07% | PR +0.005994 / ROC +0.006053 |
| [`package.json`](filetypes/package.json/README.md) | 2,222 / 2,136 | 0.998068 | 0.998202 | 0.993010 | 90.86% | — |
| [`docx`](filetypes/docx/README.md) | 501 / 58 | 0.993115 | 0.952543 | 0.959677 | 89.02% | — |
| [`shell`](filetypes/shell/README.md) | 1,745 / 6,761 | 0.982907 | 0.993411 | 0.952381 | 87.97% | — |
| [`lnk`](filetypes/lnk/README.md) | 497 / 131 | 0.990246 | 0.969235 | 0.950000 | 82.70% | — |
| [`macho`](filetypes/macho/README.md) | 326 / 1,462 | 0.986217 | 0.995999 | 0.943750 | 81.60% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,470 / 2,715 | 0.999215 | 0.993958 | 0.990967 | 73.72% | PR +0.005915 / ROC +0.002758 |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 172 | 0.998890 | 0.995834 | 0.998826 | 72.91% | — |
| [`perl`](filetypes/perl/README.md) | 34 / 4,191 | 0.929933 | 0.994414 | 0.939394 | 70.59% | — |
| [`html`](filetypes/html/README.md) | 25 / 3,225 | 0.853379 | 0.987957 | 0.809524 | 68.00% | — |
| [`javascript`](filetypes/javascript/README.md) | 12,360 / 70,684 | 0.962079 | 0.988702 | 0.890704 | 66.76% | — |
| [`pe`](filetypes/pe/README.md) | 155,642 / 19,955 | 0.999488 | 0.996354 | 0.991928 | 65.64% | PR +0.001188 / ROC -0.001846 |
| [`php`](filetypes/php/README.md) | 561 / 15,056 | 0.916493 | 0.990022 | 0.868726 | 64.88% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,254 / 427 | 0.996040 | 0.991046 | 0.984252 | 61.80% | — |
| [`jar`](filetypes/jar/README.md) | 402 / 428 | 0.984229 | 0.984813 | 0.950739 | 55.47% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,927 / 6,300 | 0.973192 | 0.974576 | 0.946777 | 48.03% | — |
| [`python`](filetypes/python/README.md) | 2,343 / 20,510 | 0.952485 | 0.990974 | 0.909735 | 47.33% | — |
| [`java_class`](filetypes/java_class/README.md) | 219 / 83,812 | 0.891368 | 0.938837 | 0.882483 | 46.58% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 6,526 / 169 | 0.998234 | 0.953044 | 0.997782 | 45.14% | — |
| [`powershell`](filetypes/powershell/README.md) | 578 / 299 | 0.982718 | 0.972029 | 0.949628 | 40.48% | — |
| [`csharp`](filetypes/csharp/README.md) | 241 / 8,112 | 0.498704 | 0.893766 | 0.492424 | 29.88% | — |
| [`text`](filetypes/text/README.md) | 171 / 8,772 | 0.216145 | 0.794111 | 0.262626 | 15.20% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 149 / 3,363 | 0.245616 | 0.626634 | 0.331658 | 14.09% | — |
| [`c`](filetypes/c/README.md) | 1,780 / 74,226 | 0.257355 | 0.718849 | 0.336832 | 12.70% | — |
| [`deb`](filetypes/deb/README.md) | 42 / 849 | 0.483167 | 0.962687 | 0.596774 | 11.90% | — |
| [`markdown`](filetypes/markdown/README.md) | 41 / 7,657 | 0.100426 | 0.548196 | 0.175439 | 9.76% | — |
| [`go`](filetypes/go/README.md) | 1,182 / 13,714 | 0.719687 | 0.936762 | 0.720032 | 6.51% | — |
| [`rust`](filetypes/rust/README.md) | 166 / 10,346 | 0.077101 | 0.681424 | 0.126214 | 3.01% | — |
| [`png`](filetypes/png/README.md) | 673 / 18,998 | 0.133374 | 0.486791 | 0.192802 | 2.67% | — |
| [`xml`](filetypes/xml/README.md) | 380 / 22,297 | 0.171847 | 0.754569 | 0.242950 | 2.37% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,581 | 0.114625 | 0.618289 | 0.166667 | 1.52% | — |
| [`json`](filetypes/json/README.md) | 93 / 3,935 | 0.065329 | 0.490574 | 0.082474 | 0.00% | — |
| [`makefile`](filetypes/makefile/README.md) | 60 / 2,952 | 0.024043 | 0.500344 | 0.078212 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose dev slice cannot resolve L50 (0.5 FP/M) empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1637343931`, score-table `db0577dd7a1b`, model-set `9c5050c6d2b3`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 600 FP/100M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
