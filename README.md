# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 58 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 17,535,482-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,187,012-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 62 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 831 / 98 | 0.998413 | 0.986045 | 0.988450 | 97.71% | — |
| [`html`](filetypes/html/README.md) | 31 / 8,477 | 0.975434 | 0.999623 | 0.983607 | 96.77% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 2,109 | 0.996333 | 0.997378 | 0.981192 | 96.14% | — |
| [`gem`](filetypes/gem/README.md) | 97 / 387 | 0.954055 | 0.967993 | 0.962567 | 92.78% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,630 / 3,960 | 0.994909 | 0.985743 | 0.966642 | 92.14% | — |
| [`elf`](filetypes/elf/README.md) | 24,248 / 98,007 | 0.997110 | 0.998611 | 0.993078 | 88.99% | PR +0.003810 / ROC +0.005311 |
| [`package.json`](filetypes/package.json/README.md) | 2,546 / 7,785 | 0.977756 | 0.983345 | 0.973568 | 83.70% | — |
| [`lnk`](filetypes/lnk/README.md) | 576 / 140 | 0.993971 | 0.980022 | 0.980017 | 81.77% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,527 | 0.801251 | 0.920378 | 0.875000 | 77.78% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`macho`](filetypes/macho/README.md) | 365 / 3,910 | 0.965874 | 0.985529 | 0.944134 | 74.52% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,594 / 472 | 0.993902 | 0.980797 | 0.963540 | 74.28% | — |
| [`tar`](filetypes/tar/README.md) | 3,217 / 9,046 | 0.963339 | 0.974720 | 0.926425 | 70.50% | — |
| [`npm`](filetypes/npm/README.md) | 715 / 996 | 0.937836 | 0.920413 | 0.882963 | 69.23% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,672 | 0.998428 | 0.991102 | 0.987699 | 68.60% | PR +0.005128 / ROC -0.000098 |
| [`pe`](filetypes/pe/README.md) | 169,815 / 28,527 | 0.999138 | 0.995080 | 0.989528 | 63.84% | PR +0.000838 / ROC -0.003120 |
| [`jar`](filetypes/jar/README.md) | 509 / 3,581 | 0.909054 | 0.958416 | 0.886772 | 58.74% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,890 / 10,561 | 0.910301 | 0.933736 | 0.878993 | 58.43% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,146 | 0.608116 | 0.839788 | 0.731707 | 57.69% | — |
| `python_bytecode` | 464 / 126,339 | 0.668503 | 0.849281 | 0.775353 | 54.53% | — |
| [`shell`](filetypes/shell/README.md) | 2,388 / 19,799 | 0.924961 | 0.963722 | 0.896731 | 51.13% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,319 / 202,186 | 0.904171 | 0.965265 | 0.866154 | 47.97% | — |
| [`whl`](filetypes/whl/README.md) | 488 / 1,708 | 0.852219 | 0.903938 | 0.790407 | 47.54% | — |
| [`powershell`](filetypes/powershell/README.md) | 739 / 663 | 0.968259 | 0.953257 | 0.945225 | 47.36% | — |
| `java_class` | 289 / 214,364 | 0.792633 | 0.937497 | 0.851224 | 47.06% | — |
| [`python`](filetypes/python/README.md) | 2,874 / 79,247 | 0.772350 | 0.909442 | 0.796651 | 46.87% | — |
| [`crx`](filetypes/crx/README.md) | 299 / 701 | 0.911389 | 0.925789 | 0.854369 | 42.81% | — |
| [`php`](filetypes/php/README.md) | 850 / 76,410 | 0.714266 | 0.915478 | 0.768908 | 42.35% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,071 | 0.548849 | 0.704323 | 0.629213 | 36.00% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 352 | 0.993815 | 0.890985 | 0.989118 | 33.84% | — |
| [`zip`](filetypes/zip/README.md) | 13,476 / 4,539 | 0.988836 | 0.966807 | 0.941026 | 31.31% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,462 | 0.331616 | 0.670207 | 0.404643 | 23.39% | — |
| [`batch`](filetypes/batch/README.md) | 22,140 / 1,003 | 0.994612 | 0.929529 | 0.993403 | 15.57% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 179 / 5,580 | 0.225851 | 0.653766 | 0.276786 | 10.61% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 3,303 | 0.153106 | 0.654953 | 0.228571 | 10.34% | — |
| [`c`](filetypes/c/README.md) | 2,289 / 208,994 | 0.229708 | 0.665988 | 0.325326 | 10.09% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 580 | 0.196922 | 0.547414 | 0.300000 | 8.00% | — |
| [`png`](filetypes/png/README.md) | 1,087 / 64,569 | 0.083548 | 0.590739 | 0.105172 | 5.24% | — |
| [`go`](filetypes/go/README.md) | 2,095 / 28,626 | 0.241578 | 0.608025 | 0.245530 | 3.87% | — |
| [`json`](filetypes/json/README.md) | 203 / 31,169 | 0.062089 | 0.698806 | 0.088106 | 3.45% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 12,517 | 0.046048 | 0.679551 | 0.067416 | 2.38% | — |
| [`xml`](filetypes/xml/README.md) | 504 / 56,023 | 0.108894 | 0.551727 | 0.183926 | 1.98% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,665 | 0.095199 | 0.482715 | 0.155598 | 1.08% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 7,834 | 0.022709 | 0.385599 | 0.047619 | 0.98% | — |
| [`text`](filetypes/text/README.md) | 490 / 39,905 | 0.060020 | 0.624902 | 0.090580 | 0.82% | — |
| `rust` | 259 / 41,422 | 0.072147 | 0.621559 | 0.146739 | 0.77% | — |
| [`7z`](filetypes/7z/README.md) | 1,167 / 27 | 0.998697 | 0.946507 | 0.989402 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 42 | 0.953514 | 0.747089 | 0.930070 | — | — |
| **Weighted avg** (by test pop) | **1,813,863** | **0.6547** | **0.8508** | **0.6851** | **41.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `3828940278`, score-table `ff405080947f`, model-set `8c070d64ee9b`. 1 general, 6 filegroup, 62 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
