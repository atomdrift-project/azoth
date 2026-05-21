# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 592,558-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 592,307-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign`, `suspicious`, or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile and suspicious thresholds at the same level; the deployed default is L3. Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 38 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at a 3 FP/M operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at 3 FP/M** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`batch`](filetypes/batch/README.md) | 21,128 / 427 | 1.0000 | 0.9998 | 0.9992 | 99.54% | — |
| [`pe`](filetypes/pe/README.md) | 110,233 / 18,952 | 1.0000 | 0.9999 | 0.9988 | 84.76% | PR +0.0017 / ROC +0.0017 |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 114 | 1.0000 | 0.9998 | 0.9988 | 96.79% | — |
| [`elf`](filetypes/elf/README.md) | 9,019 / 17,064 | 0.9999 | 0.9999 | 0.9954 | 81.43% | PR +0.0066 / ROC +0.0066 |
| [`rtf`](filetypes/rtf/README.md) | 215 / 51 | 0.9996 | 0.9983 | 0.9885 | 95.35% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,162 / 1,439 | 0.9996 | 0.9992 | 0.9975 | 88.25% | — |
| [`pdf`](filetypes/pdf/README.md) | 21,801 / 1,734 | 0.9989 | 0.9925 | 0.9959 | 17.59% | PR +0.0056 / ROC +0.0013 |
| [`kotlin`](filetypes/kotlin/README.md) | 2,843 / 5,355 | 0.9981 | 0.9982 | 0.9908 | 96.94% | — |
| [`javascript`](filetypes/javascript/README.md) | 10,529 / 59,665 | 0.9977 | 0.9995 | 0.9814 | 76.97% | — |
| [`macho`](filetypes/macho/README.md) | 262 / 1,383 | 0.9947 | 0.9990 | 0.9638 | 84.35% | — |
| [`python`](filetypes/python/README.md) | 2,272 / 16,343 | 0.9915 | 0.9978 | 0.9650 | 43.31% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3,862 | 0.9863 | 0.9940 | 0.9847 | 97.42% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 664 | 0.9817 | 0.9862 | 0.9775 | 91.40% | — |
| [`jar`](filetypes/jar/README.md) | 215 / 237 | 0.9811 | 0.9836 | 0.9333 | 61.86% | — |
| [`shell`](filetypes/shell/README.md) | 949 / 5,693 | 0.9805 | 0.9956 | 0.9523 | 85.56% | — |
| [`vbs`](filetypes/vbs/README.md) | 462 / 423 | 0.9772 | 0.9811 | 0.9523 | 26.84% | — |
| [`docx`](filetypes/docx/README.md) | 176 / 31 | 0.9751 | 0.8827 | 0.9191 | 71.59% | — |
| [`powershell`](filetypes/powershell/README.md) | 256 / 274 | 0.9704 | 0.9758 | 0.9537 | 14.06% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3,959 | 0.9632 | 0.9969 | 0.9474 | 89.29% | — |
| [`php`](filetypes/php/README.md) | 519 / 10,871 | 0.9572 | 0.9933 | 0.9496 | 76.49% | — |
| [`lnk`](filetypes/lnk/README.md) | 261 / 127 | 0.9478 | 0.9132 | 0.9030 | 51.72% | — |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47,377 | 0.9385 | 0.9815 | 0.9231 | 45.09% | — |
| [`go`](filetypes/go/README.md) | 1,177 / 11,867 | 0.8050 | 0.9716 | 0.7493 | 2.04% | — |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7,572 | 0.5506 | 0.8771 | 0.5327 | 24.79% | — |
| [`c`](filetypes/c/README.md) | 1,766 / 66,647 | 0.4890 | 0.8956 | 0.5302 | 12.85% | — |
| [`xml`](filetypes/xml/README.md) | 291 / 18,378 | 0.2875 | 0.8013 | 0.3908 | 3.44% | — |
| [`text`](filetypes/text/README.md) | 160 / 7,992 | 0.2324 | 0.5894 | 0.3273 | 12.50% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 127 / 1,319 | 0.2298 | 0.7477 | 0.3037 | 21.26% | — |
| [`png`](filetypes/png/README.md) | 657 / 14,388 | 0.1750 | 0.6568 | 0.1948 | 1.22% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 9,604 | 0.1102 | 0.7258 | 0.1660 | 1.83% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1,544 | 0.0936 | 0.6029 | 0.1218 | 1.47% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1349983353`, score-table `d16d7527d260`, model-set `d6782c82a11b`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
