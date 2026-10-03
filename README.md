# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 52 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 20,074,839-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,503,210-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 56 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 813 / 115 | 0.999238 | 0.994679 | 0.995676 | 99.14% | — |
| `gem` | 44 / 14,110 | 0.936359 | 0.989053 | 0.964706 | 93.18% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,026 / 4,153 | 0.994939 | 0.986352 | 0.958443 | 90.22% | — |
| [`html`](filetypes/html/README.md) | 37 / 37,213 | 0.922383 | 0.995629 | 0.944444 | 89.19% | — |
| [`elf`](filetypes/elf/README.md) | 24,821 / 112,755 | 0.995487 | 0.998104 | 0.986461 | 88.41% | PR +0.002187 / ROC +0.004804 |
| [`python_sdist`](filetypes/python_sdist/README.md) | 361 / 1,125 | 0.963785 | 0.977692 | 0.944928 | 88.37% | — |
| [`lnk`](filetypes/lnk/README.md) | 584 / 148 | 0.996294 | 0.985821 | 0.981293 | 80.14% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,744 / 9,525 | 0.962472 | 0.970352 | 0.958491 | 79.05% | — |
| [`batch`](filetypes/batch/README.md) | 22,277 / 1,132 | 0.999806 | 0.996415 | 0.995209 | 74.84% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,771 | 0.995498 | 0.974848 | 0.977494 | 71.35% | PR +0.002198 / ROC -0.016352 |
| [`registry`](filetypes/registry/README.md) | 80 / 13,660 | 0.886920 | 0.971604 | 0.835616 | 70.00% | — |
| [`macho`](filetypes/macho/README.md) | 308 / 4,765 | 0.907708 | 0.963095 | 0.877551 | 67.86% | — |
| [`npm`](filetypes/npm/README.md) | 3,206 / 24,893 | 0.938122 | 0.952168 | 0.927225 | 64.75% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 29 / 2,293 | 0.808268 | 0.913327 | 0.851852 | 62.07% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 414 / 152,875 | 0.668523 | 0.898037 | 0.780204 | 61.59% | — |
| [`perl`](filetypes/perl/README.md) | 52 / 10,079 | 0.789774 | 0.959337 | 0.842105 | 61.54% | — |
| `ico` | 33 / 86 | 0.696659 | 0.664553 | 0.730769 | 60.61% | — |
| [`python`](filetypes/python/README.md) | 2,734 / 84,473 | 0.817517 | 0.917413 | 0.809355 | 57.13% | — |
| [`java_class`](filetypes/java_class/README.md) | 311 / 228,620 | 0.780904 | 0.892232 | 0.835979 | 54.98% | — |
| [`tar`](filetypes/tar/README.md) | 1,936 / 10,680 | 0.951248 | 0.973219 | 0.907995 | 53.72% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,149 / 10,736 | 0.768030 | 0.817064 | 0.756788 | 52.97% | — |
| [`ruby`](filetypes/ruby/README.md) | 38 / 24,251 | 0.774852 | 0.959886 | 0.816901 | 52.63% | — |
| [`shell`](filetypes/shell/README.md) | 2,456 / 20,620 | 0.931567 | 0.968055 | 0.900402 | 51.87% | — |
| [`powershell`](filetypes/powershell/README.md) | 722 / 765 | 0.967116 | 0.959676 | 0.931915 | 51.80% | — |
| [`pe`](filetypes/pe/README.md) | 203,553 / 33,415 | 0.997385 | 0.984742 | 0.979980 | 51.68% | PR -0.000915 / ROC -0.013458 |
| [`jar`](filetypes/jar/README.md) | 454 / 5,201 | 0.924704 | 0.983439 | 0.876569 | 43.61% | — |
| [`zip`](filetypes/zip/README.md) | 13,642 / 12,302 | 0.893955 | 0.840736 | 0.818925 | 43.46% | — |
| [`php`](filetypes/php/README.md) | 832 / 77,831 | 0.720434 | 0.934829 | 0.741888 | 42.43% | — |
| [`vsix`](filetypes/vsix/README.md) | 50 / 744 | 0.706767 | 0.915753 | 0.698795 | 38.00% | — |
| [`crx`](filetypes/crx/README.md) | 301 / 1,480 | 0.952179 | 0.989021 | 0.876006 | 36.88% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,333 / 818 | 0.983660 | 0.876795 | 0.969361 | 30.43% | — |
| [`json`](filetypes/json/README.md) | 32 / 34,536 | 0.385152 | 0.691936 | 0.521739 | 28.12% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 117 / 1,436 | 0.417270 | 0.767151 | 0.418919 | 26.50% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 482 / 106 | 0.957321 | 0.836560 | 0.902184 | 25.10% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,387 / 225,155 | 0.839218 | 0.933242 | 0.808648 | 24.99% | — |
| [`deb`](filetypes/deb/README.md) | 43 / 3,429 | 0.234431 | 0.642146 | 0.346154 | 20.93% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,802 / 531 | 0.990423 | 0.967707 | 0.959161 | 19.53% | — |
| [`whl`](filetypes/whl/README.md) | 325 / 7,307 | 0.777155 | 0.965877 | 0.750383 | 18.77% | — |
| [`csharp`](filetypes/csharp/README.md) | 471 / 12,852 | 0.319924 | 0.652946 | 0.394089 | 17.62% | — |
| [`go`](filetypes/go/README.md) | 2,024 / 30,459 | 0.335824 | 0.634046 | 0.371943 | 13.88% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,645 | 0.179741 | 0.576244 | 0.262712 | 11.34% | — |
| `c` | 2,199 / 220,187 | 0.251771 | 0.699556 | 0.361233 | 8.96% | — |
| `rust` | 59 / 44,231 | 0.284641 | 0.858115 | 0.386364 | 8.47% | — |
| [`xml`](filetypes/xml/README.md) | 277 / 57,925 | 0.184954 | 0.527798 | 0.290030 | 8.30% | — |
| [`text`](filetypes/text/README.md) | 623 / 44,060 | 0.091197 | 0.546466 | 0.134953 | 5.46% | — |
| `png` | 1,132 / 67,932 | 0.066796 | 0.402574 | 0.102007 | 5.21% | — |
| [`java`](filetypes/java/README.md) | 415 / 24,946 | 0.071930 | 0.588405 | 0.126354 | 1.45% | — |
| [`7z`](filetypes/7z/README.md) | 1,121 / 47 | 0.998021 | 0.953727 | 0.979895 | — | — |
| [`gif`](filetypes/gif/README.md) | 85 / 202 | 0.348501 | 0.582324 | 0.456989 | 0.00% | — |
| **Weighted avg** (by test pop) | **2,043,228** | **0.6863** | **0.8573** | **0.7169** | **42.5%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `5659125162`, score-table `b86698e18798`, model-set `b0ffca3bf3f5`. 1 general, 7 filegroup, 56 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
