# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 44 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 860,195-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 860,189-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 48 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 785 / 54 | 0.999069 | 0.992310 | 0.991672 | 100.00% | — |
| [`batch`](filetypes/batch/README.md) | 22,089 / 596 | 0.999971 | 0.998961 | 0.997462 | 99.07% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,246 / 2,728 | 0.996536 | 0.995156 | 0.992182 | 98.84% | — |
| [`elf`](filetypes/elf/README.md) | 22,304 / 21,532 | 0.998827 | 0.998132 | 0.995820 | 98.57% | PR +0.005527 / ROC +0.004832 |
| [`ole`](filetypes/ole/README.md) | 801 / 782 | 0.994612 | 0.992452 | 0.982434 | 97.63% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,501 / 2,934 | 0.999308 | 0.995224 | 0.991966 | 97.39% | PR +0.006008 / ROC +0.004024 |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 243 | 0.998758 | 0.994186 | 0.984505 | 97.10% | — |
| [`xls`](filetypes/xls/README.md) | 4,647 / 2,652 | 0.996396 | 0.993095 | 0.979450 | 95.61% | — |
| [`macho`](filetypes/macho/README.md) | 335 / 1,507 | 0.978134 | 0.994262 | 0.965723 | 95.22% | — |
| [`lnk`](filetypes/lnk/README.md) | 542 / 131 | 0.989686 | 0.956797 | 0.959924 | 92.80% | — |
| [`tar`](filetypes/tar/README.md) | 2,774 / 3,015 | 0.991638 | 0.989293 | 0.968193 | 92.79% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 378 / 15,284 | 0.922643 | 0.955519 | 0.951591 | 91.27% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,436 / 426 | 0.995835 | 0.986581 | 0.976552 | 89.14% | — |
| [`perl`](filetypes/perl/README.md) | 39 / 4,975 | 0.846825 | 0.950396 | 0.880000 | 84.62% | — |
| [`shell`](filetypes/shell/README.md) | 1,893 / 7,497 | 0.971702 | 0.986702 | 0.949171 | 84.42% | — |
| [`docx`](filetypes/docx/README.md) | 563 / 58 | 0.987224 | 0.892463 | 0.951014 | 83.48% | — |
| [`powershell`](filetypes/powershell/README.md) | 650 / 308 | 0.974456 | 0.956508 | 0.959877 | 81.85% | — |
| [`jar`](filetypes/jar/README.md) | 454 / 456 | 0.962932 | 0.955710 | 0.901472 | 81.50% | — |
| [`rust`](filetypes/rust/README.md) | 188 / 11,023 | 0.014090 | 0.405252 | 0.032985 | 71.28% | — |
| [`pe`](filetypes/pe/README.md) | 163,879 / 19,967 | 0.999492 | 0.996007 | 0.992106 | 70.24% | PR +0.001192 / ROC -0.002193 |
| [`python`](filetypes/python/README.md) | 2,596 / 24,934 | 0.804912 | 0.874002 | 0.827333 | 65.68% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,917 / 6,462 | 0.959368 | 0.964995 | 0.902733 | 65.48% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,609 / 76,386 | 0.943062 | 0.970392 | 0.904429 | 64.32% | — |
| [`php`](filetypes/php/README.md) | 671 / 18,441 | 0.774651 | 0.909579 | 0.805438 | 63.64% | — |
| [`zip`](filetypes/zip/README.md) | 12,628 / 1,457 | 0.976185 | 0.809351 | 0.956347 | 57.23% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,425 / 198 | 0.997488 | 0.940077 | 0.996242 | 47.03% | — |
| [`java_class`](filetypes/java_class/README.md) | 230 / 88,106 | 0.867670 | 0.945221 | 0.909091 | 36.52% | — |
| [`csharp`](filetypes/csharp/README.md) | 316 / 8,367 | 0.401637 | 0.762928 | 0.455172 | 28.16% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 156 / 3,741 | 0.269359 | 0.737923 | 0.302752 | 17.95% | — |
| [`json`](filetypes/json/README.md) | 113 / 4,504 | 0.022887 | 0.473010 | 0.048027 | 16.81% | — |
| [`java`](filetypes/java/README.md) | 142 / 5,222 | 0.270636 | 0.906573 | 0.328600 | 13.38% | — |
| [`c`](filetypes/c/README.md) | 1,934 / 88,499 | 0.247702 | 0.699687 | 0.327244 | 12.00% | — |
| [`text`](filetypes/text/README.md) | 288 / 11,093 | 0.149998 | 0.627310 | 0.202454 | 11.46% | — |
| [`deb`](filetypes/deb/README.md) | 50 / 903 | 0.156850 | 0.563987 | 0.181818 | 10.00% | — |
| [`go`](filetypes/go/README.md) | 1,305 / 15,232 | 0.393963 | 0.812475 | 0.389910 | 8.43% | — |
| [`plist`](filetypes/plist/README.md) | 75 / 1,600 | 0.218049 | 0.832929 | 0.328889 | 8.00% | — |
| [`png`](filetypes/png/README.md) | 905 / 21,709 | 0.107252 | 0.464587 | 0.123839 | 6.63% | — |
| [`makefile`](filetypes/makefile/README.md) | 75 / 3,434 | 0.078275 | 0.715088 | 0.205128 | 2.67% | — |
| [`xml`](filetypes/xml/README.md) | 437 / 26,007 | 0.169459 | 0.682899 | 0.276023 | 2.52% | — |
| **Weighted avg** (by test pop) | **800,116** | **0.7592** | **0.8900** | **0.7735** | **55.2%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1670971082`, score-table `3403c7f0ff81`, model-set `bab2bd3be60b`. 1 general, 7 filegroup, 48 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
