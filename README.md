# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 812,880-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 812,235-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| [`rtf`](filetypes/rtf/README.md) | 668 / 51 | 0.999906 | 0.998826 | 0.995522 | 98.65% | — |
| [`batch`](filetypes/batch/README.md) | 21,996 / 517 | 0.999939 | 0.998417 | 0.998205 | 97.88% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 339 / 9,150 | 0.980914 | 0.986802 | 0.986587 | 97.35% | — |
| [`xls`](filetypes/xls/README.md) | 3,911 / 2,651 | 0.996493 | 0.994561 | 0.978861 | 94.30% | — |
| [`ole`](filetypes/ole/README.md) | 670 / 730 | 0.994733 | 0.994418 | 0.984940 | 92.24% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,221 / 2,056 | 0.997937 | 0.997965 | 0.993476 | 92.12% | — |
| [`elf`](filetypes/elf/README.md) | 19,689 / 20,507 | 0.999232 | 0.999356 | 0.988157 | 90.93% | PR +0.005932 / ROC +0.006056 |
| [`docx`](filetypes/docx/README.md) | 482 / 57 | 0.990084 | 0.934393 | 0.960084 | 90.87% | — |
| [`lnk`](filetypes/lnk/README.md) | 485 / 131 | 0.988323 | 0.963359 | 0.943277 | 82.47% | — |
| [`shell`](filetypes/shell/README.md) | 1,698 / 6,644 | 0.976347 | 0.992420 | 0.926017 | 77.56% | — |
| [`perl`](filetypes/perl/README.md) | 34 / 4,171 | 0.960247 | 0.996682 | 0.941176 | 76.47% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 169 | 0.998861 | 0.995434 | 0.999218 | 75.72% | — |
| [`java_class`](filetypes/java_class/README.md) | 218 / 83,138 | 0.911677 | 0.957283 | 0.870813 | 68.81% | — |
| [`html`](filetypes/html/README.md) | 25 / 3,225 | 0.842500 | 0.987882 | 0.809524 | 68.00% | — |
| [`macho`](filetypes/macho/README.md) | 318 / 1,454 | 0.991453 | 0.998062 | 0.948553 | 65.09% | — |
| [`jar`](filetypes/jar/README.md) | 383 / 421 | 0.984948 | 0.985078 | 0.955844 | 63.97% | — |
| [`javascript`](filetypes/javascript/README.md) | 12,246 / 69,937 | 0.961624 | 0.989364 | 0.892591 | 61.42% | — |
| [`php`](filetypes/php/README.md) | 561 / 14,766 | 0.909065 | 0.984746 | 0.873917 | 61.32% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 6,279 / 164 | 0.998918 | 0.968712 | 0.997775 | 58.66% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,204 / 427 | 0.997009 | 0.992430 | 0.985927 | 56.73% | — |
| [`python`](filetypes/python/README.md) | 2,342 / 20,185 | 0.951387 | 0.990140 | 0.900294 | 49.70% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,924 / 6,277 | 0.971734 | 0.972481 | 0.933491 | 43.35% | — |
| [`powershell`](filetypes/powershell/README.md) | 568 / 290 | 0.982171 | 0.973431 | 0.952215 | 41.55% | — |
| [`pe`](filetypes/pe/README.md) | 153,040 / 19,950 | 0.998995 | 0.992862 | 0.991954 | 38.26% | PR +0.000695 / ROC -0.005338 |
| [`csharp`](filetypes/csharp/README.md) | 241 / 8,112 | 0.613942 | 0.924408 | 0.601010 | 28.22% | — |
| [`xml`](filetypes/xml/README.md) | 373 / 22,164 | 0.220244 | 0.813514 | 0.407351 | 27.35% | — |
| [`text`](filetypes/text/README.md) | 170 / 8,705 | 0.217550 | 0.617390 | 0.287129 | 13.53% | — |
| [`go`](filetypes/go/README.md) | 1,182 / 13,310 | 0.750159 | 0.952502 | 0.681283 | 11.93% | — |
| [`deb`](filetypes/deb/README.md) | 42 / 845 | 0.508063 | 0.963609 | 0.601626 | 11.90% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,463 / 2,674 | 0.999172 | 0.994687 | 0.993616 | 10.36% | PR +0.005872 / ROC +0.003487 |
| [`c`](filetypes/c/README.md) | 1,779 / 73,290 | 0.287412 | 0.828180 | 0.325415 | 9.44% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 148 / 3,284 | 0.285710 | 0.709584 | 0.339286 | 5.41% | — |
| [`rust`](filetypes/rust/README.md) | 166 / 10,339 | 0.084107 | 0.720135 | 0.127764 | 3.61% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,576 | 0.127602 | 0.719952 | 0.181818 | 1.52% | — |
| [`png`](filetypes/png/README.md) | 672 / 18,697 | 0.137176 | 0.588413 | 0.179183 | 1.04% | — |
| [`makefile`](filetypes/makefile/README.md) | 59 / 2,913 | 0.431977 | 0.873958 | 0.561798 | 0.00% | — |
| [`json`](filetypes/json/README.md) | 92 / 3,865 | 0.051997 | 0.509942 | 0.080808 | 0.00% | — |
| [`markdown`](filetypes/markdown/README.md) | 41 / 7,507 | 0.006681 | 0.589958 | 0.016667 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose dev slice cannot resolve L50 (0.5 FP/M) empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1634431848`, score-table `314fcce37125`, model-set `47ffaa1fe2e1`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 600 FP/100M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
