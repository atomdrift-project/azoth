# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 48 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 18,322,760-row all partition (12.5% of the labeled corpus). The numbers in this README come from a locked 2,285,523-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://github.com/atomdrift-project/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L25000. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 6 `filegroups/<name>/`, or one of 52 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 832 / 107 | 0.998882 | 0.991446 | 0.985984 | 97.24% | — |
| [`html`](filetypes/html/README.md) | 33 / 23,284 | 0.969747 | 0.973797 | 0.984615 | 96.97% | — |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,634 / 4,030 | 0.995532 | 0.988356 | 0.966263 | 91.58% | — |
| [`elf`](filetypes/elf/README.md) | 24,428 / 107,310 | 0.998162 | 0.999217 | 0.994948 | 86.28% | PR +0.004862 / ROC +0.005917 |
| [`lnk`](filetypes/lnk/README.md) | 578 / 145 | 0.997480 | 0.990210 | 0.988822 | 82.70% | — |
| [`package.json`](filetypes/package.json/README.md) | 2,761 / 8,807 | 0.976846 | 0.982017 | 0.972663 | 80.95% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,618 / 475 | 0.991697 | 0.975272 | 0.960366 | 76.45% | — |
| [`perl`](filetypes/perl/README.md) | 45 / 9,848 | 0.834692 | 0.921848 | 0.860759 | 75.56% | — |
| [`registry`](filetypes/registry/README.md) | 77 / 13,654 | 0.920064 | 0.991861 | 0.869565 | 75.32% | — |
| [`npm`](filetypes/npm/README.md) | 2,118 / 12,544 | 0.949000 | 0.964876 | 0.931790 | 70.96% | — |
| [`tar`](filetypes/tar/README.md) | 3,224 / 10,058 | 0.961388 | 0.973370 | 0.925378 | 68.70% | — |
| [`macho`](filetypes/macho/README.md) | 369 / 4,342 | 0.968142 | 0.987868 | 0.943292 | 67.75% | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 32 / 2,193 | 0.860201 | 0.931608 | 0.888889 | 65.62% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,514 / 3,699 | 0.993132 | 0.961528 | 0.961854 | 65.52% | PR -0.000168 / ROC -0.029672 |
| [`pe`](filetypes/pe/README.md) | 170,112 / 31,490 | 0.999164 | 0.995560 | 0.988565 | 61.46% | PR +0.000864 / ROC -0.002640 |
| [`python_sdist`](filetypes/python_sdist/README.md) | 113 / 218 | 0.972632 | 0.979094 | 0.919643 | 60.18% | — |
| [`jar`](filetypes/jar/README.md) | 512 / 4,357 | 0.904446 | 0.955531 | 0.882231 | 58.59% | — |
| [`powershell`](filetypes/powershell/README.md) | 733 / 711 | 0.968222 | 0.953842 | 0.946176 | 55.25% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,881 / 10,667 | 0.941167 | 0.967086 | 0.883691 | 53.90% | — |
| [`shell`](filetypes/shell/README.md) | 2,419 / 20,664 | 0.926846 | 0.964659 | 0.896787 | 52.58% | — |
| `java_class` | 291 / 220,674 | 0.784766 | 0.922759 | 0.850662 | 49.83% | — |
| [`crx`](filetypes/crx/README.md) | 293 / 773 | 0.942126 | 0.964051 | 0.882550 | 47.44% | — |
| [`python`](filetypes/python/README.md) | 2,941 / 82,346 | 0.769219 | 0.899038 | 0.793443 | 47.06% | — |
| [`whl`](filetypes/whl/README.md) | 522 / 2,501 | 0.832679 | 0.905088 | 0.783099 | 45.59% | — |
| [`javascript`](filetypes/javascript/README.md) | 17,767 / 214,731 | 0.895500 | 0.956455 | 0.859985 | 45.49% | — |
| `python_bytecode` | 466 / 132,930 | 0.637796 | 0.824377 | 0.750978 | 43.99% | — |
| [`gem`](filetypes/gem/README.md) | 253 / 5,841 | 0.481241 | 0.795654 | 0.588889 | 41.50% | — |
| [`zip`](filetypes/zip/README.md) | 13,873 / 6,512 | 0.927105 | 0.833517 | 0.817535 | 41.02% | — |
| `php` | 898 / 76,894 | 0.678857 | 0.889414 | 0.725154 | 39.09% | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 1,147 | 0.544959 | 0.781343 | 0.606742 | 36.00% | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,564 / 710 | 0.987998 | 0.893391 | 0.973820 | 32.92% | — |
| [`csharp`](filetypes/csharp/README.md) | 467 / 12,800 | 0.341584 | 0.692112 | 0.403909 | 24.20% | — |
| [`batch`](filetypes/batch/README.md) | 22,141 / 1,036 | 0.988980 | 0.860173 | 0.989411 | 15.08% | — |
| `c` | 2,311 / 213,961 | 0.241341 | 0.635406 | 0.348581 | 12.55% | — |
| [`ruby`](filetypes/ruby/README.md) | 52 / 22,758 | 0.555877 | 0.857181 | 0.697674 | 11.54% | — |
| [`deb`](filetypes/deb/README.md) | 61 / 3,478 | 0.138088 | 0.683698 | 0.188235 | 9.84% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 193 / 5,610 | 0.197899 | 0.575433 | 0.256410 | 9.33% | — |
| [`java`](filetypes/java/README.md) | 462 / 24,115 | 0.112111 | 0.593285 | 0.150000 | 5.63% | — |
| `png` | 1,137 / 66,707 | 0.054117 | 0.435509 | 0.100164 | 5.36% | — |
| `text` | 556 / 41,130 | 0.030819 | 0.638280 | 0.077844 | 4.68% | — |
| [`xml`](filetypes/xml/README.md) | 524 / 57,605 | 0.078682 | 0.496564 | 0.144781 | 4.58% | — |
| `plist` | 81 / 12,578 | 0.016777 | 0.411047 | 0.065934 | 3.70% | — |
| [`json`](filetypes/json/README.md) | 193 / 32,228 | 0.082334 | 0.714975 | 0.129617 | 3.11% | — |
| `makefile` | 102 / 7,873 | 0.013785 | 0.399258 | 0.042857 | 2.94% | — |
| [`go`](filetypes/go/README.md) | 2,219 / 29,504 | 0.234947 | 0.628667 | 0.250163 | 2.21% | — |
| `rust` | 260 / 42,237 | 0.024680 | 0.553500 | 0.089239 | 1.15% | — |
| [`7z`](filetypes/7z/README.md) | 1,172 / 33 | 0.998533 | 0.949775 | 0.986947 | — | — |
| [`apk_android`](filetypes/apk_android/README.md) | 274 / 45 | 0.957244 | 0.874615 | 0.951872 | — | — |
| `yaml` | 91 / 1,146 | 0.080442 | 0.468260 | 0.141066 | 0.00% | — |
| **Weighted avg** (by test pop) | **1,913,753** | **0.6511** | **0.8331** | **0.6835** | **40.8%** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `4351728144`, score-table `c54aab80e0f2`, model-set `645a8bf90bfa`. 1 general, 6 filegroup, 52 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
