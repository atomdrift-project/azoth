# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 42 more. A file is flagged when any route's score crosses its operating-point threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds were fit on a 1,610,244-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 1,608,866-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can label anything firing above the configured critical level as suspicious if they want a softer tier); the deployed default is L25 (0.25 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 46 `filetypes/<name>/`. A route directory carries two files: `model.txt` (LightGBM) and `feature_spec.json` (the features the model expects). Scores are the model's raw probabilities — there is no separate probability calibrator.

Further reading: [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L25 (0.25 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L25 (0.25 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L25 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`elf`](filetypes/elf/README.md) | 23,668 / 49,142 | 0.999680 | 0.999779 | 0.995623 | — | PR +0.006380 / ROC +0.006479 |
| [`pe`](filetypes/pe/README.md) | 169,146 / 23,659 | 0.999189 | 0.994228 | 0.987825 | — | PR +0.000889 / ROC -0.003972 |
| [`rtf`](filetypes/rtf/README.md) | 830 / 94 | 0.998797 | 0.990156 | 0.988464 | — | — |
| [`pdf`](filetypes/pdf/README.md) | 22,517 / 3,421 | 0.997748 | 0.985710 | 0.986687 | — | PR +0.004448 / ROC -0.005490 |
| [`ole_doc`](filetypes/ole_doc/README.md) | 10,603 / 3,886 | 0.995156 | 0.986356 | 0.963480 | — | — |
| [`batch`](filetypes/batch/README.md) | 22,134 / 939 | 0.995053 | 0.931431 | 0.994879 | — | — |
| [`vbs`](filetypes/vbs/README.md) | 1,560 / 458 | 0.994425 | 0.981252 | 0.960101 | — | — |
| [`html`](filetypes/html/README.md) | 31 / 2,010 | 0.994058 | 0.999928 | 0.983607 | — | — |
| [`lnk`](filetypes/lnk/README.md) | 569 / 132 | 0.992758 | 0.970775 | 0.976664 | — | — |
| [`zip`](filetypes/zip/README.md) | 13,110 / 2,708 | 0.991587 | 0.964041 | 0.964919 | — | — |
| [`package.json`](filetypes/package.json/README.md) | 2,490 / 5,361 | 0.991321 | 0.990417 | 0.983374 | — | — |
| [`pkg_info`](filetypes/pkg_info/README.md) | 1,270 / 1,392 | 0.990412 | 0.987394 | 0.980769 | — | — |
| [`ooxml`](filetypes/ooxml/README.md) | 8,558 / 351 | 0.983144 | 0.695578 | 0.980518 | — | — |
| [`tar`](filetypes/tar/README.md) | 2,951 / 7,087 | 0.982122 | 0.986152 | 0.947440 | — | — |
| [`gem`](filetypes/gem/README.md) | 87 / 237 | 0.966567 | 0.974029 | 0.952381 | — | — |
| [`powershell`](filetypes/powershell/README.md) | 723 / 568 | 0.966402 | 0.955109 | 0.934659 | — | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,891 / 9,079 | 0.959253 | 0.974629 | 0.892776 | — | — |
| [`macho`](filetypes/macho/README.md) | 361 / 2,670 | 0.950025 | 0.989253 | 0.882353 | — | — |
| [`shell`](filetypes/shell/README.md) | 2,305 / 16,051 | 0.937964 | 0.968720 | 0.894283 | — | — |
| [`whl`](filetypes/whl/README.md) | 373 / 699 | 0.929484 | 0.937375 | 0.864569 | — | — |
| [`npm`](filetypes/npm/README.md) | 410 / 522 | 0.926819 | 0.904836 | 0.859278 | — | — |
| [`jar`](filetypes/jar/README.md) | 494 / 1,635 | 0.922622 | 0.958080 | 0.862869 | — | — |
| [`javascript`](filetypes/javascript/README.md) | 16,728 / 149,064 | 0.913192 | 0.963912 | 0.864160 | — | — |
| `java_class` | 280 / 188,136 | 0.820973 | 0.955031 | 0.843931 | — | — |
| [`perl`](filetypes/perl/README.md) | 46 / 8,104 | 0.809747 | 0.932692 | 0.853659 | — | — |
| `registry` | 56 / 8,954 | 0.789240 | 0.998021 | 0.725275 | — | — |
| [`python`](filetypes/python/README.md) | 2,851 / 61,653 | 0.775449 | 0.912088 | 0.746761 | — | — |
| [`php`](filetypes/php/README.md) | 798 / 67,356 | 0.702328 | 0.896618 | 0.731136 | — | — |
| [`python_bytecode`](filetypes/python_bytecode/README.md) | 461 / 81,658 | 0.697064 | 0.896518 | 0.800000 | — | — |
| [`cargo.toml`](filetypes/cargo.toml/README.md) | 50 / 823 | 0.465044 | 0.740012 | 0.571429 | — | — |
| [`ruby`](filetypes/ruby/README.md) | 35 / 20,971 | 0.369484 | 0.785749 | 0.458333 | — | — |
| [`csharp`](filetypes/csharp/README.md) | 466 / 11,125 | 0.347453 | 0.721789 | 0.404531 | — | — |
| [`go`](filetypes/go/README.md) | 2,113 / 26,285 | 0.239438 | 0.603298 | 0.249310 | — | — |
| [`jpeg`](filetypes/jpeg/README.md) | 180 / 5,391 | 0.202801 | 0.524832 | 0.293578 | — | — |
| [`deb`](filetypes/deb/README.md) | 57 / 2,336 | 0.154638 | 0.709362 | 0.190476 | — | — |
| [`xml`](filetypes/xml/README.md) | 506 / 49,660 | 0.119721 | 0.620201 | 0.165202 | — | — |
| [`text`](filetypes/text/README.md) | 500 / 31,813 | 0.085889 | 0.549597 | 0.131206 | — | — |
| [`json`](filetypes/json/README.md) | 202 / 18,700 | 0.085120 | 0.593853 | 0.129630 | — | — |
| [`png`](filetypes/png/README.md) | 1,091 / 45,357 | 0.081155 | 0.532568 | 0.106870 | — | — |
| `c` | 2,297 / 168,691 | — | — | — | — | — |
| `crx` | 230 / 174 | — | — | — | — | — |
| `dockerfile` | 25 / 541 | — | — | — | — | — |
| `java` | 459 / 19,271 | — | — | — | — | — |
| `makefile` | 102 / 7,392 | — | — | — | — | — |
| `plist` | 84 / 11,955 | — | — | — | — | — |
| `rust` | 258 / 39,635 | — | — | — | — | — |
| **Weighted avg** (by test pop) | **1,475,102** | **0.7570** | **0.8939** | **0.7631** | **—** | — |

PR AUC summarizes recall against precision across operating points. Recall@L25 is the selection-budget headline; for filetypes whose calibration slice cannot resolve L25 (0.25 FP/M) empirically, that level shares an operating point with its neighbours (its measured ceiling). EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="Corpus-weighted recall by FP level (per 100M benigns)" height="300" />

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. filetypes/elf is shown for comparison — a single strong route that resolves across levels, so the corpus-weighted line (dominated by large, near-flat routes like pe) can be read against it. The vertical dashed line marks the L25 deploy operating point.

## Provenance

Calibration snapshot `2037843653`, score-table `9934f123c59f`, model-set `2dda135a4536`. 1 general, 7 filegroup, 46 filetype routes.

## Limits

- Strict L0..L25 (FP/100M) targets can sit below the calibration benign volume's resolution (the finest non-zero rate is 1 FP / N_benign); below that, adjacent levels share one measured-ceiling operating point. Thresholds are measured (loosest score within the level's FP budget +1 slack), not extrapolated — they can't overshoot on live traffic. More benigns sharpen the low levels.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
