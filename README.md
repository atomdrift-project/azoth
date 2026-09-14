# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 19,413,768-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,421,728-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 52 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 108 | 0.998672 | 0.990641 | 0.985984 | 97.24% | — |
| [`html`](filetypes/html/README.md) | 33 / 32,781 | 0.969766 | 0.986709 | 0.984615 | 96.97% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,117 / 4,039 | 0.994856 | 0.985380 | 0.960127 | 90.51% | — |
| [`elf`](filetypes/elf/README.md) | 24,904 / 111,318 | 0.997592 | 0.998943 | 0.990343 | 87.52% | PR +0.004292 / ROC +0.005643 |
| [`lnk`](filetypes/lnk/README.md) | 584 / 145 | 0.996712 | 0.986898 | 0.982218 | 82.53% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,761 / 9,429 | 0.975633 | 0.980886 | 0.971714 | 77.62% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 118 / 1,001 | 0.841227 | 0.934709 | 0.855769 | 75.42% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,558 / 3,717 | 0.982763 | 0.894074 | 0.933915 | 72.90% | PR -0.010537 / ROC -0.097126 |
| [`macho`](filetypes/macho/README.md) | 370 / 4,664 | 0.926976 | 0.973913 | 0.920174 | 69.46% | — |
| [`tar`](filetypes/tar/README.md) | 3,155 / 10,596 | 0.955713 | 0.970542 | 0.918589 | 68.87% | — |
| [`npm`](filetypes/npm/README.md) | 2,174 / 19,745 | 0.948890 | 0.971227 | 0.930166 | 68.77% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,762 / 474 | 0.992447 | 0.976936 | 0.963067 | 62.94% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 32 / 2,218 | 0.853182 | 0.931336 | 0.885246 | 62.50% | — |
| [`perl`](filetypes/perl/README.md) | 63 / 9,986 | 0.709023 | 0.937408 | 0.769231 | 60.32% | — |
| [`pe`](filetypes/pe/README.md) | 202,703 / 33,181 | 0.998754 | 0.992551 | 0.983337 | 59.54% | PR +0.000454 / ROC -0.005649 |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 466 / 147,907 | 0.654717 | 0.846508 | 0.758893 | 56.65% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,808 / 10,678 | 0.953361 | 0.971252 | 0.903193 | 53.52% | — |
| [`jar`](filetypes/jar/README.md) | 508 / 5,055 | 0.900522 | 0.961713 | 0.881250 | 52.76% | — |
| [`shell`](filetypes/shell/README.md) | 2,434 / 21,010 | 0.924107 | 0.963401 | 0.897240 | 50.00% | — |
| [`powershell`](filetypes/powershell/README.md) | 733 / 734 | 0.967947 | 0.954097 | 0.939776 | 49.66% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 774 | 0.942159 | 0.963553 | 0.873440 | 45.73% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,984 / 223,193 | 0.886903 | 0.948103 | 0.855283 | 45.28% | — |
| [`php`](filetypes/php/README.md) | 911 / 77,376 | 0.685431 | 0.899147 | 0.737387 | 42.37% | — |
| `java_class` | 303 / 225,923 | 0.748637 | 0.931239 | 0.812500 | 41.58% | — |
| [`gem`](filetypes/gem/README.md) | 253 / 13,756 | 0.434376 | 0.658663 | 0.586592 | 41.50% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 283 / 53 | 0.979923 | 0.908827 | 0.947368 | 41.34% | — |
| [`python`](filetypes/python/README.md) | 2,950 / 83,805 | 0.761140 | 0.883202 | 0.785547 | 38.27% | — |
| [`whl`](filetypes/whl/README.md) | 500 / 5,512 | 0.849189 | 0.933195 | 0.802174 | 37.20% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 23,134 | 0.562865 | 0.846342 | 0.666667 | 36.54% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,219 | 0.520709 | 0.761296 | 0.580645 | 36.00% | — |
| [`zip`](filetypes/zip/README.md) | 13,962 / 8,045 | 0.909738 | 0.797415 | 0.818254 | 34.69% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 710 | 0.991032 | 0.910147 | 0.980037 | 32.53% | — |
| [`csharp`](filetypes/csharp/README.md) | 470 / 12,843 | 0.336212 | 0.645938 | 0.402662 | 24.26% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 246 / 1,330 | 0.690195 | 0.895880 | 0.669887 | 23.17% | — |
| [`batch`](filetypes/batch/README.md) | 22,318 / 1,046 | 0.993881 | 0.922830 | 0.992289 | 15.06% | — |
| `rust` | 260 / 42,893 | 0.010626 | 0.581263 | 0.062433 | 11.15% | — |
| `c` | 2,450 / 218,494 | 0.235409 | 0.621459 | 0.336401 | 10.20% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 195 / 5,615 | 0.169718 | 0.604252 | 0.235772 | 9.74% | — |
| [`deb`](filetypes/deb/README.md) | 62 / 3,471 | 0.130728 | 0.507412 | 0.194444 | 8.06% | — |
| `png` | 1,143 / 67,345 | 0.049403 | 0.347056 | 0.099106 | 5.34% | — |
| [`java`](filetypes/java/README.md) | 462 / 24,906 | 0.101975 | 0.566864 | 0.147208 | 4.98% | — |
| `json` | 194 / 32,680 | 0.053195 | 0.487676 | 0.097345 | 4.12% | — |
| `plist` | 81 / 12,593 | 0.009432 | 0.590936 | 0.028587 | 3.70% | — |
| [`go`](filetypes/go/README.md) | 2,226 / 29,713 | 0.271819 | 0.635608 | 0.289517 | 3.23% | — |
| `makefile` | 102 / 7,936 | 0.016003 | 0.397373 | 0.048780 | 2.94% | — |
| `xml` | 525 / 57,750 | 0.086306 | 0.525159 | 0.151515 | 2.67% | — |
| `yaml` | 134 / 2,030 | 0.068383 | 0.496074 | 0.118584 | 0.75% | — |
| [`text`](filetypes/text/README.md) | 576 / 41,680 | 0.055826 | 0.637897 | 0.075581 | 0.69% | — |
| [`7z`](filetypes/7z/README.md) | 1,173 / 40 | 0.999099 | 0.974744 | 0.987363 | — | — |
| `font` | 25 / 77 | 0.356892 | 0.631429 | 0.550725 | 0.00% | — |
| **Weighted avg** (by test pop) | **2,028,321** | **0.6541** | **0.8307** | **0.6836** | **41.1%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `4674529089`, score-table `1c8e20b260ce`, model-set `3b208a81a468`. 1 general, 7 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
