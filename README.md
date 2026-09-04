# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 17,626,984-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,198,969-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 52 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 99 | 0.998228 | 0.990160 | 0.986103 | 97.24% | — |
| [`html`](filetypes/html/README.md) | 33 / 10,259 | 0.970102 | 0.992807 | 0.984615 | 96.97% | — |
| `pkg_info` | 1,170 / 2,165 | 0.985349 | 0.985198 | 0.980000 | 95.56% | — |
| [`gem`](filetypes/gem/README.md) | 111 / 1,051 | 0.949943 | 0.959459 | 0.967442 | 93.69% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,634 / 3,963 | 0.995229 | 0.986523 | 0.966303 | 91.64% | — |
| [`elf`](filetypes/elf/README.md) | 24,380 / 101,603 | 0.998254 | 0.999265 | 0.994776 | 86.37% | PR +0.004954 / ROC +0.005965 |
| [`lnk`](filetypes/lnk/README.md) | 578 / 145 | 0.997898 | 0.991821 | 0.987952 | 82.53% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,801 | 0.799441 | 0.917224 | 0.875000 | 77.78% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,602 / 472 | 0.993784 | 0.980621 | 0.962387 | 73.22% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,579 / 8,200 | 0.975088 | 0.981259 | 0.968333 | 72.35% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,514 / 3,681 | 0.991203 | 0.951506 | 0.952942 | 71.72% | PR -0.002097 / ROC -0.039694 |
| [`macho`](filetypes/macho/README.md) | 365 / 4,018 | 0.966201 | 0.988398 | 0.943662 | 70.41% | — |
| [`tar`](filetypes/tar/README.md) | 3,160 / 9,434 | 0.959934 | 0.972036 | 0.919947 | 70.32% | — |
| [`pe`](filetypes/pe/README.md) | 170,057 / 29,511 | 0.999178 | 0.995347 | 0.988576 | 63.31% | PR +0.000878 / ROC -0.002853 |
| [`shell`](filetypes/shell/README.md) | 2,402 / 20,136 | 0.925943 | 0.962247 | 0.895700 | 62.28% | — |
| [`npm`](filetypes/npm/README.md) | 869 / 4,127 | 0.919856 | 0.947090 | 0.881880 | 59.49% | — |
| `python_bytecode` | 465 / 127,368 | 0.653268 | 0.828568 | 0.757106 | 57.85% | — |
| [`powershell`](filetypes/powershell/README.md) | 732 / 701 | 0.969125 | 0.955510 | 0.946403 | 54.78% | — |
| [`jar`](filetypes/jar/README.md) | 510 / 3,667 | 0.902814 | 0.962471 | 0.872802 | 54.12% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,889 / 10,617 | 0.952278 | 0.972336 | 0.897159 | 53.82% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,167 | 0.574422 | 0.879645 | 0.682927 | 50.00% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,411 / 206,546 | 0.899420 | 0.961200 | 0.864714 | 48.35% | — |
| [`whl`](filetypes/whl/README.md) | 485 / 2,077 | 0.838805 | 0.904920 | 0.772443 | 47.42% | — |
| [`python`](filetypes/python/README.md) | 2,884 / 80,068 | 0.764454 | 0.903846 | 0.791298 | 46.81% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 769 | 0.945958 | 0.964514 | 0.888889 | 46.42% | — |
| `java_class` | 290 / 214,456 | 0.787477 | 0.934248 | 0.842505 | 46.21% | — |
| [`php`](filetypes/php/README.md) | 853 / 76,628 | 0.730427 | 0.927411 | 0.762619 | 46.07% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,102 | 0.544112 | 0.757214 | 0.595745 | 36.00% | — |
| [`zip`](filetypes/zip/README.md) | 13,768 / 5,319 | 0.936219 | 0.832177 | 0.847861 | 33.34% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 354 | 0.993889 | 0.892386 | 0.988967 | 31.08% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,688 | 0.315392 | 0.600499 | 0.400657 | 22.32% | — |
| [`batch`](filetypes/batch/README.md) | 22,140 / 1,006 | 0.999710 | 0.995894 | 0.996922 | 15.23% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 179 / 5,605 | 0.216995 | 0.570336 | 0.274882 | 10.61% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 3,403 | 0.135068 | 0.544466 | 0.189189 | 10.34% | — |
| `png` | 1,087 / 66,193 | 0.054840 | 0.426848 | 0.104363 | 5.61% | — |
| `text` | 490 / 40,372 | 0.031830 | 0.621514 | 0.088889 | 5.31% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,708 | 0.131023 | 0.664261 | 0.161959 | 5.21% | — |
| `plist` | 80 / 12,559 | 0.009794 | 0.595460 | 0.030338 | 3.75% | — |
| `makefile` | 102 / 7,863 | 0.012642 | 0.331738 | 0.042553 | 2.94% | — |
| [`xml`](filetypes/xml/README.md) | 499 / 57,021 | 0.082399 | 0.490496 | 0.159445 | 2.20% | — |
| [`go`](filetypes/go/README.md) | 2,087 / 29,397 | 0.252497 | 0.646434 | 0.276347 | 2.20% | — |
| [`json`](filetypes/json/README.md) | 304 / 31,658 | 0.060727 | 0.601762 | 0.098462 | 1.64% | — |
| `rust` | 259 / 41,587 | 0.076644 | 0.600911 | 0.135135 | 1.54% | — |
| `c` | 2,291 / 209,955 | 0.055236 | 0.590085 | 0.217500 | 0.35% | — |
| [`7z`](filetypes/7z/README.md) | 1,169 / 27 | 0.999036 | 0.960317 | 0.988584 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 42 | 0.983441 | 0.916840 | 0.956217 | — | — |
| **Weighted avg** (by test pop) | **1,839,842** | **0.6311** | **0.8313** | **0.6680** | **40.7%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `3915237856`, score-table `4a3f4114601d`, model-set `2a7e1fdbde0a`. 1 general, 6 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
