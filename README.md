# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 49 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 19,975,007-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,490,700-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 53 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| `ico` | 33 / 85 | 0.695416 | 0.790374 | 0.730769 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 810 / 115 | 0.999278 | 0.995046 | 0.995660 | 99.14% | — |
| [`gem`](filetypes/gem/README.md) | 44 / 14,058 | 0.943214 | 0.994275 | 0.964706 | 93.18% | — |
| [`html`](filetypes/html/README.md) | 37 / 34,555 | 0.922699 | 0.996407 | 0.942857 | 89.19% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,026 / 4,153 | 0.995401 | 0.987991 | 0.958563 | 88.97% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 361 / 1,112 | 0.964999 | 0.978076 | 0.941860 | 88.37% | — |
| [`elf`](filetypes/elf/README.md) | 24,821 / 111,958 | 0.995669 | 0.998285 | 0.986911 | 86.22% | PR +0.002369 / ROC +0.004985 |
| [`package.json`](filetypes/package.json/README.md) | 2,744 / 9,520 | 0.962559 | 0.971369 | 0.958930 | 80.25% | — |
| [`lnk`](filetypes/lnk/README.md) | 584 / 148 | 0.996033 | 0.984849 | 0.981293 | 79.62% | — |
| [`pe`](filetypes/pe/README.md) | 203,540 / 33,312 | 0.997472 | 0.984272 | 0.980040 | 73.58% | PR -0.000828 / ROC -0.013928 |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,768 | 0.995343 | 0.975092 | 0.976729 | 70.44% | PR +0.002043 / ROC -0.016108 |
| [`registry`](filetypes/registry/README.md) | 80 / 13,660 | 0.886920 | 0.971604 | 0.835616 | 70.00% | — |
| [`macho`](filetypes/macho/README.md) | 305 / 4,760 | 0.951001 | 0.982874 | 0.910017 | 68.52% | — |
| [`npm`](filetypes/npm/README.md) | 3,198 / 24,527 | 0.939584 | 0.953400 | 0.924077 | 64.10% | — |
| [`perl`](filetypes/perl/README.md) | 52 / 10,066 | 0.831127 | 0.961385 | 0.854167 | 63.46% | — |
| `ruby` | 38 / 24,161 | 0.726633 | 0.950110 | 0.753247 | 55.26% | — |
| [`tar`](filetypes/tar/README.md) | 1,940 / 10,977 | 0.927440 | 0.965444 | 0.868977 | 54.85% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 414 / 149,593 | 0.670139 | 0.886334 | 0.772134 | 54.59% | — |
| [`python`](filetypes/python/README.md) | 2,734 / 84,334 | 0.804451 | 0.911588 | 0.798206 | 54.32% | — |
| [`shell`](filetypes/shell/README.md) | 2,457 / 20,596 | 0.932787 | 0.968721 | 0.900662 | 53.85% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,149 / 10,873 | 0.942158 | 0.977922 | 0.862641 | 50.84% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 29 / 2,274 | 0.798935 | 0.926083 | 0.836364 | 48.28% | — |
| [`powershell`](filetypes/powershell/README.md) | 722 / 764 | 0.970127 | 0.964347 | 0.934183 | 47.51% | — |
| [`vsix`](filetypes/vsix/README.md) | 47 / 693 | 0.629402 | 0.846336 | 0.650000 | 46.81% | — |
| [`zip`](filetypes/zip/README.md) | 13,641 / 11,827 | 0.901147 | 0.852470 | 0.821664 | 44.35% | — |
| [`php`](filetypes/php/README.md) | 832 / 77,830 | 0.713417 | 0.906162 | 0.739850 | 42.91% | — |
| [`jar`](filetypes/jar/README.md) | 457 / 5,166 | 0.952074 | 0.986090 | 0.915556 | 41.14% | — |
| [`java_class`](filetypes/java_class/README.md) | 311 / 228,350 | 0.779009 | 0.880490 | 0.838129 | 39.87% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 1,218 | 0.947586 | 0.985247 | 0.887789 | 37.88% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 482 / 104 | 0.960257 | 0.836748 | 0.903534 | 29.46% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,333 / 818 | 0.979308 | 0.842912 | 0.974947 | 29.37% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 117 / 1,422 | 0.420559 | 0.776101 | 0.426357 | 26.50% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,385 / 225,302 | 0.835820 | 0.929784 | 0.813805 | 26.41% | — |
| `json` | 32 / 33,954 | 0.352175 | 0.698115 | 0.489796 | 25.00% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,802 / 533 | 0.990026 | 0.966067 | 0.954184 | 20.03% | — |
| [`whl`](filetypes/whl/README.md) | 324 / 6,787 | 0.657025 | 0.944258 | 0.617143 | 18.83% | — |
| [`csharp`](filetypes/csharp/README.md) | 471 / 12,851 | 0.324590 | 0.702164 | 0.382979 | 16.14% | — |
| [`batch`](filetypes/batch/README.md) | 22,276 / 1,111 | 0.984369 | 0.811959 | 0.984787 | 15.27% | — |
| [`deb`](filetypes/deb/README.md) | 41 / 3,429 | 0.203412 | 0.631258 | 0.320000 | 14.63% | — |
| `c` | 2,200 / 219,983 | 0.254729 | 0.680965 | 0.356388 | 10.36% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,645 | 0.196862 | 0.627350 | 0.250951 | 9.79% | — |
| [`gif`](filetypes/gif/README.md) | 85 / 194 | 0.672957 | 0.831019 | 0.660714 | 9.41% | — |
| [`go`](filetypes/go/README.md) | 2,024 / 30,441 | 0.321841 | 0.639620 | 0.365371 | 8.84% | — |
| `text` | 623 / 42,949 | 0.091735 | 0.540637 | 0.139601 | 4.17% | — |
| `xml` | 277 / 57,930 | 0.142989 | 0.473474 | 0.271100 | 3.97% | — |
| `png` | 1,132 / 67,932 | 0.066557 | 0.387600 | 0.101413 | 3.89% | — |
| `rust` | 59 / 44,151 | 0.250798 | 0.809070 | 0.350000 | 3.39% | — |
| [`java`](filetypes/java/README.md) | 415 / 24,946 | 0.077099 | 0.618455 | 0.130081 | 1.20% | — |
| [`7z`](filetypes/7z/README.md) | 1,121 / 47 | 0.997862 | 0.951022 | 0.979895 | — | — |
| **Weighted avg** (by test pop) | **2,032,554** | **0.6830** | **0.8479** | **0.7133** | **41.7%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `5613821836`, score-table `76292bed2d85`, model-set `89c8da7a07e7`. 1 general, 7 filegroup, 53 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
