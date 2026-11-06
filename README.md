# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 66 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 2,652,880-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,653,916-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [Atomdrift Scan](https://github.com/atomdrift-project/scan). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Scan reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (one FP plus an estimated additional 24 FP/100M). Lower levels tighten the operating point; higher levels loosen it.

## False-positive levels

For N benign files, L0 allows zero observed calibration FPs; positive L has a continuous allowance `1 + (L - 1) * N / 100_000_000`, rounded down for an integer count budget. L1 allows one FP; L25 adds an estimated 24 FP/100M beyond that initial FP. Components share the final filetype decision allowance. These are calibration targets, not guaranteed future rates; interpolated or extrapolated estimates and uncertainty are separate from observed counts. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md).

Only detection regressions at L0 through L25 (inclusive) can block model acceptance. Higher levels remain reportable. Calibration allowances apply at every level; empirical test FP overruns do not block installation by default.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 60 `filegroups/<name>/`, or one of 70 `filetypes/<name>/`. A route directory carries a `models/seed_*.onnx` ensemble (LightGBM trees exported to ONNX, one file per training seed) and `feature_spec.json` (the features those models expect). Scores are the models' raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row reports the frozen routing policy on the locked test partition. PR AUC and ROC AUC rank signed policy margins; F1 and recall measure actual decisions at L25 (one FP plus an estimated additional 24 FP/100M). Observed false-positive rates can differ from the dev calibration target.

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Selection and reporting.** Models train on train; thresholds and routing policies are selected on dev using the exported production ensembles. Test measures those saved decisions. An ensemble can perform worse than a specialist on test; the report preserves that result.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 820 / 117 | 0.999770 | 0.998890 | 0.997555 | 99.51% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,166 / 10,579 | 0.990593 | 0.997525 | 0.971685 | 99.18% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,778 | 0.999846 | 0.999039 | 0.993962 | 98.87% | PR +0.006546 / ROC +0.007839 |
| [`batch`](filetypes/batch/README.md) | 22,314 / 1,166 | 0.999988 | 0.999766 | 0.992301 | 98.48% | — |
| [`elf`](filetypes/elf/README.md) | 24,963 / 113,471 | 0.999907 | 0.999970 | 0.991029 | 98.24% | PR +0.006607 / ROC +0.006670 |
| [`vbs`](filetypes/vbs/README.md) | 1,867 / 549 | 0.999197 | 0.997437 | 0.985999 | 98.07% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 500 / 120 | 0.943654 | 0.846317 | 0.949612 | 98.00% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,049 / 4,156 | 0.999601 | 0.998949 | 0.985962 | 97.89% | — |
| [`html`](filetypes/html/README.md) | 11,515 / 54,283 | 0.999664 | 0.999912 | 0.987215 | 97.57% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 367 / 1,578 | 0.998755 | 0.999698 | 0.980769 | 97.28% | — |
| [`lnk`](filetypes/lnk/README.md) | 577 / 154 | 0.999493 | 0.998087 | 0.979700 | 96.19% | — |
| [`7z`](filetypes/7z/README.md) | 1,123 / 51 | 0.998557 | 0.970300 | 0.973636 | 95.37% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,455 / 824 | 0.990183 | 0.933438 | 0.960977 | 93.49% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 72 / 1,750 | 0.916442 | 0.976857 | 0.924138 | 93.06% | — |
| [`jar`](filetypes/jar/README.md) | 480 / 5,255 | 0.970287 | 0.996474 | 0.923890 | 91.04% | — |
| [`registry`](filetypes/registry/README.md) | 59 / 13,680 | 0.960257 | 0.999609 | 0.936937 | 88.14% | — |
| [`shell`](filetypes/shell/README.md) | 2,434 / 21,622 | 0.991230 | 0.997185 | 0.933684 | 87.63% | — |
| [`gem`](filetypes/gem/README.md) | 51 / 15,048 | 0.919039 | 0.998225 | 0.926316 | 86.27% | — |
| [`ruby`](filetypes/ruby/README.md) | 34 / 24,725 | 0.924036 | 0.995627 | 0.892308 | 85.29% | — |
| [`macho`](filetypes/macho/README.md) | 336 / 4,794 | 0.975633 | 0.997149 | 0.900158 | 84.52% | — |
| [`pe`](filetypes/pe/README.md) | 204,108 / 33,876 | 0.999912 | 0.999476 | 0.907856 | 83.13% | PR +0.001612 / ROC +0.001276 |
| [`perl`](filetypes/perl/README.md) | 56 / 10,190 | 0.948574 | 0.998649 | 0.884615 | 82.14% | — |
| [`php`](filetypes/php/README.md) | 762 / 78,548 | 0.971207 | 0.998044 | 0.894203 | 80.97% | — |
| [`json`](filetypes/json/README.md) | 36 / 39,083 | 0.801853 | 0.989885 | 0.591837 | 80.56% | — |
| [`java_class`](filetypes/java_class/README.md) | 285 / 229,241 | 0.924679 | 0.985040 | 0.882012 | 80.00% | — |
| [`ico`](filetypes/ico/README.md) | 29 / 106 | 0.966201 | 0.967794 | 0.884615 | 79.31% | — |
| [`powershell`](filetypes/powershell/README.md) | 770 / 802 | 0.995978 | 0.995867 | 0.867841 | 76.75% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 403 / 154,295 | 0.940567 | 0.998587 | 0.825911 | 75.93% | — |
| [`java`](filetypes/java/README.md) | 412 / 25,210 | 0.978580 | 0.997263 | 0.846154 | 74.76% | — |
| [`npm`](filetypes/npm/README.md) | 3,657 / 44,299 | 0.975211 | 0.994746 | 0.854147 | 74.62% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,666 / 9,682 | 0.998714 | 0.999123 | 0.833516 | 71.46% | — |
| [`tar`](filetypes/tar/README.md) | 1,908 / 13,561 | 0.978276 | 0.995454 | 0.820370 | 69.65% | — |
| [`go`](filetypes/go/README.md) | 1,097 / 32,127 | 0.888644 | 0.985283 | 0.805085 | 69.28% | — |
| [`gif`](filetypes/gif/README.md) | 63 / 250 | 0.879635 | 0.983841 | 0.767857 | 68.25% | — |
| [`python`](filetypes/python/README.md) | 2,626 / 85,335 | 0.951566 | 0.995435 | 0.803815 | 67.40% | — |
| [`zip`](filetypes/zip/README.md) | 13,616 / 18,261 | 0.997275 | 0.997823 | 0.802287 | 66.99% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,072 / 227,771 | 0.990639 | 0.998502 | 0.800610 | 66.80% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 30 / 2,329 | 0.942761 | 0.986954 | 0.784314 | 66.67% | — |
| [`crx`](filetypes/crx/README.md) | 296 / 1,560 | 0.963461 | 0.992758 | 0.763860 | 62.84% | — |
| [`vsix`](filetypes/vsix/README.md) | 40 / 780 | 0.729178 | 0.924776 | 0.718750 | 57.50% | — |
| [`png`](filetypes/png/README.md) | 959 / 68,483 | 0.952665 | 0.997774 | 0.662500 | 49.74% | — |
| [`rust`](filetypes/rust/README.md) | 59 / 45,706 | 0.402433 | 0.978676 | 0.345238 | 49.15% | — |
| [`xml`](filetypes/xml/README.md) | 213 / 55,874 | 0.750013 | 0.989597 | 0.621951 | 47.89% | — |
| [`whl`](filetypes/whl/README.md) | 321 / 8,602 | 0.879848 | 0.990908 | 0.594360 | 42.68% | — |
| [`csharp`](filetypes/csharp/README.md) | 438 / 12,895 | 0.947917 | 0.997883 | 0.593301 | 42.47% | — |
| [`c`](filetypes/c/README.md) | 2,103 / 221,834 | 0.865593 | 0.996583 | 0.537445 | 37.71% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 172 / 5,674 | 0.635015 | 0.962135 | 0.475000 | 33.14% | — |
| [`text`](filetypes/text/README.md) | 801 / 63,059 | 0.863466 | 0.992734 | 0.390390 | 24.34% | — |
| **Weighted avg** (by test pop) | **2,135,793** | **0.9335** | **0.9950** | **0.7950** | **71.1%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (one FP plus an estimated additional 24 FP/100M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (pool-adjusted)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `6309383805`, score-table `3397c7e39abb`, model-set `5007a4abbfe6`. 1 general, 60 filegroup, 70 filetype routes.

## Limits

- The level is a pool-adjusted calibration target. Interpolation or extrapolation does not guarantee the future FP rate; more representative benign data improves rate estimation.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
