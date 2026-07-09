# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 57 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,689,197-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,688,446-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 61 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`html`](filetypes/html/README.md) | 31 / 2,010 | 0.994058 | 0.999928 | 0.983607 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 830 / 94 | 0.999073 | 0.991694 | 0.990315 | 98.67% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 1,458 | 0.997678 | 0.997981 | 0.979608 | 96.30% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,495 / 5,423 | 0.993639 | 0.993504 | 0.985238 | 95.59% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,604 / 3,890 | 0.996123 | 0.989342 | 0.965977 | 93.16% | — |
| [`gem`](filetypes/gem/README.md) | 87 / 238 | 0.971549 | 0.982396 | 0.958084 | 91.95% | — |
| [`elf`](filetypes/elf/README.md) | 23,701 / 51,451 | 0.999370 | 0.999570 | 0.995893 | 90.37% | PR +0.006070 / ROC +0.006270 |
| [`vbs`](filetypes/vbs/README.md) | 1,561 / 458 | 0.997083 | 0.989767 | 0.975348 | 88.53% | — |
| [`macho`](filetypes/macho/README.md) | 361 / 2,684 | 0.974612 | 0.990846 | 0.943020 | 88.37% | — |
| [`lnk`](filetypes/lnk/README.md) | 569 / 132 | 0.994279 | 0.975249 | 0.976501 | 84.89% | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,188 | 0.835574 | 0.947847 | 0.863636 | 82.61% | — |
| [`tar`](filetypes/tar/README.md) | 3,160 / 7,577 | 0.973461 | 0.977205 | 0.940448 | 76.74% | — |
| [`registry`](filetypes/registry/README.md) | 68 / 10,091 | 0.896783 | 0.998915 | 0.828571 | 75.00% | — |
| [`shell`](filetypes/shell/README.md) | 2,307 / 16,235 | 0.939367 | 0.972917 | 0.889458 | 71.56% | — |
| [`npm`](filetypes/npm/README.md) | 457 / 568 | 0.936894 | 0.917331 | 0.876712 | 71.55% | — |
| [`whl`](filetypes/whl/README.md) | 429 / 766 | 0.933950 | 0.935079 | 0.875453 | 70.16% | — |
| [`crx`](filetypes/crx/README.md) | 281 / 288 | 0.956590 | 0.939835 | 0.901408 | 68.33% | — |
| [`powershell`](filetypes/powershell/README.md) | 726 / 579 | 0.976935 | 0.969701 | 0.933884 | 67.77% | — |
| [`pe`](filetypes/pe/README.md) | 169,208 / 24,020 | 0.998918 | 0.992506 | 0.987082 | 67.49% | PR +0.000618 / ROC -0.005694 |
| [`jar`](filetypes/jar/README.md) | 495 / 1,722 | 0.917996 | 0.949727 | 0.875000 | 66.26% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,891 / 9,063 | 0.928610 | 0.949046 | 0.867898 | 65.87% | — |
| [`php`](filetypes/php/README.md) | 798 / 67,574 | 0.723619 | 0.914586 | 0.735964 | 54.89% | — |
| [`python`](filetypes/python/README.md) | 2,858 / 63,656 | 0.831726 | 0.952009 | 0.791912 | 53.67% | — |
| [`zip`](filetypes/zip/README.md) | 13,327 / 3,107 | 0.953794 | 0.799638 | 0.909517 | 51.44% | — |
| [`javascript`](filetypes/javascript/README.md) | 16,869 / 150,451 | 0.924790 | 0.969785 | 0.877333 | 48.81% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 859 | 0.559359 | 0.700233 | 0.621622 | 46.00% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 461 / 85,356 | 0.685165 | 0.843842 | 0.780612 | 45.99% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,558 / 351 | 0.989268 | 0.811769 | 0.980406 | 44.09% | — |
| [`batch`](filetypes/batch/README.md) | 22,135 / 938 | 0.992960 | 0.904207 | 0.993787 | 33.29% | — |
| [`ruby`](filetypes/ruby/README.md) | 37 / 20,998 | 0.367049 | 0.856111 | 0.448980 | 29.73% | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 11,125 | 0.334164 | 0.711335 | 0.394737 | 22.75% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 180 / 5,392 | 0.169074 | 0.522279 | 0.233010 | 20.56% | — |
| [`dockerfile`](filetypes/dockerfile/README.md) | 25 / 545 | 0.256233 | 0.687339 | 0.333333 | 16.00% | — |
| [`deb`](filetypes/deb/README.md) | 58 / 2,386 | 0.132281 | 0.717653 | 0.158730 | 13.79% | — |
| [`c`](filetypes/c/README.md) | 2,297 / 169,046 | 0.239668 | 0.645178 | 0.330115 | 11.41% | — |
| [`json`](filetypes/json/README.md) | 204 / 19,305 | 0.082913 | 0.525969 | 0.128440 | 6.86% | — |
| [`go`](filetypes/go/README.md) | 2,113 / 26,475 | 0.307553 | 0.680005 | 0.315332 | 4.21% | — |
| [`text`](filetypes/text/README.md) | 500 / 32,370 | 0.091298 | 0.583226 | 0.124444 | 4.00% | — |
| [`plist`](filetypes/plist/README.md) | 84 / 11,955 | 0.038340 | 0.486226 | 0.067416 | 3.57% | — |
| [`xml`](filetypes/xml/README.md) | 506 / 49,354 | 0.186224 | 0.675730 | 0.270866 | 2.57% | — |
| [`makefile`](filetypes/makefile/README.md) | 102 / 7,395 | 0.028883 | 0.540631 | 0.056940 | 0.98% | — |
| [`java`](filetypes/java/README.md) | 460 / 19,276 | — | — | — | — | — |
| [`java_class`](filetypes/java_class/README.md) | 281 / 190,103 | — | — | — | — | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,425 | — | — | — | — | — |
| [`png`](filetypes/png/README.md) | 1,091 / 45,477 | — | — | — | — | — |
| [`rust`](filetypes/rust/README.md) | 259 / 39,672 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,492,339** | **0.6904** | **0.8568** | **0.7049** | **45.3%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2173356472`, score-table `e4b669f7ba3b`, model-set `2c596d1343d1`. 1 general, 7 filegroup, 61 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
