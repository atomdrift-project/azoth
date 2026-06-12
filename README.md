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
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 289 | 0.997742 | 0.994288 | 0.997262 | 99.84% | — |
| [`batch`](filetypes/batch/README.md) | 22,107 / 689 | 0.999857 | 0.996784 | 0.996464 | 99.22% | — |
| [`rtf`](filetypes/rtf/README.md) | 791 / 55 | 0.999830 | 0.997851 | 0.993711 | 98.74% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,267 / 2,923 | 0.996159 | 0.994956 | 0.991563 | 98.63% | — |
| [`elf`](filetypes/elf/README.md) | 22,552 / 22,610 | 0.999749 | 0.999727 | 0.996181 | 98.26% | PR +0.006449 / ROC +0.006427 |
| [`ole`](filetypes/ole/README.md) | 813 / 799 | 0.992103 | 0.989840 | 0.983323 | 97.54% | — |
| [`xls`](filetypes/xls/README.md) | 4,697 / 2,652 | 0.997302 | 0.994475 | 0.982120 | 95.87% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,502 / 2,976 | 0.999230 | 0.994895 | 0.991786 | 95.19% | PR +0.005930 / ROC +0.003695 |
| [`macho`](filetypes/macho/README.md) | 341 / 1,570 | 0.989643 | 0.996457 | 0.959881 | 94.72% | — |
| [`tar`](filetypes/tar/README.md) | 2,806 / 3,396 | 0.990485 | 0.988615 | 0.972081 | 92.94% | — |
| [`docx`](filetypes/docx/README.md) | 569 / 59 | 0.995897 | 0.962006 | 0.962766 | 89.81% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,457 / 428 | 0.989471 | 0.964695 | 0.953878 | 86.62% | — |
| [`lnk`](filetypes/lnk/README.md) | 547 / 132 | 0.978449 | 0.914001 | 0.908184 | 86.11% | — |
| [`shell`](filetypes/shell/README.md) | 1,950 / 8,082 | 0.961324 | 0.971304 | 0.934527 | 84.56% | — |
| [`powershell`](filetypes/powershell/README.md) | 677 / 312 | 0.982531 | 0.963056 | 0.949025 | 83.90% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 415 / 24,307 | 0.860267 | 0.923657 | 0.910995 | 83.86% | — |
| [`jar`](filetypes/jar/README.md) | 459 / 489 | 0.957499 | 0.950294 | 0.889148 | 81.05% | — |
| [`perl`](filetypes/perl/README.md) | 41 / 5,328 | 0.797411 | 0.904517 | 0.868421 | 80.49% | — |
| [`whl`](filetypes/whl/README.md) | 25 / 113 | 0.877791 | 0.939469 | 0.800000 | 80.00% | — |
| [`pe`](filetypes/pe/README.md) | 164,925 / 20,260 | 0.999730 | 0.997972 | 0.993953 | 77.41% | PR +0.001430 / ROC -0.000228 |
| [`php`](filetypes/php/README.md) | 713 / 19,535 | 0.763809 | 0.906155 | 0.789216 | 62.69% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,888 / 81,081 | 0.939382 | 0.967077 | 0.905482 | 62.33% | — |
| [`java_class`](filetypes/java_class/README.md) | 240 / 98,272 | 0.867228 | 0.935053 | 0.887912 | 62.08% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,949 / 6,907 | 0.935706 | 0.944403 | 0.857182 | 60.45% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,500 / 201 | 0.997635 | 0.939629 | 0.995552 | 56.65% | — |
| [`zip`](filetypes/zip/README.md) | 12,722 / 1,543 | 0.977777 | 0.845316 | 0.951743 | 54.54% | — |
| [`python`](filetypes/python/README.md) | 2,824 / 27,179 | 0.775423 | 0.882112 | 0.799606 | 50.78% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 28 / 173 | 0.399475 | 0.493910 | 0.439024 | 35.71% | — |
| [`csharp`](filetypes/csharp/README.md) | 418 / 9,682 | 0.361684 | 0.796223 | 0.380952 | 20.57% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 176 / 3,849 | 0.227757 | 0.653780 | 0.294372 | 15.91% | — |
| [`json`](filetypes/json/README.md) | 134 / 6,384 | 0.019074 | 0.464031 | 0.040723 | 15.67% | — |
| [`plist`](filetypes/plist/README.md) | 82 / 1,623 | 0.217863 | 0.797623 | 0.286604 | 12.20% | — |
| [`deb`](filetypes/deb/README.md) | 51 / 965 | 0.155467 | 0.583603 | 0.178571 | 9.80% | — |
| [`java`](filetypes/java/README.md) | 361 / 9,905 | 0.293856 | 0.817326 | 0.346154 | 9.14% | — |
| [`c`](filetypes/c/README.md) | 2,143 / 97,740 | 0.247023 | 0.687838 | 0.328618 | 9.01% | — |
| [`xml`](filetypes/xml/README.md) | 507 / 28,364 | 0.049353 | 0.476542 | 0.142857 | 8.68% | — |
| [`text`](filetypes/text/README.md) | 598 / 13,216 | 0.232636 | 0.797062 | 0.264023 | 7.02% | — |
| [`go`](filetypes/go/README.md) | 1,396 / 16,015 | 0.330400 | 0.727444 | 0.329919 | 7.02% | — |
| [`rust`](filetypes/rust/README.md) | 228 / 11,902 | 0.072417 | 0.631177 | 0.102894 | 7.02% | — |
| [`png`](filetypes/png/README.md) | 1,053 / 22,769 | 0.191663 | 0.676274 | 0.235294 | 6.46% | — |
| [`makefile`](filetypes/makefile/README.md) | 88 / 3,996 | 0.026964 | 0.576065 | 0.054735 | 2.27% | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 36 | 0.629290 | 0.651175 | 0.658228 | — | — |
| **Weighted avg** (by test pop) | **860,149** | **0.7423** | **0.8844** | **0.7565** | **56.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1685037226`, score-table `a776ec2e200d`, model-set `8c5f0deaefcf`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
