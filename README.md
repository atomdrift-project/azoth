# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 45 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 18,146,634-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,263,091-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 49 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 99 | 0.998237 | 0.984084 | 0.985984 | 97.24% | — |
| [`html`](filetypes/html/README.md) | 33 / 22,189 | 0.969774 | 0.984455 | 0.984615 | 96.97% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,634 / 3,970 | 0.995891 | 0.989120 | 0.966487 | 91.24% | — |
| [`elf`](filetypes/elf/README.md) | 24,424 / 105,957 | 0.998051 | 0.999151 | 0.994640 | 86.41% | PR +0.004751 / ROC +0.005851 |
| [`package.json`](filetypes/package.json/README.md) | 2,761 / 8,779 | 0.976348 | 0.980880 | 0.972724 | 82.83% | — |
| [`lnk`](filetypes/lnk/README.md) | 578 / 145 | 0.995604 | 0.986803 | 0.986135 | 82.53% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,839 | 0.831772 | 0.907511 | 0.875000 | 77.78% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,613 / 473 | 0.993159 | 0.979242 | 0.963781 | 75.26% | — |
| [`npm`](filetypes/npm/README.md) | 2,128 / 11,691 | 0.935056 | 0.959733 | 0.913320 | 74.34% | — |
| [`macho`](filetypes/macho/README.md) | 369 / 4,270 | 0.966151 | 0.988089 | 0.943978 | 72.09% | — |
| [`python_sdist`](filetypes/python_sdist/README.md) | 111 / 122 | 0.977864 | 0.973268 | 0.921659 | 72.07% | — |
| [`tar`](filetypes/tar/README.md) | 3,226 / 10,007 | 0.961195 | 0.973811 | 0.920136 | 70.77% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,514 / 3,688 | 0.982440 | 0.891650 | 0.933405 | 64.08% | PR -0.010860 / ROC -0.099550 |
| [`pe`](filetypes/pe/README.md) | 170,105 / 31,191 | 0.999126 | 0.995293 | 0.988653 | 61.85% | PR +0.000826 / ROC -0.002907 |
| [`jar`](filetypes/jar/README.md) | 512 / 4,266 | 0.896993 | 0.964067 | 0.874611 | 58.20% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,883 / 10,651 | 0.941953 | 0.969835 | 0.879292 | 55.19% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 32 / 2,187 | 0.853642 | 0.937764 | 0.888889 | 53.12% | — |
| [`shell`](filetypes/shell/README.md) | 2,414 / 20,620 | 0.927982 | 0.965597 | 0.897890 | 52.36% | — |
| [`powershell`](filetypes/powershell/README.md) | 733 / 710 | 0.971411 | 0.959290 | 0.948555 | 51.57% | — |
| [`whl`](filetypes/whl/README.md) | 522 / 2,150 | 0.837557 | 0.904737 | 0.786051 | 47.89% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 773 | 0.942293 | 0.963888 | 0.882943 | 47.44% | — |
| [`python`](filetypes/python/README.md) | 2,935 / 80,925 | 0.765278 | 0.896889 | 0.791405 | 46.92% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,760 / 213,622 | 0.892114 | 0.948559 | 0.864481 | 45.15% | — |
| [`gem`](filetypes/gem/README.md) | 253 / 4,932 | 0.461706 | 0.639431 | 0.590529 | 41.90% | — |
| [`php`](filetypes/php/README.md) | 895 / 76,864 | 0.680570 | 0.895269 | 0.724777 | 41.56% | — |
| `java_class` | 291 / 219,318 | 0.780588 | 0.936563 | 0.848485 | 37.11% | — |
| `python_bytecode` | 466 / 129,072 | 0.641989 | 0.824602 | 0.749025 | 36.48% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,141 | 0.541274 | 0.717993 | 0.597403 | 36.00% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 354 | 0.991268 | 0.840694 | 0.980812 | 29.53% | — |
| [`zip`](filetypes/zip/README.md) | 13,854 / 5,642 | 0.934631 | 0.832733 | 0.839258 | 29.48% | — |
| [`csharp`](filetypes/csharp/README.md) | 467 / 12,800 | 0.343954 | 0.737622 | 0.402010 | 23.55% | — |
| [`batch`](filetypes/batch/README.md) | 22,141 / 1,033 | 0.991880 | 0.856375 | 0.992737 | 13.92% | — |
| `c` | 2,310 / 212,875 | 0.246324 | 0.686952 | 0.347180 | 11.60% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 193 / 5,610 | 0.196573 | 0.624315 | 0.257261 | 10.36% | — |
| [`deb`](filetypes/deb/README.md) | 61 / 3,474 | 0.135767 | 0.624808 | 0.194444 | 9.84% | — |
| `ruby` | 52 / 22,735 | 0.541230 | 0.850727 | 0.697674 | 5.77% | — |
| `json` | 194 / 32,082 | 0.052315 | 0.715866 | 0.152334 | 5.67% | — |
| `png` | 1,137 / 66,639 | 0.054764 | 0.445294 | 0.100164 | 5.36% | — |
| [`java`](filetypes/java/README.md) | 462 / 23,676 | 0.102667 | 0.484124 | 0.150376 | 4.76% | — |
| `text` | 549 / 40,980 | 0.031862 | 0.628613 | 0.080745 | 4.74% | — |
| `plist` | 81 / 12,575 | 0.009702 | 0.592811 | 0.030338 | 3.70% | — |
| `xml` | 524 / 57,557 | 0.085087 | 0.503624 | 0.146104 | 3.44% | — |
| `makefile` | 102 / 7,872 | 0.012633 | 0.331666 | 0.042553 | 2.94% | — |
| [`go`](filetypes/go/README.md) | 2,219 / 29,419 | 0.243467 | 0.624738 | 0.259089 | 2.43% | — |
| `rust` | 260 / 42,168 | 0.080004 | 0.718161 | 0.145773 | 1.92% | — |
| [`7z`](filetypes/7z/README.md) | 1,172 / 30 | 0.998725 | 0.951991 | 0.988196 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 45 | 0.966238 | 0.890714 | 0.953901 | — | — |
| **Weighted avg** (by test pop) | **1,895,976** | **0.6513** | **0.8419** | **0.6846** | **38.6%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `4265996154`, score-table `ecf9265d67a7`, model-set `a0164ce4edc8`. 1 general, 6 filegroup, 49 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
