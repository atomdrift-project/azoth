# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 20 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,947,600-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,946,507-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 24 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| `rtf` | 831 / 95 | 0.998671 | 0.988707 | 0.986634 | 97.23% | — |
| `html` | 31 / 7,406 | 0.969730 | 0.997981 | 0.983607 | 96.77% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,621 / 3,946 | 0.996023 | 0.988887 | 0.965946 | 90.87% | — |
| [`elf`](filetypes/elf/README.md) | 24,073 / 87,203 | 0.997043 | 0.998523 | 0.993612 | 90.32% | PR +0.003743 / ROC +0.005223 |
| `gem` | 92 / 279 | 0.950496 | 0.949431 | 0.955056 | 90.22% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 9,393 | 0.798813 | 0.885239 | 0.867470 | 76.09% | — |
| [`macho`](filetypes/macho/README.md) | 364 / 3,304 | 0.950419 | 0.976859 | 0.940678 | 75.00% | — |
| `pkg_info` | 1,270 / 2,022 | 0.995836 | 0.996842 | 0.980423 | 72.44% | — |
| `registry` | 77 / 13,654 | 0.854055 | 0.996462 | 0.815385 | 68.83% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,583 / 471 | 0.992971 | 0.978549 | 0.957947 | 66.08% | — |
| [`powershell`](filetypes/powershell/README.md) | 739 / 615 | 0.970522 | 0.954529 | 0.935282 | 64.82% | — |
| `lnk` | 574 / 137 | 0.970160 | 0.859801 | 0.910112 | 61.50% | — |
| [`pe`](filetypes/pe/README.md) | 169,589 / 25,885 | 0.999092 | 0.994208 | 0.988102 | 61.42% | PR +0.000792 / ROC -0.003992 |
| `npm` | 626 / 815 | 0.912559 | 0.897713 | 0.838095 | 58.15% | — |
| `python_bytecode` | 462 / 107,533 | 0.679968 | 0.868079 | 0.775928 | 54.33% | — |
| [`shell`](filetypes/shell/README.md) | 2,363 / 19,023 | 0.917671 | 0.962213 | 0.888091 | 53.24% | — |
| [`whl`](filetypes/whl/README.md) | 455 / 1,084 | 0.890970 | 0.914649 | 0.817797 | 52.09% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,256 / 173,979 | 0.906385 | 0.963984 | 0.859900 | 51.34% | — |
| [`python`](filetypes/python/README.md) | 2,884 / 74,830 | 0.773676 | 0.921743 | 0.793694 | 51.14% | — |
| [`php`](filetypes/php/README.md) | 840 / 74,498 | 0.696675 | 0.891452 | 0.752907 | 48.45% | — |
| `kotlin` | 3,889 / 10,462 | 0.799110 | 0.815892 | 0.772576 | 44.36% | — |
| `tar` | 3,211 / 8,440 | 0.957277 | 0.970034 | 0.905201 | 42.14% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,001 | 0.551845 | 0.690769 | 0.629213 | 36.00% | — |
| `ooxml` | 8,561 / 352 | 0.976847 | 0.566263 | 0.979968 | 29.52% | — |
| `jar` | 504 / 3,178 | 0.869544 | 0.939559 | 0.844211 | 28.57% | — |
| [`zip`](filetypes/zip/README.md) | 13,395 / 3,613 | 0.951726 | 0.832911 | 0.896019 | 28.00% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,035 | 0.338365 | 0.712790 | 0.402597 | 23.61% | — |
| [`batch`](filetypes/batch/README.md) | 22,140 / 986 | 0.991462 | 0.886561 | 0.992736 | 15.52% | — |
| `ruby` | 52 / 21,915 | 0.504389 | 0.861189 | 0.650602 | 11.54% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 26 / 580 | 0.199233 | 0.557394 | 0.300000 | 7.69% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,051 | 0.133866 | 0.689509 | 0.155756 | 5.64% | — |
| `text` | 507 / 38,124 | 0.080100 | 0.611600 | 0.116402 | 3.55% | — |
| `json` | 208 / 28,762 | 0.074777 | 0.748099 | 0.145876 | 3.37% | — |
| `plist` | 84 / 12,271 | 0.041421 | 0.606647 | 0.063830 | 2.38% | — |
| `crx` | 303 / 401 | 0.874123 | 0.887139 | 0.822257 | 1.98% | — |
| `rust` | 259 / 40,235 | 0.077310 | 0.642804 | 0.134048 | 1.93% | — |
| `deb` | 59 / 3,082 | 0.072508 | 0.628873 | 0.157895 | 1.69% | — |
| `go` | 2,222 / 27,162 | 0.226487 | 0.594265 | 0.237505 | 1.40% | — |
| `makefile` | 104 / 7,757 | 0.024303 | 0.425254 | 0.056000 | 0.96% | — |
| `apk_android` | 267 / 30 | 0.921247 | 0.472971 | 0.946809 | — | — |
| `c` | 2,302 / 203,483 | — | — | — | — | — |
| `java_class` | 283 / 212,788 | — | — | — | — | — |
| `jpeg` | 180 / 5,518 | — | — | — | — | — |
| `package.json` | 2,526 / 6,487 | — | — | — | — | — |
| `pdf` | 22,517 / 3,647 | — | — | — | — | — |
| `png` | 1,093 / 61,602 | — | — | — | — | — |
| `xml` | 507 / 54,310 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,717,396** | **0.7460** | **0.8898** | **0.7573** | **48.0%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2609513337`, score-table `d0a59e30f097`, model-set `fbfc44b40bc8`. 1 general, 7 filegroup, 24 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
