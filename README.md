# Azoth

Routed ensemble for static malware detection. A general LightGBM classifier scores every file; per-filetype specialists score files in their domain; any route above its calibrated threshold flags the file. Calibrators and L0..L9 thresholds fit on a 530492-row dev partition (12.5% of the labeled corpus). Metrics below: locked 526207-row test partition, disjoint from training and calibration. EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input: cleave-extracted JSON reports. Output: one of `benign`, `suspicious`, `hostile`, with severity level L0..L9. Loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus); deployed default is L3 hostile, L5 suspicious.

Bundle layout: `config.json` (deployed thresholds), then per-route subdirectories under `general/`, `filegroups/<name>/`, `filetypes/<name>/`, each carrying `model.txt`, `feature_spec.json`, and `calibrator.json`. Architecture and FP-budget design: [DESIGN.md](DESIGN.md). Routing detail: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Single-model baseline: [GENERALIST_MODEL.md](GENERALIST_MODEL.md). Apache 2.0.

## Performance

| File type | Mal / Ben | PR AUC [95% CI] | Recall@3FP/M [95% CI] | ROC AUC [95% CI] | F1 [95% CI] | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`pe`](filetypes/pe/README.md) | 99087 / 18558 | 0.9997 | 0.6075 | 0.9986 | 0.9937 | PR +0.0014 / ROC +0.0004 |
| [`elf`](filetypes/elf/README.md) | 4500 / 15507 | 0.9998 | 0.9373 | 0.9999 | 0.9941 | PR +0.0065 / ROC +0.0066 |
| [`macho`](filetypes/macho/README.md) | 205 / 1087 | 0.9898 | — | 0.9980 | 0.9499 | — |
| [`msi`](filetypes/msi/README.md) | 101 / 7 | 0.9997 | — | 0.9958 | 0.9950 | — |
| [`pdf`](filetypes/pdf/README.md) | 18189 / 1731 | 0.9987 | — | 0.9914 | 0.9952 | PR +0.0054 / ROC +0.0002 |
| [`rtf`](filetypes/rtf/README.md) | 196 / 50 | 0.9997 | — | 0.9989 | 0.9924 | — |
| [`javascript`](filetypes/javascript/README.md) | 9559 / 55045 | 0.9879 | 0.0000 | 0.9974 | 0.9419 | — |
| [`python`](filetypes/python/README.md) | 2238 / 15454 | 0.9795 | 0.4830 | 0.9962 | 0.9308 | — |
| [`shell`](filetypes/shell/README.md) | 533 / 5406 | 0.9711 | 0.7767 | 0.9962 | 0.9183 | — |
| [`powershell`](filetypes/powershell/README.md) | 119 / 261 | 0.9461 | — | 0.9769 | 0.9053 | — |
| [`batch`](filetypes/batch/README.md) | 17345 / 263 | 1.0000 | — | 0.9996 | 0.9992 | — |
| [`package.json`](filetypes/package.json/README.md) | 2152 / 1189 | 0.9997 | — | 0.9994 | 0.9972 | — |
| [`jar`](filetypes/jar/README.md) | 182 / 212 | 0.9849 | — | 0.9881 | 0.9568 | — |
| [`ruby`](filetypes/ruby/README.md) | 7 / 2821 | 0.9034 | — | 0.9995 | 0.8571 | — |
| [`perl`](filetypes/perl/README.md) | 27 / 3780 | 0.9523 | 0.0000 | 0.9961 | 0.9412 | — |

PR AUC summarizes recall-vs-precision across operating points; Recall@3FP/M is the deployment-budget headline. Per-severity L0..L9 thresholds (observed benign-score quantiles per route, GPD-extrapolated for FP/M targets below the empirical floor) are in [route_policies.md](route_policies.md) — they document the severity-grading curve litmus uses, not optimization targets.

## Provenance

Calibration snapshot `1234486188`, score-table `46091935de7f`, model-set `0e62cca94242`. 1 general, 8 filegroup, 48 filetype routes.

## Limits

- Strict L0..L3 FP/M targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 6 FP/M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
