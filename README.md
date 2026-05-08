# azoth (PREVIEW)

Azoth is Atomdrift's open-source routed malware detection model for broad file scanning.

It ships with [litmus](https://codeberg.org/atomdrift/litmus) and scores static analysis reports from [cleave](https://codeberg.org/atomdrift/cleave). The current bundle is a LightGBM ensemble: one general model, filegroup specialists, and filetype specialists selected by calibrated route policy.

- Model card: [MODEL.md](MODEL.md)
- Training notes: [TRAINING.md](TRAINING.md)
- Policy details: [route_policies.md](route_policies.md)

## Pipeline

```text
cleave-traits ──► cleave / litmus ──► hopper ──► collimator ──► azoth
                                                ▲
                                                │
                               autocollie ─────┘
```

### [cleave-traits](https://codeberg.org/atomdrift/cleave-traits)
YAML behavior rules aligned to MBC and MITRE ATT&CK.

### [cleave](https://codeberg.org/atomdrift/cleave)
Static analyzer that extracts capabilities from binaries, source, documents, media, packages, and archives.

### [litmus](https://codeberg.org/atomdrift/litmus)
Runtime scanner. It runs cleave, evaluates the Azoth route policy, and returns `hostile`, `suspicious`, or `benign` with supporting behaviors.

### hopper
Local job broker and labeled sample store backed by Postgres.

### collimator
Training and calibration pipeline. It builds feature vocabularies, trains LightGBM route models, calibrates false-positive budgets, writes model cards, and validates litmus compatibility.

### autocollie
Automated experiment loop for collimator. It proposes deployable knob changes, runs cached experiments, confirms promising wins, and emits candidate promotion reports.

## Default Policy Snapshot

- Corpus: 2293938 rows (472475 malware, 1821463 benign).
- Default hostile level: L3, targeting 3 false positives per million benign files across the full corpus.
- Suspicious is a higher-recall companion signal, not the primary deployment gate.

| Signal | Target FP/1M | Accuracy | Recall | Actual FP/1M | TP | FP |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Hostile L3 | 3.0 | 92.50% | 63.59% | 2.75 | 300463 | 5 |
| Suspicious L3 | 32.0 | 95.26% | 77.02% | 31.84 | 363884 | 58 |

## Raw Filetype Specialist Metrics

These are held-out specialist benchmark metrics before routed policy selection. `Acc@F1` is the accuracy at the threshold that maximizes F1 on that benchmark split.

| Filetype | Rows | Malware | Benign | Acc@F1 | AUC | AP | F1 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| `pe` | 56559 | 39743 | 16816 | 99.27% | 0.9994 | 0.9998 | 0.9948 |
| `c` | 53020 | 820 | 52200 | 98.61% | 0.9413 | 0.5243 | 0.5892 |
| `javascript` | 49195 | 7179 | 42016 | 99.36% | 0.9980 | 0.9943 | 0.9778 |
| `elf` | 14228 | 2009 | 12219 | 99.88% | 1.0000 | 0.9998 | 0.9958 |
| `python` | 13697 | 1525 | 12172 | 99.63% | 0.9987 | 0.9958 | 0.9835 |
| `go` | 10669 | 115 | 10554 | 99.44% | 0.9660 | 0.6863 | 0.6739 |
| `xml` | 10593 | 144 | 10449 | 95.39% | 0.8995 | 0.1039 | 0.1894 |
| `png` | 8126 | 432 | 7694 | 95.82% | 0.9247 | 0.5767 | 0.5330 |
| `rust` | 7928 | 7 | 7921 | 99.85% | 0.9931 | 0.1496 | 0.2500 |
| `text` | 5977 | 84 | 5893 | 96.64% | 0.8631 | 0.1563 | 0.3045 |
| `shell` | 4802 | 306 | 4496 | 99.33% | 0.9911 | 0.9657 | 0.9465 |
| `csharp` | 4503 | 88 | 4415 | 99.53% | 0.9881 | 0.8856 | 0.8727 |
| `zip` | 4113 | 3790 | 323 | 97.47% | 0.9801 | 0.9977 | 0.9864 |
| `kotlin` | 3673 | 77 | 3596 | 99.81% | 0.9970 | 0.9681 | 0.9530 |
| `gz` | 3385 | 19 | 3366 | 99.47% | 0.8571 | 0.1833 | 0.4000 |
| `perl` | 2744 | 18 | 2726 | 99.96% | 0.9999 | 0.9899 | 0.9714 |
| `package.json` | 2667 | 1844 | 823 | 99.55% | 0.9992 | 0.9996 | 0.9967 |
| `tar.gz` | 2608 | 1419 | 1189 | 99.19% | 0.9990 | 0.9993 | 0.9926 |
| `php` | 2418 | 160 | 2258 | 99.83% | 0.9999 | 0.9986 | 0.9874 |
| `zst` | 2384 | 307 | 2077 | 100.00% | 1.0000 | 1.0000 | 1.0000 |
| `makefile` | 2275 | 4 | 2271 | 99.74% | 0.8778 | 0.3366 | 0.4000 |
| `unknown` | 1800 | 12 | 1788 | 97.83% | 0.4688 | 0.0154 | 0.0930 |
| `ruby` | 1466 | 7 | 1459 | 100.00% | 1.0000 | 1.0000 | 1.0000 |
| `plist` | 1159 | 58 | 1101 | 98.53% | 0.9908 | 0.9114 | 0.8522 |
| `data` | 1151 | 43 | 1108 | 99.65% | 0.9981 | 0.9744 | 0.9512 |
| `python-bytecode` | 1088 | 9 | 1079 | 99.91% | 0.9996 | 0.9658 | 0.9412 |
| `java_class` | 918 | 41 | 877 | 99.78% | 0.9991 | 0.9816 | 0.9756 |
| `jpeg` | 839 | 65 | 774 | 92.49% | 0.9333 | 0.6416 | 0.5714 |
| `macho` | 771 | 145 | 626 | 99.35% | 0.9991 | 0.9953 | 0.9831 |
| `ole` | 702 | 47 | 655 | 99.72% | 0.9787 | 0.9603 | 0.9783 |
| `pkg-info` | 524 | 441 | 83 | 100.00% | 1.0000 | 1.0000 | 1.0000 |
| `pdf` | 287 | 10 | 277 | 97.21% | 0.9733 | 0.6095 | 0.6667 |
| `jar` | 222 | 101 | 121 | 98.20% | 0.9959 | 0.9953 | 0.9800 |
| `batch` | 206 | 44 | 162 | 97.09% | 0.9579 | 0.9429 | 0.9286 |
| `powershell` | 159 | 47 | 112 | 97.48% | 0.9953 | 0.9902 | 0.9574 |
| `tar` | 152 | 109 | 43 | 98.03% | 0.9888 | 0.9957 | 0.9860 |
| `vbs` | 88 | 70 | 18 | 88.64% | 0.9131 | 0.9751 | 0.9296 |
| `rtf` | 51 | 8 | 43 | 15.69% | 0.5000 | 0.1569 | 0.2712 |
| `docx` | 43 | 17 | 26 | 90.70% | 0.8914 | 0.8348 | 0.8750 |
| `xlsx` | 17 | 11 | 6 | 64.71% | 0.5000 | 0.6471 | 0.7857 |

## Filetype Ensemble Metrics at FP@3

These are full-corpus L3 hostile metrics for each filetype route after policy search. `Global FP/1M` is the route contribution to the whole-corpus false-positive budget.

| Filetype | Rows | Malware | Benign | Policy | Accuracy | Recall | FP | Global FP/1M |
| --- | ---: | ---: | ---: | --- | ---: | ---: | ---: | ---: |
| `pe` | 423309 | 290279 | 133030 | `specialist_primary_with_escape` | 76.09% | 65.14% | 1 | 0.549 |
| `c` | 422242 | 6558 | 415684 | `no_policy` | 98.45% | 0.00% | 0 | 0.000 |
| `javascript` | 389662 | 56551 | 333111 | `or_general_primary` | 98.12% | 87.04% | 1 | 0.549 |
| `elf` | 110933 | 15610 | 95323 | `specialist_primary_with_escape` | 99.87% | 99.05% | 1 | 0.549 |
| `python` | 109446 | 11667 | 97779 | `no_policy` | 89.34% | 0.00% | 0 | 0.000 |
| `xml` | 84391 | 1036 | 83355 | `general_only` | 98.80% | 2.61% | 0 | 0.000 |
| `go` | 84120 | 804 | 83316 | `no_policy` | 99.04% | 0.00% | 0 | 0.000 |
| `png` | 63666 | 3412 | 60254 | `general_only` | 94.64% | 0.03% | 0 | 0.000 |
| `rust` | 63601 | 52 | 63549 | `group_primary_with_escape` | 99.94% | 25.00% | 0 | 0.000 |
| `text` | 47647 | 618 | 47029 | `no_policy` | 98.70% | 0.00% | 0 | 0.000 |
| `shell` | 37332 | 1756 | 35576 | `no_policy` | 95.30% | 0.00% | 0 | 0.000 |
| `csharp` | 35134 | 647 | 34487 | `no_policy` | 98.16% | 0.00% | 0 | 0.000 |
| `zip` | 34248 | 31413 | 2835 | `specialist_primary_with_escape` | 76.79% | 74.70% | 1 | 0.549 |
| `kotlin` | 29495 | 625 | 28870 | `group_primary_with_escape` | 99.11% | 57.92% | 0 | 0.000 |
| `gz` | 27476 | 179 | 27297 | `group_only` | 99.53% | 27.37% | 0 | 0.000 |
| `swift` | 25482 | 0 | 25482 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `tar.gz` | 24948 | 15692 | 9256 | `no_policy` | 37.10% | 0.00% | 0 | 0.000 |
| `xz` | 23353 | 41 | 23312 | `group_only` | 99.94% | 65.85% | 0 | 0.000 |
| `perl` | 22066 | 149 | 21917 | `no_policy` | 99.32% | 0.00% | 0 | 0.000 |
| `package.json` | 21806 | 15355 | 6451 | `group_primary_with_escape` | 98.39% | 97.73% | 1 | 0.549 |
| `java` | 21047 | 18 | 21029 | `or_general_primary` | 99.96% | 50.00% | 0 | 0.000 |
| `zst` | 18415 | 2282 | 16133 | `or_general_primary` | 99.78% | 98.20% | 0 | 0.000 |
| `makefile` | 17827 | 65 | 17762 | `general_only` | 99.64% | 1.54% | 0 | 0.000 |
| `php` | 17622 | 1247 | 16375 | `filetype_only` | 98.75% | 82.36% | 0 | 0.000 |
| `unknown` | 14184 | 89 | 14095 | `no_policy` | 99.37% | 0.00% | 0 | 0.000 |
| `ruby` | 12013 | 69 | 11944 | `no_policy` | 99.43% | 0.00% | 0 | 0.000 |
| `bz2` | 10852 | 2 | 10850 | `no_policy` | 99.98% | 0.00% | 0 | 0.000 |
| `plist` | 9331 | 468 | 8863 | `no_policy` | 94.98% | 0.00% | 0 | 0.000 |
| `data` | 8869 | 299 | 8570 | `or_general_primary` | 99.53% | 85.95% | 0 | 0.000 |
| `python-bytecode` | 8490 | 84 | 8406 | `filetype_only` | 99.92% | 91.67% | 0 | 0.000 |
| `java_class` | 7626 | 364 | 7262 | `group_only` | 99.03% | 79.67% | 0 | 0.000 |
| `jpeg` | 7010 | 514 | 6496 | `general_only` | 92.82% | 2.14% | 0 | 0.000 |
| `macho` | 6150 | 1296 | 4854 | `no_policy` | 78.93% | 0.00% | 0 | 0.000 |
| `elixir` | 5705 | 0 | 5705 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `ole` | 5540 | 238 | 5302 | `no_policy` | 95.70% | 0.00% | 0 | 0.000 |
| `lua` | 4529 | 29 | 4500 | `group_only` | 99.49% | 20.69% | 0 | 0.000 |
| `pkg-info` | 4373 | 3671 | 702 | `no_policy` | 16.05% | 0.00% | 0 | 0.000 |
| `objc` | 4236 | 5 | 4231 | `general_only` | 99.95% | 60.00% | 0 | 0.000 |
| `deb` | 4195 | 4 | 4191 | `no_policy` | 99.90% | 0.00% | 0 | 0.000 |
| `github-actions` | 3155 | 2 | 3153 | `general_only` | 99.97% | 50.00% | 0 | 0.000 |
| `7z` | 3137 | 3115 | 22 | `no_policy` | 0.70% | 0.00% | 0 | 0.000 |
| `scala` | 2602 | 0 | 2602 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `pdf` | 2200 | 82 | 2118 | `general_only` | 96.64% | 9.76% | 0 | 0.000 |
| `batch` | 1791 | 308 | 1483 | `filetype_only` | 94.53% | 68.18% | 0 | 0.000 |
| `jar` | 1628 | 567 | 1061 | `no_policy` | 65.17% | 0.00% | 0 | 0.000 |
| `doc` | 1565 | 1550 | 15 | `general_only` | 99.68% | 99.68% | 0 | 0.000 |
| `tar` | 1379 | 1041 | 338 | `filetype_only` | 93.11% | 90.87% | 0 | 0.000 |
| `powershell` | 1209 | 337 | 872 | `no_policy` | 72.13% | 0.00% | 0 | 0.000 |
| `groovy` | 1156 | 4 | 1152 | `general_only` | 99.74% | 25.00% | 0 | 0.000 |
| `rar` | 748 | 745 | 3 | `general_only` | 96.12% | 96.11% | 0 | 0.000 |
| `vbs` | 708 | 578 | 130 | `no_policy` | 18.36% | 0.00% | 0 | 0.000 |
| `systemd` | 594 | 4 | 590 | `general_only` | 99.49% | 25.00% | 0 | 0.000 |
| `rpm` | 524 | 0 | 524 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `rtf` | 477 | 69 | 408 | `general_only` | 99.37% | 95.65% | 0 | 0.000 |
| `docx` | 359 | 160 | 199 | `no_policy` | 55.43% | 0.00% | 0 | 0.000 |
| `pickle` | 284 | 0 | 284 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `tar.xz` | 232 | 5 | 227 | `general_only` | 100.00% | 100.00% | 0 | 0.000 |
| `lnk` | 219 | 203 | 16 | `general_only` | 99.09% | 99.01% | 0 | 0.000 |
| `desktop-entry` | 214 | 2 | 212 | `general_only` | 100.00% | 100.00% | 0 | 0.000 |
| `xls` | 203 | 170 | 33 | `general_only` | 75.37% | 70.59% | 0 | 0.000 |
| `msi` | 197 | 166 | 31 | `group_only` | 19.29% | 4.22% | 0 | 0.000 |
| `tar.bz2` | 179 | 3 | 176 | `general_only` | 99.44% | 66.67% | 0 | 0.000 |
| `pptx` | 170 | 3 | 167 | `no_policy` | 98.24% | 0.00% | 0 | 0.000 |
| `xlsx` | 160 | 85 | 75 | `no_policy` | 46.88% | 0.00% | 0 | 0.000 |
| `zig` | 136 | 0 | 136 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `chrome-manifest` | 86 | 28 | 58 | `no_policy` | 67.44% | 0.00% | 0 | 0.000 |
| `applescript` | 73 | 22 | 51 | `no_policy` | 69.86% | 0.00% | 0 | 0.000 |
| `tar.zst` | 45 | 0 | 45 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `vsix_manifest` | 45 | 0 | 45 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `crx` | 43 | 31 | 12 | `no_policy` | 27.91% | 0.00% | 0 | 0.000 |
| `ooxml` | 23 | 3 | 20 | `no_policy` | 86.96% | 0.00% | 0 | 0.000 |
| `pkg` | 11 | 1 | 10 | `no_policy` | 90.91% | 0.00% | 0 | 0.000 |
| `ppt` | 9 | 0 | 9 | `no_policy` | 100.00% | - | 0 | 0.000 |
| `cab` | 4 | 3 | 1 | `general_only` | 100.00% | 100.00% | 0 | 0.000 |
| `msg` | 2 | 0 | 2 | `no_policy` | 100.00% | - | 0 | 0.000 |

## Sample Store

The training corpus is published at `r2:azoth-training`. See [TRAINING.md](TRAINING.md).
