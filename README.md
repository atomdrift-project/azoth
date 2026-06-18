# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 49 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,013,704-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,012,990-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 53 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 829 / 55 | 0.998848 | 0.990229 | 0.989666 | 100.00% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,344 / 3,158 | 0.996262 | 0.995181 | 0.991219 | 98.63% | — |
| [`elf`](filetypes/elf/README.md) | 23,425 / 24,529 | 0.999748 | 0.999734 | 0.995958 | 97.88% | PR +0.006448 / ROC +0.006434 |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,278 / 338 | 0.997198 | 0.990821 | 0.983320 | 97.18% | — |
| [`gem`](filetypes/gem/README.md) | 29 / 97 | 0.991668 | 0.997156 | 0.965517 | 96.55% | — |
| [`xls`](filetypes/xls/README.md) | 4,945 / 2,652 | 0.996209 | 0.991713 | 0.979411 | 95.96% | — |
| [`macho`](filetypes/macho/README.md) | 342 / 1,644 | 0.990628 | 0.996526 | 0.971599 | 95.61% | — |
| [`ole`](filetypes/ole/README.md) | 858 / 822 | 0.984820 | 0.978892 | 0.972813 | 95.57% | — |
| [`tar`](filetypes/tar/README.md) | 2,807 / 5,186 | 0.991008 | 0.991790 | 0.971387 | 91.02% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,531 / 429 | 0.994544 | 0.983745 | 0.969317 | 86.74% | — |
| [`shell`](filetypes/shell/README.md) | 2,039 / 8,665 | 0.978053 | 0.990506 | 0.941031 | 84.80% | — |
| [`powershell`](filetypes/powershell/README.md) | 715 / 332 | 0.982442 | 0.960626 | 0.940159 | 83.36% | — |
| [`docx`](filetypes/docx/README.md) | 595 / 62 | 0.988738 | 0.917932 | 0.954740 | 80.67% | — |
| [`perl`](filetypes/perl/README.md) | 41 / 5,536 | 0.804328 | 0.911486 | 0.857143 | 80.49% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 443 / 37,355 | 0.820398 | 0.914595 | 0.888889 | 79.91% | — |
| [`jar`](filetypes/jar/README.md) | 483 / 674 | 0.941571 | 0.941602 | 0.887417 | 78.26% | — |
| [`lnk`](filetypes/lnk/README.md) | 566 / 132 | 0.979200 | 0.913059 | 0.921803 | 76.68% | — |
| [`whl`](filetypes/whl/README.md) | 104 / 607 | 0.887052 | 0.936953 | 0.835165 | 75.96% | — |
| [`pe`](filetypes/pe/README.md) | 168,802 / 20,889 | 0.999425 | 0.995467 | 0.990536 | 75.20% | PR +0.001125 / ROC -0.002733 |
| [`pdf`](filetypes/pdf/README.md) | 22,516 / 3,091 | 0.989491 | 0.926535 | 0.966748 | 74.82% | PR -0.003809 / ROC -0.064665 |
| [`php`](filetypes/php/README.md) | 743 / 20,913 | 0.733997 | 0.883101 | 0.760099 | 62.45% | — |
| [`javascript`](filetypes/javascript/README.md) | 15,559 / 85,935 | 0.941720 | 0.972645 | 0.901999 | 59.48% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,901 / 7,344 | 0.907548 | 0.915430 | 0.869286 | 58.32% | — |
| [`zip`](filetypes/zip/README.md) | 13,116 / 2,211 | 0.970894 | 0.848844 | 0.936552 | 55.23% | — |
| [`ruby`](filetypes/ruby/README.md) | 25 / 3,536 | 0.469768 | 0.671024 | 0.585366 | 48.00% | — |
| [`python`](filetypes/python/README.md) | 2,922 / 29,969 | 0.769201 | 0.878419 | 0.782097 | 44.35% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 7,861 / 210 | 0.989283 | 0.716172 | 0.986819 | 39.16% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 30 / 244 | 0.434866 | 0.795082 | 0.418605 | 33.33% | — |
| [`csharp`](filetypes/csharp/README.md) | 458 / 9,814 | 0.374324 | 0.784269 | 0.389439 | 23.80% | — |
| [`deb`](filetypes/deb/README.md) | 54 / 1,023 | 0.153316 | 0.634427 | 0.169492 | 22.22% | — |
| [`batch`](filetypes/batch/README.md) | 22,130 / 751 | 0.994076 | 0.910754 | 0.995103 | 21.54% | — |
| [`xml`](filetypes/xml/README.md) | 583 / 33,471 | 0.203471 | 0.622033 | 0.291725 | 12.35% | — |
| [`plist`](filetypes/plist/README.md) | 83 / 1,641 | 0.188978 | 0.780453 | 0.345455 | 9.64% | — |
| [`go`](filetypes/go/README.md) | 1,937 / 16,583 | 0.522987 | 0.843839 | 0.512793 | 6.81% | — |
| [`png`](filetypes/png/README.md) | 1,116 / 24,087 | 0.109764 | 0.559741 | 0.114420 | 5.56% | — |
| [`text`](filetypes/text/README.md) | 752 / 15,564 | 0.107235 | 0.579433 | 0.128649 | 4.52% | — |
| [`java`](filetypes/java/README.md) | 448 / 11,425 | 0.155522 | 0.745996 | 0.221840 | 4.46% | — |
| [`rust`](filetypes/rust/README.md) | 244 / 12,619 | 0.068253 | 0.603878 | 0.105946 | 4.10% | — |
| [`makefile`](filetypes/makefile/README.md) | 101 / 4,367 | 0.029240 | 0.498590 | 0.074766 | 0.99% | — |
| [`json`](filetypes/json/README.md) | 148 / 8,085 | 0.018976 | 0.456131 | 0.039526 | 0.68% | — |
| [`npm`](filetypes/npm/README.md) | 172 / 28 | 0.976968 | 0.864306 | 0.955307 | — | — |
| [`applescript`](filetypes/applescript/README.md) | 26 / 40 | 0.583084 | 0.539423 | 0.590909 | — | — |
| [`c`](filetypes/c/README.md) | 2,255 / 105,462 | — | — | — | — | — |
| [`java_class`](filetypes/java_class/README.md) | 262 / 101,848 | — | — | — | — | — |
| [`jpeg`](filetypes/jpeg/README.md) | 183 / 4,001 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **927,225** | **0.7924** | **0.8923** | **0.7940** | **57.3%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1750548459`, score-table `b092cb45e4f9`, model-set `9f16b72cb032`. 1 general, 7 filegroup, 53 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
