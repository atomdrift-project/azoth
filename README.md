# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 60 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 17,074,459-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,129,520-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 64 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 831 / 98 | 0.998274 | 0.984657 | 0.985967 | 97.47% | — |
| [`html`](filetypes/html/README.md) | 31 / 7,966 | 0.975434 | 0.999599 | 0.983607 | 96.77% | — |
| `gem` | 92 / 305 | 0.964434 | 0.978190 | 0.960452 | 92.39% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,621 / 3,948 | 0.995623 | 0.987895 | 0.965715 | 92.15% | — |
| [`elf`](filetypes/elf/README.md) | 24,079 / 90,142 | 0.997540 | 0.998869 | 0.994475 | 89.36% | PR +0.004240 / ROC +0.005569 |
| [`package.json`](filetypes/package.json/README.md) | 2,524 / 6,538 | 0.979841 | 0.985126 | 0.972874 | 83.00% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,584 / 472 | 0.993559 | 0.980352 | 0.960352 | 79.42% | — |
| [`lnk`](filetypes/lnk/README.md) | 574 / 139 | 0.996810 | 0.988200 | 0.981563 | 78.92% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920177 | 0.991862 | 0.869565 | 75.32% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,651 | 0.991535 | 0.951514 | 0.961642 | 74.06% | PR -0.001765 / ROC -0.039686 |
| [`tar`](filetypes/tar/README.md) | 3,205 / 8,581 | 0.972465 | 0.977546 | 0.941568 | 71.39% | — |
| [`macho`](filetypes/macho/README.md) | 364 / 3,469 | 0.969291 | 0.988029 | 0.947518 | 70.05% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,427 | 0.796011 | 0.902793 | 0.847059 | 68.89% | — |
| [`npm`](filetypes/npm/README.md) | 625 / 864 | 0.944794 | 0.937775 | 0.899251 | 65.12% | — |
| [`pe`](filetypes/pe/README.md) | 169,591 / 26,413 | 0.999535 | 0.997185 | 0.991899 | 61.25% | PR +0.001235 / ROC -0.001015 |
| [`powershell`](filetypes/powershell/README.md) | 739 / 626 | 0.966779 | 0.947694 | 0.935933 | 61.03% | — |
| [`shell`](filetypes/shell/README.md) | 2,361 / 19,187 | 0.916814 | 0.962914 | 0.883810 | 59.72% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,889 / 10,501 | 0.961563 | 0.977026 | 0.922490 | 55.54% | — |
| [`python`](filetypes/python/README.md) | 2,869 / 76,332 | 0.770994 | 0.918573 | 0.788755 | 53.75% | — |
| [`whl`](filetypes/whl/README.md) | 468 / 1,195 | 0.880907 | 0.909387 | 0.819565 | 52.99% | — |
| [`jar`](filetypes/jar/README.md) | 505 / 3,199 | 0.889498 | 0.950622 | 0.870488 | 52.67% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 2,027 | 0.995275 | 0.996598 | 0.980800 | 49.92% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,227 / 181,624 | 0.910422 | 0.967656 | 0.866027 | 49.69% | — |
| [`crx`](filetypes/crx/README.md) | 297 / 484 | 0.911407 | 0.919815 | 0.851351 | 43.77% | — |
| [`php`](filetypes/php/README.md) | 840 / 74,572 | 0.690062 | 0.882595 | 0.728614 | 42.50% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 463 / 111,174 | 0.689700 | 0.861330 | 0.781250 | 39.74% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 21,922 | 0.601553 | 0.868259 | 0.682927 | 36.54% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,033 | 0.528864 | 0.689051 | 0.611765 | 36.00% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,561 / 352 | 0.993178 | 0.884542 | 0.989744 | 33.59% | — |
| [`java_class`](filetypes/java_class/README.md) | 283 / 212,944 | 0.783194 | 0.947992 | 0.838207 | 32.51% | — |
| [`zip`](filetypes/zip/README.md) | 13,413 / 3,827 | 0.951575 | 0.840693 | 0.892271 | 32.20% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,035 | 0.337531 | 0.692857 | 0.410596 | 22.96% | — |
| [`batch`](filetypes/batch/README.md) | 22,139 / 985 | 0.993674 | 0.916070 | 0.993066 | 15.65% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 179 / 5,552 | 0.206450 | 0.583170 | 0.266667 | 10.61% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 3,108 | 0.146201 | 0.764077 | 0.187500 | 10.34% | — |
| [`c`](filetypes/c/README.md) | 2,289 / 206,000 | 0.231575 | 0.671526 | 0.330150 | 9.17% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 585 | 0.224523 | 0.590427 | 0.324324 | 8.00% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,235 | 0.115057 | 0.688046 | 0.154135 | 4.56% | — |
| [`json`](filetypes/json/README.md) | 202 / 28,951 | 0.056421 | 0.694280 | 0.075085 | 3.47% | — |
| [`go`](filetypes/go/README.md) | 2,098 / 27,229 | 0.228899 | 0.581526 | 0.249009 | 3.19% | — |
| [`xml`](filetypes/xml/README.md) | 504 / 54,712 | 0.095061 | 0.561221 | 0.159722 | 2.78% | — |
| [`text`](filetypes/text/README.md) | 490 / 38,794 | 0.073764 | 0.573282 | 0.115523 | 2.65% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 12,298 | 0.045574 | 0.686032 | 0.065934 | 2.38% | — |
| [`png`](filetypes/png/README.md) | 1,088 / 62,705 | 0.087754 | 0.660729 | 0.104439 | 1.47% | — |
| [`rust`](filetypes/rust/README.md) | 259 / 40,446 | 0.087114 | 0.666080 | 0.160221 | 1.16% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 7,800 | 0.024760 | 0.387944 | 0.050926 | 0.98% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 267 / 30 | 0.963241 | 0.743071 | 0.946809 | — | — |
| **Weighted avg** (by test pop) | **1,740,889** | **0.6521** | **0.8555** | **0.6788** | **38.3%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `3084319633`, score-table `859f6f881e88`, model-set `d8661a0d4c88`. 1 general, 7 filegroup, 64 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
