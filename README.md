# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 19,922,689-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,484,155-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| `ico` | 33 / 83 | 0.696447 | 0.787879 | 0.730769 | 100.00% | — |
| [`rtf`](filetypes/rtf/README.md) | 810 / 115 | 0.999259 | 0.995083 | 0.995660 | 99.14% | — |
| [`gem`](filetypes/gem/README.md) | 43 / 13,980 | 0.940980 | 0.960809 | 0.963855 | 93.02% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,024 / 4,150 | 0.994810 | 0.985991 | 0.958522 | 90.88% | — |
| [`html`](filetypes/html/README.md) | 36 / 34,546 | 0.927677 | 0.996813 | 0.941176 | 88.89% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 327 / 1,092 | 0.954090 | 0.966915 | 0.938907 | 88.38% | — |
| [`elf`](filetypes/elf/README.md) | 24,819 / 111,958 | 0.995495 | 0.998152 | 0.985762 | 85.04% | PR +0.002195 / ROC +0.004852 |
| [`package.json`](filetypes/package.json/README.md) | 2,744 / 9,510 | 0.963035 | 0.972698 | 0.958162 | 80.98% | — |
| [`lnk`](filetypes/lnk/README.md) | 584 / 148 | 0.996516 | 0.986631 | 0.981293 | 80.14% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,480 / 3,768 | 0.995420 | 0.975599 | 0.973444 | 70.31% | PR +0.002120 / ROC -0.015601 |
| [`registry`](filetypes/registry/README.md) | 80 / 13,660 | 0.889445 | 0.977841 | 0.820144 | 68.75% | — |
| [`perl`](filetypes/perl/README.md) | 52 / 10,065 | 0.827405 | 0.963135 | 0.854167 | 65.38% | — |
| [`npm`](filetypes/npm/README.md) | 3,088 / 24,279 | 0.927975 | 0.957340 | 0.910026 | 64.96% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 411 / 149,366 | 0.684395 | 0.940890 | 0.781341 | 62.53% | — |
| [`macho`](filetypes/macho/README.md) | 305 / 4,752 | 0.955457 | 0.990680 | 0.911184 | 60.66% | — |
| [`python`](filetypes/python/README.md) | 2,732 / 84,295 | 0.818219 | 0.927365 | 0.809786 | 60.47% | — |
| [`tar`](filetypes/tar/README.md) | 2,054 / 10,777 | 0.935819 | 0.968524 | 0.878485 | 60.13% | — |
| [`shell`](filetypes/shell/README.md) | 2,457 / 20,602 | 0.919094 | 0.965260 | 0.875779 | 54.05% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,149 / 10,861 | 0.936375 | 0.972067 | 0.872559 | 51.54% | — |
| [`pe`](filetypes/pe/README.md) | 203,488 / 33,308 | 0.997788 | 0.986502 | 0.980007 | 50.49% | PR -0.000512 / ROC -0.011698 |
| [`jar`](filetypes/jar/README.md) | 454 / 5,162 | 0.933220 | 0.982186 | 0.880517 | 50.22% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 29 / 2,259 | 0.799904 | 0.931973 | 0.830189 | 48.28% | — |
| [`powershell`](filetypes/powershell/README.md) | 722 / 763 | 0.968228 | 0.961232 | 0.933808 | 47.65% | — |
| [`zip`](filetypes/zip/README.md) | 13,648 / 11,194 | 0.901832 | 0.845793 | 0.820245 | 46.14% | — |
| [`php`](filetypes/php/README.md) | 831 / 77,823 | 0.747177 | 0.950827 | 0.768267 | 45.97% | — |
| [`ruby`](filetypes/ruby/README.md) | 38 / 24,068 | 0.795383 | 0.988821 | 0.800000 | 44.74% | — |
| [`vsix`](filetypes/vsix/README.md) | 40 / 645 | 0.653861 | 0.915000 | 0.655738 | 42.50% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,799 / 533 | 0.990082 | 0.970114 | 0.958897 | 32.91% | — |
| [`crx`](filetypes/crx/README.md) | 286 / 926 | 0.919416 | 0.974269 | 0.855305 | 31.82% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,333 / 818 | 0.980859 | 0.849191 | 0.973852 | 29.69% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,388 / 225,017 | 0.833997 | 0.927055 | 0.805360 | 29.59% | — |
| `json` | 32 / 33,868 | 0.391061 | 0.729020 | 0.510638 | 28.12% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 479 / 103 | 0.958362 | 0.835063 | 0.904716 | 27.56% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 117 / 1,421 | 0.449174 | 0.804438 | 0.445255 | 26.50% | — |
| [`csharp`](filetypes/csharp/README.md) | 471 / 12,851 | 0.314783 | 0.613547 | 0.393990 | 21.02% | — |
| [`deb`](filetypes/deb/README.md) | 42 / 3,424 | 0.198097 | 0.725509 | 0.285714 | 16.67% | — |
| [`batch`](filetypes/batch/README.md) | 22,276 / 1,111 | 0.999573 | 0.994611 | 0.995683 | 14.98% | — |
| [`whl`](filetypes/whl/README.md) | 316 / 6,103 | 0.664317 | 0.947789 | 0.633431 | 12.97% | — |
| `rust` | 59 / 43,860 | 0.267031 | 0.832684 | 0.348837 | 11.86% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,644 | 0.196991 | 0.547971 | 0.251012 | 10.31% | — |
| `c` | 2,199 / 219,950 | 0.249594 | 0.653974 | 0.348311 | 10.00% | — |
| [`go`](filetypes/go/README.md) | 2,024 / 30,296 | 0.338251 | 0.642847 | 0.384699 | 9.83% | — |
| `java_class` | 311 / 227,817 | 0.701353 | 0.927425 | 0.752688 | 7.72% | — |
| `png` | 1,132 / 67,908 | 0.050348 | 0.421965 | 0.100000 | 5.39% | — |
| [`text`](filetypes/text/README.md) | 622 / 41,859 | 0.090919 | 0.527900 | 0.138810 | 3.86% | — |
| [`java`](filetypes/java/README.md) | 416 / 24,945 | 0.120811 | 0.734035 | 0.152305 | 2.40% | — |
| [`gif`](filetypes/gif/README.md) | 85 / 191 | 0.310113 | 0.367570 | 0.470914 | 2.35% | — |
| [`xml`](filetypes/xml/README.md) | 278 / 57,963 | 0.176571 | 0.483989 | 0.303207 | 1.80% | — |
| [`7z`](filetypes/7z/README.md) | 1,121 / 45 | 0.997890 | 0.948607 | 0.980752 | — | — |
| **Weighted avg** (by test pop) | **2,027,340** | **0.6795** | **0.8620** | **0.7061** | **36.9%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `5548950182`, score-table `78177e0ca8d7`, model-set `44b32e9002f2`. 1 general, 6 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
