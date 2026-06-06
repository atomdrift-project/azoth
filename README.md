# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 42 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 6,720,544-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 837,332-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 46 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`makefile`](filetypes/makefile/README.md) | 68 / 3,263 | 0.020220 | 0.495099 | 0.040012 | 98.53% | — |
| [`rtf`](filetypes/rtf/README.md) | 784 / 53 | 0.999501 | 0.992371 | 0.993614 | 97.45% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 354 / 10,858 | 0.980249 | 0.991574 | 0.985673 | 97.18% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 230 | 0.995445 | 0.980845 | 0.984114 | 95.46% | — |
| [`xls`](filetypes/xls/README.md) | 4,629 / 2,652 | 0.992549 | 0.985416 | 0.976319 | 94.08% | — |
| [`elf`](filetypes/elf/README.md) | 22,216 / 20,670 | 0.998603 | 0.998066 | 0.993676 | 93.84% | PR +0.005303 / ROC +0.004766 |
| [`package.json`](filetypes/package.json/README.md) | 2,244 / 2,581 | 0.995097 | 0.993934 | 0.991932 | 90.06% | — |
| [`shell`](filetypes/shell/README.md) | 1,872 / 7,344 | 0.973256 | 0.986018 | 0.953778 | 88.41% | — |
| [`tar`](filetypes/tar/README.md) | 2,762 / 2,835 | 0.990604 | 0.987980 | 0.960766 | 87.07% | — |
| [`ole`](filetypes/ole/README.md) | 792 / 778 | 0.980549 | 0.978495 | 0.955763 | 83.96% | — |
| [`lnk`](filetypes/lnk/README.md) | 538 / 131 | 0.969518 | 0.910866 | 0.910192 | 83.46% | — |
| [`docx`](filetypes/docx/README.md) | 562 / 58 | 0.992904 | 0.935222 | 0.954628 | 81.32% | — |
| [`macho`](filetypes/macho/README.md) | 334 / 1,486 | 0.973738 | 0.987729 | 0.950156 | 78.14% | — |
| [`perl`](filetypes/perl/README.md) | 36 / 4,913 | 0.913371 | 0.995214 | 0.895522 | 72.22% | — |
| [`java_class`](filetypes/java_class/README.md) | 221 / 88,047 | 0.918092 | 0.964565 | 0.924883 | 71.95% | — |
| [`javascript`](filetypes/javascript/README.md) | 14,438 / 73,486 | 0.947179 | 0.974736 | 0.909866 | 60.70% | — |
| [`pe`](filetypes/pe/README.md) | 163,459 / 19,929 | 0.999552 | 0.996557 | 0.991645 | 59.36% | PR +0.001252 / ROC -0.001643 |
| [`jar`](filetypes/jar/README.md) | 445 / 452 | 0.966684 | 0.961798 | 0.906250 | 54.83% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,901 / 6,364 | 0.949256 | 0.956926 | 0.893154 | 52.65% | — |
| [`python`](filetypes/python/README.md) | 2,432 / 22,754 | 0.822842 | 0.903360 | 0.840632 | 51.15% | — |
| [`php`](filetypes/php/README.md) | 640 / 18,231 | 0.753830 | 0.886066 | 0.772556 | 49.69% | — |
| [`powershell`](filetypes/powershell/README.md) | 636 / 306 | 0.979839 | 0.960954 | 0.952455 | 45.75% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,428 / 426 | 0.991114 | 0.977677 | 0.963605 | 44.33% | — |
| [`zip`](filetypes/zip/README.md) | 12,586 / 1,429 | 0.993683 | 0.951918 | 0.970919 | 33.38% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,394 / 198 | 0.989645 | 0.725576 | 0.986788 | 31.05% | — |
| [`csharp`](filetypes/csharp/README.md) | 242 / 8,141 | 0.403490 | 0.687490 | 0.502674 | 26.45% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,499 / 2,923 | 0.991359 | 0.937976 | 0.959122 | 20.34% | PR -0.001941 / ROC -0.053224 |
| [`jpeg`](filetypes/jpeg/README.md) | 151 / 3,720 | 0.209926 | 0.591801 | 0.305263 | 13.25% | — |
| [`c`](filetypes/c/README.md) | 1,793 / 83,253 | 0.253899 | 0.637491 | 0.339044 | 12.66% | — |
| [`text`](filetypes/text/README.md) | 214 / 10,483 | 0.174945 | 0.558287 | 0.252964 | 11.68% | — |
| [`deb`](filetypes/deb/README.md) | 45 / 872 | 0.165312 | 0.577472 | 0.200000 | 11.11% | — |
| [`go`](filetypes/go/README.md) | 1,238 / 15,176 | 0.664198 | 0.889494 | 0.703673 | 6.79% | — |
| [`png`](filetypes/png/README.md) | 811 / 21,106 | 0.111983 | 0.544168 | 0.136519 | 6.54% | — |
| [`rust`](filetypes/rust/README.md) | 167 / 10,881 | 0.030291 | 0.469490 | 0.083770 | 4.79% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,584 | 0.105511 | 0.610523 | 0.153846 | 3.03% | — |
| [`xml`](filetypes/xml/README.md) | 393 / 25,634 | 0.251497 | 0.643517 | 0.376754 | 1.78% | — |
| [`batch`](filetypes/batch/README.md) | 22,079 / 556 | 0.997429 | 0.950240 | 0.997236 | 1.31% | — |
| [`json`](filetypes/json/README.md) | 103 / 3,859 | 0.035524 | 0.572865 | 0.089744 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1658771605`, score-table `02f59097455e`, model-set `19acbcd12d15`. 1 general, 7 filegroup, 46 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
