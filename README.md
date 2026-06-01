# Azoth

Static malware detection by routed ensemble. A general LightGBM model scores every file. Per-filetype specialists score files in their domain — PE, ELF, JavaScript, PDF, and 47 more. A file is flagged when any route's score crosses its calibrated threshold.

The point of routing is that the evidence differs by format. A PE's section table is signal. A PDF's stream dictionary is signal. A shell script's token distribution is signal. One generalist trained over all of them learns averages; a specialist trained on one of them learns the format.

Thresholds and isotonic calibrators were fit on a 822,241-row dev partition (12.5% of the labeled corpus). The numbers in this README come from a locked 821,686-row test partition, disjoint from training and calibration. The bundle is loaded at scan time by [litmus](https://codeberg.org/atomdrift/litmus). EMBER 2024 reference: Joyce et al., *KDD'25*.

## Use

Input is a JSON report produced by `cleave`. Output is one verdict — `benign` or `hostile` — qualified by a severity level L0..L20. Litmus reads the hostile threshold at the chosen level (consumers can derive a suspicious band as crit/4 if they want a softer tier); the deployed default is L50 (0.5 FP/M). Lower levels tighten the operating point; higher levels loosen it.

## Bundle layout

`config.json` records the deployed thresholds. Each route lives in its own subdirectory: `general/`, one of 7 `filegroups/<name>/`, or one of 51 `filetypes/<name>/`. A route directory carries three files: `model.txt` (LightGBM), `feature_spec.json` (the features the model expects), and `calibrator.json` (isotonic probability calibrator).

Further reading: [DESIGN.md](DESIGN.md) for architecture and FP-budget design, [ENSEMBLE_MODEL.md](ENSEMBLE_MODEL.md) for routing details, [GENERALIST_MODEL.md](GENERALIST_MODEL.md) for the single-model baseline. License: Apache 2.0.

## Per-filetype Ensemble Performance

Each row is the routed ensemble's intrinsic ranking quality on that filetype's slice of the locked test partition — PR AUC, ROC AUC, F1 at the F-beta-tuned threshold, and recall at the L50 (0.5 FP/M) operating point. These are properties of the model's scores; how litmus chooses to threshold those scores at each severity level is a runtime concern documented in [`route_policies.md`](route_policies.md).

A filetype appears here when it has at least 25 malware and 25 benign in the test slice, or at least 100 of each across the full labeled corpus. Pure archive wrappers (zip, tar, gz, …), `data`, and `unknown` are excluded — their score reflects the container's shape, not the classifier's quality.

**Optimization target.** Each filetype's ensemble combiner is selected to maximize **recall at L50 (0.5 FP/M)** on the dev partition, with PR AUC as a tiebreak. Selection is constrained so the ensemble can never report worse than the specialist alone — when no combiner clears the specialist on dev, the ensemble falls back to `specialist_priority` (which equals the specialist by construction). This matches the deployment budget litmus operates at and the design intent that routing must improve, not degrade, the per-filetype model.

| File type | Test mal / ben | PR AUC | ROC AUC | F1 | Recall @ L50 | Δ vs EMBER 2024 |
|---|---:|---:|---:|---:|---:|---:|
| [`rtf`](filetypes/rtf/README.md) | 691 / 51 | 0.999323 | 0.990352 | 0.992722 | 98.55% | — |
| [`batch`](filetypes/batch/README.md) | 22,011 / 520 | 0.999940 | 0.998434 | 0.998184 | 98.51% | — |
| [`python-bytecode`](filetypes/python-bytecode/README.md) | 343 / 9,233 | 0.982102 | 0.986615 | 0.989691 | 97.96% | — |
| [`ole`](filetypes/ole/README.md) | 700 / 737 | 0.992155 | 0.988493 | 0.980449 | 94.57% | — |
| [`xls`](filetypes/xls/README.md) | 4,076 / 2,651 | 0.996953 | 0.995219 | 0.982043 | 94.19% | — |
| [`elf`](filetypes/elf/README.md) | 20,227 / 20,699 | 0.999294 | 0.999353 | 0.987453 | 91.07% | PR +0.005994 / ROC +0.006053 |
| [`package.json`](filetypes/package.json/README.md) | 2,222 / 2,136 | 0.998068 | 0.998202 | 0.993010 | 90.86% | — |
| [`docx`](filetypes/docx/README.md) | 501 / 58 | 0.993115 | 0.952543 | 0.959677 | 89.02% | — |
| [`lnk`](filetypes/lnk/README.md) | 497 / 131 | 0.990246 | 0.969235 | 0.950000 | 82.70% | — |
| [`macho`](filetypes/macho/README.md) | 326 / 1,462 | 0.986217 | 0.995999 | 0.943750 | 81.60% | — |
| [`pkg-info`](filetypes/pkg-info/README.md) | 1,277 / 172 | 0.998890 | 0.995834 | 0.998826 | 72.91% | — |
| [`perl`](filetypes/perl/README.md) | 34 / 4,191 | 0.929933 | 0.994414 | 0.939394 | 70.59% | — |
| [`shell`](filetypes/shell/README.md) | 1,745 / 6,761 | 0.976137 | 0.991807 | 0.918113 | 69.68% | — |
| [`html`](filetypes/html/README.md) | 25 / 3,225 | 0.853379 | 0.987957 | 0.809524 | 68.00% | — |
| [`javascript`](filetypes/javascript/README.md) | 12,360 / 70,684 | 0.962079 | 0.988702 | 0.890704 | 66.76% | — |
| [`pe`](filetypes/pe/README.md) | 155,642 / 19,955 | 0.999488 | 0.996354 | 0.991928 | 65.64% | PR +0.001188 / ROC -0.001846 |
| [`php`](filetypes/php/README.md) | 561 / 15,056 | 0.916493 | 0.990022 | 0.868726 | 64.88% | — |
| [`vbs`](filetypes/vbs/README.md) | 1,254 / 427 | 0.996040 | 0.991046 | 0.984252 | 61.80% | — |
| [`jar`](filetypes/jar/README.md) | 402 / 428 | 0.984229 | 0.984813 | 0.950739 | 55.47% | — |
| [`kotlin`](filetypes/kotlin/README.md) | 3,927 / 6,300 | 0.973672 | 0.974490 | 0.947313 | 48.05% | — |
| [`python`](filetypes/python/README.md) | 2,343 / 20,510 | 0.952485 | 0.990974 | 0.909735 | 47.33% | — |
| [`java_class`](filetypes/java_class/README.md) | 219 / 83,812 | 0.891368 | 0.938837 | 0.882483 | 46.58% | — |
| [`xlsx`](filetypes/xlsx/README.md) | 6,526 / 169 | 0.998224 | 0.952715 | 0.997782 | 45.07% | — |
| [`powershell`](filetypes/powershell/README.md) | 578 / 299 | 0.982718 | 0.972029 | 0.949628 | 40.48% | — |
| [`csharp`](filetypes/csharp/README.md) | 241 / 8,112 | 0.638641 | 0.949621 | 0.580977 | 32.78% | — |
| [`text`](filetypes/text/README.md) | 171 / 8,772 | 0.216145 | 0.794111 | 0.262626 | 15.20% | — |
| [`jpeg`](filetypes/jpeg/README.md) | 149 / 3,363 | 0.245616 | 0.626634 | 0.331658 | 14.09% | — |
| [`deb`](filetypes/deb/README.md) | 42 / 849 | 0.483167 | 0.962687 | 0.596774 | 11.90% | — |
| [`c`](filetypes/c/README.md) | 1,780 / 74,226 | 0.303839 | 0.837032 | 0.338101 | 11.52% | — |
| [`pdf`](filetypes/pdf/README.md) | 22,470 / 2,715 | 0.999048 | 0.994843 | 0.993538 | 10.85% | PR +0.005748 / ROC +0.003643 |
| [`makefile`](filetypes/makefile/README.md) | 60 / 2,952 | 0.533601 | 0.866486 | 0.578947 | 10.00% | — |
| [`markdown`](filetypes/markdown/README.md) | 41 / 7,657 | 0.100426 | 0.548196 | 0.175439 | 9.76% | — |
| [`go`](filetypes/go/README.md) | 1,182 / 13,714 | 0.644731 | 0.906934 | 0.594858 | 7.02% | — |
| [`rust`](filetypes/rust/README.md) | 166 / 10,346 | 0.083979 | 0.675916 | 0.140187 | 3.01% | — |
| [`png`](filetypes/png/README.md) | 673 / 18,998 | 0.133374 | 0.486791 | 0.192802 | 2.67% | — |
| [`xml`](filetypes/xml/README.md) | 380 / 22,297 | 0.171847 | 0.754569 | 0.242950 | 2.37% | — |
| [`plist`](filetypes/plist/README.md) | 66 / 1,581 | 0.114625 | 0.618289 | 0.166667 | 1.52% | — |
| [`json`](filetypes/json/README.md) | 93 / 3,935 | 0.065329 | 0.490574 | 0.082474 | 0.00% | — |

PR AUC summarizes recall against precision across operating points. Recall@L50 is the selection-budget headline; for filetypes whose dev slice cannot resolve L50 (0.5 FP/M) empirically it is GPD-tail-extrapolated. EMBER 2024 deltas are reported where Joyce et al. publish per-filetype numbers (Table 5, All files → X).

## Recall by FP level (per 100M benigns)

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 600 280" width="600" height="280" role="img" aria-label="Corpus recall by FP level"><rect x="52" y="18" width="532" height="220" fill="#fff" stroke="#ccc" stroke-width="1"/><line x1="52" y1="238.0" x2="584" y2="238.0" stroke="#eee" stroke-width="1"/><text x="46" y="242.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#555">0%</text><line x1="52" y1="183.0" x2="584" y2="183.0" stroke="#eee" stroke-width="1"/><text x="46" y="187.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#555">25%</text><line x1="52" y1="128.0" x2="584" y2="128.0" stroke="#eee" stroke-width="1"/><text x="46" y="132.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#555">50%</text><line x1="52" y1="73.0" x2="584" y2="73.0" stroke="#eee" stroke-width="1"/><text x="46" y="77.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#555">75%</text><line x1="52" y1="18.0" x2="584" y2="18.0" stroke="#eee" stroke-width="1"/><text x="46" y="22.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#555">100%</text><line x1="318.0" y1="18" x2="318.0" y2="238" stroke="#999" stroke-width="1" stroke-dasharray="4,3"/><line x1="52.0" y1="238" x2="52.0" y2="241" stroke="#999" stroke-width="1"/><text x="52.0" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L0</text><line x1="81.6" y1="238" x2="81.6" y2="241" stroke="#999" stroke-width="1"/><text x="81.6" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L1</text><line x1="111.1" y1="238" x2="111.1" y2="241" stroke="#999" stroke-width="1"/><text x="111.1" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L2</text><line x1="140.7" y1="238" x2="140.7" y2="241" stroke="#999" stroke-width="1"/><text x="140.7" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L3</text><line x1="170.2" y1="238" x2="170.2" y2="241" stroke="#999" stroke-width="1"/><text x="170.2" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L5</text><line x1="199.8" y1="238" x2="199.8" y2="241" stroke="#999" stroke-width="1"/><text x="199.8" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L10</text><line x1="229.3" y1="238" x2="229.3" y2="241" stroke="#999" stroke-width="1"/><text x="229.3" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L20</text><line x1="258.9" y1="238" x2="258.9" y2="241" stroke="#999" stroke-width="1"/><text x="258.9" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L30</text><line x1="288.4" y1="238" x2="288.4" y2="241" stroke="#999" stroke-width="1"/><text x="288.4" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L40</text><line x1="318.0" y1="238" x2="318.0" y2="241" stroke="#999" stroke-width="1"/><text x="318.0" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L50</text><line x1="347.6" y1="238" x2="347.6" y2="241" stroke="#999" stroke-width="1"/><text x="347.6" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L60</text><line x1="377.1" y1="238" x2="377.1" y2="241" stroke="#999" stroke-width="1"/><text x="377.1" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L70</text><line x1="406.7" y1="238" x2="406.7" y2="241" stroke="#999" stroke-width="1"/><text x="406.7" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L80</text><line x1="436.2" y1="238" x2="436.2" y2="241" stroke="#999" stroke-width="1"/><text x="436.2" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L90</text><line x1="465.8" y1="238" x2="465.8" y2="241" stroke="#999" stroke-width="1"/><text x="465.8" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L100</text><line x1="495.3" y1="238" x2="495.3" y2="241" stroke="#999" stroke-width="1"/><text x="495.3" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L200</text><line x1="524.9" y1="238" x2="524.9" y2="241" stroke="#999" stroke-width="1"/><text x="524.9" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L300</text><line x1="554.4" y1="238" x2="554.4" y2="241" stroke="#999" stroke-width="1"/><text x="554.4" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L500</text><line x1="584.0" y1="238" x2="584.0" y2="241" stroke="#999" stroke-width="1"/><text x="584.0" y="254" text-anchor="middle" font-family="sans-serif" font-size="10" fill="#555">L1000</text><text x="318.0" y="274" text-anchor="middle" font-family="sans-serif" font-size="11" fill="#333">Severity level (FP per 100M benigns)</text><path d="M81.6,128.7 L111.1,128.7 L140.7,128.7 L170.2,128.7 L199.8,128.7 L229.3,128.7 L258.9,128.7 L288.4,128.7 L318.0,128.7 L347.6,128.7 L377.1,128.7 L406.7,128.7 L436.2,128.7 L465.8,128.7 L495.3,128.7 L524.9,128.7 L554.4,128.8 L584.0,128.6" fill="none" stroke="#06c" stroke-width="2" stroke-linejoin="round" stroke-linecap="round"/><circle cx="81.6" cy="128.7" r="3" fill="#06c"/><circle cx="111.1" cy="128.7" r="3" fill="#06c"/><circle cx="140.7" cy="128.7" r="3" fill="#06c"/><circle cx="170.2" cy="128.7" r="3" fill="#06c"/><circle cx="199.8" cy="128.7" r="3" fill="#06c"/><circle cx="229.3" cy="128.7" r="3" fill="#06c"/><circle cx="258.9" cy="128.7" r="3" fill="#06c"/><circle cx="288.4" cy="128.7" r="3" fill="#06c"/><circle cx="318.0" cy="128.7" r="3" fill="#06c"/><circle cx="347.6" cy="128.7" r="3" fill="#06c"/><circle cx="377.1" cy="128.7" r="3" fill="#06c"/><circle cx="406.7" cy="128.7" r="3" fill="#06c"/><circle cx="436.2" cy="128.7" r="3" fill="#06c"/><circle cx="465.8" cy="128.7" r="3" fill="#06c"/><circle cx="495.3" cy="128.7" r="3" fill="#06c"/><circle cx="524.9" cy="128.7" r="3" fill="#06c"/><circle cx="554.4" cy="128.8" r="3" fill="#06c"/><circle cx="584.0" cy="128.6" r="3" fill="#06c"/><path d="M81.6,187.9 L111.1,187.9 L140.7,187.9 L170.2,187.9 L199.8,187.8 L229.3,187.7 L258.9,187.6 L288.4,187.5 L318.0,187.3 L347.6,187.2 L377.1,187.1 L406.7,186.9 L436.2,186.8 L465.8,186.7 L495.3,167.3 L524.9,167.3 L554.4,160.1 L584.0,146.3" fill="none" stroke="#888" stroke-width="2" stroke-linejoin="round" stroke-linecap="round"/><circle cx="81.6" cy="187.9" r="3" fill="#888"/><circle cx="111.1" cy="187.9" r="3" fill="#888"/><circle cx="140.7" cy="187.9" r="3" fill="#888"/><circle cx="170.2" cy="187.9" r="3" fill="#888"/><circle cx="199.8" cy="187.8" r="3" fill="#888"/><circle cx="229.3" cy="187.7" r="3" fill="#888"/><circle cx="258.9" cy="187.6" r="3" fill="#888"/><circle cx="288.4" cy="187.5" r="3" fill="#888"/><circle cx="318.0" cy="187.3" r="3" fill="#888"/><circle cx="347.6" cy="187.2" r="3" fill="#888"/><circle cx="377.1" cy="187.1" r="3" fill="#888"/><circle cx="406.7" cy="186.9" r="3" fill="#888"/><circle cx="436.2" cy="186.8" r="3" fill="#888"/><circle cx="465.8" cy="186.7" r="3" fill="#888"/><circle cx="495.3" cy="167.3" r="3" fill="#888"/><circle cx="524.9" cy="167.3" r="3" fill="#888"/><circle cx="554.4" cy="160.1" r="3" fill="#888"/><circle cx="584.0" cy="146.3" r="3" fill="#888"/><line x1="544" y1="30.0" x2="566" y2="30.0" stroke="#06c" stroke-width="2"/><circle cx="555" cy="30.0" r="3" fill="#06c"/><text x="540" y="34.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#333">corpus-weighted ensemble</text><line x1="544" y1="44.0" x2="566" y2="44.0" stroke="#888" stroke-width="2"/><circle cx="555" cy="44.0" r="3" fill="#888"/><text x="540" y="48.0" text-anchor="end" font-family="sans-serif" font-size="11" fill="#333">general</text></svg>

The corpus-weighted ensemble curve weights each filetype's ensemble recall by the number of labeled files in that filetype, answering: "If I draw a random file from the labeled corpus, what fraction of malware do we catch at this FP budget?" The general curve is the single-model baseline on the full evaluated dataset. The vertical dashed line marks the L50 deploy operating point.

## Provenance

Calibration snapshot `1637343931`, score-table `43b1f8aeb574`, model-set `c59605ac0f68`. 1 general, 7 filegroup, 51 filetype routes.

## Limits

- Strict L0..L50 (FP/100M) targets sit below empirical resolution on a single dev partition (one FP per 150k benigns ≈ 600 FP/100M); their thresholds are GPD tail-extrapolations.
- The split is content-deduplicated by `canonical_sha256`, not family-aware. Campaign-level generalization may be overstated.
- Deployment distribution may differ from the training corpus.

## Sources

[MalwareBazaar](https://bazaar.abuse.ch/), [VirusShare](https://virusshare.com/), [Backstabber's Knife Collection](https://dasfreak.github.io/Backstabbers-Knife-Collection/), [DataDog malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset), [VX Underground](https://vx-underground.org/), [PyPI MalRegistry](https://github.com/lxyeternal/pypi_malregistry), [Linux Malware Samples](https://github.com/MalwareSamples/Linux-Malware-Samples), [Tim (Wadhwa-)Brown's Linux Malware Repo](https://github.com/timb-machine/linux-malware), [Javascript Malware Collection](https://github.com/HynekPetrak/javascript-malware-collection), [ObjectiveSee macOS Malware Collection](https://github.com/objective-see/Malware), [Practical Security Analytics PE Malware ML Dataset](https://practicalsecurityanalytics.com/pe-malware-machine-learning-dataset/), [Ultimate RAT Collection](https://github.com/Cryakl/Ultimate-RAT-Collection).
