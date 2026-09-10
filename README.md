# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 49 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 18,454,063-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,301,701-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 53 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 108 | 0.998620 | 0.991002 | 0.985984 | 97.24% | — |
| `html` | 33 / 24,541 | 0.969744 | 0.973520 | 0.984615 | 96.97% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,634 / 4,030 | 0.995723 | 0.989023 | 0.966490 | 91.50% | — |
| [`elf`](filetypes/elf/README.md) | 24,435 / 108,043 | 0.998072 | 0.999177 | 0.994747 | 86.21% | PR +0.004772 / ROC +0.005877 |
| [`lnk`](filetypes/lnk/README.md) | 579 / 145 | 0.997452 | 0.990048 | 0.987952 | 82.38% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,761 / 8,913 | 0.975006 | 0.979223 | 0.972883 | 80.41% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,853 | 0.836554 | 0.930242 | 0.864198 | 75.56% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,620 / 475 | 0.992737 | 0.976234 | 0.960000 | 73.15% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 116 / 307 | 0.971765 | 0.983320 | 0.923729 | 71.55% | — |
| [`npm`](filetypes/npm/README.md) | 2,115 / 13,451 | 0.948583 | 0.967007 | 0.929067 | 70.17% | — |
| `xml` | 524 / 57,669 | 0.007729 | 0.422190 | 0.017848 | 69.85% | — |
| [`macho`](filetypes/macho/README.md) | 369 / 4,378 | 0.970460 | 0.989643 | 0.945055 | 69.65% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 32 / 2,200 | 0.848665 | 0.944936 | 0.852459 | 68.75% | — |
| [`tar`](filetypes/tar/README.md) | 3,224 / 10,133 | 0.959343 | 0.972633 | 0.917521 | 68.55% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,514 / 3,704 | 0.993757 | 0.964733 | 0.974505 | 66.08% | PR +0.000457 / ROC -0.026467 |
| [`shell`](filetypes/shell/README.md) | 2,421 / 20,695 | 0.928855 | 0.964980 | 0.896640 | 62.87% | — |
| [`pe`](filetypes/pe/README.md) | 170,120 / 31,807 | 0.999134 | 0.995462 | 0.988467 | 62.57% | PR +0.000834 / ROC -0.002738 |
| [`kotlin`](filetypes/kotlin/README.md) | 3,881 / 10,655 | 0.939492 | 0.965563 | 0.864056 | 54.78% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 466 / 134,646 | 0.657157 | 0.883091 | 0.758256 | 50.00% | — |
| [`php`](filetypes/php/README.md) | 898 / 77,029 | 0.685573 | 0.898833 | 0.742633 | 49.33% | — |
| [`jar`](filetypes/jar/README.md) | 511 / 4,415 | 0.903698 | 0.956870 | 0.889583 | 49.32% | — |
| [`python`](filetypes/python/README.md) | 2,939 / 82,661 | 0.767909 | 0.886631 | 0.792299 | 47.16% | — |
| [`whl`](filetypes/whl/README.md) | 521 / 3,009 | 0.829248 | 0.909110 | 0.777882 | 47.02% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,768 / 216,359 | 0.891468 | 0.949223 | 0.864996 | 45.63% | — |
| [`powershell`](filetypes/powershell/README.md) | 733 / 727 | 0.968936 | 0.959295 | 0.942335 | 44.75% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 772 | 0.941459 | 0.962782 | 0.871080 | 43.34% | — |
| [`gem`](filetypes/gem/README.md) | 253 / 7,274 | 0.446076 | 0.570862 | 0.590529 | 41.90% | — |
| [`zip`](filetypes/zip/README.md) | 13,899 / 7,195 | 0.924701 | 0.843276 | 0.807885 | 38.19% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,180 | 0.517517 | 0.755678 | 0.567901 | 36.00% | — |
| `java_class` | 291 / 220,868 | 0.779687 | 0.939596 | 0.838095 | 35.40% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 710 | 0.988882 | 0.897301 | 0.970966 | 32.75% | — |
| [`csharp`](filetypes/csharp/README.md) | 467 / 12,802 | 0.333901 | 0.661423 | 0.407051 | 23.98% | — |
| [`batch`](filetypes/batch/README.md) | 22,141 / 1,038 | 0.991514 | 0.893231 | 0.993140 | 15.41% | — |
| [`c`](filetypes/c/README.md) | 2,311 / 214,280 | 0.250023 | 0.703922 | 0.356137 | 12.89% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,847 | 0.561745 | 0.824131 | 0.705882 | 11.54% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 193 / 5,611 | 0.199040 | 0.556652 | 0.251121 | 9.84% | — |
| [`deb`](filetypes/deb/README.md) | 61 / 3,480 | 0.128313 | 0.489773 | 0.194444 | 8.20% | — |
| `json` | 193 / 32,309 | 0.023114 | 0.696591 | 0.077465 | 5.70% | — |
| `png` | 1,137 / 66,767 | 0.054110 | 0.432082 | 0.100164 | 5.36% | — |
| [`java`](filetypes/java/README.md) | 462 / 24,117 | 0.133557 | 0.740159 | 0.150659 | 4.33% | — |
| `plist` | 81 / 12,580 | 0.016609 | 0.401976 | 0.065934 | 3.70% | — |
| [`text`](filetypes/text/README.md) | 563 / 41,240 | 0.061527 | 0.613725 | 0.085526 | 3.02% | — |
| `makefile` | 102 / 7,878 | 0.013724 | 0.399474 | 0.042553 | 2.94% | — |
| [`go`](filetypes/go/README.md) | 2,219 / 29,526 | 0.237037 | 0.620121 | 0.248599 | 2.30% | — |
| `rust` | 260 / 42,572 | 0.073453 | 0.671448 | 0.127226 | 1.54% | — |
| `yaml` | 109 / 1,476 | 0.063544 | 0.384373 | 0.130072 | 0.92% | — |
| [`7z`](filetypes/7z/README.md) | 1,172 / 36 | 0.998429 | 0.950145 | 0.985702 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 45 | 0.963896 | 0.883617 | 0.954386 | — | — |
| **Weighted avg** (by test pop) | **1,925,525** | **0.6518** | **0.8458** | **0.6813** | **42.3%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `4407144194`, score-table `4d0652e80290`, model-set `7e34169fa52c`. 1 general, 6 filegroup, 53 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
