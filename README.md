# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 40 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 991,058-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 991,247-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 44 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 829 / 55 | 0.998848 | 0.990229 | 0.989666 | 100.00% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,338 / 3,126 | 0.996181 | 0.994935 | 0.991831 | 98.67% | — |
| [`elf`](filetypes/elf/README.md) | 23,423 / 24,158 | 0.999869 | 0.999860 | 0.997225 | 98.28% | PR +0.006569 / ROC +0.006560 |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,278 / 321 | 0.999195 | 0.996925 | 0.984114 | 97.65% | — |
| [`xls`](filetypes/xls/README.md) | 4,944 / 2,652 | 0.995151 | 0.988857 | 0.979735 | 95.95% | — |
| [`macho`](filetypes/macho/README.md) | 342 / 1,623 | 0.990276 | 0.996470 | 0.969343 | 95.61% | — |
| [`ole`](filetypes/ole/README.md) | 858 / 817 | 0.990359 | 0.988385 | 0.963899 | 93.82% | — |
| [`tar`](filetypes/tar/README.md) | 2,788 / 5,078 | 0.991340 | 0.991827 | 0.976272 | 92.04% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,531 / 429 | 0.993080 | 0.975519 | 0.958026 | 88.05% | — |
| [`lnk`](filetypes/lnk/README.md) | 566 / 132 | 0.973384 | 0.909238 | 0.912919 | 84.45% | — |
| [`shell`](filetypes/shell/README.md) | 2,037 / 8,488 | 0.965939 | 0.981256 | 0.936041 | 81.79% | — |
| [`perl`](filetypes/perl/README.md) | 41 / 5,434 | 0.803674 | 0.919666 | 0.868421 | 80.49% | — |
| [`docx`](filetypes/docx/README.md) | 595 / 62 | 0.988332 | 0.913960 | 0.955298 | 80.34% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 443 / 33,989 | 0.833241 | 0.910026 | 0.891386 | 79.91% | — |
| [`powershell`](filetypes/powershell/README.md) | 714 / 331 | 0.987127 | 0.975395 | 0.950213 | 79.41% | — |
| [`jar`](filetypes/jar/README.md) | 482 / 540 | 0.969664 | 0.964632 | 0.916213 | 79.05% | — |
| [`whl`](filetypes/whl/README.md) | 82 / 598 | 0.868329 | 0.938931 | 0.851064 | 78.21% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,516 / 3,090 | 0.993543 | 0.955852 | 0.974481 | 74.81% | PR +0.000243 / ROC -0.035348 |
| [`java_class`](filetypes/java_class/README.md) | 262 / 99,313 | 0.860369 | 0.967738 | 0.887574 | 73.28% | — |
| [`pe`](filetypes/pe/README.md) | 168,742 / 20,645 | 0.999650 | 0.997360 | 0.993031 | 69.73% | PR +0.001350 / ROC -0.000840 |
| [`javascript`](filetypes/javascript/README.md) | 15,405 / 85,275 | 0.934167 | 0.968785 | 0.901089 | 66.00% | — |
| [`php`](filetypes/php/README.md) | 743 / 20,768 | 0.791942 | 0.908350 | 0.798172 | 63.93% | — |
| [`batch`](filetypes/batch/README.md) | 22,130 / 745 | 0.999115 | 0.987919 | 0.997175 | 60.15% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,923 / 7,339 | 0.904745 | 0.921106 | 0.821485 | 58.63% | — |
| [`zip`](filetypes/zip/README.md) | 13,091 / 2,139 | 0.970782 | 0.843233 | 0.937372 | 55.21% | — |
| [`ruby`](filetypes/ruby/README.md) | 25 / 3,513 | 0.483429 | 0.734728 | 0.615385 | 48.00% | — |
| [`python`](filetypes/python/README.md) | 2,918 / 29,621 | 0.777281 | 0.878626 | 0.792965 | 47.02% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,859 / 210 | 0.989563 | 0.723395 | 0.986816 | 43.11% | — |
| `cargo.toml` | 30 / 242 | 0.414646 | 0.751309 | 0.425532 | 33.33% | — |
| [`csharp`](filetypes/csharp/README.md) | 457 / 9,815 | 0.349777 | 0.729584 | 0.371773 | 22.10% | — |
| `c` | 2,205 / 104,725 | 0.178436 | 0.613174 | 0.303628 | 19.00% | — |
| `jpeg` | 183 / 3,996 | 0.194551 | 0.620173 | 0.228228 | 18.58% | — |
| [`deb`](filetypes/deb/README.md) | 54 / 1,008 | 0.144851 | 0.568471 | 0.169492 | 16.67% | — |
| [`go`](filetypes/go/README.md) | 1,432 / 16,708 | 0.260379 | 0.701534 | 0.273354 | 8.59% | — |
| [`plist`](filetypes/plist/README.md) | 83 / 1,637 | 0.142860 | 0.683476 | 0.248996 | 7.23% | — |
| `java` | 447 / 10,298 | 0.172645 | 0.731921 | 0.260355 | 5.82% | — |
| `rust` | 243 / 12,565 | 0.079066 | 0.597762 | 0.110638 | 5.76% | — |
| [`png`](filetypes/png/README.md) | 1,115 / 24,068 | 0.108311 | 0.546295 | 0.127395 | 5.38% | — |
| [`xml`](filetypes/xml/README.md) | 536 / 33,302 | 0.108818 | 0.585172 | 0.149750 | 5.22% | — |
| `text` | 745 / 15,124 | 0.122661 | 0.659140 | 0.161672 | 4.56% | — |
| `makefile` | 94 / 4,264 | 0.024629 | 0.490000 | 0.042400 | 1.06% | — |
| [`gem`](filetypes/gem/README.md) | 27 / 48 | 0.982353 | 0.988426 | 0.941176 | — | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 40 | 0.557110 | 0.561538 | 0.565217 | — | — |
| `json` | 146 / 7,802 | 0.043264 | 0.692383 | 0.124041 | 0.00% | — |
| **Weighted avg** (by test pop) | **914,861** | **0.7197** | **0.8681** | **0.7386** | **54.9%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1727088862`, score-table `7854df8d0093`, model-set `9036a3057623`. 1 general, 7 filegroup, 44 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
