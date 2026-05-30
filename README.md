# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 700,588-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 700,173-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign`, `suspicious`, or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile and suspicious thresholds at the same level; the deployed default is L3. Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 51 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at a 3 FP/M operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at 3 FP/M** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 139 | 0.999999 | 0.999994 | 0.999608 | 99.84% | — |
| [`batch`](filetypes/batch/README.md) | 21,717 / 473 | 0.999990 | 0.999543 | 0.998688 | 98.71% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 264 / 7,750 | 0.996089 | 0.999828 | 0.988506 | 97.73% | — |
| [`rtf`](filetypes/rtf/README.md) | 263 / 51 | 0.999630 | 0.998136 | 0.990403 | 97.72% | — |
| [`xls`](filetypes/xls/README.md) | 1,639 / 2,647 | 0.996541 | 0.997036 | 0.981696 | 95.24% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,212 / 1,622 | 0.998340 | 0.997531 | 0.995922 | 92.81% | — |
| [`elf`](filetypes/elf/README.md) | 11,097 / 19,285 | 0.999276 | 0.999640 | 0.989281 | 88.84% | PR +0.005976 / ROC +0.006340 |
| [`ole`](filetypes/ole/README.md) | 286 / 714 | 0.992713 | 0.995367 | 0.980462 | 88.46% | — |
| [`macho`](filetypes/macho/README.md) | 276 / 1,409 | 0.993931 | 0.998807 | 0.957486 | 81.52% | — |
| [`shell`](filetypes/shell/README.md) | 1,158 / 6,129 | 0.971603 | 0.991567 | 0.933211 | 81.35% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 2,717 / 63 | 0.998803 | 0.960750 | 0.996150 | 81.08% | — |
| [`deb`](filetypes/deb/README.md) | 28 / 784 | 0.321129 | 0.952920 | 0.529412 | 78.57% | — |
| [`lnk`](filetypes/lnk/README.md) | 309 / 131 | 0.976411 | 0.951654 | 0.919658 | 73.14% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 4,040 | 0.935868 | 0.997931 | 0.945455 | 71.43% | — |
| [`pe`](filetypes/pe/README.md) | 116,874 / 19,246 | 0.999653 | 0.998076 | 0.992848 | 69.12% | PR +0.001353 / ROC -0.000124 |
| [`java_class`](filetypes/java_class/README.md) | 184 / 57,544 | 0.930808 | 0.967033 | 0.947075 | 66.85% | — |
| [`javascript`](filetypes/javascript/README.md) | 11,383 / 67,772 | 0.961654 | 0.989447 | 0.904010 | 65.75% | — |
| [`docx`](filetypes/docx/README.md) | 204 / 42 | 0.972192 | 0.887838 | 0.910941 | 65.20% | — |
| [`jar`](filetypes/jar/README.md) | 241 / 348 | 0.978085 | 0.987212 | 0.940452 | 61.00% | — |
| [`python`](filetypes/python/README.md) | 2,306 / 18,170 | 0.956526 | 0.991105 | 0.909050 | 55.59% | — |
| [`php`](filetypes/php/README.md) | 545 / 13,616 | 0.881028 | 0.986175 | 0.837696 | 54.31% | — |
| [`powershell`](filetypes/powershell/README.md) | 389 / 284 | 0.977268 | 0.970175 | 0.930769 | 53.73% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,892 / 5,971 | 0.976765 | 0.979471 | 0.946106 | 48.30% | — |
| [`vbs`](filetypes/vbs/README.md) | 611 / 426 | 0.985543 | 0.985714 | 0.967015 | 29.13% | — |
| [`csharp`](filetypes/csharp/README.md) | 239 / 8,097 | 0.489080 | 0.898768 | 0.489712 | 28.03% | — |
| [`makefile`](filetypes/makefile/README.md) | 40 / 2,796 | 0.410799 | 0.796245 | 0.491803 | 25.00% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,329 / 2,089 | 0.998852 | 0.992404 | 0.994386 | 12.71% | PR +0.005552 / ROC +0.001204 |
| [`jpeg`](filetypes/jpeg/README.md) | 132 / 2,259 | 0.244771 | 0.680992 | 0.292398 | 12.12% | — |
| [`c`](filetypes/c/README.md) | 1,776 / 70,036 | 0.328535 | 0.844979 | 0.345248 | 11.71% | — |
| [`text`](filetypes/text/README.md) | 162 / 8,197 | 0.188747 | 0.689891 | 0.263158 | 7.41% | — |
| [`png`](filetypes/png/README.md) | 657 / 17,396 | 0.148375 | 0.553923 | 0.192405 | 5.63% | — |
| [`rust`](filetypes/rust/README.md) | 165 / 10,264 | 0.118590 | 0.724733 | 0.166667 | 3.03% | — |
| [`xml`](filetypes/xml/README.md) | 313 / 19,968 | 0.282981 | 0.798890 | 0.388007 | 2.24% | — |
| [`go`](filetypes/go/README.md) | 1,179 / 12,119 | 0.647420 | 0.919031 | 0.651447 | 2.12% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,567 | 0.121151 | 0.664767 | 0.189655 | 1.52% | — |
| [`json`](filetypes/json/README.md) | 49 / 3,128 | 0.015423 | 0.500000 | 0.030378 | — | — |
| [`markdown`](filetypes/markdown/README.md) | 41 / 6,639 | 0.007195 | 0.541253 | 0.022556 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1618843881`, score-table `4fe5cbee092b`, model-set `d6cb889521aa`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
