# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 42 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 633,220-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 633,178-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign`, `suspicious`, or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile and suspicious thresholds at the same level; the deployed default is L3. Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 46 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at a 3 FP/M operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at 3 FP/M** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`batch`](filetypes/batch/README.md) | 21,695 / 457 | 0.999943 | 0.998441 | 0.998641 | 98.82% | — |
| [`rtf`](filetypes/rtf/README.md) | 216 / 51 | 0.999452 | 0.997640 | 0.988290 | 97.69% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 259 / 6,750 | 0.995696 | 0.999764 | 0.990253 | 97.68% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 133 | 0.999123 | 0.995460 | 0.997254 | 97.34% | — |
| [`xls`](filetypes/xls/README.md) | 1,302 / 2,646 | 0.999470 | 0.999738 | 0.985653 | 95.85% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 702 | 0.989845 | 0.994263 | 0.977064 | 91.86% | — |
| [`perl`](filetypes/perl/README.md) | 29 / 4,001 | 0.957916 | 0.998496 | 0.945455 | 89.66% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,200 / 1,563 | 0.999509 | 0.999149 | 0.997041 | 89.14% | — |
| [`elf`](filetypes/elf/README.md) | 10,199 / 18,869 | 0.999353 | 0.999677 | 0.991420 | 88.47% | PR +0.006053 / ROC +0.006377 |
| [`shell`](filetypes/shell/README.md) | 1,093 / 5,958 | 0.973418 | 0.992192 | 0.943089 | 85.82% | — |
| [`macho`](filetypes/macho/README.md) | 274 / 1,403 | 0.992418 | 0.998504 | 0.950998 | 79.20% | — |
| [`lnk`](filetypes/lnk/README.md) | 297 / 131 | 0.970875 | 0.943018 | 0.909938 | 72.39% | — |
| [`javascript`](filetypes/javascript/README.md) | 11,363 / 65,280 | 0.970109 | 0.992084 | 0.926334 | 71.78% | — |
| [`docx`](filetypes/docx/README.md) | 183 / 31 | 0.977481 | 0.914419 | 0.926209 | 70.49% | — |
| [`php`](filetypes/php/README.md) | 537 / 13,350 | 0.881498 | 0.985934 | 0.852941 | 68.90% | — |
| [`java_class`](filetypes/java_class/README.md) | 177 / 55,387 | 0.960505 | 0.984525 | 0.944134 | 67.23% | — |
| [`pe`](filetypes/pe/README.md) | 112,470 / 19,176 | 0.999637 | 0.998163 | 0.993038 | 61.98% | PR +0.001337 / ROC -0.000037 |
| [`jar`](filetypes/jar/README.md) | 225 / 299 | 0.979629 | 0.985269 | 0.933638 | 55.56% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,881 / 5,617 | 0.980499 | 0.981821 | 0.952530 | 51.92% | — |
| [`python`](filetypes/python/README.md) | 2,296 / 16,991 | 0.959959 | 0.991785 | 0.912652 | 50.65% | — |
| [`xml`](filetypes/xml/README.md) | 306 / 19,746 | 0.165250 | 0.768203 | 0.360153 | 28.43% | — |
| [`csharp`](filetypes/csharp/README.md) | 236 / 7,613 | 0.608452 | 0.888167 | 0.594848 | 28.39% | — |
| [`powershell`](filetypes/powershell/README.md) | 372 / 284 | 0.969126 | 0.968338 | 0.939314 | 25.00% | — |
| [`vbs`](filetypes/vbs/README.md) | 555 / 426 | 0.975713 | 0.982103 | 0.959292 | 21.98% | — |
| [`c`](filetypes/c/README.md) | 1,767 / 68,272 | 0.279865 | 0.767449 | 0.332257 | 13.75% | — |
| [`text`](filetypes/text/README.md) | 163 / 8,144 | 0.206690 | 0.751910 | 0.263158 | 13.50% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,310 / 1,743 | 0.999276 | 0.994735 | 0.995153 | 7.08% | PR +0.005976 / ROC +0.003535 |
| [`go`](filetypes/go/README.md) | 1,177 / 12,102 | 0.736098 | 0.954217 | 0.711094 | 5.01% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 131 / 1,344 | 0.587416 | 0.894697 | 0.686667 | 3.05% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1,555 | 0.203533 | 0.693536 | 0.366013 | 2.94% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 10,209 | 0.083821 | 0.679077 | 0.135501 | 1.83% | — |
| [`png`](filetypes/png/README.md) | 660 / 14,991 | 0.141525 | 0.533348 | 0.188235 | 1.36% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1525145935`, score-table `d31a6525e901`, model-set `0aa10f9147eb`. 1 general, 7 filegroup, 46 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
