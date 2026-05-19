# Azoth

Routed ensemble for static malware detection. A general LightGBM classifier scores every file; per-filetype specialists score files in their domain; any route above its calibrated threshold flags the file. Calibrators and L0..L20 thresholds fit on a 583032-row dev partition (12.5% of the labeled corpus). Metrics below: locked 585889-row test partition, disjoint from training and calibration. EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input: cleave-extracted JSON reports. Output: one of `benign`, `suspicious`, `hostile`, with severity level L0..L20. Loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus); deployed default is L3 (litmus loads both hostile and suspicious thresholds at the same level).

Bundle layout: `config.json` (deployed thresholds), then per-route subdirectories under `general/`, `filegroups/<name>/`, `filetypes/<name>/`, each carrying `model.txt`, `feature_spec.json`, and `calibrator.json`. Architecture and FP-budget design: [DESIGN.md](DESIGN.md). Routing detail: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Single-model baseline: [GENERALIST_MODEL.md](GENERALIST_MODEL.md). Apache 2.0.

## Routed Ensemble Performance

Deployed ensemble (general + filegroup + filetype combined per `route_policies.json`) measured on each filetype's slice of the locked test partition. Sorted by PR AUC, best first. Filetypes included: ≥25/25 in test, or ≥100/100 in the full labeled corpus.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ 3FP/M | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`batch`](filetypes/batch/README.md) | 21095 / 425 | 1.0000 | 0.9996 | 0.9988 | 98.84% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1276 / 114 | 0.9999 | 0.9994 | 0.9973 | 96.94% | — |
| [`elf`](filetypes/elf/README.md) | 8826 / 16927 | 0.9998 | 0.9999 | 0.9946 | 93.55% | PR +0.0065 / ROC +0.0066 |
| [`pe`](filetypes/pe/README.md) | 109970 / 18938 | 0.9998 | 0.9991 | 0.9955 | 73.42% | PR +0.0015 / ROC +0.0009 |
| [`package.json`](filetypes/package.json/README.md) | 2162 / 1361 | 0.9996 | 0.9992 | 0.9972 | 90.61% | — |
| [`rtf`](filetypes/rtf/README.md) | 214 / 51 | 0.9995 | 0.9980 | 0.9882 | 95.33% | — |
| [`pdf`](filetypes/pdf/README.md) | 21777 / 1734 | 0.9979 | 0.9813 | 0.9910 | 6.59% | PR +0.0046 / ROC -0.0099 |
| [`macho`](filetypes/macho/README.md) | 258 / 1382 | 0.9936 | 0.9988 | 0.9594 | 80.62% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 233 / 3841 | 0.9929 | 0.9993 | 0.9892 | 97.85% | — |
| [`ole`](filetypes/ole/README.md) | 221 / 664 | 0.9858 | 0.9863 | 0.9775 | 90.95% | — |
| [`shell`](filetypes/shell/README.md) | 920 / 5682 | 0.9854 | 0.9969 | 0.9461 | 80.87% | — |
| [`javascript`](filetypes/javascript/README.md) | 10488 / 59418 | 0.9818 | 0.9960 | 0.9316 | 68.36% | — |
| [`vbs`](filetypes/vbs/README.md) | 445 / 423 | 0.9816 | 0.9847 | 0.9587 | 36.40% | — |
| [`jar`](filetypes/jar/README.md) | 215 / 236 | 0.9812 | 0.9839 | 0.9388 | 58.60% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 2829 / 5341 | 0.9786 | 0.9821 | 0.9555 | 54.68% | — |
| [`python`](filetypes/python/README.md) | 2271 / 16286 | 0.9765 | 0.9950 | 0.9324 | 53.63% | — |
| [`docx`](filetypes/docx/README.md) | 173 / 31 | 0.9761 | 0.9153 | 0.9227 | 62.43% | — |
| [`powershell`](filetypes/powershell/README.md) | 240 / 274 | 0.9673 | 0.9797 | 0.9421 | 4.58% | — |
| [`lnk`](filetypes/lnk/README.md) | 257 / 127 | 0.9467 | 0.9114 | 0.9000 | 59.92% | — |
| [`php`](filetypes/php/README.md) | 516 / 10809 | 0.9275 | 0.9897 | 0.8852 | 67.25% | — |
| [`java_class`](filetypes/java_class/README.md) | 173 / 47070 | 0.9265 | 0.9855 | 0.9186 | 6.36% | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3956 | 0.9231 | 0.9979 | 0.9057 | 82.14% | — |
| [`go`](filetypes/go/README.md) | 1177 / 11858 | 0.6324 | 0.9344 | 0.6485 | 1.53% | — |
| [`csharp`](filetypes/csharp/README.md) | 234 / 7572 | 0.5185 | 0.8946 | 0.4847 | 22.22% | — |
| [`c`](filetypes/c/README.md) | 1766 / 66562 | 0.5098 | 0.8817 | 0.5612 | 11.16% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 125 / 1319 | 0.3336 | 0.7716 | 0.3212 | 0.80% | — |
| [`text`](filetypes/text/README.md) | 159 / 7979 | 0.2044 | 0.7609 | 0.2581 | 11.95% | — |
| [`png`](filetypes/png/README.md) | 657 / 14338 | 0.1546 | 0.6161 | 0.1871 | 1.37% | — |
| [`xml`](filetypes/xml/README.md) | 288 / 17921 | 0.1440 | 0.7434 | 0.3299 | 0.00% | — |
| [`plist`](filetypes/plist/README.md) | 68 / 1544 | 0.1100 | 0.6439 | 0.1695 | 1.47% | — |
| [`rust`](filetypes/rust/README.md) | 164 / 9604 | 0.1056 | 0.7708 | 0.1798 | 1.22% | — |

PR AUC summarizes recall-vs-precision across operating points; Recall@3FP/M is the deployment-budget headline (GPD-extrapolated for filetypes whose dev slice can't resolve 3 FP/M empirically). Per-severity L0..L20 thresholds are in [route_policies.md](route_policies.md) — they document the severity-grading curve litmus uses, not optimization targets.

## Provenance

Calibration snapshot `1310931333`, score-table `ad73d201a7a0`, model-set `fba7b85a30a9`. 1 general, 7 filegroup, 40 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
