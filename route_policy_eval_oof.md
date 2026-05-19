# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 585889 (208185 malware, 377704 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 109970 | 18938 | `general,filetypes/pe` | general: 54.02% | 0 | 32.16% | -21.86% | general: 71.82% | 1.000 | 1.000 |
| pdf | 21777 | 1734 | `general,filegroups/documents,filetypes/pdf` | general: 6.47% | 0 | 6.81% | 0.34% | filetypes/pdf: 7.88% | 0.992 | 0.994 |
| batch | 21095 | 425 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 98.85% | 1 | 98.78% | — | filegroups/scripts: 98.98% | 1.000 | 1.000 |
| javascript | 10488 | 59418 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 68.02% | 0 | 63.83% | -4.19% | filetypes/javascript: 73.60% | 0.982 | 0.979 |
| elf | 8826 | 16927 | `general,filetypes/elf` | filetypes/elf: 93.61% | 0 | 92.06% | -1.55% | filetypes/elf: 94.50% | 1.000 | 1.000 |
| zip | 7095 | 878 | `general` | general: 46.06% | 0 | 38.37% | -7.70% | general: 60.28% | — | 0.987 |
| kotlin | 2829 | 5341 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 52.34% | 0 | 50.80% | -1.54% | filegroups/source: 68.70% | 0.979 | 0.966 |
| tar.gz | 2390 | 1610 | `general` | general: 64.52% | 0 | 47.78% | -16.74% | general: 81.26% | — | 0.995 |
| python | 2271 | 16286 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 53.59% | 0 | 49.19% | -4.40% | filetypes/python: 65.65% | 0.976 | 0.969 |
| xlsx | 2232 | 12 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 90.27% | 0 | 28.58% | -61.69% | general: 91.76% | 0.981 | 0.996 |
| package.json | 2162 | 1361 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 92.59% | 0 | 79.00% | -13.59% | filegroups/config: 99.58% | 1.000 | 1.000 |
| c | 1766 | 66562 | `general,filegroups/source,filetypes/c` | filetypes/c: 11.16% | 0 | 0.57% | -10.60% | filegroups/source: 13.48% | 0.510 | 0.440 |
| unknown | 1342 | 2020 | `general,filetypes/unknown` | general: 0.00% | 1 | 54.55% | — | filetypes/unknown: 58.89% | 0.787 | 0.786 |
| xls | 1297 | 7 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 95.61% | 0 | 91.36% | -4.24% | filegroups/documents: 99.85% | 0.980 | 0.999 |
| doc | 1287 | 3 | `general,filegroups/documents` | filegroups/documents: 99.84% | 0 | 72.18% | -27.66% | general: 100.00% | — | 1.000 |
| zst | 1283 | 2030 | `general` | general: 87.76% | 0 | 84.26% | -3.51% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 114 | `general,filetypes/pkg-info` | filetypes/pkg-info: 98.20% | 0 | 97.02% | -1.18% | filetypes/pkg-info: 98.67% | 1.000 | 1.000 |
| go | 1177 | 11858 | `general,filegroups/source,filetypes/go` | filegroups/source: 1.02% | 0 | 0.68% | -0.34% | filetypes/go: 4.76% | 0.653 | 0.634 |
| shell | 920 | 5682 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 82.01% | 0 | 75.54% | -6.47% | filetypes/shell: 87.53% | 0.985 | 0.976 |
| rar | 759 | 0 | `general` | general: 100.00% | 0 | 67.46% | -32.54% | general: 100.00% | — | — |
| png | 657 | 14338 | `general,filegroups/media,filetypes/png` | filegroups/media: 1.07% | 0 | 0.00% | -1.07% | general: 9.13% | 0.125 | 0.184 |
| 7z | 561 | 14 | `general` | general: 91.44% | 0 | 83.24% | -8.20% | general: 93.94% | — | 0.999 |
| php | 516 | 10809 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 67.25% | 0 | 40.89% | -26.36% | filetypes/php: 72.48% | 0.928 | 0.915 |
| vbs | 445 | 423 | `general,filetypes/vbs` | filetypes/vbs: 36.84% | 0 | 36.63% | -0.21% | filetypes/vbs: 48.51% | 0.982 | 0.980 |
| xml | 288 | 17921 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.11% | 0 | 4.51% | 2.41% | general: 5.21% | 0.125 | 0.138 |
| macho | 258 | 1382 | `general,filetypes/macho` | filetypes/macho: 80.62% | 0 | 71.71% | -8.91% | filetypes/macho: 87.60% | 0.994 | 0.989 |
| lnk | 257 | 127 | `general,filetypes/lnk` | filetypes/lnk: 59.61% | 0 | 45.14% | -14.47% | filetypes/lnk: 69.41% | 0.974 | 0.973 |
| powershell | 240 | 274 | `general,filegroups/scripts,filetypes/powershell` | general: 21.67% | 0 | 23.33% | 1.67% | filetypes/powershell: 69.79% | 0.967 | 0.951 |
| csharp | 234 | 7572 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 29.91% | 0 | 27.35% | -2.56% | filegroups/source: 30.34% | 0.571 | 0.573 |
| python-bytecode | 233 | 3841 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.85% | 0 | 29.61% | -68.24% | filetypes/python-bytecode: 97.85% | 0.993 | 0.993 |
| ole | 221 | 664 | `general,filegroups/documents,filetypes/ole` | general: 90.95% | 0 | 88.69% | -2.26% | filetypes/ole: 96.83% | 0.986 | 0.992 |
| jar | 215 | 236 | `general,filetypes/jar` | filetypes/jar: 58.60% | 0 | 55.35% | -3.26% | general: 66.05% | 0.982 | 0.981 |
| msi | 215 | 8 | `general,filetypes/msi` | filetypes/msi: 92.49% | 0 | 32.09% | -60.40% | filetypes/msi: 99.06% | 0.999 | 0.997 |
| rtf | 214 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.66% | 0 | 95.33% | -2.34% | filetypes/rtf: 98.13% | 1.000 | 0.999 |
| docx | 173 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 53.22% | 0 | 65.32% | 12.10% | filegroups/documents: 85.38% | 0.974 | 0.972 |
| java_class | 173 | 47070 | `general,filegroups/portable,filetypes/java_class` | general: 75.72% | 0 | 34.68% | -41.04% | filegroups/portable: 86.05% | 0.924 | 0.945 |
| gz | 168 | 6384 | `general` | general: 29.76% | 0 | 0.00% | -29.76% | general: 48.21% | — | 0.635 |
| rust | 164 | 9604 | `general,filegroups/source,filetypes/rust` | general: 1.83% | 0 | 1.22% | -0.61% | filegroups/source: 3.66% | 0.105 | 0.068 |
| text | 159 | 7979 | `general,filetypes/text` | general: 12.58% | 0 | 11.95% | -0.63% | general: 15.09% | 0.217 | 0.250 |
| jpeg | 125 | 1319 | `general,filegroups/media,filetypes/jpeg` | general: 13.60% | 0 | 11.20% | -2.40% | filegroups/media: 19.20% | 0.335 | 0.341 |
| tar | 125 | 47 | `general` | general: 88.00% | 0 | 62.40% | -25.60% | general: 89.60% | — | 0.987 |
| plist | 68 | 1544 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.41% | 0 | 1.47% | -2.94% | general: 5.88% | 0.104 | 0.117 |
| data | 58 | 1157 | `general,filetypes/data` | filetypes/data: 77.59% | 0 | 1.72% | -75.86% | filetypes/data: 79.31% | 0.881 | 0.891 |
| perl | 28 | 3956 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 82.14% | 0 | 85.71% | 3.57% | filegroups/scripts: 85.71% | 0.923 | 0.923 |
| cab | 27 | 11 | `general` | general: 44.44% | 0 | 0.00% | -44.44% | general: 100.00% | — | 0.959 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filetypes/pptx: 27.27% | 0 | 4.55% | -22.73% | general: 31.82% | 0.583 | 0.591 |
| makefile | 17 | 2740 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.018 | 0.016 |
| groovy | 15 | 648 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.021 | 0.021 |
| chm | 10 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 737 | `general` | general: 71.43% | 0 | 0.00% | -71.43% | general: 71.43% | — | 0.726 |
| ruby | 7 | 2943 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 100.00% | 0 | 14.29% | -85.71% | general: 100.00% | 0.860 | 0.893 |
| crx | 6 | 5 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.758 |
| html | 6 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| lua | 6 | 1839 | `general,filegroups/scripts` | general: 50.00% | 0 | 0.00% | -50.00% | filegroups/scripts: 66.67% | — | 0.625 |
| xz | 6 | 3448 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 83.33% | — | 0.833 |
| java | 4 | 4192 | `general,filegroups/source` | general: 50.00% | 0 | 0.00% | -50.00% | general: 75.00% | — | 0.690 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 65 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.048 |
| applescript | 2 | 32 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 2 | 1410 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.501 |
| chrome-manifest | 2 | 46 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.643 |
| github-actions | 1 | 703 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.200 |
| objc | 1 | 2308 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 134 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.010 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `` | 0 | 0.00% | 66.67% | -66.67% |
| tar.gz | `` | 0 | 0.00% | 64.52% | -64.52% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `` | 0 | 0.00% | 50.00% | -50.00% |
| zip | `` | 0 | 0.00% | 46.06% | -46.06% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| pe | `general,filetypes/pe` | 0 | 12.48% | 54.02% | -41.54% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 66.80% | 100.00% | -33.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| 7z | `general` | 0 | 69.16% | 91.44% | -22.28% |
| zst | `general` | 0 | 67.19% | 87.76% | -20.58% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 66.80% | 100.00% | -33.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 47.49% | 64.52% | -17.03% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 37.83% | 46.06% | -8.23% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| rar | `general` | 0 | 56.92% | 100.00% | -43.08% |
| shell | `filetypes/shell` | 0 | 40.87% | 82.01% | -41.14% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| zst | `general` | 0 | 48.09% | 87.76% | -39.67% |
| 7z | `general` | 0 | 52.76% | 91.44% | -38.68% |
| tar | `general` | 0 | 50.40% | 88.00% | -37.60% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| tar.gz | `general` | 0 | 41.38% | 64.52% | -23.14% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| zip | `general` | 0 | 31.39% | 46.06% | -14.67% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 68.64% | 100.00% | -31.36% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 70.59% | 91.44% | -20.86% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 39.20% | 46.06% | -6.86% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 91.83% | 93.61% | -1.77% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| pe | `general,filetypes/pe` | 0 | 56.59% | 54.02% | 2.57% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| rar | `general` | 0 | 57.05% | 100.00% | -42.95% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| zst | `general` | 0 | 48.64% | 87.76% | -39.13% |
| shell | `filetypes/shell` | 0 | 43.15% | 82.01% | -38.86% |
| 7z | `general` | 0 | 52.76% | 91.44% | -38.68% |
| tar | `general` | 0 | 52.80% | 88.00% | -35.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| tar.gz | `general` | 0 | 41.38% | 64.52% | -23.14% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| zip | `general` | 0 | 31.57% | 46.06% | -14.49% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| rar | `general` | 0 | 72.33% | 100.00% | -27.67% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 63.20% | 88.00% | -24.80% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 73.44% | 91.44% | -18.00% |
| tar.gz | `general` | 0 | 46.57% | 64.52% | -17.95% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| pe | `general,filetypes/pe` | 3 | 61.75% | 71.82% | -10.07% |
| zst | `general` | 0 | 78.33% | 87.76% | -9.43% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| zip | `general` | 0 | 41.75% | 46.06% | -4.31% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| shell | `filetypes/shell` | 0 | 45.54% | 82.01% | -36.47% |
| rar | `general` | 0 | 65.22% | 100.00% | -34.78% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| 7z | `general` | 0 | 65.95% | 91.44% | -25.49% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| zst | `general` | 0 | 63.52% | 87.76% | -24.24% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| tar.gz | `general` | 0 | 46.19% | 64.52% | -18.33% |
| javascript | `filetypes/javascript` | 0 | 53.35% | 68.02% | -14.67% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| zip | `general` | 0 | 36.04% | 46.06% | -10.02% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| rar | `general` | 0 | 74.70% | 100.00% | -25.30% |
| tar | `general` | 0 | 64.80% | 88.00% | -23.20% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| tar.gz | `general` | 0 | 49.62% | 64.52% | -14.90% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| pe | `general,filetypes/pe` | 3 | 63.21% | 71.82% | -8.61% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| zip | `general` | 0 | 42.58% | 46.06% | -3.48% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 65.22% | 100.00% | -34.78% |
| shell | `filetypes/shell` | 0 | 51.85% | 82.01% | -30.16% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| 7z | `general` | 0 | 65.95% | 91.44% | -25.49% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| tar.gz | `general` | 0 | 46.19% | 64.52% | -18.33% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| zip | `general` | 0 | 36.04% | 46.06% | -10.02% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| rar | `general` | 0 | 76.28% | 100.00% | -23.72% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| tar | `general` | 0 | 66.40% | 88.00% | -21.60% |
| tar.gz | `general` | 0 | 49.83% | 64.52% | -14.69% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 83.90% | 92.59% | -8.69% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| pe | `general,filetypes/pe` | 3 | 64.63% | 71.82% | -7.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| zip | `general` | 0 | 43.66% | 46.06% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| javascript | `filetypes/javascript` | 0 | 66.93% | 68.02% | -1.08% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents` | 0 | 90.95% | 90.95% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 65.22% | 100.00% | -34.78% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| 7z | `general` | 0 | 65.95% | 91.44% | -25.49% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| tar.gz | `general` | 0 | 46.19% | 64.52% | -18.33% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| zip | `general` | 0 | 36.04% | 46.06% | -10.02% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| javascript | `filetypes/javascript` | 0 | 60.69% | 68.02% | -7.33% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.57% | 82.01% | -2.44% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| rar | `general` | 0 | 77.21% | 100.00% | -22.79% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| tar.gz | `general` | 0 | 50.21% | 64.52% | -14.31% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 84.55% | 92.59% | -8.04% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| pe | `general,filetypes/pe` | 3 | 66.15% | 71.82% | -5.67% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| tar | `general` | 0 | 86.40% | 88.00% | -1.60% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| zip | `general` | 0 | 44.71% | 46.06% | -1.35% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 69.05% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents` | 0 | 90.95% | 90.95% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 66.80% | 100.00% | -33.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pe | `general,filetypes/pe` | 0 | 29.19% | 54.02% | -24.83% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 69.16% | 91.44% | -22.28% |
| tar.gz | `general` | 0 | 47.49% | 64.52% | -17.03% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 37.83% | 46.06% | -8.23% |
| javascript | `filetypes/javascript` | 0 | 60.69% | 68.02% | -7.33% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.57% | 82.01% | -2.44% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 0.60% | 29.76% | -29.17% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 78.00% | 100.00% | -22.00% |
| tar | `general` | 0 | 66.40% | 88.00% | -21.60% |
| tar.gz | `general` | 0 | 46.57% | 64.52% | -17.95% |
| 7z | `general` | 0 | 76.47% | 91.44% | -14.97% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| zip | `general` | 0 | 35.60% | 46.06% | -10.46% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| zst | `general` | 0 | 81.76% | 87.76% | -6.00% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| pe | `general,filetypes/pe` | 3 | 67.83% | 71.82% | -3.99% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 9 | 8.58% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 66.80% | 100.00% | -33.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 69.16% | 91.44% | -22.28% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 47.49% | 64.52% | -17.03% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| shell | `filetypes/shell` | 0 | 67.93% | 82.01% | -14.07% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 37.83% | 46.06% | -8.23% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 78.79% | 100.00% | -21.21% |
| tar | `general` | 0 | 68.80% | 88.00% | -19.20% |
| tar.gz | `general` | 0 | 46.57% | 64.52% | -17.95% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| zst | `general` | 0 | 82.77% | 87.76% | -4.99% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 89.14% | 90.95% | -1.81% |
| pe | `general,filetypes/pe` | 3 | 70.12% | 71.82% | -1.70% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 2 | 71.10% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 1 | 48.40% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 66.80% | 100.00% | -33.20% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 47.49% | 64.52% | -17.03% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 37.83% | 46.06% | -8.23% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| cab | `general` | 0 | 3.70% | 44.44% | -40.74% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 79.18% | 100.00% | -20.82% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| tar.gz | `general` | 0 | 53.93% | 64.52% | -10.59% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 83.55% | 87.76% | -4.21% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 89.14% | 90.95% | -1.81% |
| tar | `general` | 0 | 86.40% | 88.00% | -1.60% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 1 | 50.87% | — | — |
| pe | `general,filetypes/pe` | 3 | 71.86% | 71.82% | 0.03% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 67.46% | 100.00% | -32.54% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 47.78% | 64.52% | -16.74% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| zip | `general` | 0 | 38.37% | 46.06% | -7.70% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.83% | 68.02% | -4.19% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| cab | `general` | 0 | 7.41% | 44.44% | -37.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 79.71% | 100.00% | -20.29% |
| tar | `general` | 0 | 71.20% | 88.00% | -16.80% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| 7z | `general` | 0 | 79.32% | 91.44% | -12.12% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| zip | `general` | 0 | 35.86% | 46.06% | -10.20% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 83.71% | 87.76% | -4.05% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 9 | 8.58% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 3 | 72.47% | 71.82% | 0.65% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 67.46% | 100.00% | -32.54% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| 7z | `general` | 0 | 69.88% | 91.44% | -21.57% |
| tar.gz | `general` | 0 | 47.78% | 64.52% | -16.74% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 38.37% | 46.06% | -7.70% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 65.11% | 68.02% | -2.90% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| cab | `general` | 0 | 7.41% | 44.44% | -37.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 79.84% | 100.00% | -20.16% |
| tar | `general` | 0 | 71.20% | 88.00% | -16.80% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| 7z | `general` | 0 | 79.50% | 91.44% | -11.94% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.18% | 87.76% | -3.59% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 9 | 8.58% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 1 | 52.22% | — | — |
| pe | `general,filetypes/pe` | 3 | 73.24% | 71.82% | 1.42% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 67.72% | 100.00% | -32.28% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| zip | `general` | 0 | 38.97% | 46.06% | -7.09% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| tar | `general` | 0 | 86.40% | 88.00% | -1.60% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 29.76% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| cab | `general` | 0 | 7.41% | 44.44% | -37.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 80.76% | 100.00% | -19.24% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| zst | `general` | 0 | 84.80% | 87.76% | -2.96% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 89.14% | 90.95% | -1.81% |
| tar | `general` | 0 | 86.40% | 88.00% | -1.60% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.01% | — | — |
| pdf | `general,filetypes/pdf` | 1 | 7.57% | — | — |
| pe | `general,filetypes/pe` | 7 | 78.93% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 1 | 53.78% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 67.72% | 100.00% | -32.28% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| pe | `general,filetypes/pe` | 0 | 32.16% | 54.02% | -21.86% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| zip | `general` | 0 | 38.97% | 46.06% | -7.09% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.47% | 92.59% | -5.13% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 65.26% | 68.02% | -2.76% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.81% | 6.47% | 0.34% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| cab | `general` | 0 | 14.81% | 44.44% | -29.63% |
| gz | `general` | 0 | 1.19% | 29.76% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 81.03% | 100.00% | -18.97% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| tar | `general` | 0 | 72.80% | 88.00% | -15.20% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| 7z | `general` | 0 | 83.24% | 91.44% | -8.20% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| zst | `general` | 0 | 84.96% | 87.76% | -2.81% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 9 | 8.58% | — | — |
| pe | `general,filetypes/pe` | 7 | 79.09% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| zip | `general` | 1 | 54.22% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 67.72% | 100.00% | -32.28% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| 7z | `general` | 0 | 70.41% | 91.44% | -21.03% |
| zst | `general` | 0 | 68.04% | 87.76% | -19.72% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| zip | `general` | 0 | 35.31% | 46.06% | -10.75% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| pe | `general,filetypes/pe` | 0 | 56.00% | 54.02% | 1.98% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| cab | `general` | 0 | 14.81% | 44.44% | -29.63% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| gz | `general` | 0 | 2.38% | 29.76% | -27.38% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 81.16% | 100.00% | -18.84% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| 7z | `general` | 0 | 80.39% | 91.44% | -11.05% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| tar.gz | `general` | 0 | 61.30% | 64.52% | -3.22% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| zst | `general` | 0 | 85.04% | 87.76% | -2.73% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 89.14% | 90.95% | -1.81% |
| tar | `general` | 0 | 86.40% | 88.00% | -1.60% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filetypes/pdf` | 1 | 7.57% | — | — |
| pe | `general,filetypes/pe` | 6 | 77.49% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 2 | 54.67% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 68.64% | 100.00% | -31.36% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 70.59% | 91.44% | -20.86% |
| zst | `general` | 0 | 68.98% | 87.76% | -18.78% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| zip | `general` | 0 | 35.31% | 46.06% | -10.75% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| elf | `filetypes/elf` | 0 | 91.12% | 93.61% | -2.49% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| pe | `general,filetypes/pe` | 0 | 56.44% | 54.02% | 2.43% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| lua | `general,filegroups/scripts` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| gz | `general` | 0 | 3.57% | 29.76% | -26.19% |
| cab | `general` | 0 | 18.52% | 44.44% | -25.93% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 81.55% | 100.00% | -18.45% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| tar | `general` | 0 | 72.80% | 88.00% | -15.20% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| 7z | `general` | 0 | 80.75% | 91.44% | -10.70% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| zst | `general` | 0 | 85.66% | 87.76% | -2.10% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filetypes/pdf` | 1 | 7.57% | — | — |
| pe | `general,filetypes/pe` | 6 | 78.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 2 | 55.28% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 68.64% | 100.00% | -31.36% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 70.59% | 91.44% | -20.86% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 39.20% | 46.06% | -6.86% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 91.83% | 93.61% | -1.77% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| pe | `general,filetypes/pe` | 0 | 56.55% | 54.02% | 2.53% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| lua | `general,filegroups/scripts` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| gz | `general` | 0 | 3.57% | 29.76% | -26.19% |
| cab | `general` | 0 | 18.52% | 44.44% | -25.93% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 81.69% | 100.00% | -18.31% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| tar | `general` | 0 | 72.80% | 88.00% | -15.20% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 80.93% | 91.44% | -10.52% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filetypes/pdf` | 1 | 7.57% | — | — |
| pe | `general,filetypes/pe` | 14 | 76.16% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 2 | 55.62% | — | — |
| zst | `general` | 0 | 87.76% | 87.76% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| rar | `general` | 0 | 68.64% | 100.00% | -31.36% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| tar | `general` | 0 | 62.40% | 88.00% | -25.60% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 70.59% | 91.44% | -20.86% |
| tar.gz | `general` | 0 | 48.08% | 64.52% | -16.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 39.20% | 46.06% | -6.86% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| zst | `general` | 0 | 84.26% | 87.76% | -3.51% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 91.83% | 93.61% | -1.77% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| pe | `general,filetypes/pe` | 0 | 56.59% | 54.02% | 2.57% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| gz | `general` | 0 | 5.36% | 29.76% | -24.40% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 82.74% | 100.00% | -17.26% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| cab | `general` | 0 | 29.63% | 44.44% | -14.81% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| tar | `general` | 0 | 74.40% | 88.00% | -13.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 81.64% | 91.44% | -9.80% |
| zip | `general` | 0 | 36.60% | 46.06% | -9.46% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 13 | 82.57% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| zst | `general` | 0 | 87.76% | 87.76% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| rar | `general` | 0 | 70.36% | 100.00% | -29.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 63.20% | 88.00% | -24.80% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| 7z | `general` | 0 | 71.66% | 91.44% | -19.79% |
| zst | `general` | 0 | 70.85% | 87.76% | -16.91% |
| tar.gz | `general` | 0 | 48.58% | 64.52% | -15.94% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| zip | `general` | 0 | 35.32% | 46.06% | -10.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 1 | 58.99% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| gz | `general` | 0 | 6.55% | 29.76% | -23.21% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| rar | `general` | 0 | 83.14% | 100.00% | -16.86% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| tar | `general` | 0 | 74.40% | 88.00% | -13.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| cab | `general` | 0 | 33.33% | 44.44% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 81.82% | 91.44% | -9.63% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 38.45% | 46.06% | -7.61% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 17 | 78.32% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| rar | `general` | 0 | 70.36% | 100.00% | -29.64% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 63.20% | 88.00% | -24.80% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| 7z | `general` | 0 | 71.66% | 91.44% | -19.79% |
| zst | `general` | 0 | 70.85% | 87.76% | -16.91% |
| tar.gz | `general` | 0 | 48.58% | 64.52% | -15.94% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| zip | `general` | 0 | 35.32% | 46.06% | -10.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| elf | `filetypes/elf` | 0 | 91.83% | 93.61% | -1.77% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 1 | 59.02% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| ole | `filetypes/ole` | 0 | 61.99% | 90.95% | -28.96% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| gz | `general` | 0 | 7.74% | 29.76% | -22.02% |
| rar | `general` | 0 | 83.14% | 100.00% | -16.86% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general` | 0 | 48.45% | 64.52% | -16.07% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| tar | `general` | 0 | 76.00% | 88.00% | -12.00% |
| cab | `general` | 0 | 33.33% | 44.44% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 82.17% | 91.44% | -9.27% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| zip | `general` | 0 | 38.45% | 46.06% | -7.61% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| zst | `general` | 0 | 86.36% | 87.76% | -1.40% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 13 | 83.61% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| rar | `general` | 0 | 71.94% | 100.00% | -28.06% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 63.20% | 88.00% | -24.80% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| 7z | `general` | 0 | 72.19% | 91.44% | -19.25% |
| tar.gz | `general` | 0 | 46.57% | 64.52% | -17.95% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| zst | `general` | 0 | 73.42% | 87.76% | -14.34% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| pe | `general,filetypes/pe` | 3 | 60.82% | 71.82% | -11.01% |
| zip | `general` | 0 | 35.33% | 46.06% | -10.73% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| gz | `general` | 0 | 7.74% | 29.76% | -22.02% |
| rar | `general` | 0 | 83.27% | 100.00% | -16.73% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general` | 0 | 49.08% | 64.52% | -15.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| tar | `general` | 0 | 76.80% | 88.00% | -11.20% |
| cab | `general` | 0 | 33.33% | 44.44% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 82.17% | 91.44% | -9.27% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| ole | `filegroups/documents` | 0 | 87.78% | 90.95% | -3.17% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| zst | `general` | 0 | 86.52% | 87.76% | -1.25% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filetypes/pe` | 13 | 83.81% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 2 | 56.80% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xz | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents` | 0 | 28.58% | 90.27% | -61.69% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| crx | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 44.44% | -44.44% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| gz | `general` | 0 | 0.00% | 29.76% | -29.76% |
| rar | `general` | 0 | 71.94% | 100.00% | -28.06% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 42.27% | 68.02% | -25.75% |
| tar | `general` | 0 | 63.20% | 88.00% | -24.80% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| elf | `general,filetypes/elf` | 0 | 71.04% | 93.61% | -22.56% |
| 7z | `general` | 0 | 72.19% | 91.44% | -19.25% |
| tar.gz | `general` | 0 | 46.57% | 64.52% | -17.95% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| zst | `general` | 0 | 73.42% | 87.76% | -14.34% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| pe | `general,filetypes/pe` | 3 | 60.85% | 71.82% | -10.98% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.54% | 82.01% | -6.47% |
| zip | `general` | 0 | 41.28% | 46.06% | -4.78% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.19% | 53.59% | -4.40% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 88.69% | 90.95% | -2.26% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 50.80% | 52.34% | -1.54% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.37% | 6.47% | -1.10% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.32% | 98.85% | -0.53% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| ruby | `general,filegroups/scripts` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general,filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| deb | `general` | 0 | 0.00% | 71.43% | -71.43% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 29.61% | 97.85% | -68.24% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.72% | 90.27% | -61.55% |
| msi | `general,filetypes/msi` | 0 | 32.09% | 92.49% | -60.40% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 34.68% | 75.72% | -41.04% |
| crx | `general` | 0 | 16.67% | 50.00% | -33.33% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.84% | -27.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.89% | 67.25% | -26.36% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 4.55% | 27.27% | -22.73% |
| gz | `general` | 0 | 8.33% | 29.76% | -21.43% |
| rar | `general` | 0 | 83.27% | 100.00% | -16.73% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general` | 0 | 49.08% | 64.52% | -15.44% |
| lnk | `general,filetypes/lnk` | 0 | 45.14% | 59.61% | -14.47% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 79.00% | 92.59% | -13.59% |
| tar | `general` | 0 | 76.80% | 88.00% | -11.20% |
| cab | `general` | 0 | 33.33% | 44.44% | -11.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 0.57% | 11.16% | -10.60% |
| 7z | `general` | 0 | 82.35% | 91.44% | -9.09% |
| macho | `general,filetypes/macho` | 0 | 71.71% | 80.62% | -8.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.99% | 68.02% | -6.02% |
| xls | `general,filegroups/documents` | 0 | 91.36% | 95.61% | -4.24% |
| jar | `general,filetypes/jar` | 0 | 55.35% | 58.60% | -3.26% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.47% | 4.41% | -2.94% |
| ole | `filegroups/documents` | 0 | 88.24% | 90.95% | -2.71% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.35% | 29.91% | -2.56% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.20% | 13.60% | -2.40% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 95.33% | 97.66% | -2.34% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.78% | 82.01% | -2.23% |
| elf | `filetypes/elf` | 0 | 92.06% | 93.61% | -1.55% |
| zst | `general` | 0 | 86.52% | 87.76% | -1.25% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 98.20% | -1.18% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 1.07% | -1.07% |
| text | `general` | 0 | 11.95% | 12.58% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| go | `general,filegroups/source,filetypes/go` | 0 | 0.68% | 1.02% | -0.34% |
| vbs | `general,filetypes/vbs` | 0 | 36.63% | 36.84% | -0.21% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 53.50% | 53.59% | -0.09% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 98.78% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 56.45% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filetypes/pdf` | 1 | 7.58% | — | — |
| pe | `general,filetypes/pe` | 13 | 83.94% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `filetypes/unknown` | 1 | 54.55% | — | — |
| zip | `general` | 2 | 56.89% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 23.33% | 21.67% | 1.67% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.51% | 2.11% | 2.41% |
| perl | `general,filetypes/perl` | 0 | 85.71% | 82.14% | 3.57% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 65.32% | 53.22% | 12.10% |
