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
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,778 | 0.999854 | 0.999086 | 0.993760 | 98.83% | PR +0.006554 / ROC +0.007886 |
| [`kotlin`](filetypes/kotlin/README.md) | 3,262 / 10,373 | 0.999108 | 0.999730 | 0.985170 | 98.77% | — |
| [`batch`](filetypes/batch/README.md) | 22,320 / 1,163 | 0.999989 | 0.999780 | 0.993621 | 98.74% | — |
| [`elf`](filetypes/elf/README.md) | 25,147 / 113,493 | 0.999915 | 0.999975 | 0.991662 | 98.37% | PR +0.006615 / ROC +0.006675 |
| [`vbs`](filetypes/vbs/README.md) | 1,869 / 551 | 0.999354 | 0.997866 | 0.987104 | 98.29% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,058 / 4,155 | 0.999569 | 0.998867 | 0.986708 | 98.01% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 517 / 121 | 0.944361 | 0.845101 | 0.948454 | 97.87% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 368 / 1,580 | 0.998074 | 0.999419 | 0.979592 | 97.83% | — |
| [`html`](filetypes/html/README.md) | 11,512 / 54,350 | 0.999718 | 0.999930 | 0.988234 | 97.77% | — |
| [`lnk`](filetypes/lnk/README.md) | 577 / 154 | 0.999497 | 0.998109 | 0.979736 | 96.36% | — |
| [`7z`](filetypes/7z/README.md) | 1,124 / 50 | 0.998127 | 0.963274 | 0.972235 | 95.02% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,460 / 822 | 0.993803 | 0.952712 | 0.967446 | 94.67% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 72 / 1,740 | 0.939551 | 0.995123 | 0.925170 | 94.44% | — |
| [`jar`](filetypes/jar/README.md) | 485 / 5,252 | 0.970306 | 0.996240 | 0.922432 | 90.72% | — |
| [`gem`](filetypes/gem/README.md) | 51 / 14,932 | 0.934632 | 0.997714 | 0.937500 | 88.24% | — |
| [`registry`](filetypes/registry/README.md) | 59 / 13,680 | 0.959953 | 0.999607 | 0.936937 | 88.14% | — |
| [`shell`](filetypes/shell/README.md) | 2,447 / 21,731 | 0.991077 | 0.997044 | 0.931065 | 87.21% | — |
| [`macho`](filetypes/macho/README.md) | 336 / 4,794 | 0.970458 | 0.996183 | 0.901408 | 85.71% | — |
| [`json`](filetypes/json/README.md) | 36 / 39,110 | 0.796495 | 0.989997 | 0.582524 | 83.33% | — |
| [`pe`](filetypes/pe/README.md) | 205,788 / 33,895 | 0.999914 | 0.999488 | 0.907129 | 83.01% | PR +0.001614 / ROC +0.001288 |
| [`ruby`](filetypes/ruby/README.md) | 29 / 24,735 | 0.937614 | 0.997186 | 0.872727 | 82.76% | — |
| [`php`](filetypes/php/README.md) | 764 / 78,554 | 0.968916 | 0.997628 | 0.904011 | 82.59% | — |
| [`gif`](filetypes/gif/README.md) | 63 / 256 | 0.826919 | 0.972997 | 0.806202 | 82.54% | — |
| [`perl`](filetypes/perl/README.md) | 56 / 10,188 | 0.963002 | 0.994729 | 0.893204 | 82.14% | — |
| [`zip`](filetypes/zip/README.md) | 13,684 / 17,977 | 0.997394 | 0.997838 | 0.893871 | 80.85% | — |
| [`java_class`](filetypes/java_class/README.md) | 285 / 229,241 | 0.928184 | 0.986482 | 0.885437 | 80.00% | — |
| [`ico`](filetypes/ico/README.md) | 29 / 106 | 0.967589 | 0.969421 | 0.884615 | 79.31% | — |
| [`vsix`](filetypes/vsix/README.md) | 28 / 794 | 0.932825 | 0.988170 | 0.880000 | 78.57% | — |
| [`powershell`](filetypes/powershell/README.md) | 781 / 803 | 0.995495 | 0.995258 | 0.863372 | 76.06% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 403 / 154,301 | 0.950086 | 0.999770 | 0.825613 | 75.19% | — |
| [`java`](filetypes/java/README.md) | 412 / 25,210 | 0.979069 | 0.997416 | 0.844567 | 74.51% | — |
| [`npm`](filetypes/npm/README.md) | 3,679 / 45,910 | 0.972831 | 0.994210 | 0.853138 | 74.45% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,106 / 227,683 | 0.992318 | 0.998767 | 0.849941 | 73.94% | — |
| [`crx`](filetypes/crx/README.md) | 306 / 1,657 | 0.978591 | 0.994709 | 0.841121 | 73.53% | — |
| [`go`](filetypes/go/README.md) | 1,097 / 32,131 | 0.887948 | 0.983995 | 0.814932 | 70.65% | — |
| [`tar`](filetypes/tar/README.md) | 1,783 / 13,620 | 0.979220 | 0.996119 | 0.821629 | 69.88% | — |
| [`python`](filetypes/python/README.md) | 2,593 / 85,299 | 0.949821 | 0.995449 | 0.783974 | 64.52% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,666 / 9,681 | 0.998580 | 0.999089 | 0.781536 | 64.14% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 26 / 2,322 | 0.904335 | 0.972603 | 0.714286 | 57.69% | — |
| [`whl`](filetypes/whl/README.md) | 296 / 8,864 | 0.921263 | 0.995014 | 0.687225 | 52.70% | — |
| [`png`](filetypes/png/README.md) | 959 / 68,484 | 0.952120 | 0.997585 | 0.665281 | 50.05% | — |
| [`xml`](filetypes/xml/README.md) | 211 / 55,568 | 0.783062 | 0.990750 | 0.644172 | 49.76% | — |
| [`csharp`](filetypes/csharp/README.md) | 438 / 12,895 | 0.979339 | 0.999374 | 0.578352 | 40.87% | — |
| [`rust`](filetypes/rust/README.md) | 59 / 45,706 | 0.388362 | 0.988462 | 0.326531 | 40.68% | — |
| [`c`](filetypes/c/README.md) | 2,099 / 221,858 | 0.854122 | 0.995775 | 0.557507 | 40.07% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 172 / 5,675 | 0.525401 | 0.930828 | 0.504274 | 34.30% | — |
| [`text`](filetypes/text/README.md) | 801 / 63,621 | 0.870991 | 0.992451 | 0.401990 | 25.22% | — |
| **Weighted avg** (by test pop) | **2,139,593** | **0.9347** | **0.9955** | **0.8047** | **72.2%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (one FP plus an estimated additional 24 FP/100M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (pool-adjusted)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `6309383805`, score-table `193a99b431ae`, model-set `f793ca396e86`. 1 general, 60 filegroup, 72 filetype routes.

## Limits

- The level is a pool-adjusted calibration target. Interpolation or extrapolation does not guarantee the future FP rate; more representative benign data improves rate estimation.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
