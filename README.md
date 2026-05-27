# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 593,146-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 592,885-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

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
| [`batch`](filetypes/batch/README.md) | 21,129 / 427 | 0.999944 | 0.998433 | 0.998769 | 98.80% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3,910 | 0.995084 | 0.999544 | 0.989154 | 97.85% | — |
| [`rtf`](filetypes/rtf/README.md) | 215 / 51 | 0.999595 | 0.998267 | 0.988453 | 97.67% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 114 | 0.999456 | 0.994191 | 0.989915 | 96.87% | — |
| [`xls`](filetypes/xls/README.md) | 1,297 / 48 | 0.999520 | 0.987078 | 0.987739 | 95.45% | — |
| [`elf`](filetypes/elf/README.md) | 9,038 / 17,158 | 0.999639 | 0.999846 | 0.994057 | 93.37% | PR +0.006339 / ROC +0.006546 |
| [`package.json`](filetypes/package.json/README.md) | 2,162 / 1,440 | 0.998638 | 0.998609 | 0.997224 | 91.54% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 665 | 0.992121 | 0.995087 | 0.979866 | 90.95% | — |
| [`macho`](filetypes/macho/README.md) | 262 / 1,383 | 0.996984 | 0.999412 | 0.971209 | 88.17% | — |
| [`shell`](filetypes/shell/README.md) | 952 / 5,695 | 0.970822 | 0.992719 | 0.939092 | 84.35% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3,959 | 0.934150 | 0.996225 | 0.901961 | 82.14% | — |
| [`javascript`](filetypes/javascript/README.md) | 10,536 / 59,721 | 0.975580 | 0.994041 | 0.926175 | 74.52% | — |
| [`docx`](filetypes/docx/README.md) | 176 / 31 | 0.970000 | 0.873625 | 0.919060 | 74.43% | — |
| [`php`](filetypes/php/README.md) | 520 / 10,871 | 0.919046 | 0.986453 | 0.886179 | 70.58% | — |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47,394 | 0.900926 | 0.934622 | 0.921687 | 66.47% | — |
| [`lnk`](filetypes/lnk/README.md) | 261 / 127 | 0.950958 | 0.900836 | 0.896309 | 63.60% | — |
| [`pe`](filetypes/pe/README.md) | 110,264 / 18,952 | 0.999642 | 0.998163 | 0.993138 | 62.40% | PR +0.001342 / ROC -0.000037 |
| [`jar`](filetypes/jar/README.md) | 215 / 237 | 0.981657 | 0.984270 | 0.936471 | 59.53% | — |
| [`python`](filetypes/python/README.md) | 2,271 / 16,344 | 0.966352 | 0.992660 | 0.930295 | 51.96% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 2,856 / 5,360 | 0.971744 | 0.976583 | 0.947948 | 50.63% | — |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7,572 | 0.577510 | 0.876339 | 0.573099 | 32.48% | — |
| [`powershell`](filetypes/powershell/README.md) | 259 / 274 | 0.964099 | 0.973015 | 0.925490 | 31.66% | — |
| [`vbs`](filetypes/vbs/README.md) | 463 / 423 | 0.974756 | 0.980587 | 0.947594 | 26.78% | — |
| [`c`](filetypes/c/README.md) | 1,766 / 66,650 | 0.351150 | 0.853056 | 0.341767 | 12.97% | — |
| [`text`](filetypes/text/README.md) | 160 / 7,993 | 0.260664 | 0.764861 | 0.303419 | 11.88% | — |
| [`pdf`](filetypes/pdf/README.md) | 21,804 / 1,734 | 0.999372 | 0.995320 | 0.995284 | 10.52% | PR +0.006072 / ROC +0.004120 |
| [`png`](filetypes/png/README.md) | 657 / 14,393 | 0.156400 | 0.605552 | 0.179657 | 8.98% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 9,604 | 0.102036 | 0.623744 | 0.136752 | 5.49% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 128 / 1,319 | 0.285369 | 0.669808 | 0.312796 | 5.47% | — |
| [`xml`](filetypes/xml/README.md) | 291 / 18,398 | 0.234673 | 0.717127 | 0.358407 | 5.15% | — |
| [`go`](filetypes/go/README.md) | 1,177 / 11,867 | 0.579758 | 0.933275 | 0.657069 | 2.04% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1,544 | 0.139318 | 0.700563 | 0.241611 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@3FP/M is the deployment-budget headline; for filetypes whose dev slice cannot resolve 3 FP/M empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Provenance

Calibration snapshot `1464203399`, score-table `a85a3c0705a1`, model-set `a793ee5bfab8`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
