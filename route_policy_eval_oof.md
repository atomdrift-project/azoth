# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 592338 (213033 malware, 379305 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 113023 | 18905 | `general,filegroups/native,filetypes/pe` | filegroups/native: 86.38% | 6 | 94.24% | — | filegroups/native: 90.36% | 1.000 | 1.000 |
| pdf | 21801 | 1734 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 98.37% | 0 | 98.26% | -0.11% | filegroups/documents: 99.14% | 1.000 | 1.000 |
| batch | 21128 | 427 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 99.66% | 0 | 99.53% | -0.14% | filegroups/scripts: 99.86% | 1.000 | 1.000 |
| javascript | 10621 | 59664 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 74.84% | 12 | 93.48% | — | filegroups/scripts: 89.97% | 0.998 | 0.998 |
| elf | 8974 | 17067 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 98.57% | 1 | 98.99% | — | filetypes/elf: 99.21% | 1.000 | 1.000 |
| zip | 7407 | 870 | `general` | general: 46.40% | 0 | 41.02% | -5.39% | general: 68.00% | — | 0.990 |
| tar.gz | 3466 | 1674 | `general` | general: 65.84% | 0 | 60.04% | -5.80% | general: 81.97% | — | 0.996 |
| kotlin | 2890 | 5355 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 97.23% | 0 | 97.13% | -0.10% | filetypes/kotlin: 97.82% | 0.998 | 0.997 |
| python | 2273 | 16342 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 61.59% | 3 | 84.34% | -0.13% | filetypes/python: 84.47% | 0.995 | 0.994 |
| xlsx | 2237 | 12 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 89.58% | 0 | 74.16% | -15.42% | filegroups/documents: 91.69% | 0.981 | 1.000 |
| package.json | 2163 | 1439 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 93.30% | 0 | 93.48% | 0.18% | filetypes/package.json: 99.63% | 1.000 | 1.000 |
| c | 1766 | 66647 | `general,filegroups/source,filetypes/c` | general: 6.51% | 1 | 6.68% | — | general: 11.72% | 0.622 | 0.727 |
| unknown | 1348 | 2020 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 31.60% | — | 0.772 |
| zst | 1312 | 2034 | `general` | general: 99.24% | 0 | 87.50% | -11.74% | general: 100.00% | — | 1.000 |
| xls | 1297 | 7 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 99.54% | 0 | 99.23% | -0.31% | filegroups/documents: 99.85% | 0.980 | 1.000 |
| doc | 1287 | 3 | `general,filegroups/documents` | filegroups/documents: 99.61% | 0 | 98.76% | -0.85% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 114 | `general,filetypes/pkg-info` | filetypes/pkg-info: 99.84% | 0 | 99.69% | -0.16% | filetypes/pkg-info: 100.00% | 1.000 | 1.000 |
| go | 1177 | 11867 | `general,filegroups/source,filetypes/go` | filetypes/go: 9.09% | 1 | 33.64% | — | filetypes/go: 40.02% | 0.938 | 0.934 |
| shell | 817 | 5695 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 91.31% | 0 | 91.19% | -0.12% | filetypes/shell: 94.74% | 0.995 | 0.994 |
| rar | 741 | 0 | `general` | general: 100.00% | 0 | 74.36% | -25.64% | general: 100.00% | — | — |
| png | 657 | 14388 | `general,filegroups/media,filetypes/png` | general: 0.00% | 2 | 8.98% | — | general: 9.13% | 0.214 | 0.212 |
| 7z | 565 | 12 | `general` | general: 88.67% | 0 | 76.99% | -11.68% | general: 92.57% | — | 0.999 |
| php | 511 | 10870 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 69.86% | 1 | 90.61% | — | filetypes/php: 91.19% | 0.989 | 0.988 |
| vbs | 462 | 423 | `general,filetypes/vbs` | filetypes/vbs: 69.26% | 0 | 69.91% | 0.65% | filetypes/vbs: 94.37% | 0.998 | 0.997 |
| xml | 292 | 18378 | `general,filegroups/config,filetypes/xml` | filegroups/config: 27.05% | 1 | 29.11% | — | filegroups/config: 37.33% | 0.186 | 0.588 |
| macho | 262 | 1383 | `general,filegroups/native,filetypes/macho` | filegroups/native: 89.31% | 0 | 91.98% | 2.67% | filetypes/macho: 98.47% | 0.999 | 0.999 |
| lnk | 261 | 127 | `general,filetypes/lnk` | filetypes/lnk: 68.58% | 0 | 68.58% | 0.00% | filetypes/lnk: 70.11% | 0.991 | 0.983 |
| powershell | 258 | 274 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 33.72% | 0 | 49.61% | 15.89% | filetypes/powershell: 86.05% | 0.987 | 0.985 |
| csharp | 234 | 7572 | `general,filegroups/source,filetypes/csharp` | filetypes/csharp: 64.10% | 1 | 64.53% | — | filetypes/csharp: 66.67% | 0.951 | 0.926 |
| msi | 234 | 13 | `general,filetypes/msi` | filetypes/msi: 98.72% | 0 | 74.79% | -23.93% | filetypes/msi: 98.72% | 1.000 | 0.999 |
| python-bytecode | 233 | 3863 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 98.28% | 0 | 97.42% | -0.86% | filetypes/python-bytecode: 98.28% | 0.996 | 0.996 |
| ole | 229 | 664 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 97.82% | 0 | 95.20% | -2.62% | filegroups/documents: 99.13% | 0.993 | 0.993 |
| rtf | 215 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.14% | 0 | 98.14% | 0.00% | filetypes/rtf: 100.00% | 1.000 | 1.000 |
| jar | 191 | 249 | `general,filetypes/jar` | filetypes/jar: 75.39% | 0 | 75.92% | 0.52% | filetypes/jar: 87.43% | 0.992 | 0.993 |
| docx | 176 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 77.84% | 0 | 84.66% | 6.82% | filegroups/documents: 85.80% | 0.976 | 0.976 |
| gz | 173 | 6366 | `general` | general: 28.90% | 1 | 28.90% | — | general: 50.29% | — | 0.652 |
| java_class | 173 | 47377 | `general,filegroups/portable,filetypes/java_class` | filegroups/portable: 75.72% | 3 | 87.28% | 0.00% | filegroups/portable: 87.28% | 0.949 | 0.949 |
| rust | 164 | 9604 | `general,filegroups/source,filetypes/rust` | general: 1.83% | 0 | 1.83% | 0.00% | general: 1.83% | 0.128 | 0.164 |
| text | 160 | 7992 | `general,filetypes/text` | general: 12.50% | 0 | 11.88% | -0.63% | general: 14.37% | 0.238 | 0.311 |
| tar | 150 | 51 | `general` | general: 93.33% | 0 | 80.00% | -13.33% | general: 95.33% | — | 0.994 |
| jpeg | 127 | 1319 | `general,filegroups/media,filetypes/jpeg` | general: 14.17% | 0 | 11.02% | -3.15% | general: 14.17% | 0.300 | 0.357 |
| plist | 68 | 1544 | `general,filegroups/config,filetypes/plist` | filetypes/plist: 52.94% | 0 | 41.18% | -11.76% | filetypes/plist: 72.06% | 0.916 | 0.914 |
| data | 58 | 1157 | `general` | general: 72.41% | 0 | 0.00% | -72.41% | general: 77.59% | — | 0.822 |
| cab | 29 | 12 | `general` | general: 58.62% | 0 | 3.45% | -55.17% | general: 100.00% | — | 0.967 |
| perl | 27 | 3960 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 92.59% | 0 | 92.59% | 0.00% | filegroups/scripts: 92.59% | 0.964 | 0.957 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filegroups/documents: 31.82% | 0 | 31.82% | 0.00% | general: 31.82% | 0.328 | 0.597 |
| makefile | 17 | 2741 | `general,filegroups/source,filetypes/makefile` | filetypes/makefile: 11.76% | 0 | 0.00% | -11.76% | filetypes/makefile: 23.53% | 0.244 | 0.226 |
| groovy | 15 | 648 | `general,filetypes/groovy` | filetypes/groovy: 53.33% | 0 | 53.33% | 0.00% | filetypes/groovy: 73.33% | 0.821 | 0.821 |
| chm | 9 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| crx | 7 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 708 | `general` | general: 28.57% | 0 | 0.00% | -28.57% | general: 71.43% | — | 0.583 |
| ruby | 7 | 2945 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 85.71% | 0 | 85.71% | 0.00% | general: 100.00% | 0.968 | 0.968 |
| html | 6 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| lua | 6 | 1839 | `general,filegroups/scripts` | filegroups/scripts: 83.33% | 0 | 66.67% | -16.67% | filegroups/scripts: 83.33% | — | 0.900 |
| java | 4 | 4192 | `general,filegroups/source` | general: 50.00% | 0 | 25.00% | -25.00% | general: 75.00% | — | 0.631 |
| xz | 4 | 3477 | `general` | general: 25.00% | 0 | 25.00% | 0.00% | general: 50.00% | — | 0.376 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 65 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.039 |
| applescript | 2 | 32 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 2 | 1405 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.501 |
| chrome-manifest | 2 | 46 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.643 |
| github-actions | 1 | 707 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| objc | 1 | 2308 | `general` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 134 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.011 |
| tar.bz2 | 1 | 21 | `general` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| tar.gz | `` | 0 | 0.00% | 65.84% | -65.84% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| zip | `` | 0 | 0.00% | 46.40% | -46.40% |
| deb | `` | 0 | 0.00% | 28.57% | -28.57% |
| gz | `general` | 0 | 1.73% | 28.90% | -27.17% |
| zst | `general` | 0 | 73.55% | 99.24% | -25.69% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 39.32% | 64.10% | -24.79% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| c | `general` | 0 | 2.77% | 6.51% | -3.74% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 95.02% | 97.23% | -2.21% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 97.88% | 98.57% | -0.69% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| png | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 86.64% | 86.38% | 0.26% |
| xml | `general,filegroups/config` | 0 | 27.40% | 27.05% | 0.34% |
| go | `general,filegroups/source,filetypes/go` | 0 | 9.52% | 9.09% | 0.42% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 0 | 76.30% | 75.72% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 75.55% | 74.84% | 0.71% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 71.04% | 69.86% | 1.17% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 63.18% | 61.59% | 1.58% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 60.04% | 65.84% | -5.80% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 91.19% | 91.31% | -0.12% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.68% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 33.64% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

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
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| zst | `general` | 0 | 48.93% | 99.24% | -50.30% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 60.32% | 100.00% | -39.68% |
| tar | `general` | 0 | 61.33% | 93.33% | -32.00% |
| 7z | `general` | 0 | 59.12% | 88.67% | -29.56% |
| gz | `general` | 0 | 0.00% | 28.90% | -28.90% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 39.32% | 64.10% | -24.79% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar.gz | `general` | 0 | 50.58% | 65.84% | -15.26% |
| zip | `general` | 0 | 34.62% | 46.40% | -11.79% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 95.02% | 97.23% | -2.21% |
| rtf | `filetypes/rtf` | 0 | 97.21% | 98.14% | -0.93% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 97.88% | 98.57% | -0.69% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| c | `general,filegroups/source,filetypes/c` | 1 | 7.02% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| java_class | `general,filetypes/java_class` | 1 | 85.55% | — | — |
| javascript | `general,filetypes/javascript` | 1 | 89.05% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| png | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 86.64% | 86.38% | 0.26% |
| xml | `general,filegroups/config` | 0 | 27.40% | 27.05% | 0.34% |
| go | `general,filegroups/source,filetypes/go` | 0 | 9.52% | 9.09% | 0.42% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 71.04% | 69.86% | 1.17% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 63.18% | 61.59% | 1.58% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.33% | 98.37% | -0.04% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source` | 8 | 10.93% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

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
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 51.07% | 99.24% | -48.17% |
| rar | `general` | 0 | 61.40% | 100.00% | -38.60% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| 7z | `general` | 0 | 60.88% | 88.67% | -27.79% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 39.32% | 64.10% | -24.79% |
| tar | `general` | 0 | 68.67% | 93.33% | -24.67% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar.gz | `general` | 0 | 51.13% | 65.84% | -14.71% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zip | `general` | 0 | 35.34% | 46.40% | -11.06% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 95.02% | 97.23% | -2.21% |
| rtf | `filetypes/rtf` | 0 | 97.21% | 98.14% | -0.93% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 97.88% | 98.57% | -0.69% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 4.02% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filetypes/go` | 1 | 10.54% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 1 | 85.55% | — | — |
| javascript | `general,filetypes/javascript` | 1 | 89.05% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 79.98% | — | — |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 90.53% | 90.36% | 0.17% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| xml | `general,filegroups/config` | 0 | 27.40% | 27.05% | 0.34% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 71.04% | 69.86% | 1.17% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 77.06% | 100.00% | -22.94% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 83.33% | 93.33% | -10.00% |
| 7z | `general` | 0 | 78.76% | 88.67% | -9.91% |
| tar.gz | `general` | 0 | 62.41% | 65.84% | -3.43% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| go | `general,filegroups/source,filetypes/go` | 3 | 37.55% | 40.02% | -2.46% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 92.66% | 94.74% | -2.08% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 13.76% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 4 | 99.26% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 31.21% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 7 | 90.17% | — | — |
| javascript | `filetypes/javascript` | 19 | 94.35% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 98.42% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 9 | 95.33% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 3 | 91.19% | 91.19% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 87.02% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 1 | 0.22% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 28.77% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 65.93% | 99.24% | -33.31% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 39.32% | 64.10% | -24.79% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| 7z | `general` | 0 | 72.92% | 88.67% | -15.75% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| tar.gz | `general` | 0 | 55.42% | 65.84% | -10.42% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| zip | `general` | 0 | 41.02% | 46.40% | -5.39% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 95.02% | 97.23% | -2.21% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| rust | `general` | 0 | 1.22% | 1.83% | -0.61% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 4.02% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 16.82% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 85.55% | — | — |
| javascript | `general,filetypes/javascript` | 2 | 89.16% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 87.48% | — | — |
| png | `general,filegroups/media,filetypes/png` | 1 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 82.84% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 98.65% | 98.57% | 0.08% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 90.53% | 90.36% | 0.17% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 24.14% | 58.62% | -34.48% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 78.00% | 100.00% | -22.00% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 84.67% | 93.33% | -8.67% |
| 7z | `general` | 0 | 80.18% | 88.67% | -8.50% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 99.84% | -3.13% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| tar.gz | `general` | 0 | 64.83% | 65.84% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 14.61% | — | — |
| csharp | `general,filegroups/source,filetypes/csharp` | 7 | 75.21% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 38.49% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 31.21% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 7 | 91.33% | — | — |
| javascript | `filetypes/javascript` | 19 | 94.47% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `general,filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| macho | `filegroups/native,filetypes/macho` | 2 | 96.18% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 98.44% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 12 | 96.26% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 3 | 91.19% | 91.19% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 5 | 88.21% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 93.51% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 1 | 0.22% | — | — |
| vbs | `filetypes/vbs` | 1 | 71.86% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 28.77% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general` | 1 | 46.98% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 65.93% | 99.24% | -33.31% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 39.32% | 64.10% | -24.79% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| 7z | `general` | 0 | 72.92% | 88.67% | -15.75% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| tar.gz | `general` | 0 | 55.42% | 65.84% | -10.42% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| zip | `general` | 0 | 41.02% | 46.40% | -5.39% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 95.02% | 97.23% | -2.21% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.06% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 30.76% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 85.55% | — | — |
| javascript | `general,filetypes/javascript` | 2 | 89.16% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 87.87% | — | — |
| png | `general,filegroups/media,filetypes/png` | 1 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 82.84% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 98.65% | 98.57% | 0.08% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 90.53% | 90.36% | 0.17% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 78.95% | 100.00% | -21.05% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| cab | `general` | 0 | 44.83% | 58.62% | -13.79% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 80.88% | 88.67% | -7.79% |
| tar | `general` | 0 | 86.67% | 93.33% | -6.67% |
| tar.gz | `general` | 0 | 60.10% | 65.84% | -5.74% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.87% | 99.84% | -2.98% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 15.23% | — | — |
| csharp | `general,filegroups/source,filetypes/csharp` | 7 | 75.21% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 41.38% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.21% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 7 | 92.49% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 23 | 94.95% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 5 | 97.82% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `general,filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| macho | `filegroups/native,filetypes/macho` | 2 | 96.18% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.40% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 98.52% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 96.95% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 4 | 91.19% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 6 | 89.49% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 93.64% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 1 | 0.22% | — | — |
| vbs | `filetypes/vbs` | 1 | 72.51% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 30.48% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 47.44% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 65.93% | 99.24% | -33.31% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| 7z | `general` | 0 | 72.92% | 88.67% | -15.75% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| tar.gz | `general` | 0 | 55.42% | 65.84% | -10.42% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| zip | `general` | 0 | 41.02% | 46.40% | -5.39% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.89% | 97.23% | -0.35% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.06% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 30.76% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 85.55% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 82.84% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 98.65% | 98.57% | 0.08% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 90.53% | 90.36% | 0.17% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 79.62% | 100.00% | -20.38% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| cab | `general` | 0 | 44.83% | 58.62% | -13.79% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 81.06% | 88.67% | -7.61% |
| tar | `general` | 0 | 87.33% | 93.33% | -6.00% |
| tar.gz | `general` | 0 | 60.13% | 65.84% | -5.71% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.51% | 99.84% | -1.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 14 | 15.57% | — | — |
| csharp | `general,filegroups/source,filetypes/csharp` | 7 | 75.21% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 41.38% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.21% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 7 | 91.91% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 23 | 94.95% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 6 | 97.89% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `general,filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 98.52% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 97.03% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 5 | 91.39% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 7 | 90.41% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 93.64% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.50% | 12.50% | 0.00% |
| unknown | `general` | 1 | 0.22% | — | — |
| vbs | `filetypes/vbs` | 1 | 73.38% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 35.27% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 47.78% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 70.72% | 100.00% | -29.28% |
| zst | `general` | 0 | 70.20% | 99.24% | -29.04% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| tar | `general` | 0 | 77.33% | 93.33% | -16.00% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| 7z | `general` | 0 | 75.40% | 88.67% | -13.27% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| tar.gz | `general` | 0 | 56.78% | 65.84% | -9.06% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 98.28% | -6.01% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| zip | `general` | 0 | 43.94% | 46.40% | -2.46% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 88.98% | 91.31% | -2.33% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.89% | 97.23% | -0.35% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.51% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 30.76% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 86.13% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 82.84% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 98.65% | 98.57% | 0.08% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 90.53% | 90.36% | 0.17% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 80.16% | 100.00% | -19.84% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| cab | `general` | 0 | 44.83% | 58.62% | -13.79% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 81.42% | 88.67% | -7.26% |
| tar | `general` | 0 | 87.33% | 93.33% | -6.00% |
| tar.gz | `general` | 0 | 60.16% | 65.84% | -5.68% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| pkg-info | `filetypes/pkg-info` | 0 | 99.37% | 99.84% | -0.47% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 16 | 16.42% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 41.38% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.21% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 8 | 91.91% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 35 | 95.42% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 6 | 97.89% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `general,filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 19 | 98.10% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 5 | 91.39% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 8 | 90.76% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 94.25% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.50% | 12.50% | 0.00% |
| unknown | `general` | 1 | 0.22% | — | — |
| vbs | `filetypes/vbs` | 1 | 74.03% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 36.30% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 48.05% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 58.62% | -58.62% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 70.72% | 100.00% | -29.28% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| tar | `general` | 0 | 77.33% | 93.33% | -16.00% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| 7z | `general` | 0 | 75.40% | 88.67% | -13.27% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar.gz | `general` | 0 | 56.78% | 65.84% | -9.06% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| zip | `general` | 0 | 43.94% | 46.40% | -2.46% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.89% | 97.23% | -0.35% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 91.19% | 91.31% | -0.12% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.28% | 98.37% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.51% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 33.64% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 86.13% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 82.84% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 98.65% | 98.57% | 0.08% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 80.70% | 100.00% | -19.30% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| cab | `general` | 0 | 44.83% | 58.62% | -13.79% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 81.42% | 88.67% | -7.26% |
| tar | `general` | 0 | 87.33% | 93.33% | -6.00% |
| tar.gz | `general` | 0 | 60.18% | 65.84% | -5.65% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 96.51% | 97.82% | -1.31% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| xml | `general,filegroups/config,filetypes/xml` | 3 | 36.64% | 37.33% | -0.68% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 16 | 16.53% | — | — |
| csharp | `filetypes/csharp` | 14 | 82.48% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 43.67% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.21% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 10 | 91.33% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 35 | 95.45% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 6 | 97.89% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `general,filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 22 | 98.18% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 6 | 92.59% | — | — |
| php | `filetypes/php` | 7 | 93.15% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.13% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 10 | 91.77% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 94.25% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 2 | 93.94% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 48.52% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 60.04% | 65.84% | -5.80% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 91.19% | 91.31% | -0.12% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.68% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 33.64% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 22.22% | 100.00% | -77.78% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 80.84% | 100.00% | -19.16% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 81.95% | 88.67% | -6.73% |
| tar | `general` | 0 | 88.00% | 93.33% | -5.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 96.51% | 97.82% | -1.31% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| xml | `general,filegroups/config,filetypes/xml` | 3 | 36.64% | 37.33% | -0.68% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 16.70% | — | — |
| csharp | `filetypes/csharp` | 14 | 82.48% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 43.67% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.21% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 10 | 91.33% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 37 | 95.76% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 11.76% | 11.76% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 24 | 98.57% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 6 | 92.59% | — | — |
| php | `filetypes/php` | 8 | 93.15% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 12 | 92.26% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 94.49% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 69.62% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 2 | 93.94% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 48.83% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 60.04% | 65.84% | -5.80% |
| jpeg | `general` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 91.19% | 91.31% | -0.12% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 6.68% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 33.64% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.48% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| chm | `general` | 0 | 22.22% | 100.00% | -77.78% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 80.97% | 100.00% | -19.03% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 82.12% | 88.67% | -6.55% |
| tar | `general` | 0 | 88.00% | 93.33% | -5.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 16.76% | — | — |
| csharp | `filetypes/csharp` | 17 | 84.19% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filetypes/go` | 11 | 48.09% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.79% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 11 | 93.64% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 37 | 95.76% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 2 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.40% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 26 | 98.76% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 6 | 92.59% | — | — |
| php | `filetypes/php` | 8 | 93.15% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 57.35% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 49 | 96.13% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 94.49% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 70.25% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 2 | 93.94% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 37.33% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 49.22% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 60.04% | 65.84% | -5.80% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 91.19% | 91.31% | -0.12% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 7.08% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 35.43% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| java_class | `general,filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 82.83% | 88.67% | -5.84% |
| tar | `general` | 0 | 88.00% | 93.33% | -5.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 16.99% | — | — |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 11 | 49.87% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.79% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filetypes/java_class` | 11 | 93.64% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 38 | 95.86% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 2 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 29 | 98.86% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 6 | 92.59% | — | — |
| php | `filetypes/php` | 9 | 93.74% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 49 | 96.13% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 3 | 94.74% | 94.74% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 71.75% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 2 | 93.94% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 38.70% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 49.63% | — | — |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 59.92% | 65.84% | -5.91% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 7.08% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 82.05% | 100.00% | -17.95% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.01% | 88.67% | -5.66% |
| tar | `general` | 0 | 88.00% | 93.33% | -5.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 37 | 19.25% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 12 | 50.47% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| gz | `general` | 2 | 31.79% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filetypes/java_class` | 11 | 93.64% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 38 | 95.86% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 30 | 98.96% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 12 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 49 | 96.13% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 3 | 94.74% | 94.74% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 72.42% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `filegroups/config` | 4 | 39.04% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 60.25% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 59.92% | 65.84% | -5.91% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 7.19% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 31.79% | 50.29% | -18.50% |
| rar | `general` | 0 | 82.19% | 100.00% | -17.81% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.01% | 88.67% | -5.66% |
| tar | `general` | 0 | 88.00% | 93.33% | -5.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 38 | 19.31% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 12 | 50.47% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filetypes/java_class` | 11 | 94.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 42 | 95.97% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.31% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 33 | 98.99% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 13 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 50 | 96.17% | — | — |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 3 | 94.74% | 94.74% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 73.23% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 39.04% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general` | 1 | 60.48% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.36% | 100.00% | -25.64% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 80.00% | 93.33% | -13.33% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 11.76% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 76.99% | 88.67% | -11.68% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 7.19% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 94.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 31.79% | 50.29% | -18.50% |
| rar | `general` | 0 | 82.32% | 100.00% | -17.68% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.01% | 88.67% | -5.66% |
| tar | `general` | 0 | 88.67% | 93.33% | -4.67% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 38 | 19.37% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 15 | 99.89% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 12 | 50.81% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 11 | 94.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 44 | 95.99% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 36 | 99.08% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 13 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 52 | 96.26% | — | — |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 73.54% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `filegroups/config` | 4 | 39.04% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 60.63% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.25% | 100.00% | -23.75% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 78.05% | 88.67% | -10.62% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| zip | `general` | 0 | 46.35% | 46.40% | -0.05% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source` | 8 | 10.93% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `filegroups/native,filetypes/elf` | 1 | 98.99% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java_class | `filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 8.98% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 31.79% | 50.29% | -18.50% |
| rar | `general` | 0 | 82.73% | 100.00% | -17.27% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.01% | 88.67% | -5.66% |
| tar | `general` | 0 | 88.67% | 93.33% | -4.67% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 39 | 19.37% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 11 | 94.80% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 46 | 96.05% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 39 | 99.14% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 13 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 52 | 96.26% | — | — |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 75.07% | — | — |
| text | `general,filetypes/text` | 1 | 12.50% | — | — |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 39.73% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 51.05% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.25% | 100.00% | -23.75% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 78.05% | 88.67% | -10.62% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 84.34% | 84.47% | -0.13% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.33% | 98.37% | -0.04% |
| zip | `general` | 0 | 46.39% | 46.40% | -0.01% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source` | 8 | 10.93% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java_class | `filetypes/java_class` | 3 | 87.28% | 87.28% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 31.79% | 50.29% | -18.50% |
| rar | `general` | 0 | 82.73% | 100.00% | -17.27% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.19% | 88.67% | -5.49% |
| tar | `general` | 0 | 89.33% | 93.33% | -4.00% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 39 | 19.42% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 19 | 85.47% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 11 | 94.80% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 47 | 96.09% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 40 | 99.15% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 15 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.35% | — | — |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 76.00% | — | — |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 39.73% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 51.29% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 98.33% | 98.37% | -0.04% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source` | 8 | 10.93% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 93.72% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 31.79% | 50.29% | -18.50% |
| rar | `general` | 0 | 82.86% | 100.00% | -17.14% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| cab | `general` | 0 | 51.72% | 58.62% | -6.90% |
| 7z | `general` | 0 | 83.19% | 88.67% | -5.49% |
| tar | `general` | 0 | 90.00% | 93.33% | -3.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 40 | 19.59% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 22 | 86.32% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| jar | `filetypes/jar` | 2 | 86.39% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 11 | 93.64% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 47 | 96.09% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 42 | 99.17% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 15 | 94.13% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.35% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general` | 2 | 1.83% | — | — |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 76.60% | — | — |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 4 | 39.73% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 51.34% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 13.08% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| javascript | `filetypes/javascript` | 18 | 94.28% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 32.95% | 50.29% | -17.34% |
| rar | `general` | 0 | 82.86% | 100.00% | -17.14% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 83.54% | 88.67% | -5.13% |
| cab | `general` | 0 | 55.17% | 58.62% | -3.45% |
| tar | `general` | 0 | 90.00% | 93.33% | -3.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| jar | `filetypes/jar` | 3 | 86.91% | 87.43% | -0.52% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 40 | 19.59% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 22 | 86.32% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 11 | 94.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 47 | 96.12% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 98.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 43 | 99.18% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 15 | 94.32% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.39% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general` | 2 | 1.83% | — | — |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 77.38% | — | — |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 5 | 39.73% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 46.40% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 13.08% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `filetypes/javascript` | 18 | 94.28% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| java_class | `general,filetypes/java_class` | 3 | 87.86% | 87.28% | 0.58% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 91.98% | 89.31% | 2.67% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 32.95% | 50.29% | -17.34% |
| rar | `general` | 0 | 82.86% | 100.00% | -17.14% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 83.54% | 88.67% | -5.13% |
| cab | `general` | 0 | 55.17% | 58.62% | -3.45% |
| tar | `general` | 0 | 90.00% | 93.33% | -3.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| jar | `filetypes/jar` | 3 | 86.91% | 87.43% | -0.52% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `filetypes/pkg-info` | 0 | 99.61% | 99.84% | -0.24% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 40 | 19.76% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 22 | 86.32% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 15 | 94.80% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 47 | 96.12% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 99.14% | 99.14% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 48 | 99.25% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 16 | 94.32% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| powershell | `general,filetypes/powershell` | 2 | 86.43% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.39% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general` | 2 | 1.83% | — | — |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 77.55% | — | — |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 5 | 40.07% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 13.25% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 28.90% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 4 | 88.44% | — | — |
| javascript | `filetypes/javascript` | 18 | 94.28% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.01% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.61% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 1 | 0.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 91.68% | 91.31% | 0.37% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 32.95% | 50.29% | -17.34% |
| rar | `general` | 0 | 83.00% | 100.00% | -17.00% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 83.54% | 88.67% | -5.13% |
| tar.gz | `general` | 3 | 77.87% | 81.97% | -4.10% |
| cab | `general` | 0 | 55.17% | 58.62% | -3.45% |
| tar | `general` | 0 | 90.00% | 93.33% | -3.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| jar | `filetypes/jar` | 3 | 86.91% | 87.43% | -0.52% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `filetypes/pkg-info` | 0 | 99.61% | 99.84% | -0.24% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 41 | 19.76% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 22 | 86.32% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 15 | 94.80% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 49 | 96.15% | — | — |
| kotlin | `filetypes/kotlin` | 7 | 98.27% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 99.14% | 99.14% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 49 | 99.26% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 16 | 94.32% | — | — |
| plist | `filegroups/config,filetypes/plist` | 2 | 72.06% | — | — |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| powershell | `general,filetypes/powershell` | 2 | 86.43% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.39% | — | — |
| python-bytecode | `filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general` | 2 | 1.83% | — | — |
| shell | `filegroups/scripts,filetypes/shell` | 5 | 94.86% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `filegroups/config` | 5 | 40.07% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.10% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| cab | `general` | 0 | 3.45% | 58.62% | -55.17% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| rar | `general` | 0 | 76.79% | 100.00% | -23.21% |
| lua | `general,filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 41.18% | 52.94% | -11.76% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| 7z | `general` | 0 | 78.58% | 88.67% | -10.09% |
| tar.gz | `general` | 0 | 59.95% | 65.84% | -5.89% |
| makefile | `general,filetypes/makefile` | 0 | 5.88% | 11.76% | -5.88% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| ole | `general,filetypes/ole` | 0 | 95.20% | 97.82% | -2.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 92.66% | 94.74% | -2.08% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.42% | 98.28% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| text | `general,filetypes/text` | 0 | 11.88% | 12.50% | -0.63% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 99.69% | 99.84% | -0.16% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.53% | 99.66% | -0.14% |
| pdf | `filegroups/documents` | 0 | 98.26% | 98.37% | -0.11% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 97.13% | 97.23% | -0.10% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 13 | 13.25% | — | — |
| csharp | `filetypes/csharp` | 1 | 64.53% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 99.21% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 36.36% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 53.33% | 53.33% | 0.00% |
| gz | `general` | 1 | 31.21% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 4 | 88.44% | — | — |
| javascript | `filetypes/javascript` | 19 | 94.35% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 9 | 95.33% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 1 | 90.80% | — | — |
| png | `filetypes/png` | 3 | 9.13% | 9.13% | 0.00% |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 4 | 85.31% | — | — |
| rtf | `filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `filetypes/ruby` | 1 | 85.71% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| unknown | `general` | 1 | 0.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 1 | 29.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.48% | 93.30% | 0.18% |
| jar | `general,filetypes/jar` | 0 | 75.92% | 75.39% | 0.52% |
| vbs | `general,filetypes/vbs` | 0 | 69.91% | 69.26% | 0.65% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 49.61% | 33.72% | 15.89% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 72.41% | -70.69% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| msi | `general,filetypes/msi` | 0 | 74.79% | 98.72% | -23.93% |
| gz | `general` | 3 | 32.95% | 50.29% | -17.34% |
| rar | `general` | 0 | 83.13% | 100.00% | -16.87% |
| xlsx | `general,filegroups/documents` | 0 | 74.16% | 89.58% | -15.42% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 83.54% | 88.67% | -5.13% |
| tar.gz | `general` | 3 | 78.27% | 81.97% | -3.69% |
| cab | `general` | 0 | 55.17% | 58.62% | -3.45% |
| tar | `general` | 0 | 90.00% | 93.33% | -3.33% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.02% | 14.17% | -3.15% |
| doc | `general,filegroups/documents` | 0 | 98.76% | 99.61% | -0.85% |
| jar | `filetypes/jar` | 3 | 86.91% | 87.43% | -0.52% |
| ole | `filetypes/ole` | 0 | 97.38% | 97.82% | -0.44% |
| macho | `filegroups/native,filetypes/macho` | 3 | 98.09% | 98.47% | -0.38% |
| xls | `filegroups/documents` | 0 | 99.23% | 99.54% | -0.31% |
| pkg-info | `filetypes/pkg-info` | 0 | 99.61% | 99.84% | -0.24% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.66% | — | — |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 42 | 19.76% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `filetypes/csharp` | 22 | 86.32% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `filetypes/elf` | 19 | 99.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 13 | 51.06% | — | — |
| groovy | `general,filetypes/groovy` | 1 | 60.00% | — | — |
| html | `general,filegroups/documents` | 2 | 100.00% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 17 | 94.80% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 50 | 96.20% | — | — |
| kotlin | `filetypes/kotlin` | 8 | 98.34% | — | — |
| lnk | `general,filetypes/lnk` | 0 | 68.58% | 68.58% | 0.00% |
| lua | `filegroups/scripts` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 11.76% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 99.14% | 99.14% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 51 | 99.35% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `filetypes/php` | 16 | 94.72% | — | — |
| plist | `filegroups/config,filetypes/plist` | 3 | 72.06% | 72.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 17 | 10.20% | — | — |
| powershell | `general,filetypes/powershell` | 2 | 86.43% | — | — |
| pptx | `filegroups/documents` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 53 | 96.52% | — | — |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 98.28% | 98.28% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.14% | 98.14% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 2 | 100.00% | — | — |
| rust | `general` | 2 | 1.83% | — | — |
| shell | `filegroups/scripts,filetypes/shell` | 7 | 94.98% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| unknown | `general` | 1 | 0.00% | — | — |
| vbs | `filetypes/vbs` | 3 | 94.37% | 94.37% | 0.00% |
| xml | `filegroups/config` | 5 | 40.41% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.37% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 84.66% | 77.84% | 6.82% |
