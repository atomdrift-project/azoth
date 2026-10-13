# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 52 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 20,801,151-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,593,965-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 56 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 810 / 115 | 1.000000 | 1.000000 | 1.000000 | 100.00% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,030 / 4,154 | 0.994848 | 0.986475 | 0.958314 | 90.02% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 365 / 1,178 | 0.960215 | 0.974677 | 0.944206 | 88.49% | — |
| [`gem`](filetypes/gem/README.md) | 51 / 14,247 | 0.901938 | 0.988939 | 0.937500 | 88.24% | — |
| [`elf`](filetypes/elf/README.md) | 24,856 / 113,274 | 0.995299 | 0.998072 | 0.985097 | 86.82% | PR +0.001999 / ROC +0.004772 |
| [`package.json`](filetypes/package.json/README.md) | 2,744 / 9,584 | 0.963811 | 0.967672 | 0.962712 | 85.31% | — |
| [`lnk`](filetypes/lnk/README.md) | 584 / 153 | 0.995777 | 0.984410 | 0.981324 | 79.45% | — |
| [`html`](filetypes/html/README.md) | 11,419 / 53,722 | 0.969899 | 0.985975 | 0.959353 | 77.60% | — |
| [`batch`](filetypes/batch/README.md) | 22,293 / 1,142 | 0.999849 | 0.997202 | 0.995705 | 75.32% | — |
| [`npm`](filetypes/npm/README.md) | 3,328 / 28,954 | 0.923911 | 0.954656 | 0.900942 | 73.23% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,661 | 0.926682 | 0.999279 | 0.857143 | 71.43% | — |
| [`perl`](filetypes/perl/README.md) | 54 / 10,176 | 0.853533 | 0.980532 | 0.842105 | 66.67% | — |
| [`macho`](filetypes/macho/README.md) | 307 / 4,784 | 0.961617 | 0.994064 | 0.911263 | 66.12% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 414 / 153,072 | 0.687370 | 0.920068 | 0.787879 | 62.56% | — |
| [`powershell`](filetypes/powershell/README.md) | 765 / 772 | 0.973871 | 0.967860 | 0.933422 | 61.57% | — |
| `ico` | 33 / 90 | 0.689579 | 0.785522 | 0.730769 | 57.58% | — |
| [`php`](filetypes/php/README.md) | 850 / 78,155 | 0.731336 | 0.904538 | 0.747048 | 55.88% | — |
| [`pe`](filetypes/pe/README.md) | 203,621 / 33,705 | 0.997392 | 0.984949 | 0.980929 | 54.82% | PR -0.000908 / ROC -0.013251 |
| [`python`](filetypes/python/README.md) | 2,746 / 84,734 | 0.799923 | 0.915104 | 0.793239 | 54.44% | — |
| [`shell`](filetypes/shell/README.md) | 2,516 / 21,016 | 0.922752 | 0.963783 | 0.877113 | 53.90% | — |
| [`tar`](filetypes/tar/README.md) | 1,910 / 10,950 | 0.933726 | 0.971104 | 0.881894 | 53.14% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,165 / 10,781 | 0.770556 | 0.819694 | 0.751460 | 52.58% | — |
| [`zip`](filetypes/zip/README.md) | 13,628 / 13,685 | 0.890602 | 0.847321 | 0.821512 | 46.02% | — |
| [`jar`](filetypes/jar/README.md) | 453 / 5,246 | 0.965697 | 0.993923 | 0.926130 | 41.72% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 30 / 2,325 | 0.881461 | 0.961584 | 0.881356 | 40.00% | — |
| `java_class` | 311 / 229,075 | 0.738199 | 0.951272 | 0.767824 | 39.23% | — |
| [`vsix`](filetypes/vsix/README.md) | 52 / 761 | 0.610760 | 0.883301 | 0.625000 | 38.46% | — |
| [`crx`](filetypes/crx/README.md) | 302 / 1,535 | 0.954234 | 0.990640 | 0.885191 | 36.09% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 101 / 1,604 | 0.738621 | 0.956165 | 0.714286 | 35.64% | — |
| `ruby` | 38 / 24,515 | 0.711654 | 0.978377 | 0.760563 | 34.21% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,332 / 818 | 0.984628 | 0.885839 | 0.969604 | 32.07% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 485 / 111 | 0.968577 | 0.867419 | 0.910798 | 27.01% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,845 / 538 | 0.990308 | 0.971568 | 0.959979 | 24.93% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,602 / 226,674 | 0.840481 | 0.919157 | 0.814534 | 24.34% | — |
| [`whl`](filetypes/whl/README.md) | 332 / 7,701 | 0.803717 | 0.973745 | 0.755832 | 17.77% | — |
| [`csharp`](filetypes/csharp/README.md) | 453 / 12,867 | 0.325784 | 0.707394 | 0.397329 | 17.22% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,772 | 0.994807 | 0.972926 | 0.976538 | 12.71% | PR +0.001507 / ROC -0.018274 |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,648 | 0.204839 | 0.611268 | 0.276151 | 11.86% | — |
| [`go`](filetypes/go/README.md) | 1,988 / 30,614 | 0.346042 | 0.678047 | 0.367658 | 7.70% | — |
| `rust` | 59 / 44,590 | 0.298887 | 0.668465 | 0.441860 | 5.08% | — |
| `gif` | 85 / 207 | 0.594534 | 0.772094 | 0.647343 | 4.71% | — |
| [`xml`](filetypes/xml/README.md) | 259 / 57,058 | 0.199835 | 0.600256 | 0.326154 | 3.09% | — |
| `text` | 901 / 53,495 | 0.076490 | 0.538630 | 0.109091 | 2.89% | — |
| [`java`](filetypes/java/README.md) | 415 / 25,170 | 0.072570 | 0.486618 | 0.126582 | 2.17% | — |
| [`png`](filetypes/png/README.md) | 1,124 / 68,059 | 0.066432 | 0.426260 | 0.102607 | 1.87% | — |
| [`7z`](filetypes/7z/README.md) | 1,119 / 47 | 0.998721 | 0.969977 | 0.981946 | — | — |
| `json` | 32 / 34,972 | 0.060420 | 0.751454 | 0.211765 | 0.00% | — |
| `c` | 2,213 / 221,430 | 0.040947 | 0.551334 | 0.149844 | 0.00% | — |
| **Weighted avg** (by test pop) | **2,090,707** | **0.6586** | **0.8479** | **0.6850** | **39.0%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `5922715835`, score-table `b2e44f0f9689`, model-set `a9aab169bf83`. 1 general, 6 filegroup, 56 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
