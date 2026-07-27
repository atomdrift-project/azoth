# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 57 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 14,692,357-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,832,565-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 61 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`html`](filetypes/html/README.md) | 31 / 2,012 | 0.994058 | 0.999928 | 0.983607 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 830 / 95 | 0.998924 | 0.991116 | 0.990279 | 98.19% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 1,717 | 0.996923 | 0.997075 | 0.979984 | 96.38% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,612 / 3,918 | 0.995332 | 0.986233 | 0.965822 | 93.21% | — |
| [`gem`](filetypes/gem/README.md) | 88 / 259 | 0.954834 | 0.965054 | 0.958580 | 92.05% | — |
| [`elf`](filetypes/elf/README.md) | 23,938 / 67,912 | 0.997374 | 0.998283 | 0.993715 | 89.79% | PR +0.004074 / ROC +0.004983 |
| [`vbs`](filetypes/vbs/README.md) | 1,576 / 466 | 0.994197 | 0.979888 | 0.958347 | 85.91% | — |
| [`lnk`](filetypes/lnk/README.md) | 572 / 134 | 0.994424 | 0.977305 | 0.976583 | 85.49% | — |
| [`macho`](filetypes/macho/README.md) | 364 / 2,953 | 0.970759 | 0.988392 | 0.944290 | 84.89% | — |
| [`jar`](filetypes/jar/README.md) | 502 / 2,881 | 0.943951 | 0.967667 | 0.919305 | 81.27% | — |
| [`powershell`](filetypes/powershell/README.md) | 734 / 597 | 0.985456 | 0.978777 | 0.940434 | 80.65% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,919 | 0.795422 | 0.904469 | 0.839506 | 76.09% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,619 | 0.922265 | 0.999254 | 0.844444 | 75.32% | — |
| [`tar`](filetypes/tar/README.md) | 3,187 / 7,977 | 0.972268 | 0.977206 | 0.938519 | 75.15% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,591 | 0.993352 | 0.962419 | 0.974155 | 74.79% | PR +0.000052 / ROC -0.028781 |
| [`shell`](filetypes/shell/README.md) | 2,344 / 17,155 | 0.939226 | 0.969155 | 0.907371 | 72.78% | — |
| [`npm`](filetypes/npm/README.md) | 588 / 763 | 0.943946 | 0.927586 | 0.880416 | 71.77% | — |
| [`crx`](filetypes/crx/README.md) | 294 / 320 | 0.936286 | 0.933041 | 0.898246 | 71.43% | — |
| [`whl`](filetypes/whl/README.md) | 439 / 914 | 0.927506 | 0.932116 | 0.867299 | 69.93% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,889 / 9,341 | 0.959925 | 0.974195 | 0.910659 | 58.65% | — |
| [`pe`](filetypes/pe/README.md) | 169,412 / 25,390 | 0.999008 | 0.993502 | 0.988333 | 56.92% | PR +0.000708 / ROC -0.004698 |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 462 / 102,591 | 0.693049 | 0.860246 | 0.778061 | 55.41% | — |
| [`zip`](filetypes/zip/README.md) | 13,367 / 3,345 | 0.992307 | 0.970939 | 0.956895 | 52.91% | — |
| [`python`](filetypes/python/README.md) | 2,872 / 70,542 | 0.797638 | 0.936873 | 0.795185 | 51.18% | — |
| [`php`](filetypes/php/README.md) | 814 / 72,699 | 0.684744 | 0.872186 | 0.734756 | 50.74% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 21,710 | 0.545557 | 0.820225 | 0.642857 | 50.00% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,560 / 351 | 0.993217 | 0.891275 | 0.992056 | 45.48% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,191 / 168,692 | 0.909555 | 0.963719 | 0.873527 | 43.94% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 986 | 0.528306 | 0.716836 | 0.583333 | 42.00% | — |
| [`batch`](filetypes/batch/README.md) | 22,138 / 959 | 0.994745 | 0.928906 | 0.994813 | 33.23% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,027 | 0.336545 | 0.697080 | 0.401327 | 23.61% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 567 | 0.222059 | 0.480106 | 0.324324 | 20.00% | — |
| [`c`](filetypes/c/README.md) | 2,297 / 184,219 | 0.230577 | 0.638711 | 0.328868 | 9.88% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 2,633 | 0.138633 | 0.749928 | 0.158730 | 8.62% | — |
| [`go`](filetypes/go/README.md) | 2,114 / 26,969 | 0.239882 | 0.631245 | 0.246575 | 4.49% | — |
| [`text`](filetypes/text/README.md) | 500 / 35,691 | 0.086265 | 0.601735 | 0.123779 | 4.00% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 12,006 | 0.038071 | 0.489021 | 0.067416 | 3.57% | — |
| [`json`](filetypes/json/README.md) | 207 / 27,475 | 0.065638 | 0.699836 | 0.096270 | 3.38% | — |
| [`rust`](filetypes/rust/README.md) | 259 / 40,096 | 0.092373 | 0.637795 | 0.155224 | 1.93% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 7,464 | 0.026666 | 0.505307 | 0.040323 | 0.98% | — |
| [`java`](filetypes/java/README.md) | 461 / 21,704 | — | — | — | — | — |
| [`java_class`](filetypes/java_class/README.md) | 282 / 210,477 | — | — | — | — | — |
| [`jpeg`](filetypes/jpeg/README.md) | 180 / 5,436 | — | — | — | — | — |
| [`package.json`](filetypes/package.json/README.md) | 2,522 / 6,245 | — | — | — | — | — |
| [`png`](filetypes/png/README.md) | 1,091 / 48,550 | — | — | — | — | — |
| [`xml`](filetypes/xml/README.md) | 506 / 45,740 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,620,077** | **0.6910** | **0.8608** | **0.7110** | **44.1%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2538267239`, score-table `f8145015dc94`, model-set `71485dd3e686`. 1 general, 7 filegroup, 61 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
