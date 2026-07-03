# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 53 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,610,244-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,608,866-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 57 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`html`](filetypes/html/README.md) | 31 / 1,993 | 1.000000 | 1.000000 | 1.000000 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 830 / 55 | 0.999098 | 0.986221 | 0.988478 | 97.95% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,264 / 484 | 0.998356 | 0.995977 | 0.982315 | 97.23% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,379 / 3,512 | 0.997523 | 0.997258 | 0.989878 | 96.93% | — |
| [`registry`](filetypes/registry/README.md) | 42 / 4,160 | 0.775017 | 0.998060 | 0.756757 | 95.24% | — |
| [`gem`](filetypes/gem/README.md) | 74 / 125 | 0.961984 | 0.960216 | 0.957746 | 94.59% | — |
| [`macho`](filetypes/macho/README.md) | 346 / 1,794 | 0.983369 | 0.994704 | 0.946108 | 91.62% | — |
| [`elf`](filetypes/elf/README.md) | 23,502 / 35,713 | 0.999938 | 0.999956 | 0.998064 | 91.43% | PR +0.006638 / ROC +0.006656 |
| [`tar`](filetypes/tar/README.md) | 2,774 / 6,035 | 0.991590 | 0.993042 | 0.974744 | 91.31% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,588 / 3,518 | 0.994263 | 0.981213 | 0.964140 | 90.98% | — |
| [`npm`](filetypes/npm/README.md) | 250 / 169 | 0.989385 | 0.984142 | 0.955466 | 90.80% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,553 / 434 | 0.992209 | 0.971292 | 0.957454 | 88.35% | — |
| [`jar`](filetypes/jar/README.md) | 481 / 1,159 | 0.958461 | 0.969880 | 0.923574 | 85.24% | — |
| [`whl`](filetypes/whl/README.md) | 339 / 652 | 0.948916 | 0.953945 | 0.906298 | 84.96% | — |
| [`shell`](filetypes/shell/README.md) | 2,055 / 9,594 | 0.970904 | 0.987080 | 0.925608 | 83.84% | — |
| [`powershell`](filetypes/powershell/README.md) | 717 / 333 | 0.987303 | 0.973890 | 0.949650 | 81.45% | — |
| [`perl`](filetypes/perl/README.md) | 43 / 5,691 | 0.806096 | 0.958104 | 0.839506 | 79.07% | — |
| [`pe`](filetypes/pe/README.md) | 169,035 / 22,111 | 0.999584 | 0.996939 | 0.992922 | 77.63% | PR +0.001284 / ROC -0.001261 |
| [`pdf`](filetypes/pdf/README.md) | 22,516 / 3,103 | 0.997834 | 0.985852 | 0.986752 | 76.49% | PR +0.004534 / ROC -0.005348 |
| [`lnk`](filetypes/lnk/README.md) | 567 / 132 | 0.975740 | 0.898596 | 0.904084 | 75.31% | — |
| [`java_class`](filetypes/java_class/README.md) | 266 / 104,445 | 0.830619 | 0.954711 | 0.867188 | 72.56% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 445 / 56,346 | 0.768788 | 0.885057 | 0.836272 | 66.74% | — |
| [`php`](filetypes/php/README.md) | 773 / 22,018 | 0.788798 | 0.908070 | 0.792227 | 63.26% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,896 / 6,920 | 0.955423 | 0.961603 | 0.901782 | 61.45% | — |
| [`javascript`](filetypes/javascript/README.md) | 15,583 / 93,214 | 0.944588 | 0.976975 | 0.898102 | 61.03% | — |
| [`python`](filetypes/python/README.md) | 2,584 / 33,556 | 0.818080 | 0.927506 | 0.802658 | 57.89% | — |
| [`zip`](filetypes/zip/README.md) | 12,973 / 2,097 | 0.993860 | 0.965653 | 0.975384 | 55.05% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,541 / 295 | 0.987044 | 0.722723 | 0.983024 | 39.84% | — |
| [`ruby`](filetypes/ruby/README.md) | 26 / 4,769 | 0.362894 | 0.774642 | 0.450000 | 34.62% | — |
| [`csharp`](filetypes/csharp/README.md) | 452 / 9,833 | 0.409328 | 0.843619 | 0.400691 | 25.22% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 179 / 4,123 | 0.197596 | 0.592137 | 0.239234 | 21.23% | — |
| [`deb`](filetypes/deb/README.md) | 43 / 1,476 | 0.175565 | 0.742768 | 0.208333 | 18.60% | — |
| [`batch`](filetypes/batch/README.md) | 22,123 / 765 | 0.989857 | 0.821600 | 0.990518 | 14.71% | — |
| [`go`](filetypes/go/README.md) | 1,938 / 18,126 | 0.242392 | 0.670368 | 0.232938 | 6.91% | — |
| [`text`](filetypes/text/README.md) | 494 / 18,924 | 0.080226 | 0.496782 | 0.108209 | 5.67% | — |
| [`png`](filetypes/png/README.md) | 1,090 / 24,532 | 0.117939 | 0.587128 | 0.125443 | 5.50% | — |
| [`java`](filetypes/java/README.md) | 456 / 15,874 | 0.080299 | 0.459816 | 0.137405 | 5.26% | — |
| [`xml`](filetypes/xml/README.md) | 504 / 31,117 | 0.179242 | 0.517772 | 0.267537 | 4.76% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 1,677 | 0.106874 | 0.644682 | 0.149733 | 4.76% | — |
| [`rust`](filetypes/rust/README.md) | 246 / 12,733 | 0.073727 | 0.574489 | 0.099010 | 4.47% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 4,585 | 0.033679 | 0.441990 | 0.048193 | 2.94% | — |
| [`json`](filetypes/json/README.md) | 187 / 10,867 | 0.038455 | 0.605379 | 0.051125 | 1.60% | — |
| [`crx`](filetypes/crx/README.md) | 199 / 28 | 1.000000 | 1.000000 | 1.000000 | — | — |
| [`c`](filetypes/c/README.md) | 2,267 / 109,281 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,003,205** | **0.7854** | **0.8913** | **0.7894** | **59.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L50 (0.5 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `2037843653`, score-table `354360b608db`, model-set `cb439c0755af`. 1 general, 7 filegroup, 57 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
