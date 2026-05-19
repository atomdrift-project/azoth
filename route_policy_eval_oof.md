# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 589899 (212262 malware, 377637 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 112731 | 18891 | `general,filegroups/native,filetypes/pe` | filegroups/native: 66.89% | 3 | 78.71% | -5.10% | filegroups/native: 83.81% | 1.000 | 1.000 |
| pdf | 21777 | 1734 | `general,filegroups/documents,filetypes/pdf` | general: 6.47% | 0 | 5.87% | -0.60% | filetypes/pdf: 7.86% | 0.992 | 0.994 |
| batch | 21095 | 425 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 98.85% | 0 | 98.85% | 0.00% | filegroups/scripts: 98.97% | 1.000 | 1.000 |
| javascript | 10580 | 59415 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 68.25% | 0 | 67.95% | -0.30% | filetypes/javascript: 73.89% | 0.983 | 0.979 |
| elf | 8757 | 16927 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 93.56% | 1 | 94.96% | — | filegroups/native: 96.63% | 1.000 | 1.000 |
| zip | 7378 | 859 | `general` | general: 50.49% | 0 | 41.16% | -9.33% | general: 67.08% | — | 0.991 |
| tar.gz | 3459 | 1667 | `general` | general: 59.99% | 0 | 53.54% | -6.45% | general: 66.49% | — | 0.996 |
| kotlin | 2874 | 5341 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 53.72% | 1 | 60.68% | — | filegroups/source: 69.14% | 0.979 | 0.967 |
| python | 2272 | 16285 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 53.57% | 1 | 63.29% | — | filetypes/python: 66.46% | 0.977 | 0.969 |
| xlsx | 2232 | 12 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 90.28% | 0 | 28.23% | -62.05% | general: 91.76% | 0.981 | 0.996 |
| package.json | 2163 | 1361 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 92.55% | 0 | 92.74% | 0.19% | filegroups/config: 99.58% | 1.000 | 1.000 |
| c | 1766 | 66562 | `general,filegroups/source,filetypes/c` | filetypes/c: 11.16% | 0 | 5.44% | -5.72% | filegroups/source: 13.48% | 0.510 | 0.440 |
| unknown | 1342 | 2020 | `general,filetypes/unknown` | general: 0.00% | 1 | 34.87% | — | filetypes/unknown: 58.94% | 0.788 | 0.788 |
| zst | 1312 | 2034 | `general` | general: 98.93% | 0 | 84.30% | -14.63% | general: 99.92% | — | 1.000 |
| xls | 1297 | 7 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 95.61% | 0 | 95.45% | -0.15% | filegroups/documents: 99.85% | 0.980 | 0.999 |
| doc | 1287 | 3 | `general,filegroups/documents` | filegroups/documents: 99.77% | 0 | 72.18% | -27.58% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 114 | `general,filetypes/pkg-info` | filetypes/pkg-info: 98.20% | 0 | 97.02% | -1.18% | filetypes/pkg-info: 98.67% | 1.000 | 1.000 |
| go | 1177 | 11858 | `general,filegroups/source,filetypes/go` | filegroups/source: 1.02% | 0 | 0.93% | -0.08% | filetypes/go: 4.76% | 0.653 | 0.634 |
| shell | 792 | 5683 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 79.06% | 0 | 80.56% | 1.49% | filetypes/shell: 85.66% | 0.981 | 0.970 |
| rar | 736 | 0 | `general` | general: 100.00% | 0 | 63.86% | -36.14% | general: 100.00% | — | — |
| png | 657 | 14338 | `general,filegroups/media,filetypes/png` | filegroups/media: 1.07% | 0 | 6.85% | 5.78% | general: 9.13% | 0.125 | 0.184 |
| 7z | 563 | 12 | `general` | general: 87.74% | 0 | 83.13% | -4.62% | general: 93.25% | — | 0.999 |
| php | 508 | 10808 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 66.73% | 0 | 50.20% | -16.54% | filetypes/php: 72.05% | 0.926 | 0.913 |
| vbs | 445 | 423 | `general,filetypes/vbs` | filetypes/vbs: 36.73% | 0 | 27.19% | -9.54% | filetypes/vbs: 48.98% | 0.982 | 0.981 |
| xml | 289 | 17921 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.43% | 0 | 2.42% | -0.01% | general: 5.54% | 0.131 | 0.146 |
| macho | 258 | 1382 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 80.62% | 0 | 81.40% | 0.78% | filetypes/macho: 87.60% | 0.994 | 0.984 |
| lnk | 257 | 127 | `general,filetypes/lnk` | filetypes/lnk: 59.77% | 0 | 46.69% | -13.07% | filetypes/lnk: 69.53% | 0.974 | 0.973 |
| powershell | 241 | 274 | `general,filegroups/scripts,filetypes/powershell` | general: 21.99% | 0 | 24.90% | 2.90% | filetypes/powershell: 70.00% | 0.967 | 0.953 |
| csharp | 234 | 7572 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 29.91% | 0 | 18.80% | -11.11% | filegroups/source: 30.34% | 0.571 | 0.573 |
| python-bytecode | 233 | 3841 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.85% | 0 | 29.61% | -68.24% | filetypes/python-bytecode: 97.85% | 0.993 | 0.993 |
| ole | 229 | 664 | `general,filegroups/documents,filetypes/ole` | general: 91.27% | 0 | 90.83% | -0.44% | filetypes/ole: 96.94% | 0.986 | 0.993 |
| msi | 221 | 13 | `general,filetypes/msi` | filetypes/msi: 95.02% | 0 | 70.59% | -24.43% | filetypes/msi: 99.10% | 0.999 | 0.992 |
| rtf | 214 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.66% | 0 | 97.66% | 0.00% | filetypes/rtf: 98.13% | 1.000 | 0.999 |
| jar | 191 | 245 | `general,filetypes/jar` | filetypes/jar: 56.02% | 0 | 54.97% | -1.05% | filetypes/jar: 68.59% | 0.976 | 0.975 |
| docx | 173 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 52.60% | 0 | 69.94% | 17.34% | filegroups/documents: 85.55% | 0.975 | 0.973 |
| gz | 173 | 6353 | `general` | general: 30.64% | 0 | 0.00% | -30.64% | general: 46.24% | — | 0.667 |
| java_class | 173 | 47070 | `general,filegroups/portable,filetypes/java_class` | general: 75.72% | 0 | 32.37% | -43.35% | filegroups/portable: 86.05% | 0.924 | 0.945 |
| rust | 164 | 9604 | `general,filegroups/source,filetypes/rust` | general: 1.83% | 0 | 1.22% | -0.61% | filegroups/source: 3.66% | 0.105 | 0.068 |
| text | 159 | 7979 | `general,filetypes/text` | general: 11.95% | 0 | 11.32% | -0.63% | general: 14.47% | 0.208 | 0.245 |
| tar | 150 | 49 | `general` | general: 93.33% | 0 | 76.00% | -17.33% | general: 95.33% | — | 0.994 |
| jpeg | 125 | 1319 | `general,filegroups/media,filetypes/jpeg` | general: 13.60% | 0 | 11.20% | -2.40% | filegroups/media: 19.20% | 0.335 | 0.341 |
| plist | 68 | 1544 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.41% | 0 | 1.47% | -2.94% | general: 5.88% | 0.104 | 0.117 |
| data | 58 | 1157 | `general,filetypes/data` | filetypes/data: 77.59% | 0 | 77.59% | 0.00% | filetypes/data: 79.31% | 0.881 | 0.891 |
| cab | 29 | 12 | `general` | general: 58.62% | 0 | 0.00% | -58.62% | general: 100.00% | — | 0.967 |
| perl | 27 | 3957 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 85.19% | 0 | 85.19% | 0.00% | filegroups/scripts: 85.19% | 0.921 | 0.921 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filetypes/pptx: 27.27% | 0 | 27.27% | 0.00% | general: 31.82% | 0.583 | 0.591 |
| makefile | 17 | 2740 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.018 | 0.016 |
| groovy | 15 | 648 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.021 | 0.021 |
| chm | 9 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| crx | 7 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 707 | `general` | general: 71.43% | 0 | 0.00% | -71.43% | general: 71.43% | — | 0.727 |
| ruby | 7 | 2943 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 100.00% | 0 | 42.86% | -57.14% | general: 100.00% | 0.860 | 0.893 |
| html | 6 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | — | 1.000 |
| lua | 6 | 1839 | `general,filegroups/scripts` | general: 50.00% | 0 | 0.00% | -50.00% | filegroups/scripts: 66.67% | — | 0.625 |
| java | 4 | 4192 | `general,filegroups/source` | general: 50.00% | 0 | 0.00% | -50.00% | general: 75.00% | — | 0.690 |
| xz | 4 | 3476 | `general` | general: 25.00% | 0 | 0.00% | -25.00% | general: 50.00% | — | 0.408 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 65 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.048 |
| applescript | 2 | 32 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 2 | 1405 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.501 |
| chrome-manifest | 2 | 46 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.643 |
| github-actions | 1 | 703 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.200 |
| objc | 1 | 2308 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 134 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.010 |
| tar.bz2 | 1 | 21 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| tar.gz | `` | 0 | 0.00% | 59.99% | -59.99% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| zip | `` | 0 | 0.00% | 50.49% | -50.49% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 63.04% | 100.00% | -36.96% |
| zst | `general` | 0 | 66.01% | 98.93% | -32.93% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 66.25% | 87.74% | -21.49% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 67.39% | 66.89% | 0.50% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 57.94% | 97.85% | -39.91% |
| rar | `general` | 0 | 63.04% | 100.00% | -36.96% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| text | `general,filetypes/text` | 0 | 0.63% | 11.95% | -11.32% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| zip | `general` | 0 | 40.39% | 50.49% | -10.10% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 53.14% | 59.99% | -6.85% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.81% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| rar | `general` | 0 | 43.21% | 100.00% | -56.79% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| 7z | `general` | 0 | 52.40% | 87.74% | -35.35% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| tar | `general` | 0 | 66.00% | 93.33% | -27.33% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| tar.gz | `general` | 0 | 44.35% | 59.99% | -15.64% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| zip | `general` | 0 | 36.51% | 50.49% | -13.97% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 70.93% | 80.62% | -9.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 67.39% | 66.89% | 0.50% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 66.03% | 100.00% | -33.97% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 68.92% | 87.74% | -18.83% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 43.20% | 50.49% | -7.29% |
| tar.gz | `general` | 0 | 54.24% | 59.99% | -5.75% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 82.52% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| rar | `general` | 0 | 44.16% | 100.00% | -55.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| 7z | `general` | 0 | 52.58% | 87.74% | -35.17% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| tar | `general` | 0 | 67.33% | 93.33% | -26.00% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| zip | `general` | 0 | 31.53% | 50.49% | -18.96% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| tar.gz | `general` | 0 | 44.67% | 59.99% | -15.32% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.32% | 80.62% | -9.30% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| gz | `general` | 0 | 0.58% | 30.64% | -30.06% |
| rar | `general` | 0 | 69.97% | 100.00% | -30.03% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| zst | `general` | 0 | 77.52% | 98.93% | -21.42% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| 7z | `general` | 0 | 73.71% | 87.74% | -14.03% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 52.12% | 59.99% | -7.86% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| zip | `general` | 0 | 46.22% | 50.49% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 9 | 84.07% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 59.78% | 100.00% | -40.22% |
| shell | `filetypes/shell` | 0 | 46.21% | 79.06% | -32.85% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 64.12% | 87.74% | -23.62% |
| tar | `general` | 0 | 75.33% | 93.33% | -18.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| zip | `general` | 0 | 38.03% | 50.49% | -12.46% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| tar.gz | `general` | 0 | 51.63% | 59.99% | -8.36% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| cab | `general` | 0 | 6.90% | 58.62% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| gz | `general` | 0 | 1.16% | 30.64% | -29.48% |
| rar | `general` | 0 | 71.33% | 100.00% | -28.67% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| tar | `general` | 0 | 77.33% | 93.33% | -16.00% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| zip | `general` | 0 | 47.02% | 50.49% | -3.47% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| tar.gz | `general` | 0 | 57.56% | 59.99% | -2.43% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 4 | 75.35% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 84.48% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 59.78% | 100.00% | -40.22% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| shell | `filetypes/shell` | 0 | 51.14% | 79.06% | -27.92% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 64.12% | 87.74% | -23.62% |
| tar | `general` | 0 | 75.33% | 93.33% | -18.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| zip | `general` | 0 | 38.03% | 50.49% | -12.46% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 51.63% | 59.99% | -8.36% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| cab | `general` | 0 | 6.90% | 58.62% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 72.15% | 100.00% | -27.85% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 78.97% | 97.85% | -18.88% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| zip | `general` | 0 | 47.98% | 50.49% | -2.51% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| tar.gz | `general` | 0 | 58.75% | 59.99% | -1.24% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 33.53% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 5 | 76.47% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 87.33% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 59.78% | 100.00% | -40.22% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 64.12% | 87.74% | -23.62% |
| tar | `general` | 0 | 75.33% | 93.33% | -18.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| shell | `filetypes/shell` | 0 | 62.63% | 79.06% | -16.43% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| zip | `general` | 0 | 38.03% | 50.49% | -12.46% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 51.63% | 59.99% | -8.36% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| javascript | `filetypes/javascript` | 0 | 67.47% | 68.25% | -0.78% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 73.23% | 100.00% | -26.77% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 78.97% | 97.85% | -18.88% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| zip | `general` | 0 | 49.15% | 50.49% | -1.34% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| tar.gz | `general` | 0 | 59.64% | 59.99% | -0.35% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| cab | `general` | 1 | 58.62% | — | — |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 33.53% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 76.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.80% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 87.59% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filetypes/python` | 2 | 65.05% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 63.04% | 100.00% | -36.96% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 66.25% | 87.74% | -21.49% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| shell | `filetypes/shell` | 0 | 68.18% | 79.06% | -10.88% |
| zip | `general` | 0 | 40.39% | 50.49% | -10.10% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 53.14% | 59.99% | -6.85% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| javascript | `filetypes/javascript` | 0 | 67.47% | 68.25% | -0.78% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.81% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 10.34% | 58.62% | -48.28% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| gz | `general` | 0 | 1.16% | 30.64% | -29.48% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 73.64% | 100.00% | -26.36% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 78.97% | 97.85% | -18.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| tar | `general` | 0 | 78.67% | 93.33% | -14.67% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| msi | `general,filetypes/msi` | 0 | 91.86% | 95.02% | -3.17% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| zip | `general` | 0 | 49.85% | 50.49% | -0.64% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.80% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 91.15% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.gz | `general` | 1 | 60.28% | — | — |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| html | `general,filegroups/documents` | 0 | 50.00% | 100.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 57.94% | 97.85% | -39.91% |
| rar | `general` | 0 | 63.04% | 100.00% | -36.96% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| zip | `general` | 0 | 40.39% | 50.49% | -10.10% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 53.14% | 59.99% | -6.85% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.81% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 10.34% | 58.62% | -48.28% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| gz | `general` | 0 | 1.73% | 30.64% | -28.90% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 74.59% | 100.00% | -25.41% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 78.97% | 97.85% | -18.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 82.62% | 98.93% | -16.31% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| 7z | `general` | 0 | 78.33% | 87.74% | -9.41% |
| tar.gz | `general` | 0 | 52.12% | 59.99% | -7.86% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.80% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 91.36% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| zip | `general` | 1 | 52.34% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 57.94% | 97.85% | -39.91% |
| rar | `general` | 0 | 63.04% | 100.00% | -36.96% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| text | `general,filetypes/text` | 0 | 0.63% | 11.95% | -11.32% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| zip | `general` | 0 | 40.39% | 50.49% | -10.10% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| tar.gz | `general` | 0 | 53.14% | 59.99% | -6.85% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.81% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 13.79% | 58.62% | -44.83% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| gz | `general` | 0 | 1.73% | 30.64% | -28.90% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 75.27% | 100.00% | -24.73% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 83.38% | 98.93% | -15.55% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| 7z | `general` | 0 | 79.22% | 87.74% | -8.53% |
| tar.gz | `general` | 0 | 52.12% | 59.99% | -7.86% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 91.52% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| zip | `general` | 1 | 53.92% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.63% | 6.47% | 0.16% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 63.86% | 100.00% | -36.14% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 41.16% | 50.49% | -9.33% |
| tar.gz | `general` | 0 | 53.54% | 59.99% | -6.45% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 76.36% | 100.00% | -23.64% |
| zst | `general` | 0 | 84.60% | 98.93% | -14.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.84% | 97.85% | -12.02% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| cab | `general` | 1 | 58.62% | — | — |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 5 | 96.61% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 33.53% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 58.64% | — | — |
| javascript | `filetypes/javascript` | 5 | 76.37% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 62.21% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.57% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 12 | 90.94% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 67.52% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 4 | 79.25% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 71.30% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 64.27% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| zip | `general` | 1 | 54.47% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 57.94% | 97.85% | -39.91% |
| rar | `general` | 0 | 63.86% | 100.00% | -36.14% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 41.16% | 50.49% | -9.33% |
| tar.gz | `general` | 0 | 53.54% | 59.99% | -6.45% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| msi | `general,filetypes/msi` | 0 | 91.86% | 95.02% | -3.17% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| cab | `general` | 0 | 17.24% | 58.62% | -41.38% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| gz | `general` | 0 | 4.05% | 30.64% | -26.59% |
| rar | `general` | 0 | 76.77% | 100.00% | -23.23% |
| zst | `general` | 0 | 83.99% | 98.93% | -14.94% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.84% | 97.85% | -12.02% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 6 | 76.59% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `filegroups/native` | 10 | 91.89% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 65.34% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 55.07% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.47% | 0.03% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 64.95% | 100.00% | -35.05% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 42.56% | 50.49% | -7.93% |
| tar.gz | `general` | 0 | 53.98% | 59.99% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| msi | `general,filetypes/msi` | 0 | 91.86% | 95.02% | -3.17% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| cab | `general` | 0 | 20.69% | 58.62% | -37.93% |
| lua | `general,filegroups/scripts` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| gz | `general` | 0 | 5.20% | 30.64% | -25.43% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| rar | `general` | 0 | 77.72% | 100.00% | -22.28% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.91% | 98.93% | -14.02% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.84% | 97.85% | -12.02% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| 7z | `general` | 0 | 80.11% | 87.74% | -7.64% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 7 | 76.71% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 92.14% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 5 | 67.82% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 56.30% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.47% | 0.03% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 64.95% | 100.00% | -35.05% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 42.56% | 50.49% | -7.93% |
| tar.gz | `general` | 0 | 53.98% | 59.99% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| msi | `general,filetypes/msi` | 0 | 91.86% | 95.02% | -3.17% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.56% | 79.06% | 1.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| lua | `general,filegroups/scripts` | 0 | 16.67% | 50.00% | -33.33% |
| cab | `general` | 0 | 27.59% | 58.62% | -31.03% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| gz | `general` | 0 | 5.78% | 30.64% | -24.86% |
| rar | `general` | 0 | 78.12% | 100.00% | -21.88% |
| zst | `general` | 0 | 84.98% | 98.93% | -13.95% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 7 | 76.83% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 92.16% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 5 | 68.26% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 56.71% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.50% | 6.47% | 0.03% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 64.95% | 100.00% | -35.05% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 42.56% | 50.49% | -7.93% |
| tar.gz | `general` | 0 | 53.98% | 59.99% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 78.71% | 83.81% | -5.10% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 72.64% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| cab | `general` | 0 | 27.59% | 58.62% | -31.03% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| gz | `general` | 0 | 6.36% | 30.64% | -24.28% |
| rar | `general` | 0 | 78.12% | 100.00% | -21.88% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 85.06% | 98.93% | -13.87% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| 7z | `general` | 0 | 80.64% | 87.74% | -7.10% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 8 | 76.88% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 92.31% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 5 | 68.86% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 57.13% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 66.03% | 100.00% | -33.97% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 43.20% | 50.49% | -7.29% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 77.77% | 83.81% | -6.04% |
| tar.gz | `general` | 0 | 54.24% | 59.99% | -5.75% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 67.95% | 68.25% | -0.30% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 1 | 63.29% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| gz | `general` | 0 | 8.67% | 30.64% | -21.97% |
| rar | `general` | 0 | 78.67% | 100.00% | -21.33% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 85.44% | 98.93% | -13.49% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| cab | `general` | 1 | 58.62% | — | — |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 9 | 77.00% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 62.21% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `filegroups/native` | 13 | 93.49% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 75.97% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 6 | 69.96% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 38.65% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 57.62% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 66.03% | 100.00% | -33.97% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| zst | `general` | 0 | 70.58% | 98.93% | -28.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 68.92% | 87.74% | -18.83% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zip | `general` | 0 | 36.60% | 50.49% | -13.89% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 82.41% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| cab | `general` | 0 | 34.48% | 58.62% | -24.14% |
| gz | `general` | 0 | 9.25% | 30.64% | -21.39% |
| rar | `general` | 0 | 78.80% | 100.00% | -21.20% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| 7z | `general` | 0 | 81.17% | 87.74% | -6.57% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 10 | 77.08% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 93.84% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 9 | 78.70% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 70.48% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 57.89% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 66.03% | 100.00% | -33.97% |
| gz | `general` | 0 | 0.00% | 30.64% | -30.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| 7z | `general` | 0 | 68.92% | 87.74% | -18.83% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| zip | `general` | 0 | 43.20% | 50.49% | -7.29% |
| tar.gz | `general` | 0 | 54.24% | 59.99% | -5.75% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 82.52% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 79.48% | 100.00% | -20.52% |
| gz | `general` | 0 | 10.40% | 30.64% | -20.23% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| cab | `general` | 0 | 44.83% | 58.62% | -13.79% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 10 | 77.16% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 94.23% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 81.51% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 71.96% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 58.76% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 68.34% | 100.00% | -31.66% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 77.77% | 83.81% | -6.04% |
| zip | `general` | 0 | 44.71% | 50.49% | -5.77% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| tar.gz | `general` | 0 | 55.10% | 59.99% | -4.89% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 73.13% | 73.89% | -0.76% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filetypes/python` | 1 | 62.85% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 79.62% | 100.00% | -20.38% |
| gz | `general` | 0 | 10.98% | 30.64% | -19.65% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| cab | `general` | 0 | 48.28% | 58.62% | -10.34% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 12 | 77.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 62.32% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 94.44% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 11 | 81.56% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 72.62% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 59.08% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 68.34% | 100.00% | -31.66% |
| gz | `general` | 0 | 0.58% | 30.64% | -30.06% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| zst | `general` | 0 | 72.48% | 98.93% | -26.45% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| 7z | `general` | 0 | 71.05% | 87.74% | -16.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zip | `general` | 0 | 36.64% | 50.49% | -13.85% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.70% | 98.85% | -5.15% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 48.96% | 53.72% | -4.77% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 64.25% | 68.25% | -3.99% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.07% | 93.56% | -0.49% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 83.02% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 54.31% | 53.57% | 0.75% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 79.62% | 100.00% | -20.38% |
| gz | `general` | 0 | 11.56% | 30.64% | -19.08% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| cab | `general` | 0 | 48.28% | 58.62% | -10.34% |
| 7z | `general` | 0 | 82.06% | 87.74% | -5.68% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 96.27% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 13 | 77.61% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 62.32% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 18 | 94.64% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 11 | 81.56% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 72.80% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 59.22% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 64.81% | 97.85% | -33.05% |
| rar | `general` | 0 | 69.29% | 100.00% | -30.71% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 77.77% | 83.81% | -6.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| zip | `general` | 0 | 45.77% | 50.49% | -4.72% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| tar.gz | `general` | 0 | 56.14% | 59.99% | -3.85% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 73.25% | 73.89% | -0.64% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 30.64% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filetypes/python` | 1 | 62.85% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.20% | 93.56% | 0.64% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 79.89% | 100.00% | -20.11% |
| gz | `general` | 0 | 11.56% | 30.64% | -19.08% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| cab | `general` | 0 | 48.28% | 58.62% | -10.34% |
| tar | `general` | 0 | 84.67% | 93.33% | -8.67% |
| 7z | `general` | 0 | 82.24% | 87.74% | -5.51% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.07% | — | — |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 96.35% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 13 | 77.77% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 63.36% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 18 | 94.66% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 12 | 81.82% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 73.11% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 38.43% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 59.31% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.23% | 90.28% | -62.05% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| rar | `general` | 0 | 69.29% | 100.00% | -30.71% |
| gz | `general` | 0 | 0.58% | 30.64% | -30.06% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 70.59% | 95.02% | -24.43% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.20% | 66.73% | -16.54% |
| zst | `general` | 0 | 84.30% | 98.93% | -14.63% |
| lnk | `general,filetypes/lnk` | 0 | 46.69% | 59.77% | -13.07% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| vbs | `general,filetypes/vbs` | 0 | 27.19% | 36.73% | -9.54% |
| c | `general,filegroups/source,filetypes/c` | 0 | 5.44% | 11.16% | -5.72% |
| zip | `general` | 0 | 45.77% | 50.49% | -4.72% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| tar.gz | `general` | 0 | 56.14% | 59.99% | -3.85% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 77.90% | 79.06% | -1.16% |
| jar | `general,filetypes/jar` | 0 | 54.97% | 56.02% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.87% | 6.47% | -0.60% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 73.55% | 73.89% | -0.34% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.85% | 98.85% | 0.00% |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 4 | 80.25% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `filetypes/python` | 1 | 62.85% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 34.87% | — | — |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 92.74% | 92.55% | 0.19% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.20% | 93.56% | 0.64% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 24.90% | 21.99% | 2.90% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 69.94% | 52.60% | 17.34% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 32.37% | 75.72% | -43.35% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.77% | -27.58% |
| rar | `general` | 0 | 79.89% | 100.00% | -20.11% |
| gz | `general` | 0 | 11.56% | 30.64% | -19.08% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 98.93% | -11.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 86.70% | 97.85% | -11.16% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 18.80% | 29.91% | -11.11% |
| cab | `general` | 0 | 48.28% | 58.62% | -10.34% |
| vbs | `general,filetypes/vbs` | 3 | 41.12% | 48.98% | -7.86% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 61.61% | 66.73% | -5.12% |
| 7z | `general` | 0 | 83.13% | 87.74% | -4.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 3 | 65.14% | 69.14% | -4.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.53% | 11.16% | -3.62% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| tar | `general` | 0 | 92.00% | 93.33% | -1.33% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| text | `general,filetypes/text` | 0 | 11.32% | 11.95% | -0.63% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| msi | `general,filetypes/msi` | 0 | 94.57% | 95.02% | -0.45% |
| ole | `general,filetypes/ole` | 0 | 90.83% | 91.27% | -0.44% |
| xls | `general,filegroups/documents` | 0 | 95.45% | 95.61% | -0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.93% | 1.02% | -0.08% |
| xml | `general,filegroups/config` | 0 | 2.42% | 2.43% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.07% | — | — |
| data | `filetypes/data` | 0 | 77.59% | 77.59% | 0.00% |
| docx | `filegroups/documents,filetypes/docx` | 1 | 81.50% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 96.49% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 58.64% | — | — |
| javascript | `filetypes/javascript` | 13 | 77.80% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.69% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.86% | 7.86% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 19 | 94.69% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 85.19% | 85.19% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 53.53% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 27.27% | 27.27% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 12 | 81.82% | — | — |
| rtf | `general,filetypes/rtf` | 0 | 97.66% | 97.66% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 7 | 73.29% | — | — |
| unknown | `filetypes/unknown` | 1 | 54.69% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| zip | `general` | 1 | 59.39% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 59.92% | 59.77% | 0.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 81.40% | 80.62% | 0.78% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.58% | 79.06% | 3.51% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.85% | 1.07% | 5.78% |
