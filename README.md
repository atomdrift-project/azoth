# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 67 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 2,652,931-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,653,951-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [Atomdrift Scan](https://github.com/atomdrift-project/scan). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Scan reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (one FP plus an estimated additional 24 FP/100M). Lower levels tighten the operating point; higher levels loosen it.

## False-positive levels

For N benign files, L0 allows zero observed calibration FPs; positive L has a continuous allowance `1 + (L - 1) * N / 100_000_000`, rounded down for an integer count budget. L1 allows one FP; L25 adds an estimated 24 FP/100M beyond that initial FP. Components share the final filetype decision allowance. These are calibration targets, not guaranteed future rates; interpolated or extrapolated estimates and uncertainty are separate from observed counts. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md).

Only detection regressions at L0 through L25 (inclusive) can block model acceptance. Higher levels remain reportable. Calibration allowances apply at every level; empirical test FP overruns do not block installation by default.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 60 `filegroups/<name>/`, or one of 71 `filetypes/<name>/`. A route directory carries a `models/seed_*.onnx` ensemble (LightGBM trees exported to ONNX, one file per training seed) and `feature_spec.json` (the features those models expect). Scores are the models' raw probabilities — there is no separate probability calibrator.

`route_policies.json` retains every selected policy, level, metric, and provenance field. Collimator's runtime staging removes rejected search candidates and compacts the JSON; full candidate diagnostics remain in its training output. Inspect a policy with `jq '.routes["filetypes/elf"]' route_policies.json`. Scan distributes the bundle as a compressed `.tar.zst` archive and reads the installed JSON directly.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row reports the frozen routing policy on the locked test partition. PR AUC and ROC AUC rank signed policy margins; F1 and recall measure actual decisions at L25 (one FP plus an estimated additional 24 FP/100M). Observed false-positive rates can differ from the dev calibration target.

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Selection and reporting.** Models train on train; thresholds and routing policies are selected on dev using the exported production ensembles. Test measures those saved decisions. An ensemble can perform worse than a specialist on test; the report preserves that result.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 821 / 116 | 0.999732 | 0.998771 | 0.996946 | 99.39% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,172 / 10,599 | 0.989991 | 0.997275 | 0.970447 | 98.87% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,484 / 3,774 | 0.999835 | 0.998963 | 0.993648 | 98.80% | PR +0.006535 / ROC +0.007763 |
| [`batch`](filetypes/batch/README.md) | 22,316 / 1,167 | 0.999819 | 0.998285 | 0.993415 | 98.70% | — |
| [`elf`](filetypes/elf/README.md) | 24,970 / 113,467 | 0.999777 | 0.999931 | 0.991582 | 98.36% | PR +0.006477 / ROC +0.006631 |
| [`python_sdist`](filetypes/python_sdist/README.md) | 368 / 1,575 | 0.998614 | 0.999662 | 0.982313 | 98.10% | — |
| [`apk_android`](filetypes/apk_android/README.md) | 505 / 123 | 0.931955 | 0.830927 | 0.943649 | 97.82% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,868 / 547 | 0.999141 | 0.997256 | 0.984632 | 97.75% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 11,052 / 4,154 | 0.999546 | 0.998789 | 0.982077 | 96.92% | — |
| [`html`](filetypes/html/README.md) | 11,513 / 54,275 | 0.999510 | 0.999791 | 0.979541 | 96.07% | — |
| [`7z`](filetypes/7z/README.md) | 1,126 / 50 | 0.998740 | 0.972416 | 0.973218 | 95.20% | — |
| [`lnk`](filetypes/lnk/README.md) | 585 / 153 | 0.999204 | 0.996939 | 0.972831 | 94.87% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,457 / 822 | 0.989698 | 0.931145 | 0.961118 | 93.53% | — |
| [`static-lib`](filetypes/static-lib/README.md) | 72 / 1,614 | 0.925460 | 0.985096 | 0.930556 | 93.06% | — |
| [`jar`](filetypes/jar/README.md) | 481 / 5,255 | 0.970308 | 0.996783 | 0.927900 | 92.31% | — |
| [`gem`](filetypes/gem/README.md) | 51 / 15,028 | 0.914069 | 0.994134 | 0.937500 | 88.24% | — |
| [`registry`](filetypes/registry/README.md) | 59 / 13,680 | 0.967229 | 0.999676 | 0.936937 | 88.14% | — |
| [`shell`](filetypes/shell/README.md) | 2,439 / 21,618 | 0.990678 | 0.996060 | 0.931495 | 87.25% | — |
| [`macho`](filetypes/macho/README.md) | 339 / 4,792 | 0.966588 | 0.994534 | 0.889236 | 84.07% | — |
| [`pe`](filetypes/pe/README.md) | 204,116 / 33,872 | 0.999916 | 0.999500 | 0.904591 | 82.58% | PR +0.001616 / ROC +0.001300 |
| [`php`](filetypes/php/README.md) | 766 / 78,544 | 0.965781 | 0.997145 | 0.902073 | 82.38% | — |
| [`json`](filetypes/json/README.md) | 37 / 39,080 | 0.824993 | 0.990197 | 0.606061 | 81.08% | — |
| [`perl`](filetypes/perl/README.md) | 57 / 10,188 | 0.931015 | 0.998626 | 0.876190 | 80.70% | — |
| [`java_class`](filetypes/java_class/README.md) | 296 / 229,234 | 0.903520 | 0.981869 | 0.875472 | 78.38% | — |
| [`powershell`](filetypes/powershell/README.md) | 778 / 795 | 0.994967 | 0.994660 | 0.871832 | 77.38% | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 403 / 154,295 | 0.948054 | 0.991586 | 0.852006 | 76.43% | — |
| [`rust`](filetypes/rust/README.md) | 59 / 45,705 | 0.372388 | 0.974949 | 0.347490 | 76.27% | — |
| [`zip`](filetypes/zip/README.md) | 13,626 / 18,640 | 0.997887 | 0.998348 | 0.858841 | 75.28% | — |
| [`npm`](filetypes/npm/README.md) | 3,675 / 44,281 | 0.973833 | 0.993752 | 0.849546 | 73.90% | — |
| [`ico`](filetypes/ico/README.md) | 33 / 101 | 0.941694 | 0.956196 | 0.842105 | 72.73% | — |
| [`java`](filetypes/java/README.md) | 414 / 25,208 | 0.977308 | 0.997385 | 0.825967 | 72.22% | — |
| [`tar`](filetypes/tar/README.md) | 1,919 / 13,525 | 0.972485 | 0.993590 | 0.815887 | 69.05% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,673 / 9,675 | 0.998039 | 0.998535 | 0.810414 | 68.13% | — |
| [`javascript`](filetypes/javascript/README.md) | 18,081 / 227,861 | 0.990108 | 0.998143 | 0.801722 | 66.94% | — |
| [`python`](filetypes/python/README.md) | 2,630 / 85,342 | 0.948804 | 0.994162 | 0.782709 | 64.37% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 30 / 2,338 | 0.906722 | 0.980639 | 0.760000 | 63.33% | — |
| [`go`](filetypes/go/README.md) | 1,111 / 32,114 | 0.861585 | 0.976661 | 0.748763 | 61.30% | — |
| [`gif`](filetypes/gif/README.md) | 77 / 236 | 0.875862 | 0.933634 | 0.723077 | 61.04% | — |
| [`crx`](filetypes/crx/README.md) | 310 / 1,550 | 0.952546 | 0.987309 | 0.744467 | 59.68% | — |
| [`ruby`](filetypes/ruby/README.md) | 33 / 24,722 | 0.908990 | 0.993128 | 0.730769 | 57.58% | — |
| [`png`](filetypes/png/README.md) | 983 / 68,459 | 0.900313 | 0.979634 | 0.674293 | 50.97% | — |
| [`csharp`](filetypes/csharp/README.md) | 454 / 12,879 | 0.914852 | 0.989537 | 0.627451 | 45.81% | — |
| [`xml`](filetypes/xml/README.md) | 225 / 55,957 | 0.649505 | 0.969601 | 0.571429 | 44.44% | — |
| [`whl`](filetypes/whl/README.md) | 330 / 8,589 | 0.847617 | 0.986932 | 0.504464 | 34.24% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 194 / 5,652 | 0.694264 | 0.947396 | 0.496241 | 34.02% | — |
| [`vsix`](filetypes/vsix/README.md) | 45 / 773 | 0.692408 | 0.914460 | 0.474576 | 31.11% | — |
| [`c`](filetypes/c/README.md) | 2,113 / 221,833 | 0.851096 | 0.994891 | 0.463104 | 30.15% | — |
| [`text`](filetypes/text/README.md) | 817 / 62,341 | 0.845749 | 0.984037 | 0.384236 | 23.87% | — |
| **Weighted avg** (by test pop) | **2,135,561** | **0.9238** | **0.9920** | **0.7840** | **70.1%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (one FP plus an estimated additional 24 FP/100M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (pool-adjusted)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `6309383805`, score-table `fd28846c793d`, model-set `115e8755a6b5`. 1 general, 60 filegroup, 71 filetype routes.

## Limits

- The level is a pool-adjusted calibration target. Interpolation or extrapolation does not guarantee the future FP rate; more representative benign data improves rate estimation.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
