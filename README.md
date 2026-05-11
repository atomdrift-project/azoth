# Azoth

Routed ensemble for static malware detection. A general LightGBM classifier scores every file; per-filetype specialists score files in their domain; any route above its calibrated threshold flags the file. Calibrators and L0..L9 thresholds fit on a 411836-row dev partition (12.5% of the labeled corpus). Metrics below: locked 408858-row test partition, disjoint from training and calibration. EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input: cleave-extracted JSON reports. Output: one of `benign`, `suspicious`, `hostile`, with severity level L0..L9. Loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus); deployed default is L3 hostile, L5 suspicious.

Bundle layout: `config.json` (deployed thresholds), then per-route subdirectories under `general/`, `filegroups/<name>/`, `filetypes/<name>/`, each carrying `model.txt`, `feature_spec.json`, and `calibrator.json`. Architecture and FP-budget design: [DESIGN.md](DESIGN.md). Routing detail: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Single-model baseline: [GENERALIST_MODEL.md](GENERALIST_MODEL.md). Apache 2.0.

## Performance

| File type | Mal / Ben | PR AUC [95% CI] | Recall@3FP/M [95% CI] | ROC AUC [95% CI] | F1 [95% CI] | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`pe`](filetypes/pe/README.md) | 56704 / 18001 | 0.9996 [0.9995, 0.9996] | 0.6716 [0.6684, 0.7756] | 0.9986 [0.9985, 0.9988] | 0.9906 [0.9901, 0.9911] | PR +0.0013 / ROC +0.0004 |
| [`elf`](filetypes/elf/README.md) | 2793 / 14875 | 0.9986 [0.9975, 0.9995] | 0.9048 [0.8944, 0.9452] | 0.9998 [0.9997, 0.9999] | 0.9912 [0.9887, 0.9936] | PR +0.0053 / ROC +0.0065 |
| [`macho`](filetypes/macho/README.md) | 152 / 797 | 0.9949 [0.9902, 0.9981] | — | 0.9990 [0.9979, 0.9996] | 0.9589 [0.9481, 0.9803] | — |
| [`msi`](filetypes/msi/README.md) | 31 / 7 | 0.9969 | — | 0.9862 | 0.9841 | — |
| [`pdf`](filetypes/pdf/README.md) | 9 / 349 | 0.2365 [0.1568, 0.4079] | — | 0.9335 [0.8939, 0.9698] | 0.4375 [0.3028, 0.6429] | PR -0.7568 / ROC -0.0577 |
| [`rtf`](filetypes/rtf/README.md) | 11 / 49 | 1.0000 [1.0000, 1.0000] | — | 1.0000 [1.0000, 1.0000] | 1.0000 [1.0000, 1.0000] | — |
| [`javascript`](filetypes/javascript/README.md) | 7439 / 50135 | 0.9816 [0.9802, 0.9832] | 0.0000 [0.0000, 0.0000] | 0.9959 [0.9956, 0.9963] | 0.9506 [0.9475, 0.9547] | — |
| [`python`](filetypes/python/README.md) | 1843 / 14605 | 0.9711 [0.9655, 0.9760] | 0.4645 [0.0000, 0.8101] | 0.9949 [0.9938, 0.9959] | 0.9195 [0.9109, 0.9322] | — |
| [`shell`](filetypes/shell/README.md) | 417 / 5303 | 0.9655 [0.9550, 0.9752] | 0.0072 [0.0000, 0.7938] | 0.9954 [0.9924, 0.9975] | 0.9029 [0.8851, 0.9227] | — |
| [`powershell`](filetypes/powershell/README.md) | 66 / 257 | 0.9569 [0.9215, 0.9822] | — | 0.9869 [0.9767, 0.9947] | 0.8923 [0.8507, 0.9482] | — |
| [`batch`](filetypes/batch/README.md) | 63 / 244 | 0.9680 [0.9380, 0.9884] | — | 0.9908 [0.9810, 0.9967] | 0.9134 [0.8615, 0.9613] | — |
| [`package.json`](filetypes/package.json/README.md) | 1886 / 1121 | 0.9997 [0.9995, 0.9999] | — | 0.9995 [0.9990, 0.9999] | 0.9968 [0.9952, 0.9984] | — |
| [`jar`](filetypes/jar/README.md) | 108 / 199 | 0.9811 [0.9645, 0.9927] | — | 0.9846 [0.9666, 0.9961] | 0.9488 [0.9296, 0.9722] | — |
| [`ruby`](filetypes/ruby/README.md) | 7 / 2817 | 0.9098 [0.7143, 1.0000] | — | 0.9995 [0.9981, 1.0000] | 0.9231 [0.7273, 1.0000] | — |
| [`perl`](filetypes/perl/README.md) | 25 / 3766 | 0.9565 [0.8793, 1.0000] | 0.0000 [0.0000, 0.9600] | 0.9961 [0.9882, 1.0000] | 0.9388 [0.8889, 1.0000] | — |

PR AUC summarizes recall-vs-precision across operating points; Recall@3FP/M is the deployment-budget headline. Per-severity L0..L9 thresholds (observed benign-score quantiles per route, GPD-extrapolated for FP/M targets below the empirical floor) are in [route_policies.md](route_policies.md) — they document the severity-grading curve litmus uses, not optimization targets.

## Provenance

Calibration snapshot `1123787257`, score-table `90a2da149603`, model-set `bda9148ae3a2`. 1 general, 8 filegroup, 41 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
