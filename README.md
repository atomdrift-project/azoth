# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,795,811-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,794,414-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 38 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`html`](filetypes/html/README.md) | 31 / 2,011 | 0.994058 | 0.999928 | 0.983607 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 830 / 95 | 0.998608 | 0.988484 | 0.989078 | 98.31% | — |
| `pkg_info` | 1,270 / 1,714 | 0.992300 | 0.993118 | 0.979984 | 96.38% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,522 / 6,222 | 0.983551 | 0.985995 | 0.975728 | 93.06% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,612 / 3,918 | 0.995002 | 0.985507 | 0.965765 | 92.91% | — |
| [`gem`](filetypes/gem/README.md) | 88 / 260 | 0.961962 | 0.975262 | 0.958580 | 92.05% | — |
| [`elf`](filetypes/elf/README.md) | 23,925 / 67,071 | 0.997851 | 0.998837 | 0.994481 | 89.65% | PR +0.004551 / ROC +0.005537 |
| [`macho`](filetypes/macho/README.md) | 364 / 2,947 | 0.970802 | 0.986808 | 0.944444 | 89.01% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,576 / 466 | 0.994775 | 0.981502 | 0.960127 | 86.87% | — |
| [`lnk`](filetypes/lnk/README.md) | 572 / 134 | 0.994424 | 0.977305 | 0.976583 | 85.49% | — |
| [`powershell`](filetypes/powershell/README.md) | 733 / 597 | 0.974726 | 0.957107 | 0.938862 | 82.13% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,892 | 0.793003 | 0.886307 | 0.843373 | 76.09% | — |
| [`registry`](filetypes/registry/README.md) | 79 / 26,307 | 0.918337 | 0.987021 | 0.867133 | 75.95% | — |
| [`tar`](filetypes/tar/README.md) | 3,188 / 7,986 | 0.971776 | 0.977177 | 0.937311 | 75.00% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,591 | 0.997862 | 0.988234 | 0.987018 | 74.55% | PR +0.004562 / ROC -0.002966 |
| [`npm`](filetypes/npm/README.md) | 590 / 858 | 0.941934 | 0.931696 | 0.876937 | 71.19% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 318 | 0.942556 | 0.935100 | 0.893238 | 70.65% | — |
| [`shell`](filetypes/shell/README.md) | 2,343 / 17,115 | 0.936962 | 0.969860 | 0.897056 | 70.21% | — |
| [`whl`](filetypes/whl/README.md) | 439 / 909 | 0.920883 | 0.925813 | 0.859880 | 68.34% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,889 / 9,357 | 0.959960 | 0.973130 | 0.903461 | 63.10% | — |
| [`jar`](filetypes/jar/README.md) | 502 / 2,881 | 0.915896 | 0.965436 | 0.882227 | 62.75% | — |
| [`pe`](filetypes/pe/README.md) | 169,400 / 25,388 | 0.999158 | 0.994554 | 0.988611 | 56.71% | PR +0.000858 / ROC -0.003646 |
| `python_bytecode` | 462 / 102,472 | 0.680918 | 0.860355 | 0.780178 | 56.49% | — |
| [`zip`](filetypes/zip/README.md) | 13,365 / 3,342 | 0.948820 | 0.789075 | 0.898730 | 51.84% | — |
| [`python`](filetypes/python/README.md) | 2,871 / 70,592 | 0.776935 | 0.923672 | 0.795437 | 48.66% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,188 / 167,897 | 0.901988 | 0.961906 | 0.865582 | 46.95% | — |
| [`php`](filetypes/php/README.md) | 813 / 72,680 | 0.693827 | 0.881214 | 0.748538 | 45.88% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,559 / 351 | 0.993490 | 0.896369 | 0.992514 | 45.19% | — |
| `ruby` | 52 / 21,706 | 0.535607 | 0.865968 | 0.658824 | 44.23% | — |
| `java_class` | 282 / 210,477 | 0.781695 | 0.950698 | 0.831721 | 42.20% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 982 | 0.526705 | 0.681039 | 0.583333 | 42.00% | — |
| [`batch`](filetypes/batch/README.md) | 22,138 / 959 | 0.989253 | 0.853443 | 0.991380 | 33.25% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,027 | 0.336561 | 0.697082 | 0.401327 | 23.61% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 566 | 0.192195 | 0.654170 | 0.307692 | 16.00% | — |
| `jpeg` | 180 / 5,436 | 0.195647 | 0.626074 | 0.271186 | 14.44% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 2,639 | 0.143476 | 0.783091 | 0.164384 | 8.62% | — |
| `c` | 2,297 / 184,210 | 0.224243 | 0.647404 | 0.332434 | 6.53% | — |
| `text` | 500 / 35,586 | 0.086008 | 0.652157 | 0.116814 | 3.60% | — |
| `plist` | 84 / 12,001 | 0.040903 | 0.573202 | 0.065934 | 3.57% | — |
| `makefile` | 102 / 7,463 | 0.012513 | 0.297470 | 0.040541 | 2.94% | — |
| `json` | 207 / 27,356 | 0.083420 | 0.759877 | 0.158431 | 2.90% | — |
| `go` | 2,114 / 26,964 | 0.235508 | 0.653984 | 0.246543 | 2.41% | — |
| `rust` | 259 / 40,085 | 0.077514 | 0.635950 | 0.147541 | 1.16% | — |
| `java` | 461 / 21,704 | — | — | — | — | — |
| `png` | 1,091 / 48,532 | — | — | — | — | — |
| `xml` | 506 / 46,009 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,631,012** | **0.7011** | **0.8751** | **0.7297** | **43.7%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2448147370`, score-table `55980705c354`, model-set `29af87edef57`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
