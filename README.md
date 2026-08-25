# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 62 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 17,132,677-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,138,242-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 66 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 831 / 98 | 0.998304 | 0.985038 | 0.989051 | 97.83% | — |
| [`html`](filetypes/html/README.md) | 31 / 8,468 | 0.976075 | 0.999661 | 0.983607 | 96.77% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 2,108 | 0.992282 | 0.994043 | 0.979968 | 95.98% | — |
| [`gem`](filetypes/gem/README.md) | 97 / 382 | 0.956124 | 0.969585 | 0.962567 | 92.78% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,627 / 3,960 | 0.994842 | 0.986088 | 0.966689 | 92.03% | — |
| [`elf`](filetypes/elf/README.md) | 24,228 / 97,932 | 0.998904 | 0.999478 | 0.995548 | 90.30% | PR +0.005604 / ROC +0.006178 |
| [`package.json`](filetypes/package.json/README.md) | 2,546 / 7,763 | 0.976233 | 0.980204 | 0.972919 | 83.39% | — |
| [`lnk`](filetypes/lnk/README.md) | 576 / 140 | 0.995148 | 0.984660 | 0.983435 | 82.64% | — |
| [`macho`](filetypes/macho/README.md) | 365 / 3,904 | 0.967799 | 0.985932 | 0.946779 | 75.89% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`tar`](filetypes/tar/README.md) | 3,214 / 9,046 | 0.971408 | 0.976746 | 0.941459 | 72.84% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,592 / 472 | 0.994162 | 0.982287 | 0.964230 | 72.49% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,672 | 0.992123 | 0.958918 | 0.972857 | 71.40% | PR -0.001177 / ROC -0.032282 |
| [`perl`](filetypes/perl/README.md) | 45 / 9,525 | 0.794483 | 0.916044 | 0.864198 | 71.11% | — |
| [`npm`](filetypes/npm/README.md) | 714 / 992 | 0.921692 | 0.908152 | 0.863331 | 68.49% | — |
| [`powershell`](filetypes/powershell/README.md) | 739 / 662 | 0.979322 | 0.970640 | 0.948169 | 66.31% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 464 / 126,333 | 0.686814 | 0.898099 | 0.788586 | 60.99% | — |
| [`shell`](filetypes/shell/README.md) | 2,385 / 19,792 | 0.920529 | 0.961609 | 0.894163 | 60.59% | — |
| [`pe`](filetypes/pe/README.md) | 169,785 / 28,519 | 0.999052 | 0.994209 | 0.989184 | 56.19% | PR +0.000752 / ROC -0.003991 |
| [`kotlin`](filetypes/kotlin/README.md) | 3,890 / 10,538 | 0.954051 | 0.973586 | 0.897556 | 54.83% | — |
| [`python`](filetypes/python/README.md) | 2,874 / 79,001 | 0.769879 | 0.909616 | 0.794418 | 53.69% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,312 / 201,824 | 0.896171 | 0.958601 | 0.872322 | 50.44% | — |
| [`whl`](filetypes/whl/README.md) | 488 / 1,698 | 0.860806 | 0.908702 | 0.785276 | 46.72% | — |
| [`php`](filetypes/php/README.md) | 850 / 76,410 | 0.713158 | 0.923493 | 0.762376 | 44.35% | — |
| [`crx`](filetypes/crx/README.md) | 299 / 700 | 0.908854 | 0.929907 | 0.853543 | 41.81% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,119 | 0.550771 | 0.873931 | 0.651163 | 38.46% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,070 | 0.556738 | 0.719318 | 0.636364 | 36.00% | — |
| [`jar`](filetypes/jar/README.md) | 508 / 3,580 | 0.870527 | 0.952522 | 0.841779 | 35.63% | — |
| [`java_class`](filetypes/java_class/README.md) | 287 / 214,359 | 0.791513 | 0.954734 | 0.846300 | 34.49% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,563 / 352 | 0.991759 | 0.852270 | 0.984191 | 33.81% | — |
| [`zip`](filetypes/zip/README.md) | 13,475 / 4,532 | 0.941161 | 0.824909 | 0.863842 | 30.62% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 12,462 | 0.336792 | 0.686770 | 0.403909 | 23.39% | — |
| [`batch`](filetypes/batch/README.md) | 22,140 / 1,003 | 0.994982 | 0.934516 | 0.994365 | 15.61% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 179 / 5,580 | 0.195570 | 0.599710 | 0.279476 | 13.41% | — |
| [`c`](filetypes/c/README.md) | 2,289 / 208,056 | 0.232238 | 0.644013 | 0.327739 | 11.01% | — |
| [`png`](filetypes/png/README.md) | 1,087 / 64,556 | 0.074327 | 0.558300 | 0.104901 | 5.52% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 579 | 0.188322 | 0.617651 | 0.324324 | 4.00% | — |
| [`go`](filetypes/go/README.md) | 2,095 / 28,545 | 0.245440 | 0.621200 | 0.260768 | 3.96% | — |
| [`json`](filetypes/json/README.md) | 203 / 31,118 | 0.049009 | 0.416193 | 0.082949 | 3.94% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 3,302 | 0.080009 | 0.519176 | 0.150000 | 3.45% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 12,517 | 0.040380 | 0.607718 | 0.066667 | 2.38% | — |
| [`xml`](filetypes/xml/README.md) | 504 / 56,014 | 0.084355 | 0.552189 | 0.156250 | 2.18% | — |
| [`java`](filetypes/java/README.md) | 461 / 22,665 | 0.111871 | 0.765762 | 0.156489 | 1.95% | — |
| [`rust`](filetypes/rust/README.md) | 259 / 41,421 | 0.075886 | 0.622449 | 0.144509 | 1.54% | — |
| [`text`](filetypes/text/README.md) | 490 / 39,864 | 0.058295 | 0.565323 | 0.090253 | 1.22% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 7,834 | 0.023231 | 0.389066 | 0.049180 | 0.98% | — |
| [`7z`](filetypes/7z/README.md) | 1,167 / 27 | 0.998772 | 0.950586 | 0.989402 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 42 | 0.953880 | 0.753172 | 0.933566 | — | — |
| **Weighted avg** (by test pop) | **1,811,824** | **0.6530** | **0.8477** | **0.6836** | **40.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `3450504705`, score-table `b624ff12d530`, model-set `b3d7dde50c0a`. 1 general, 7 filegroup, 66 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
