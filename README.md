# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 19,811,828-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,470,304-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| `ico` | 33 / 81 | 0.698565 | 0.787879 | 0.730769 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 810 / 115 | 0.999062 | 0.994369 | 0.995660 | 99.14% | — |
| [`gem`](filetypes/gem/README.md) | 43 / 13,952 | 0.944900 | 0.991991 | 0.963855 | 93.02% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,024 / 4,149 | 0.994115 | 0.983775 | 0.958553 | 90.53% | — |
| [`html`](filetypes/html/README.md) | 36 / 34,526 | 0.924653 | 0.994833 | 0.942857 | 88.89% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 327 / 1,064 | 0.957041 | 0.971618 | 0.940419 | 88.38% | — |
| [`elf`](filetypes/elf/README.md) | 24,819 / 111,955 | 0.995489 | 0.998143 | 0.985786 | 85.02% | PR +0.002189 / ROC +0.004843 |
| [`lnk`](filetypes/lnk/README.md) | 584 / 148 | 0.996307 | 0.985920 | 0.981293 | 79.45% | — |
| [`perl`](filetypes/perl/README.md) | 48 / 10,066 | 0.832202 | 0.967089 | 0.870588 | 77.08% | — |
| [`pe`](filetypes/pe/README.md) | 203,476 / 33,309 | 0.997766 | 0.986462 | 0.981717 | 76.93% | PR -0.000534 / ROC -0.011738 |
| [`package.json`](filetypes/package.json/README.md) | 2,744 / 9,510 | 0.959189 | 0.963619 | 0.957901 | 74.20% | — |
| [`registry`](filetypes/registry/README.md) | 80 / 13,660 | 0.887584 | 0.974156 | 0.820144 | 68.75% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,768 | 0.982631 | 0.894818 | 0.933708 | 63.39% | PR -0.010669 / ROC -0.096382 |
| [`macho`](filetypes/macho/README.md) | 305 / 4,746 | 0.902972 | 0.967712 | 0.862676 | 63.28% | — |
| [`npm`](filetypes/npm/README.md) | 3,082 / 23,954 | 0.923677 | 0.952661 | 0.907636 | 62.36% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 411 / 149,366 | 0.679959 | 0.921385 | 0.783862 | 59.37% | — |
| [`ruby`](filetypes/ruby/README.md) | 38 / 23,956 | 0.731178 | 0.925860 | 0.733333 | 57.89% | — |
| [`python`](filetypes/python/README.md) | 2,733 / 84,279 | 0.806105 | 0.913696 | 0.798145 | 57.89% | — |
| [`tar`](filetypes/tar/README.md) | 2,055 / 10,690 | 0.932821 | 0.967778 | 0.873437 | 57.66% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 29 / 2,258 | 0.774402 | 0.926545 | 0.830189 | 55.17% | — |
| [`shell`](filetypes/shell/README.md) | 2,452 / 20,634 | 0.919578 | 0.964498 | 0.873853 | 53.67% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,147 / 10,795 | 0.948392 | 0.980792 | 0.877022 | 52.65% | — |
| [`php`](filetypes/php/README.md) | 830 / 77,815 | 0.717845 | 0.928476 | 0.738061 | 50.72% | — |
| [`java_class`](filetypes/java_class/README.md) | 311 / 227,817 | 0.783283 | 0.905404 | 0.829016 | 50.16% | — |
| [`powershell`](filetypes/powershell/README.md) | 713 / 762 | 0.966555 | 0.962277 | 0.930565 | 49.79% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,731 / 534 | 0.991234 | 0.973258 | 0.963979 | 48.99% | — |
| [`jar`](filetypes/jar/README.md) | 454 / 5,145 | 0.927568 | 0.982701 | 0.869658 | 47.80% | — |
| [`zip`](filetypes/zip/README.md) | 13,647 / 10,911 | 0.900470 | 0.837424 | 0.817422 | 46.46% | — |
| [`vsix`](filetypes/vsix/README.md) | 40 / 625 | 0.639915 | 0.915160 | 0.634921 | 37.50% | — |
| [`json`](filetypes/json/README.md) | 32 / 33,838 | 0.402816 | 0.724457 | 0.533333 | 37.50% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,383 / 224,702 | 0.835248 | 0.923129 | 0.807220 | 35.71% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,333 / 818 | 0.985244 | 0.890197 | 0.974887 | 31.32% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 479 / 103 | 0.956434 | 0.830209 | 0.904215 | 31.32% | — |
| [`crx`](filetypes/crx/README.md) | 286 / 809 | 0.938625 | 0.974072 | 0.871795 | 26.92% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 117 / 1,420 | 0.434558 | 0.800954 | 0.458647 | 26.50% | — |
| [`whl`](filetypes/whl/README.md) | 314 / 5,887 | 0.793372 | 0.969266 | 0.752381 | 18.79% | — |
| [`csharp`](filetypes/csharp/README.md) | 471 / 12,851 | 0.311688 | 0.693680 | 0.383117 | 18.26% | — |
| [`batch`](filetypes/batch/README.md) | 22,256 / 1,110 | 0.985212 | 0.820811 | 0.984115 | 15.07% | — |
| [`go`](filetypes/go/README.md) | 2,027 / 30,271 | 0.331601 | 0.654768 | 0.370259 | 13.42% | — |
| [`deb`](filetypes/deb/README.md) | 60 / 3,418 | 0.146608 | 0.658899 | 0.208955 | 11.67% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,644 | 0.198329 | 0.584663 | 0.248889 | 10.31% | — |
| `c` | 2,197 / 219,631 | 0.247695 | 0.616282 | 0.359306 | 9.15% | — |
| `png` | 1,132 / 67,908 | 0.049643 | 0.392443 | 0.100000 | 5.39% | — |
| [`xml`](filetypes/xml/README.md) | 272 / 57,933 | 0.197049 | 0.747220 | 0.293413 | 3.68% | — |
| [`text`](filetypes/text/README.md) | 604 / 41,919 | 0.092464 | 0.570675 | 0.140762 | 3.48% | — |
| `rust` | 59 / 43,795 | 0.270026 | 0.823345 | 0.369565 | 3.39% | — |
| `java` | 416 / 24,945 | 0.076805 | 0.434265 | 0.136461 | 1.92% | — |
| [`7z`](filetypes/7z/README.md) | 1,123 / 44 | 0.997975 | 0.950346 | 0.981215 | — | — |
| [`gif`](filetypes/gif/README.md) | 85 / 184 | 0.325689 | 0.504731 | 0.480226 | 0.00% | — |
| **Weighted avg** (by test pop) | **2,025,142** | **0.6858** | **0.8526** | **0.7135** | **45.4%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `5502527281`, score-table `e9e47c665a76`, model-set `12d95653f5e9`. 1 general, 6 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
