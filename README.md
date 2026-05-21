# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 592,592-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 592,338-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign`, `suspicious`, or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile and suspicious thresholds at the same level; the deployed default is L3. Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 38 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at a 3 FP/M operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at 3 FP/M** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 114 | 0.999189 | 0.995322 | 0.999216 | 99.84% | — |
| [`batch`](filetypes/batch/README.md) | 21,128 / 427 | 0.999949 | 0.998643 | 0.999148 | 99.39% | — |
| [`elf`](filetypes/elf/README.md) | 9,026 / 17,067 | 0.999989 | 0.999994 | 0.998671 | 98.59% | PR +0.006689 / ROC +0.006694 |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3,863 | 0.996366 | 0.999703 | 0.991342 | 98.28% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 664 | 0.993075 | 0.995421 | 0.988713 | 98.19% | — |
| [`rtf`](filetypes/rtf/README.md) | 215 / 51 | 0.999827 | 0.999316 | 0.995370 | 98.14% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 2,845 / 5,355 | 0.998171 | 0.998315 | 0.990302 | 97.19% | — |
| [`pdf`](filetypes/pdf/README.md) | 21,801 / 1,734 | 0.999954 | 0.999445 | 0.997544 | 97.04% | PR +0.006654 / ROC +0.008245 |
| [`package.json`](filetypes/package.json/README.md) | 2,162 / 1,439 | 0.999736 | 0.999496 | 0.997454 | 93.34% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3,959 | 0.965883 | 0.999314 | 0.962963 | 92.86% | — |
| [`shell`](filetypes/shell/README.md) | 950 / 5,694 | 0.986966 | 0.997138 | 0.969828 | 92.42% | — |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47,377 | 0.915496 | 0.982355 | 0.943284 | 91.33% | — |
| [`macho`](filetypes/macho/README.md) | 262 / 1,383 | 0.998792 | 0.999771 | 0.988593 | 88.93% | — |
| [`javascript`](filetypes/javascript/README.md) | 10,529 / 59,667 | 0.992660 | 0.998261 | 0.972287 | 78.27% | — |
| [`pe`](filetypes/pe/README.md) | 110,244 / 18,952 | 0.999979 | 0.999880 | 0.998771 | 78.03% | PR +0.001679 / ROC +0.001680 |
| [`docx`](filetypes/docx/README.md) | 176 / 31 | 0.977220 | 0.918530 | 0.919060 | 77.84% | — |
| [`jar`](filetypes/jar/README.md) | 215 / 237 | 0.990034 | 0.990717 | 0.946387 | 71.63% | — |
| [`php`](filetypes/php/README.md) | 519 / 10,871 | 0.989303 | 0.998369 | 0.960707 | 70.33% | — |
| [`vbs`](filetypes/vbs/README.md) | 462 / 423 | 0.998390 | 0.998383 | 0.988210 | 69.26% | — |
| [`lnk`](filetypes/lnk/README.md) | 261 / 127 | 0.958748 | 0.942710 | 0.920578 | 68.58% | — |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7,572 | 0.951240 | 0.997727 | 0.885965 | 64.10% | — |
| [`python`](filetypes/python/README.md) | 2,272 / 16,343 | 0.986563 | 0.997502 | 0.954217 | 57.75% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1,544 | 0.916016 | 0.986504 | 0.848000 | 52.94% | — |
| [`xml`](filetypes/xml/README.md) | 291 / 18,378 | 0.212186 | 0.893647 | 0.318280 | 24.05% | — |
| [`powershell`](filetypes/powershell/README.md) | 257 / 274 | 0.986730 | 0.990826 | 0.963671 | 17.90% | — |
| [`text`](filetypes/text/README.md) | 160 / 7,992 | 0.192871 | 0.659870 | 0.258065 | 14.37% | — |
| [`go`](filetypes/go/README.md) | 1,177 / 11,867 | 0.868307 | 0.982540 | 0.765319 | 13.08% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 9,604 | 0.152262 | 0.834783 | 0.246220 | 11.59% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 127 / 1,319 | 0.277459 | 0.655833 | 0.313953 | 8.66% | — |
| [`c`](filetypes/c/README.md) | 1,766 / 66,647 | 0.525525 | 0.935285 | 0.538895 | 0.91% | — |
| [`png`](filetypes/png/README.md) | 657 / 14,388 | 0.192414 | 0.687783 | 0.217160 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1384435807`, score-table `2366b041b18b`, model-set `5c2f3d449a67`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
