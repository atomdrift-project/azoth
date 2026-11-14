# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 68 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 2,658,700-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,659,751-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [Atomdrift Scan](https://github.com/atomdrift-project/scan). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Scan reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (one FP plus an estimated additional 24 FP/100M). Lower levels tighten the operating point; higher levels loosen it.

## False-positive levels

For N benign files, L0 allows zero observed calibration FPs; positive L has a continuous allowance `1 + (L - 1) * N / 100_000_000`, rounded down for an integer count budget. L1 allows one FP; L25 adds an estimated 24 FP/100M beyond that initial FP. Components share the final filetype decision allowance. These are calibration targets, not guaranteed future rates; interpolated or extrapolated estimates and uncertainty are separate from observed counts. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md).

Only detection regressions at L0 through L25 (inclusive) can block model acceptance. Higher levels remain reportable. Calibration allowances apply at every level; empirical test FP overruns do not block installation by default.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 60 `filegroups/<name>/`, or one of 72 `filetypes/<name>/`. A route directory carries a `models/seed_*.onnx` ensemble (LightGBM trees exported to ONNX, one file per training seed) and `feature_spec.json` (the features those models expect). Scores are the models' raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row reports the frozen routing policy on the locked test partition. PR AUC and ROC AUC rank signed policy margins; F1 and recall measure actual decisions at L25 (one FP plus an estimated additional 24 FP/100M). Observed false-positive rates can differ from the dev calibration target.

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Selection and reporting.** Models train on train; thresholds and routing policies are selected on dev using the exported production ensembles. Test measures those saved decisions. An ensemble can perform worse than a specialist on test; the report preserves that result.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 820 / 117 | 0.999772 | 0.998958 | 0.997555 | 99.51% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,262 / 10,373 | 0.999103 | 0.999729 | 0.985636 | 98.87% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,778 | 0.999854 | 0.999085 | 0.993737 | 98.82% | PR +0.006554 / ROC +0.007885 |
| [`batch`](filetypes/batch/README.md) | 22,320 / 1,163 | 0.999988 | 0.999768 | 0.993416 | 98.70% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,869 / 551 | 0.999346 | 0.997842 | 0.987369 | 98.29% | — |
| [`elf`](filetypes/elf/README.md) | 25,147 / 113,493 | 0.999904 | 0.999969 | 0.991237 | 98.28% | PR +0.006604 / ROC +0.006669 |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,058 / 4,155 | 0.999587 | 0.998912 | 0.986616 | 97.99% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 517 / 121 | 0.946771 | 0.853989 | 0.950235 | 97.87% | — |
| [`html`](filetypes/html/README.md) | 11,512 / 54,350 | 0.999708 | 0.999927 | 0.988234 | 97.77% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 368 / 1,580 | 0.998163 | 0.999444 | 0.979536 | 97.55% | — |
| [`lnk`](filetypes/lnk/README.md) | 577 / 154 | 0.999508 | 0.998154 | 0.979700 | 96.19% | — |
| [`7z`](filetypes/7z/README.md) | 1,124 / 50 | 0.998247 | 0.966032 | 0.971741 | 94.84% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,460 / 822 | 0.991887 | 0.943586 | 0.967325 | 94.66% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 72 / 1,740 | 0.942337 | 0.995027 | 0.931507 | 94.44% | — |
| [`jar`](filetypes/jar/README.md) | 485 / 5,252 | 0.966046 | 0.996212 | 0.923077 | 90.31% | — |
| [`gem`](filetypes/gem/README.md) | 51 / 14,932 | 0.924489 | 0.993325 | 0.948454 | 90.20% | — |
| [`registry`](filetypes/registry/README.md) | 59 / 13,680 | 0.962478 | 0.999629 | 0.936937 | 88.14% | — |
| [`shell`](filetypes/shell/README.md) | 2,447 / 21,731 | 0.990913 | 0.996801 | 0.932665 | 87.45% | — |
| [`macho`](filetypes/macho/README.md) | 336 / 4,794 | 0.970368 | 0.996286 | 0.898596 | 85.71% | — |
| [`perl`](filetypes/perl/README.md) | 56 / 10,188 | 0.956404 | 0.997783 | 0.903846 | 83.93% | — |
| [`json`](filetypes/json/README.md) | 36 / 39,110 | 0.796450 | 0.989998 | 0.582524 | 83.33% | — |
| [`php`](filetypes/php/README.md) | 764 / 78,554 | 0.969910 | 0.998157 | 0.905714 | 82.98% | — |
| [`pe`](filetypes/pe/README.md) | 205,788 / 33,895 | 0.999916 | 0.999501 | 0.905780 | 82.78% | PR +0.001616 / ROC +0.001301 |
| [`zip`](filetypes/zip/README.md) | 13,684 / 17,977 | 0.997431 | 0.997869 | 0.890681 | 80.32% | — |
| [`java_class`](filetypes/java_class/README.md) | 285 / 229,241 | 0.928510 | 0.984019 | 0.883721 | 80.00% | — |
| [`ico`](filetypes/ico/README.md) | 29 / 106 | 0.967589 | 0.969421 | 0.884615 | 79.31% | — |
| [`vsix`](filetypes/vsix/README.md) | 28 / 794 | 0.935627 | 0.988170 | 0.880000 | 78.57% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,106 / 227,683 | 0.990889 | 0.998567 | 0.865320 | 76.31% | — |
| [`ruby`](filetypes/ruby/README.md) | 29 / 24,735 | 0.932652 | 0.999728 | 0.814815 | 75.86% | — |
| [`powershell`](filetypes/powershell/README.md) | 781 / 803 | 0.995594 | 0.995303 | 0.861718 | 75.80% | — |
| [`crx`](filetypes/crx/README.md) | 306 / 1,657 | 0.978187 | 0.993951 | 0.849722 | 74.84% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 403 / 154,301 | 0.948306 | 0.999766 | 0.817439 | 74.44% | — |
| [`java`](filetypes/java/README.md) | 412 / 25,210 | 0.979100 | 0.997484 | 0.842541 | 74.03% | — |
| [`npm`](filetypes/npm/README.md) | 3,679 / 45,910 | 0.972783 | 0.994365 | 0.849555 | 73.91% | — |
| [`go`](filetypes/go/README.md) | 1,097 / 32,131 | 0.884854 | 0.983862 | 0.814308 | 70.56% | — |
| [`tar`](filetypes/tar/README.md) | 1,783 / 13,620 | 0.979599 | 0.996224 | 0.820851 | 69.77% | — |
| [`python`](filetypes/python/README.md) | 2,593 / 85,299 | 0.950885 | 0.995927 | 0.797407 | 66.41% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,666 / 9,681 | 0.998578 | 0.999029 | 0.780142 | 63.95% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 26 / 2,322 | 0.923234 | 0.984297 | 0.714286 | 57.69% | — |
| [`whl`](filetypes/whl/README.md) | 296 / 8,864 | 0.919545 | 0.994655 | 0.678492 | 51.69% | — |
| [`png`](filetypes/png/README.md) | 959 / 68,484 | 0.942462 | 0.992829 | 0.662509 | 49.84% | — |
| [`xml`](filetypes/xml/README.md) | 211 / 55,568 | 0.767333 | 0.992287 | 0.646154 | 49.76% | — |
| [`gif`](filetypes/gif/README.md) | 63 / 256 | 0.847608 | 0.964720 | 0.577320 | 44.44% | — |
| [`csharp`](filetypes/csharp/README.md) | 438 / 12,895 | 0.980638 | 0.999400 | 0.570033 | 39.95% | — |
| [`c`](filetypes/c/README.md) | 2,099 / 221,858 | 0.858815 | 0.996153 | 0.556072 | 39.92% | — |
| [`rust`](filetypes/rust/README.md) | 59 / 45,706 | 0.388168 | 0.988111 | 0.301370 | 37.29% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 172 / 5,675 | 0.463403 | 0.841169 | 0.504274 | 34.30% | — |
| [`text`](filetypes/text/README.md) | 801 / 63,621 | 0.870752 | 0.992392 | 0.401990 | 25.22% | — |
| **Weighted avg** (by test pop) | **2,139,593** | **0.9339** | **0.9949** | **0.8046** | **72.3%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (one FP plus an estimated additional 24 FP/100M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (pool-adjusted)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `6309383805`, score-table `5d8c79958f09`, model-set `972afe88a603`. 1 general, 60 filegroup, 72 filetype routes.

## Limits

- The level is a pool-adjusted calibration target. Interpolation or extrapolation does not guarantee the future FP rate; more representative benign data improves rate estimation.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
