# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 592,592-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 592,338-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 114 | 0.9992 | 0.9953 | 0.9992 | 99.84% | — |
| [`batch`](filetypes/batch/README.md) | 21,128 / 427 | 0.9999 | 0.9986 | 0.9991 | 99.39% | — |
| [`elf`](filetypes/elf/README.md) | 9,026 / 17,067 | 1.0000 | 1.0000 | 0.9987 | 98.59% | PR +0.0067 / ROC +0.0067 |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3,863 | 0.9964 | 0.9997 | 0.9913 | 98.28% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 664 | 0.9931 | 0.9954 | 0.9887 | 98.19% | — |
| [`rtf`](filetypes/rtf/README.md) | 215 / 51 | 0.9998 | 0.9993 | 0.9954 | 98.14% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 2,845 / 5,355 | 0.9982 | 0.9983 | 0.9903 | 97.19% | — |
| [`pdf`](filetypes/pdf/README.md) | 21,801 / 1,734 | 1.0000 | 0.9994 | 0.9975 | 97.04% | PR +0.0067 / ROC +0.0082 |
| [`package.json`](filetypes/package.json/README.md) | 2,162 / 1,439 | 0.9997 | 0.9995 | 0.9975 | 93.34% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3,959 | 0.9659 | 0.9993 | 0.9630 | 92.86% | — |
| [`shell`](filetypes/shell/README.md) | 950 / 5,694 | 0.9870 | 0.9971 | 0.9698 | 92.42% | — |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47,377 | 0.9155 | 0.9824 | 0.9433 | 91.33% | — |
| [`macho`](filetypes/macho/README.md) | 262 / 1,383 | 0.9988 | 0.9998 | 0.9886 | 88.93% | — |
| [`javascript`](filetypes/javascript/README.md) | 10,529 / 59,667 | 0.9927 | 0.9983 | 0.9723 | 78.27% | — |
| [`pe`](filetypes/pe/README.md) | 110,244 / 18,952 | 1.0000 | 0.9999 | 0.9988 | 78.03% | PR +0.0017 / ROC +0.0017 |
| [`docx`](filetypes/docx/README.md) | 176 / 31 | 0.9772 | 0.9185 | 0.9191 | 77.84% | — |
| [`jar`](filetypes/jar/README.md) | 215 / 237 | 0.9900 | 0.9907 | 0.9464 | 71.63% | — |
| [`php`](filetypes/php/README.md) | 519 / 10,871 | 0.9893 | 0.9984 | 0.9607 | 70.33% | — |
| [`vbs`](filetypes/vbs/README.md) | 462 / 423 | 0.9984 | 0.9984 | 0.9882 | 69.26% | — |
| [`lnk`](filetypes/lnk/README.md) | 261 / 127 | 0.9587 | 0.9427 | 0.9206 | 68.58% | — |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7,572 | 0.9512 | 0.9977 | 0.8860 | 64.10% | — |
| [`python`](filetypes/python/README.md) | 2,272 / 16,343 | 0.9866 | 0.9975 | 0.9542 | 57.75% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1,544 | 0.9160 | 0.9865 | 0.8480 | 52.94% | — |
| [`xml`](filetypes/xml/README.md) | 291 / 18,378 | 0.2122 | 0.8936 | 0.3183 | 24.05% | — |
| [`powershell`](filetypes/powershell/README.md) | 257 / 274 | 0.9867 | 0.9908 | 0.9637 | 17.90% | — |
| [`text`](filetypes/text/README.md) | 160 / 7,992 | 0.1929 | 0.6599 | 0.2581 | 14.37% | — |
| [`go`](filetypes/go/README.md) | 1,177 / 11,867 | 0.8683 | 0.9825 | 0.7653 | 13.08% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 9,604 | 0.1523 | 0.8348 | 0.2462 | 11.59% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 127 / 1,319 | 0.2775 | 0.6558 | 0.3140 | 8.66% | — |
| [`c`](filetypes/c/README.md) | 1,766 / 66,647 | 0.5255 | 0.9353 | 0.5389 | 0.91% | — |
| [`png`](filetypes/png/README.md) | 657 / 14,388 | 0.1924 | 0.6878 | 0.2172 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1384435807`, score-table `2366b041b18b`, model-set `5c2f3d449a67`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
