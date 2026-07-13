# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 37 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,720,070-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,719,220-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| [`rtf`](filetypes/rtf/README.md) | 830 / 95 | 0.998618 | 0.992023 | 0.989078 | 98.31% | — |
| `pkg_info` | 1,270 / 1,655 | 0.995862 | 0.996702 | 0.980831 | 96.30% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,515 / 5,974 | 0.982270 | 0.983020 | 0.976368 | 94.79% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,604 / 3,904 | 0.995324 | 0.986357 | 0.965762 | 92.77% | — |
| [`gem`](filetypes/gem/README.md) | 88 / 256 | 0.967146 | 0.980291 | 0.958580 | 92.05% | — |
| [`elf`](filetypes/elf/README.md) | 23,750 / 58,662 | 0.997488 | 0.998429 | 0.993914 | 90.60% | PR +0.004188 / ROC +0.005129 |
| [`vbs`](filetypes/vbs/README.md) | 1,569 / 460 | 0.996932 | 0.989118 | 0.974149 | 89.36% | — |
| [`macho`](filetypes/macho/README.md) | 362 / 2,740 | 0.973984 | 0.988738 | 0.950355 | 87.85% | — |
| [`lnk`](filetypes/lnk/README.md) | 569 / 132 | 0.993218 | 0.972107 | 0.975779 | 85.06% | — |
| [`powershell`](filetypes/powershell/README.md) | 727 / 593 | 0.974305 | 0.956773 | 0.937677 | 80.19% | — |
| [`registry`](filetypes/registry/README.md) | 79 / 15,740 | 0.926281 | 0.990142 | 0.855072 | 77.22% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,638 | 0.806647 | 0.943575 | 0.839506 | 76.09% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,575 | 0.991369 | 0.947206 | 0.960701 | 74.67% | PR -0.001931 / ROC -0.043994 |
| [`crx`](filetypes/crx/README.md) | 286 / 298 | 0.947845 | 0.936617 | 0.891344 | 74.13% | — |
| [`tar`](filetypes/tar/README.md) | 3,187 / 7,792 | 0.972589 | 0.978552 | 0.939307 | 73.52% | — |
| [`shell`](filetypes/shell/README.md) | 2,316 / 16,637 | 0.940548 | 0.969834 | 0.901495 | 72.93% | — |
| [`npm`](filetypes/npm/README.md) | 521 / 682 | 0.932682 | 0.918390 | 0.864809 | 67.56% | — |
| [`whl`](filetypes/whl/README.md) | 431 / 815 | 0.928532 | 0.932263 | 0.871429 | 67.29% | — |
| [`pe`](filetypes/pe/README.md) | 169,247 / 24,513 | 0.999514 | 0.996795 | 0.991745 | 67.27% | PR +0.001214 / ROC -0.001405 |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 461 / 95,311 | 0.703858 | 0.893507 | 0.792746 | 64.64% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,890 / 9,191 | 0.892163 | 0.899475 | 0.852911 | 62.03% | — |
| [`python`](filetypes/python/README.md) | 2,870 / 67,581 | 0.793087 | 0.936401 | 0.796332 | 52.89% | — |
| [`zip`](filetypes/zip/README.md) | 13,349 / 3,221 | 0.950447 | 0.789528 | 0.899557 | 51.12% | — |
| [`php`](filetypes/php/README.md) | 800 / 69,963 | 0.742420 | 0.900377 | 0.751323 | 51.00% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 21,381 | 0.618497 | 0.868375 | 0.681818 | 48.08% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,559 / 351 | 0.992692 | 0.884054 | 0.992862 | 46.50% | — |
| `jar` | 498 / 2,371 | 0.879945 | 0.949773 | 0.844864 | 45.98% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 918 | 0.531723 | 0.700773 | 0.574713 | 38.00% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,010 | 0.536387 | 0.845386 | 0.516854 | 28.33% | — |
| `jpeg` | 180 / 5,414 | 0.173810 | 0.531772 | 0.240385 | 21.11% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 554 | 0.274753 | 0.705451 | 0.315789 | 20.00% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 2,461 | 0.130624 | 0.716778 | 0.158730 | 17.24% | — |
| `xml` | 505 / 46,777 | 0.126954 | 0.602914 | 0.209830 | 4.75% | — |
| `text` | 500 / 34,589 | 0.085724 | 0.612855 | 0.118492 | 3.80% | — |
| `go` | 2,114 / 26,711 | 0.228728 | 0.590955 | 0.254403 | 2.60% | — |
| `rust` | 259 / 39,936 | 0.087465 | 0.607898 | 0.154362 | 1.54% | — |
| `java` | 461 / 21,482 | 0.093962 | 0.711785 | 0.164049 | 1.30% | — |
| `makefile` | 102 / 7,428 | 0.028487 | 0.393687 | 0.077348 | 0.98% | — |
| `batch` | 22,136 / 956 | — | — | — | — | — |
| `c` | 2,297 / 170,627 | — | — | — | — | — |
| `java_class` | 281 / 206,933 | — | — | — | — | — |
| `javascript` | 17,142 / 162,108 | — | — | — | — | — |
| `json` | 206 / 26,101 | — | — | — | — | — |
| `plist` | 84 / 11,978 | — | — | — | — | — |
| `png` | 1,091 / 48,266 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,569,171** | **0.7216** | **0.8761** | **0.7377** | **53.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2269663951`, score-table `c432e1f3d36a`, model-set `f94770ed508f`. 1 general, 7 filegroup, 41 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
