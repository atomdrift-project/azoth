# Azoth

Routed ensemble for static malware detection. A general LightGBM classifier scores every file; per-filetype specialists score files in their domain; any route above its calibrated threshold flags the file. Calibrators and L0..L9 thresholds fit on a 2990924-row dev partition (12.5% of the labeled corpus). Metrics below: locked 372198-row test partition, disjoint from training and calibration. EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input: cleave-extracted JSON reports. Output: one of `benign`, `suspicious`, `hostile`, with severity level L0..L9. Loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus); deployed default is L3 hostile, L5 suspicious.

Bundle layout: `config.json` (deployed thresholds), then per-route subdirectories under `general/`, `filegroups/<name>/`, `filetypes/<name>/`, each carrying `model.txt`, `feature_spec.json`, and `calibrator.json`. Architecture and FP-budget design: [DESIGN.md](DESIGN.md). Routing detail: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md). Single-model baseline: [GENERALIST_MODEL.md](GENERALIST_MODEL.md). Apache 2.0.

## Performance

| File type | Mal / Ben | Routed ROC AUC [95% CI] | Routed PR AUC [95% CI] | Routed F1 [95% CI] | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|
| [`pe`](filetypes/pe/README.md) | 49589 / 17544 | 0.9970 [0.9967, 0.9972] | 0.9989 [0.9988, 0.9990] | 0.9872 [0.9865, 0.9878] | ROC -0.0012 / PR +0.0006 |
| [`elf`](filetypes/elf/README.md) | 2742 / 14144 | 0.9998 [0.9997, 0.9998] | 0.9989 [0.9985, 0.9992] | 0.9842 [0.9816, 0.9879] | ROC +0.0065 / PR +0.0056 |
| [`macho`](filetypes/macho/README.md) | 151 / 770 | 0.9730 [0.9612, 0.9837] | 0.9062 [0.8731, 0.9366] | 0.8571 [0.8212, 0.8984] | — |
| [`msi`](filetypes/msi/README.md) | 31 / 6 | 0.7634 | 0.9524 | 0.9118 | — |
| [`pdf`](filetypes/pdf/README.md) | 9 / 343 | 0.8788 [0.8226, 0.9266] | 0.1043 [0.0761, 0.1731] | 0.2333 [0.1586, 0.3405] | ROC -0.1124 / PR -0.8890 |
| [`rtf`](filetypes/rtf/README.md) | 11 / 45 | 1.0000 [1.0000, 1.0000] | 1.0000 [1.0000, 1.0000] | 1.0000 [1.0000, 1.0000] | — |
| [`javascript`](filetypes/javascript/README.md) | 7314 / 47376 | 0.9881 [0.9864, 0.9895] | 0.9740 [0.9712, 0.9767] | 0.9549 [0.9518, 0.9585] | — |
| [`python`](filetypes/python/README.md) | 1689 / 14015 | 0.9904 [0.9872, 0.9935] | 0.9763 [0.9702, 0.9822] | 0.9591 [0.9519, 0.9664] | — |
| [`shell`](filetypes/shell/README.md) | 392 / 5063 | 0.9690 [0.9548, 0.9791] | 0.9299 [0.9081, 0.9485] | 0.9105 [0.8909, 0.9341] | — |
| [`powershell`](filetypes/powershell/README.md) | 59 / 182 | 0.9830 [0.9639, 0.9956] | 0.9638 [0.9364, 0.9877] | 0.8983 [0.8688, 0.9500] | — |
| [`batch`](filetypes/batch/README.md) | 60 / 231 | 0.9578 [0.9180, 0.9852] | 0.9196 [0.8616, 0.9623] | 0.8598 [0.8107, 0.9204] | — |
| [`package.json`](filetypes/package.json/README.md) | 1875 / 907 | 0.9991 [0.9982, 0.9999] | 0.9996 [0.9993, 0.9999] | 0.9971 [0.9955, 0.9987] | — |
| [`jar`](filetypes/jar/README.md) | 107 / 182 | 0.9935 [0.9879, 0.9981] | 0.9890 [0.9796, 0.9968] | 0.9626 [0.9332, 0.9860] | — |
| [`ruby`](filetypes/ruby/README.md) | 7 / 2806 | 1.0000 [1.0000, 1.0000] | 1.0000 [1.0000, 1.0000] | 1.0000 [1.0000, 1.0000] | — |
| [`perl`](filetypes/perl/README.md) | 18 / 3703 | 0.9983 [0.9958, 0.9999] | 0.8562 [0.7109, 0.9684] | 0.8485 [0.7141, 0.9714] | — |

## Operating points

| L | H target/1M | H recall | H FP/1M | H 95% CI upper | S target/1M | S recall | S FP/1M | S 95% CI upper |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0.0† | 70.95% | 36.97 | 61.20 | 8.0† | 70.95% | 36.97 | 61.20 |
| 1 | 1.0† | 70.95% | 36.97 | 61.20 | 16.0 | 71.30% | 36.97 | 61.20 |
| 2 | 2.0† | 70.95% | 36.97 | 61.20 | 24.0 | 72.74% | 47.06 | 73.57 |
| 3 | 3.0† | 70.95% | 36.97 | 61.20 | 32.0 | 73.67% | 50.42 | 77.64 |
| 4 | 4.0† | 70.95% | 36.97 | 61.20 | 40.0 | 74.85% | 50.42 | 77.64 |
| 5 | 5.0† | 70.95% | 36.97 | 61.20 | 48.0 | 75.97% | 57.14 | 85.71 |
| 6 | 6.0† | 70.95% | 36.97 | 61.20 | 56.0 | 76.08% | 60.50 | 89.72 |
| 7 | 7.0† | 70.95% | 36.97 | 61.20 | 64.0 | 76.27% | 63.86 | 93.71 |
| 8 | 8.0† | 70.95% | 36.97 | 61.20 | 72.0 | 76.47% | 67.23 | 97.68 |
| 9 | 9.0† | 70.95% | 36.97 | 61.20 | 80.0 | 76.72% | 67.23 | 97.68 |

*95% CI upper* is the Clopper-Pearson upper bound on the deployment FP rate given the observed FP count in 297,504 test-partition benigns. The honest deployment-FP/M claim sits below this number with 95% confidence.

† below data resolution: the dev calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The deployed threshold falls back to the loosest empirical 0-FP fit; the FP/M and 95% CI columns show what the test partition actually achieves under that threshold, which exceeds the L target.

## Provenance

Calibration snapshot `762136079`, score-table `30d34ec9c941`, model-set `8454dfc478df`. 1 general, 8 filegroup, 41 filetype routes.

## Limits

- L0..L3 FP/M targets are volume-floored: ~150k benign rows in test, one FP ≈ 6 FP/M. Wide CI.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
