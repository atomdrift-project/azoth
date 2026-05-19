# Azoth

Routed ensemble for static malware detection. A general LightGBM classifier scores every file; per-filetype specialists score files in their domain; any route above its calibrated threshold flags the file. Calibrators and L0..L9 thresholds fit on a 583032-row dev partition (12.5% of the labeled corpus). Metrics below: locked 585889-row test partition, disjoint from training and calibration. EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input: cleave-extracted JSON reports. Output: one of `benign`, `suspicious`, `hostile`, with severity level L0..L9. Loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus); deployed default is L3 hostile, L5 suspicious.

Bundle layout: `config.json` (deployed thresholds), then per-route subdirectories under `general/`, `filegroups/<name>/`, `filetypes/<name>/`, each carrying `model.txt`, `feature_spec.json`, and `calibrator.json`. Architecture and FP-budget design: [DESIGN.md](DESIGN.md). Routing detail: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Single-model baseline: [GENERALIST_MODEL.md](GENERALIST_MODEL.md). Apache 2.0.

## Performance

| File type | Mal / Ben | PR AUC [95% CI] | Recall@3FP/M [95% CI] | ROC AUC [95% CI] | F1 [95% CI] | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`pe`](filetypes/pe/README.md) | 109970 / 18938 | 0.9997 | 0.1881 | 0.9991 | 0.9976 | PR +0.0014 / ROC +0.0009 |
| [`elf`](filetypes/elf/README.md) | 8826 / 16927 | 0.9998 | 0.9355 | 0.9999 | 0.9946 | PR +0.0065 / ROC +0.0066 |
| [`macho`](filetypes/macho/README.md) | 258 / 1382 | 0.9942 | — | 0.9989 | 0.9602 | — |
| [`msi`](filetypes/msi/README.md) | 215 / 8 | 0.9992 | — | 0.9785 | 0.9885 | — |
| [`pdf`](filetypes/pdf/README.md) | 21777 / 1734 | 0.9988 | — | 0.9923 | 0.9954 | PR +0.0055 / ROC +0.0011 |
| [`rtf`](filetypes/rtf/README.md) | 214 / 51 | 0.9995 | — | 0.9980 | 0.9882 | — |
| [`javascript`](filetypes/javascript/README.md) | 10488 / 59418 | 0.9818 | — | 0.9960 | 0.9316 | — |
| [`python`](filetypes/python/README.md) | 2271 / 16286 | 0.9765 | 0.5363 | 0.9950 | 0.9324 | — |
| [`shell`](filetypes/shell/README.md) | 920 / 5682 | 0.9854 | 0.8087 | 0.9969 | 0.9461 | — |
| [`powershell`](filetypes/powershell/README.md) | 240 / 274 | 0.9673 | — | 0.9797 | 0.9421 | — |
| [`batch`](filetypes/batch/README.md) | 21095 / 425 | 1.0000 | — | 0.9996 | 0.9988 | — |
| [`package.json`](filetypes/package.json/README.md) | 2162 / 1361 | 0.9996 | — | 0.9992 | 0.9972 | — |
| [`jar`](filetypes/jar/README.md) | 215 / 236 | 0.9812 | — | 0.9839 | 0.9388 | — |
| [`ruby`](filetypes/ruby/README.md) | 7 / 2943 | 1.0000 | — | 1.0000 | 1.0000 | — |
| [`perl`](filetypes/perl/README.md) | 28 / 3956 | 0.9231 | — | 0.9979 | 0.9057 | — |

PR AUC summarizes recall-vs-precision across operating points; Recall@3FP/M is the deployment-budget headline. Per-severity L0..L9 thresholds (observed benign-score quantiles per route, GPD-extrapolated for FP/M targets below the empirical floor) are in [route_policies.md](route_policies.md) — they document the severity-grading curve litmus uses, not optimization targets.

## Provenance

Calibration snapshot `1310931333`, score-table `ad73d201a7a0`, model-set `fba7b85a30a9`. 1 general, 7 filegroup, 40 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
