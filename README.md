# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 34 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 592,558-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 592,307-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign`, `suspicious`, or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile and suspicious thresholds at the same level; the deployed default is L3. Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 38 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Deployed Performance

Each row is the deployed ensemble — the OR-rule or learned blend in `route_policies.json` at L3 hostile — measured on the filetype's slice of the locked test partition. Recall and FP are exactly what litmus would produce on these files at scan time; FP/M normalizes against the benign slice. The policy column names the rule that fires (`joint_or_at_fp_N` is an OR across allowed routes at an FP/M target of N per million; `learned_blend_at_fp_N` is a logit blend at the same budget; see [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md)).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

| File type | Test mal / ben | Recall | FP | FP / M | Policy |
|---|---:|---:|---:|---:|---|
| [`batch`](filetypes/batch/README.md) | 21,128 / 427 | 99.46% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,276 / 114 | 98.43% | 0 | 0.0 | `filetype_only_at_fp_0` |
| [`rtf`](filetypes/rtf/README.md) | 215 / 51 | 97.67% | 0 | 0.0 | `max_rule` |
| [`kotlin`](filetypes/kotlin/README.md) | 2,843 / 5,355 | 94.77% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`elf`](filetypes/elf/README.md) | 9,019 / 17,064 | 93.14% | 0 | 0.0 | `learned_blend_at_fp_3` |
| [`perl`](filetypes/perl/README.md) | 28 / 3,959 | 92.59% | 0 | 0.0 | `learned_blend_at_fp_0` |
| [`package.json`](filetypes/package.json/README.md) | 2,162 / 1,439 | 91.68% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`ole`](filetypes/ole/README.md) | 221 / 664 | 91.27% | 0 | 0.0 | `filetype_only_at_fp_0` |
| [`pe`](filetypes/pe/README.md) | 110,233 / 18,952 | 91.11% | 3 | 158.3 | `learned_blend_at_fp_4` |
| [`javascript`](filetypes/javascript/README.md) | 10,529 / 59,665 | 88.33% | 2 | 33.5 | `filetype_only` |
| [`shell`](filetypes/shell/README.md) | 949 / 5,693 | 84.80% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`php`](filetypes/php/README.md) | 519 / 10,871 | 73.58% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`docx`](filetypes/docx/README.md) | 176 / 31 | 70.45% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3,862 | 68.67% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`macho`](filetypes/macho/README.md) | 262 / 1,383 | 67.18% | 0 | 0.0 | `learned_blend_at_fp_1` |
| [`python`](filetypes/python/README.md) | 2,272 / 16,343 | 60.05% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`jar`](filetypes/jar/README.md) | 215 / 237 | 56.54% | 0 | 0.0 | `filetype_only_at_fp_0` |
| [`lnk`](filetypes/lnk/README.md) | 261 / 127 | 49.04% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47,377 | 45.66% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`powershell`](filetypes/powershell/README.md) | 256 / 274 | 39.69% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`vbs`](filetypes/vbs/README.md) | 462 / 423 | 27.71% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7,572 | 17.52% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`jpeg`](filetypes/jpeg/README.md) | 127 / 1,319 | 12.60% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`text`](filetypes/text/README.md) | 160 / 7,992 | 11.25% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`pdf`](filetypes/pdf/README.md) | 21,801 / 1,734 | 6.48% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`c`](filetypes/c/README.md) | 1,766 / 66,647 | 3.74% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`plist`](filetypes/plist/README.md) | 68 / 1,544 | 2.94% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`xml`](filetypes/xml/README.md) | 291 / 18,378 | 2.74% | 0 | 0.0 | `learned_blend_at_fp_3` |
| [`rust`](filetypes/rust/README.md) | 164 / 9,604 | 1.22% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`go`](filetypes/go/README.md) | 1,177 / 11,867 | 0.85% | 0 | 0.0 | `joint_or_at_fp_0` |
| [`png`](filetypes/png/README.md) | 657 / 14,388 | 0.15% | 0 | 0.0 | `learned_blend_at_fp_0` |

Recall and FP are the operational headline: what fraction of the filetype's malware does litmus flag at L3 hostile, and at what false-positive cost? The per-severity thresholds in [route_policies.md](route_policies.md) document the L0..L20 curve — L0 is tightest, L20 is loosest — alongside the same tp/fp/recall numbers for every level.

## Provenance

Calibration snapshot `1349983353`, score-table `d16d7527d260`, model-set `d6782c82a11b`. 1 general, 7 filegroup, 38 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
