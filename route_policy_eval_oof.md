# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 836005 (307476 malware, 528529 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 163397 | 19933 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 50.65% | 0 | 51.78% | 1.14% | filegroups/native: 54.47% | 0.999 | 0.999 |
| pdf | 22499 | 2922 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 6.31% | 0 | 6.50% | 0.19% | filetypes/pdf: 10.39% | 0.999 | 0.996 |
| elf | 22208 | 20659 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 92.00% | 0 | 95.93% | 3.93% | filetypes/elf: 96.24% | 1.000 | 0.999 |
| batch | 22076 | 557 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 97.40% | 0 | 97.46% | 0.06% | filegroups/scripts: 97.82% | 1.000 | 1.000 |
| javascript | 14329 | 73436 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 65.54% | 0 | 59.50% | -6.04% | filetypes/javascript: 66.71% | 0.973 | 0.970 |
| zip | 12583 | 1426 | `general,filetypes/zip` | general: 36.04% | 0 | 31.45% | -4.59% | general: 36.50% | 0.987 | 0.984 |
| xlsx | 7384 | 198 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.12% | 0 | 36.08% | 4.96% | general: 45.91% | 0.999 | 0.999 |
| xls | 4625 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 92.95% | 0 | 93.19% | 0.24% | filetypes/xls: 93.73% | 0.999 | 0.999 |
| doc | 3921 | 7 | `general,filegroups/documents` | filegroups/documents: 80.77% | 0 | 38.51% | -42.26% | filegroups/documents: 99.67% | — | 1.000 |
| kotlin | 3896 | 6375 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 49.10% | 0 | 51.39% | 2.28% | filetypes/kotlin: 54.44% | 0.980 | 0.974 |
| tar | 2760 | 2815 | `general,filetypes/tar` | filetypes/tar: 88.08% | 0 | 88.19% | 0.11% | filetypes/tar: 90.72% | 0.999 | 0.995 |
| rar | 2543 | 0 | `general` | general: 100.00% | 0 | 13.17% | -86.83% | general: 100.00% | — | — |
| python | 2362 | 22592 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 47.54% | 0 | 48.01% | 0.47% | general: 61.94% | 0.969 | 0.963 |
| package.json | 2231 | 2579 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 89.87% | 0 | 90.45% | 0.58% | general: 94.17% | 0.999 | 0.999 |
| unknown | 2098 | 6142 | `general` | general: 1.76% | 0 | 0.00% | -1.76% | general: 21.31% | — | 0.817 |
| shell | 1868 | 7336 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 83.62% | 0 | 81.64% | -1.98% | filetypes/shell: 84.10% | 0.990 | 0.985 |
| c | 1781 | 83259 | `general,filegroups/source,filetypes/c` | general: 7.86% | 0 | 3.93% | -3.93% | filegroups/source: 11.96% | 0.061 | 0.197 |
| vbs | 1428 | 426 | `general,filetypes/vbs` | filetypes/vbs: 38.24% | 0 | 42.72% | 4.48% | filetypes/vbs: 52.31% | 0.997 | 0.996 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 6.39% | -81.37% | general: 97.04% | — | 1.000 |
| pkg-info | 1277 | 225 | `general,filetypes/pkg-info` | general: 78.07% | 0 | 87.00% | 8.93% | filetypes/pkg-info: 99.92% | 1.000 | 1.000 |
| go | 1183 | 15122 | `general,filegroups/source,filetypes/go` | filetypes/go: 2.03% | 0 | 2.20% | 0.17% | filetypes/go: 2.20% | 0.459 | 0.624 |
| ole | 791 | 778 | `general,filegroups/documents,filetypes/ole` | general: 89.25% | 0 | 82.17% | -7.08% | filegroups/documents: 93.68% | 0.997 | 0.997 |
| rtf | 784 | 53 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.60% | 0 | 98.47% | -0.13% | general: 98.72% | 1.000 | 1.000 |
| 7z | 776 | 14 | `general` | general: 75.52% | 0 | 16.24% | -59.28% | general: 82.47% | — | 0.999 |
| png | 682 | 21152 | `general,filegroups/media,filetypes/png` | general: 0.00% | 0 | 0.00% | 0.00% | general: 3.96% | 0.053 | 0.139 |
| powershell | 633 | 306 | `general,filegroups/scripts,filetypes/powershell` | general: 44.23% | 0 | 52.76% | 8.53% | filegroups/scripts: 67.93% | 0.988 | 0.990 |
| php | 566 | 18259 | `general,filegroups/scripts,filetypes/php` | general: 52.12% | 0 | 47.88% | -4.24% | filetypes/php: 61.31% | 0.905 | 0.913 |
| docx | 562 | 58 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 88.61% | 0 | 82.92% | -5.69% | filetypes/docx: 89.15% | 0.996 | 0.991 |
| msi | 552 | 11 | `general` | general: 61.78% | 0 | 0.00% | -61.78% | general: 62.86% | — | 0.998 |
| lnk | 537 | 131 | `general,filetypes/lnk` | filetypes/lnk: 83.61% | 0 | 82.68% | -0.93% | filetypes/lnk: 83.99% | 0.992 | 0.990 |
| gz | 524 | 8634 | `general` | general: 23.09% | 0 | 0.00% | -23.09% | general: 23.66% | — | 0.686 |
| jar | 443 | 451 | `general,filetypes/jar` | filetypes/jar: 70.65% | 0 | 70.65% | 0.00% | filetypes/jar: 72.46% | 0.989 | 0.986 |
| xml | 392 | 25662 | `general,filegroups/config,filetypes/xml` | general: 2.55% | 0 | 2.55% | 0.00% | general: 2.81% | 0.070 | 0.210 |
| python-bytecode | 354 | 10701 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 98.02% | 0 | 92.09% | -5.93% | filetypes/python-bytecode: 98.02% | 0.986 | 0.986 |
| macho | 334 | 1486 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 82.04% | 0 | 80.24% | -1.80% | filetypes/macho: 92.22% | 0.995 | 0.961 |
| csharp | 242 | 8141 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 31.40% | 0 | 24.38% | -7.02% | filegroups/source: 31.40% | 0.604 | 0.572 |
| java_class | 221 | 88038 | `general,filegroups/portable,filetypes/java_class` | general: 60.18% | 0 | 17.65% | -42.53% | general: 67.42% | 0.612 | 0.671 |
| text | 196 | 10485 | `general,filetypes/text` | general: 12.76% | 0 | 10.71% | -2.04% | general: 13.27% | 0.150 | 0.181 |
| rust | 166 | 10730 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 3.61% | 0 | 2.41% | -1.20% | filetypes/rust: 4.82% | 0.111 | 0.098 |
| jpeg | 151 | 3733 | `general,filegroups/media,filetypes/jpeg` | general: 11.92% | 0 | 10.60% | -1.32% | general: 11.92% | 0.165 | 0.231 |
| crx | 119 | 10 | `general,filetypes/crx` | filetypes/crx: 96.64% | 0 | 36.97% | -59.66% | filetypes/crx: 96.64% | 0.999 | 0.980 |
| json | 100 | 3761 | `general,filegroups/config,filetypes/json` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.062 | 0.051 |
| cab | 96 | 11 | `general` | general: 13.54% | 0 | 0.00% | -13.54% | general: 31.25% | — | 0.968 |
| pptx | 72 | 21 | `general,filegroups/documents,filetypes/pptx` | filegroups/documents: 9.72% | 0 | 22.22% | 12.50% | general: 44.44% | 0.786 | 0.799 |
| makefile | 67 | 3260 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.107 | 0.074 |
| plist | 66 | 1586 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.55% | 0 | 4.55% | 0.00% | general: 6.06% | 0.108 | 0.126 |
| deb | 45 | 874 | `general,filetypes/deb` | general: 11.11% | — | — | — | general: 11.11% | 0.086 | 0.164 |
| chm | 38 | 6 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| perl | 36 | 4912 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 77.78% | 0 | 69.44% | -8.33% | filetypes/perl: 94.44% | 0.959 | 0.955 |
| data | 32 | 1337 | `general` | general: 34.38% | 0 | 0.00% | -34.38% | general: 34.38% | — | 0.578 |
| asar | 17 | 1 | `general` | general: 88.24% | 0 | 0.00% | -88.24% | general: 100.00% | — | 0.993 |
| groovy | 15 | 791 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.096 | 0.095 |
| html | 14 | 1371 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2321 | `general,filegroups/scripts,filetypes/lua` | general: 76.92% | 0 | 30.77% | -46.15% | general: 76.92% | 0.769 | 0.782 |
| ruby | 12 | 3020 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 66.67% | 0 | 50.00% | -16.67% | filegroups/scripts: 66.67% | 0.768 | 0.768 |
| java | 10 | 5214 | `general,filegroups/source,filetypes/java` | filegroups/source: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | 0.346 | 0.587 |
| xz | 10 | 3943 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 20.00% | — | 0.394 |
| package-lock.json | 9 | 79 | `general,filetypes/package-lock.json` | general: 0.00% | — | — | — | general: 0.00% | 0.199 | 0.192 |
| markdown | 8 | 2355 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| chrome-manifest | 7 | 55 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 28.57% | 0 | 28.57% | 0.00% | filetypes/chrome-manifest: 71.43% | 0.754 | 0.693 |
| clojure | 7 | 612 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.618 | 0.618 |
| dockerfile | 6 | 230 | `general,filetypes/dockerfile` | general: 0.00% | — | — | — | general: 0.00% | 0.415 | 0.157 |
| objc | 5 | 2770 | `general` | general: 60.00% | 0 | 0.00% | -60.00% | general: 60.00% | — | 0.703 |
| zig | 5 | 21 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.609 |
| cargo.toml | 4 | 50 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.218 |
| swift | 4 | 3872 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.100 |
| applescript | 3 | 36 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 100.00% | — | 0.917 |
| bz2 | 3 | 1429 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| whl | 3 | 77 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.065 |
| pyproject.toml | 2 | 6 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 0.833 |
| desktop-entry | 1 | 90 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| github-actions | 1 | 893 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| ooxml | 1 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.143 |
| pkg | 1 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| systemd | 1 | 173 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.008 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 6 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.24% | 100.00% | -99.76% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| 7z | `general` | 0 | 1.29% | 75.52% | -74.23% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 12.43% | 100.00% | -87.57% |
| zst | `general` | 0 | 6.16% | 87.76% | -81.61% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| 7z | `general` | 0 | 14.82% | 75.52% | -60.70% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 12.43% | 100.00% | -87.57% |
| zst | `general` | 0 | 6.16% | 87.76% | -81.61% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| 7z | `general` | 0 | 14.82% | 75.52% | -60.70% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 13.17% | 100.00% | -86.83% |
| zst | `general` | 0 | 6.39% | 87.76% | -81.37% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 16.24% | 75.52% | -59.28% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 13.17% | 100.00% | -86.83% |
| zst | `general` | 0 | 6.39% | 87.76% | -81.37% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 16.24% | 75.52% | -59.28% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 13.17% | 100.00% | -86.83% |
| zst | `general` | 0 | 6.39% | 87.76% | -81.37% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 16.24% | 75.52% | -59.28% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 20.68% | 100.00% | -79.32% |
| zst | `general` | 0 | 10.60% | 87.76% | -77.16% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 23.20% | 75.52% | -52.32% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 20.68% | 100.00% | -79.32% |
| zst | `general` | 0 | 10.60% | 87.76% | -77.16% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.00% | 61.78% | -61.78% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 23.20% | 75.52% | -52.32% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 0.00% | 13.54% | -13.54% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 23.00% | 100.00% | -77.00% |
| zst | `general` | 0 | 13.41% | 87.76% | -74.36% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `general` | 0 | 0.18% | 61.78% | -61.59% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| 7z | `general` | 0 | 24.74% | 75.52% | -50.77% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.51% | 80.77% | -42.26% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 0.00% | 23.09% | -23.09% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 1.04% | 13.54% | -12.50% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.54% | 100.00% | -66.46% |
| msi | `general` | 0 | 1.63% | 61.78% | -60.14% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 40.37% | 87.76% | -47.39% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.59% | 80.77% | -42.18% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| 7z | `general` | 0 | 35.57% | 75.52% | -39.95% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 1.72% | 23.09% | -21.37% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 1.04% | 13.54% | -12.50% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 35.23% | 100.00% | -64.77% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| msi | `general` | 0 | 2.90% | 61.78% | -58.88% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.59% | 80.77% | -42.18% |
| zst | `general` | 0 | 45.75% | 87.76% | -42.01% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| 7z | `general` | 0 | 37.76% | 75.52% | -37.76% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| gz | `general` | 0 | 1.91% | 23.09% | -21.18% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 1.04% | 13.54% | -12.50% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.85% | 100.00% | -63.15% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| msi | `general` | 0 | 3.80% | 61.78% | -57.97% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 38.64% | 80.77% | -42.13% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| zst | `general` | 0 | 52.77% | 87.76% | -35.00% |
| 7z | `general` | 0 | 40.85% | 75.52% | -34.66% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| xz | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 4.01% | 23.09% | -19.08% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 1.04% | 13.54% | -12.50% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 0.00% | 88.24% | -88.24% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.13% | 100.00% | -60.87% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| msi | `general` | 0 | 11.05% | 61.78% | -50.72% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| doc | `general,filegroups/documents` | 0 | 39.00% | 80.77% | -41.78% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| 7z | `general` | 0 | 46.91% | 75.52% | -28.61% |
| zst | `general` | 0 | 61.81% | 87.76% | -25.95% |
| gz | `general` | 0 | 5.92% | 23.09% | -17.18% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 2.08% | 13.54% | -11.46% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 0.00% | 88.24% | -88.24% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 40.27% | 100.00% | -59.73% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| java_class | `general` | 0 | 17.65% | 60.18% | -42.53% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| msi | `general` | 0 | 22.64% | 61.78% | -39.13% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| 7z | `general` | 0 | 53.35% | 75.52% | -22.16% |
| zst | `general` | 0 | 68.90% | 87.76% | -18.86% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| gz | `general` | 0 | 10.50% | 23.09% | -12.60% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| cab | `general` | 0 | 5.21% | 13.54% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| doc | `general,filegroups/documents` | 0 | 76.43% | 80.77% | -4.34% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.93% | 7.86% | -3.93% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 100.00% | -94.74% |
| asar | `general` | 0 | 11.76% | 88.24% | -76.47% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| rar | `general` | 0 | 41.17% | 100.00% | -58.83% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| msi | `general` | 0 | 37.86% | 61.78% | -23.91% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| 7z | `general` | 0 | 59.79% | 75.52% | -15.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 57.47% | 67.42% | -9.95% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| zst | `general` | 0 | 81.22% | 87.76% | -6.55% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 59.50% | 65.54% | -6.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| gz | `general` | 0 | 17.56% | 23.09% | -5.53% |
| cab | `general` | 0 | 8.33% | 13.54% | -5.21% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| doc | `general,filegroups/documents` | 0 | 78.30% | 80.77% | -2.47% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.63% | 7.86% | -1.24% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 100.00% | -94.74% |
| asar | `general` | 0 | 11.76% | 88.24% | -76.47% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| rar | `general` | 0 | 41.60% | 100.00% | -58.40% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| msi | `general` | 0 | 40.22% | 61.78% | -21.56% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| 7z | `general` | 0 | 62.50% | 75.52% | -13.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 57.47% | 67.42% | -9.95% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| gz | `general` | 0 | 18.13% | 23.09% | -4.96% |
| zst | `general` | 0 | 83.16% | 87.76% | -4.60% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| doc | `general,filegroups/documents` | 0 | 78.98% | 80.77% | -1.79% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.63% | 7.86% | -1.24% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.54% | 65.54% | -1.00% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.55% | 2.55% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 100.00% | -94.74% |
| asar | `general` | 0 | 11.76% | 88.24% | -76.47% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 36.97% | 96.64% | -59.66% |
| rar | `general` | 0 | 42.04% | 100.00% | -57.96% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 30.77% | 76.92% | -46.15% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| data | `general` | 0 | 0.00% | 34.38% | -34.38% |
| msi | `general` | 0 | 40.94% | 61.78% | -20.83% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 50.00% | 66.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| 7z | `general` | 0 | 63.79% | 75.52% | -11.73% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 57.47% | 67.42% | -9.95% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 77.78% | -8.33% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.17% | 89.25% | -7.08% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.38% | 31.40% | -7.02% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.09% | 98.02% | -5.93% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 82.92% | 88.61% | -5.69% |
| zip | `general,filetypes/zip` | 0 | 31.45% | 36.04% | -4.59% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.88% | 52.12% | -4.24% |
| gz | `general` | 0 | 19.27% | 23.09% | -3.82% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| text | `general,filetypes/text` | 0 | 10.71% | 12.76% | -2.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 81.64% | 83.62% | -1.98% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.24% | 82.04% | -1.80% |
| unknown | `general` | 0 | 0.00% | 1.76% | -1.76% |
| doc | `general,filegroups/documents` | 0 | 79.01% | 80.77% | -1.76% |
| jpeg | `general` | 0 | 10.60% | 11.92% | -1.32% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.63% | 7.86% | -1.24% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.61% | -1.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.54% | 65.54% | -1.00% |
| lnk | `general,filetypes/lnk` | 0 | 82.68% | 83.61% | -0.93% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.47% | 98.60% | -0.13% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 28.57% | 28.57% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 70.65% | 70.65% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 4.55% | 4.55% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 97.46% | 97.40% | 0.06% |
| tar | `general,filetypes/tar` | 0 | 88.19% | 88.08% | 0.11% |
| go | `general,filegroups/source,filetypes/go` | 0 | 2.20% | 2.03% | 0.17% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.31% | 0.19% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 93.19% | 92.95% | 0.24% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.01% | 47.54% | 0.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.45% | 89.87% | 0.58% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 3.32% | 2.55% | 0.77% |
| pe | `filegroups/native,filetypes/pe` | 0 | 51.78% | 50.65% | 1.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.39% | 49.10% | 2.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 95.93% | 92.00% | 3.93% |
| vbs | `general,filetypes/vbs` | 0 | 42.72% | 38.24% | 4.48% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 36.08% | 31.12% | 4.96% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.76% | 44.23% | 8.53% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 87.00% | 78.07% | 8.93% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 22.22% | 9.72% | 12.50% |
