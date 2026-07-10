# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 37 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 13,597,415-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,694,889-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 41 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`html`](filetypes/html/README.md) | 31 / 2,010 | 0.994058 | 0.999928 | 0.983607 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 830 / 94 | 0.998243 | 0.990458 | 0.989078 | 98.31% | — |
| `pkg_info` | 1,270 / 1,624 | 0.984438 | 0.978706 | 0.980439 | 96.38% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,501 / 5,848 | 0.983965 | 0.983908 | 0.978672 | 94.88% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,604 / 3,897 | 0.995770 | 0.988106 | 0.965802 | 92.97% | — |
| [`gem`](filetypes/gem/README.md) | 87 / 255 | 0.960153 | 0.972504 | 0.958084 | 91.95% | — |
| [`elf`](filetypes/elf/README.md) | 23,712 / 55,862 | 0.998692 | 0.999196 | 0.995622 | 90.38% | PR +0.005392 / ROC +0.005896 |
| `java` | 461 / 21,185 | 0.020080 | 0.469199 | 0.042019 | 89.15% | — |
| [`macho`](filetypes/macho/README.md) | 361 / 2,709 | 0.974226 | 0.989961 | 0.947368 | 88.92% | — |
| [`lnk`](filetypes/lnk/README.md) | 569 / 132 | 0.993392 | 0.971841 | 0.975779 | 85.06% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,561 / 459 | 0.993686 | 0.980740 | 0.961622 | 83.66% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,424 | 0.819841 | 0.915860 | 0.878049 | 78.26% | — |
| [`tar`](filetypes/tar/README.md) | 3,176 / 7,729 | 0.973319 | 0.977736 | 0.939408 | 76.76% | — |
| [`jar`](filetypes/jar/README.md) | 496 / 2,217 | 0.921035 | 0.964107 | 0.874730 | 74.40% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,428 | 0.990295 | 0.940883 | 0.959264 | 74.33% | PR -0.003005 / ROC -0.050317 |
| [`crx`](filetypes/crx/README.md) | 286 / 294 | 0.957421 | 0.941993 | 0.890459 | 73.43% | — |
| [`registry`](filetypes/registry/README.md) | 74 / 12,612 | 0.918040 | 0.999163 | 0.840580 | 72.97% | — |
| [`npm`](filetypes/npm/README.md) | 483 / 611 | 0.937553 | 0.916391 | 0.877268 | 72.26% | — |
| [`shell`](filetypes/shell/README.md) | 2,307 / 16,453 | 0.942112 | 0.973249 | 0.899978 | 70.74% | — |
| [`powershell`](filetypes/powershell/README.md) | 726 / 586 | 0.973411 | 0.957648 | 0.934844 | 67.36% | — |
| [`pe`](filetypes/pe/README.md) | 169,221 / 24,237 | 0.998591 | 0.990495 | 0.985041 | 66.52% | PR +0.000291 / ROC -0.007705 |
| [`whl`](filetypes/whl/README.md) | 432 / 798 | 0.926356 | 0.928033 | 0.869359 | 65.05% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,891 / 9,232 | 0.950790 | 0.967974 | 0.886931 | 58.49% | — |
| [`python`](filetypes/python/README.md) | 2,864 / 66,768 | 0.787990 | 0.924310 | 0.797363 | 50.00% | — |
| [`zip`](filetypes/zip/README.md) | 13,333 / 3,184 | 0.950449 | 0.787824 | 0.900406 | 48.14% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,559 / 351 | 0.992222 | 0.875799 | 0.992804 | 47.07% | — |
| `python_bytecode` | 461 / 92,578 | 0.679765 | 0.841400 | 0.788036 | 45.77% | — |
| `php` | 798 / 68,648 | 0.697034 | 0.874045 | 0.749258 | 42.61% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 861 | 0.533194 | 0.700221 | 0.565657 | 40.00% | — |
| [`javascript`](filetypes/javascript/README.md) | 16,924 / 158,020 | 0.908599 | 0.964876 | 0.869243 | 39.41% | — |
| [`batch`](filetypes/batch/README.md) | 22,135 / 952 | 0.995830 | 0.943006 | 0.995440 | 33.26% | — |
| `ruby` | 37 / 21,312 | 0.001387 | 0.247667 | 0.003565 | 32.43% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 11,223 | 0.327582 | 0.684264 | 0.386777 | 23.18% | — |
| [`json`](filetypes/json/README.md) | 206 / 24,955 | 0.075699 | 0.505547 | 0.127273 | 22.82% | — |
| `java_class` | 281 / 203,287 | 0.780133 | 0.944442 | 0.826667 | 21.71% | — |
| `dockerfile` | 25 / 547 | 0.152940 | 0.724168 | 0.187500 | 12.00% | — |
| `rust` | 259 / 39,672 | 0.012270 | 0.528084 | 0.076261 | 11.97% | — |
| `jpeg` | 180 / 5,395 | 0.208993 | 0.649791 | 0.283186 | 11.67% | — |
| `c` | 2,297 / 169,571 | 0.230375 | 0.734278 | 0.325911 | 9.93% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 2,449 | 0.142202 | 0.740499 | 0.158730 | 8.62% | — |
| `png` | 1,091 / 46,594 | 0.077456 | 0.527723 | 0.105536 | 5.50% | — |
| `plist` | 84 / 11,958 | 0.045983 | 0.548803 | 0.068966 | 3.57% | — |
| `makefile` | 102 / 7,408 | 0.044993 | 0.687362 | 0.062668 | 2.94% | — |
| [`go`](filetypes/go/README.md) | 2,114 / 26,526 | 0.216691 | 0.592338 | 0.248135 | 2.74% | — |
| `text` | 500 / 33,466 | 0.088909 | 0.637857 | 0.129496 | 2.00% | — |
| [`xml`](filetypes/xml/README.md) | 505 / 49,566 | 0.141770 | 0.632392 | 0.253669 | 1.78% | — |
| **Weighted avg** (by test pop) | **1,544,958** | **0.6471** | **0.8432** | **0.6734** | **39.2%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2203636289`, score-table `4de59aeb53c8`, model-set `72934c6f512b`. 1 general, 7 filegroup, 41 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
