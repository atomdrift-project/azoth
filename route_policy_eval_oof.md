# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 592307 (213009 malware, 379298 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 113010 | 18905 | `general,filegroups/native,filetypes/pe` | filegroups/native: 85.89% | 16 | 97.52% | — | filegroups/native: 90.84% | 1.000 | 1.000 |
| pdf | 21801 | 1734 | `general,filegroups/documents,filetypes/pdf` | general: 6.44% | 0 | 6.48% | 0.03% | filetypes/pdf: 7.84% | 0.997 | 0.995 |
| batch | 21128 | 427 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 99.67% | 0 | 99.46% | -0.21% | filegroups/scripts: 99.80% | 1.000 | 1.000 |
| javascript | 10621 | 59662 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 74.64% | 2 | 88.33% | — | filegroups/scripts: 90.07% | 0.998 | 0.998 |
| elf | 8967 | 17064 | `general,filegroups/native,filetypes/elf` | filegroups/native: 97.86% | 0 | 93.14% | -4.72% | filegroups/native: 99.17% | 1.000 | 1.000 |
| zip | 7407 | 870 | `general` | general: 53.29% | 0 | 49.71% | -3.58% | general: 66.46% | — | 0.990 |
| tar.gz | 3466 | 1674 | `general` | general: 66.56% | 0 | 62.58% | -3.98% | general: 81.65% | — | 0.995 |
| kotlin | 2888 | 5355 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 96.99% | 0 | 94.77% | -2.22% | filetypes/kotlin: 97.89% | 0.998 | 0.997 |
| python | 2273 | 16342 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 59.30% | 0 | 60.05% | 0.75% | filegroups/scripts: 74.84% | 0.974 | 0.991 |
| xlsx | 2237 | 12 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 90.17% | 0 | 29.32% | -60.84% | general: 91.69% | 0.981 | 0.996 |
| package.json | 2163 | 1439 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 91.59% | 0 | 91.68% | 0.09% | filetypes/package.json: 99.63% | 1.000 | 1.000 |
| c | 1766 | 66647 | `general,filegroups/source,filetypes/c` | filetypes/c: 12.85% | 0 | 3.74% | -9.12% | filetypes/c: 13.36% | 0.489 | 0.743 |
| unknown | 1348 | 2020 | `general` | general: 0.22% | 0 | 0.00% | -0.22% | general: 35.09% | — | 0.761 |
| zst | 1312 | 2034 | `general` | general: 99.16% | 0 | 87.50% | -11.66% | general: 100.00% | — | 1.000 |
| xls | 1297 | 7 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 95.37% | 0 | 96.07% | 0.69% | filegroups/documents: 99.85% | 0.980 | 0.997 |
| doc | 1287 | 3 | `general,filegroups/documents` | general: 99.61% | 0 | 72.18% | -27.43% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 114 | `general,filetypes/pkg-info` | filetypes/pkg-info: 98.75% | 0 | 98.43% | -0.31% | filetypes/pkg-info: 99.92% | 1.000 | 1.000 |
| go | 1177 | 11867 | `general,filegroups/source,filetypes/go` | filetypes/go: 1.19% | 0 | 0.85% | -0.34% | filetypes/go: 5.01% | 0.654 | 0.728 |
| shell | 816 | 5694 | `general,filegroups/scripts,filetypes/shell` | filegroups/scripts: 84.31% | 0 | 80.76% | -3.55% | filegroups/scripts: 87.87% | 0.981 | 0.991 |
| rar | 741 | 0 | `general` | general: 100.00% | 0 | 71.39% | -28.61% | general: 100.00% | — | — |
| png | 657 | 14388 | `general,filegroups/media,filetypes/png` | general: 0.00% | 0 | 0.15% | 0.15% | general: 8.98% | 0.135 | 0.169 |
| 7z | 565 | 12 | `general` | general: 90.97% | 0 | 70.97% | -20.00% | general: 93.81% | — | 0.999 |
| php | 511 | 10870 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 72.99% | 0 | 73.58% | 0.59% | filetypes/php: 90.22% | 0.989 | 0.988 |
| vbs | 462 | 423 | `general,filetypes/vbs` | filetypes/vbs: 26.84% | 0 | 27.71% | 0.87% | filetypes/vbs: 40.04% | 0.977 | 0.977 |
| xml | 292 | 18378 | `general,filegroups/config,filetypes/xml` | general: 2.74% | 0 | 2.74% | 0.00% | filegroups/config: 5.14% | 0.158 | 0.207 |
| macho | 262 | 1383 | `general,filegroups/native,filetypes/macho` | filegroups/native: 87.79% | 0 | 89.69% | 1.91% | filegroups/native: 97.33% | 0.995 | 0.995 |
| lnk | 261 | 127 | `general,filetypes/lnk` | filetypes/lnk: 51.72% | 0 | 49.04% | -2.68% | filetypes/lnk: 70.50% | 0.975 | 0.974 |
| powershell | 257 | 274 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 35.80% | 0 | 39.69% | 3.89% | filegroups/scripts: 78.99% | 0.972 | 0.985 |
| csharp | 234 | 7572 | `general,filegroups/source,filetypes/csharp` | filetypes/csharp: 24.79% | 0 | 17.52% | -7.26% | filetypes/csharp: 29.49% | 0.550 | 0.671 |
| msi | 234 | 13 | `general,filetypes/msi` | filetypes/msi: 97.86% | 0 | 61.97% | -35.90% | filetypes/msi: 98.29% | 1.000 | 0.997 |
| python-bytecode | 233 | 3862 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.85% | 0 | 68.67% | -29.18% | filetypes/python-bytecode: 97.85% | 0.996 | 0.996 |
| ole | 229 | 664 | `general,filegroups/documents,filetypes/ole` | general: 91.27% | 0 | 91.27% | 0.00% | filetypes/ole: 96.94% | 0.992 | 0.992 |
| rtf | 215 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.67% | 0 | 97.67% | 0.00% | general: 98.14% | 1.000 | 1.000 |
| jar | 191 | 249 | `general,filetypes/jar` | general: 60.21% | 0 | 56.54% | -3.66% | filetypes/jar: 70.68% | 0.974 | 0.974 |
| docx | 176 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 52.27% | 0 | 70.45% | 18.18% | general: 85.80% | 0.975 | 0.975 |
| gz | 173 | 6366 | `general` | general: 26.59% | 0 | 0.00% | -26.59% | general: 49.13% | — | 0.658 |
| java_class | 173 | 47377 | `general,filegroups/portable,filetypes/java_class` | general: 65.90% | 0 | 45.66% | -20.23% | filegroups/portable: 83.24% | 0.938 | 0.934 |
| rust | 164 | 9604 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 2.44% | 0 | 1.22% | -1.22% | filetypes/rust: 3.66% | 0.110 | 0.168 |
| text | 160 | 7992 | `general,filetypes/text` | general: 11.88% | 0 | 11.25% | -0.62% | general: 14.37% | 0.230 | 0.235 |
| tar | 150 | 51 | `general` | general: 93.33% | 0 | 76.00% | -17.33% | general: 95.33% | — | 0.994 |
| jpeg | 127 | 1319 | `general,filegroups/media,filetypes/jpeg` | general: 14.17% | 0 | 12.60% | -1.57% | filegroups/media: 17.32% | 0.208 | 0.318 |
| plist | 68 | 1544 | `general,filegroups/config,filetypes/plist` | filegroups/config: 2.94% | 0 | 2.94% | 0.00% | general: 5.88% | 0.093 | 0.100 |
| data | 58 | 1157 | `general` | general: 72.41% | 0 | 0.00% | -72.41% | general: 79.31% | — | 0.821 |
| cab | 29 | 12 | `general` | general: 62.07% | 0 | 0.00% | -62.07% | general: 100.00% | — | 0.968 |
| perl | 27 | 3960 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 92.59% | 0 | 92.59% | 0.00% | filetypes/perl: 96.30% | 0.963 | 0.964 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filegroups/documents: 22.73% | 0 | 22.73% | 0.00% | general: 31.82% | 0.328 | 0.591 |
| makefile | 17 | 2741 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.014 | 0.029 |
| groovy | 15 | 648 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.044 | 0.044 |
| chm | 9 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| crx | 7 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 708 | `general` | general: 28.57% | 0 | 0.00% | -28.57% | general: 71.43% | — | 0.600 |
| ruby | 7 | 2945 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 85.71% | 0 | 71.43% | -14.29% | general: 100.00% | 0.948 | 0.948 |
| html | 6 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | — | 1.000 |
| lua | 6 | 1839 | `general,filegroups/scripts` | filegroups/scripts: 83.33% | 0 | 0.00% | -83.33% | filegroups/scripts: 83.33% | — | 0.883 |
| java | 4 | 4192 | `general,filegroups/source` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.644 |
| xz | 4 | 3477 | `general` | general: 25.00% | 0 | 0.00% | -25.00% | general: 50.00% | — | 0.379 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 65 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.045 |
| applescript | 2 | 32 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 2 | 1405 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.501 |
| chrome-manifest | 2 | 46 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.625 |
| github-actions | 1 | 707 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| objc | 1 | 2308 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 134 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.013 |
| tar.bz2 | 1 | 21 | `general` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| rar | `general` | 0 | 71.39% | 100.00% | -28.61% |
| deb | `` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 77.67% | 99.16% | -21.49% |
| msi | `general,filetypes/msi` | 0 | 77.35% | 97.86% | -20.51% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| 7z | `general` | 0 | 70.97% | 90.97% | -20.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zip | `general` | 0 | 43.20% | 53.29% | -10.09% |
| tar.gz | `general` | 0 | 57.33% | 66.56% | -9.23% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 86.22% | 85.89% | 0.34% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 76.26% | 74.64% | 1.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.97% | 97.86% | -35.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| rar | `general` | 0 | 71.39% | 100.00% | -28.61% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 77.67% | 99.16% | -21.49% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| 7z | `general` | 0 | 70.97% | 90.97% | -20.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zip | `general` | 0 | 43.20% | 53.29% | -10.09% |
| tar.gz | `general` | 0 | 57.33% | 66.56% | -9.23% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.90% | 84.31% | -4.41% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 97.52% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L1 hostile

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
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 58.97% | 97.86% | -38.89% |
| rar | `general` | 0 | 65.99% | 100.00% | -34.01% |
| zst | `general` | 0 | 66.01% | 99.16% | -33.16% |
| tar | `general` | 0 | 62.67% | 93.33% | -30.67% |
| 7z | `general` | 0 | 61.59% | 90.97% | -29.38% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| macho | `filetypes/macho` | 0 | 67.18% | 87.79% | -20.61% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zip | `general` | 0 | 37.30% | 53.29% | -15.98% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar.gz | `general` | 0 | 54.27% | 66.56% | -12.29% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 91.11% | 90.84% | 0.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 76.26% | 74.64% | 1.62% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.10% | 97.86% | -33.76% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 82.85% | 99.16% | -16.31% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 76.81% | 90.97% | -14.16% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 60.56% | 66.56% | -6.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.05% | 53.29% | -2.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 84.31% | -1.23% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L2 hostile

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
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.11% | 97.86% | -36.75% |
| rar | `general` | 0 | 66.13% | 100.00% | -33.87% |
| zst | `general` | 0 | 67.07% | 99.16% | -32.09% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| tar | `general` | 0 | 65.33% | 93.33% | -28.00% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| 7z | `general` | 0 | 63.89% | 90.97% | -27.08% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| macho | `filetypes/macho` | 0 | 67.18% | 87.79% | -20.61% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar.gz | `general` | 0 | 54.67% | 66.56% | -11.89% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| zip | `general` | 0 | 49.53% | 53.29% | -3.75% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 87.78% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 91.11% | 90.84% | 0.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.96% | 97.86% | -32.91% |
| cab | `general` | 0 | 31.03% | 62.07% | -31.03% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 3.47% | 26.59% | -23.12% |
| rar | `general` | 0 | 77.46% | 100.00% | -22.54% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 84.07% | 99.16% | -15.09% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar | `general` | 0 | 83.33% | 93.33% | -10.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| tar.gz | `general` | 0 | 62.90% | 66.56% | -3.66% |
| zip | `general` | 0 | 50.14% | 53.29% | -3.15% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 42 | 99.23% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

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
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.11% | 97.86% | -36.75% |
| rar | `general` | 0 | 65.45% | 100.00% | -34.55% |
| tar | `general` | 0 | 62.00% | 93.33% | -31.33% |
| 7z | `general` | 0 | 60.71% | 90.97% | -30.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| macho | `filetypes/macho` | 0 | 67.18% | 87.79% | -20.61% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| zip | `general` | 0 | 49.56% | 53.29% | -3.73% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 91.11% | 90.84% | 0.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| msi | `filetypes/msi` | 0 | 66.24% | 97.86% | -31.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 4.62% | 26.59% | -21.97% |
| cab | `general` | 0 | 41.38% | 62.07% | -20.69% |
| rar | `general` | 0 | 79.35% | 100.00% | -20.65% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 85.29% | 99.16% | -13.87% |
| 7z | `general` | 0 | 80.00% | 90.97% | -10.97% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| tar | `general` | 0 | 85.33% | 93.33% | -8.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.61% | 66.56% | -3.95% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 50.30% | 53.29% | -2.98% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 59 | 99.55% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

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
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.54% | 97.86% | -36.32% |
| rar | `general` | 0 | 65.45% | 100.00% | -34.55% |
| tar | `general` | 0 | 62.00% | 93.33% | -31.33% |
| 7z | `general` | 0 | 60.71% | 90.97% | -30.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| macho | `filetypes/macho` | 0 | 67.18% | 87.79% | -20.61% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| zip | `general` | 0 | 49.59% | 53.29% | -3.70% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| pe | `general,filegroups/native,filetypes/pe` | 3 | 91.11% | 90.84% | 0.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| msi | `filetypes/msi` | 0 | 66.24% | 97.86% | -31.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 5.20% | 26.59% | -21.39% |
| cab | `general` | 0 | 41.38% | 62.07% | -20.69% |
| rar | `general` | 0 | 79.76% | 100.00% | -20.24% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 85.59% | 99.16% | -13.57% |
| 7z | `general` | 0 | 80.18% | 90.97% | -10.80% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| tar | `general` | 0 | 86.00% | 93.33% | -7.33% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.64% | 66.56% | -3.92% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 70 | 99.63% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 56.84% | — | — |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

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
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.54% | 97.86% | -36.32% |
| rar | `general` | 0 | 65.45% | 100.00% | -34.55% |
| tar | `general` | 0 | 62.00% | 93.33% | -31.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.63% | 53.29% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 2 | 87.78% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 91.98% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 4 | 92.14% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts` | 0 | 50.00% | 83.33% | -33.33% |
| msi | `filetypes/msi` | 0 | 67.09% | 97.86% | -30.77% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| cab | `general` | 0 | 41.38% | 62.07% | -20.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 80.03% | 100.00% | -19.97% |
| gz | `general` | 0 | 7.51% | 26.59% | -19.08% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 85.90% | 99.16% | -13.26% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| tar | `general` | 0 | 86.00% | 93.33% | -7.33% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.64% | 66.56% | -3.92% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 84 | 99.73% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 1 | 58.37% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 57.61% | — | — |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| html | `general,filegroups/documents` | 0 | 33.33% | 100.00% | -66.67% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.97% | 97.86% | -35.90% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| java | `general,filegroups/source` | 0 | 25.00% | 50.00% | -25.00% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| tar | `general` | 0 | 75.33% | 93.33% | -18.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.64% | 53.29% | -3.65% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.19% | 84.31% | -0.12% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 2 | 87.78% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 4 | 92.14% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `filegroups/scripts` | 0 | 50.00% | 83.33% | -33.33% |
| msi | `filetypes/msi` | 0 | 67.52% | 97.86% | -30.34% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 80.16% | 100.00% | -19.84% |
| gz | `general` | 0 | 9.25% | 26.59% | -17.34% |
| cab | `general` | 0 | 44.83% | 62.07% | -17.24% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 85.98% | 99.16% | -13.19% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar | `general` | 0 | 86.67% | 93.33% | -6.67% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 93 | 99.79% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 67.40% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 57.85% | — | — |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.97% | 97.86% | -35.90% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 74.39% | 99.16% | -24.77% |
| 7z | `general` | 0 | 69.38% | 90.97% | -21.59% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| tar | `general` | 0 | 75.33% | 93.33% | -18.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zip | `general` | 0 | 42.16% | 53.29% | -11.12% |
| tar.gz | `general` | 0 | 56.64% | 66.56% | -9.92% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.78% | 84.31% | -4.53% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 97.26% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 76.26% | 74.64% | 1.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 80.57% | 100.00% | -19.43% |
| cab | `general` | 0 | 44.83% | 62.07% | -17.24% |
| gz | `general` | 0 | 9.83% | 26.59% | -16.76% |
| lua | `filegroups/scripts` | 0 | 66.67% | 83.33% | -16.67% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 86.05% | 99.16% | -13.11% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar | `general` | 0 | 86.67% | 93.33% | -6.67% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.58% | 99.67% | -0.09% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 97 | 99.82% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 73.54% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 5 | 80.03% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 68.09% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 58.32% | — | — |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.97% | 97.86% | -35.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| rar | `general` | 0 | 71.39% | 100.00% | -28.61% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 77.67% | 99.16% | -21.49% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| 7z | `general` | 0 | 70.97% | 90.97% | -20.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zip | `general` | 0 | 43.20% | 53.29% | -10.09% |
| tar.gz | `general` | 0 | 57.33% | 66.56% | -9.23% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 79.90% | 84.31% | -4.41% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 97.52% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 22.22% | 100.00% | -77.78% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| msi | `filetypes/msi` | 0 | 67.52% | 97.86% | -30.34% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 80.97% | 100.00% | -19.03% |
| cab | `general` | 0 | 44.83% | 62.07% | -17.24% |
| gz | `general` | 0 | 12.14% | 26.59% | -14.45% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 86.28% | 99.16% | -12.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar | `general` | 0 | 87.33% | 93.33% | -6.00% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 110 | 99.86% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 73.54% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 69.91% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 59.23% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 84.80% | 84.31% | 0.49% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 61.97% | 97.86% | -35.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| rar | `general` | 0 | 71.39% | 100.00% | -28.61% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| 7z | `general` | 0 | 70.97% | 90.97% | -20.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.71% | 53.29% | -3.58% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 80.76% | 84.31% | -3.55% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 97.52% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 31.79% | 49.13% | -17.34% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 97.85% | -5.58% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 2 | 98.91% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 60.73% | — | — |
| javascript | `filetypes/javascript` | 18 | 93.94% | — | — |
| jpeg | `filegroups/media` | 1 | 14.96% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.54% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 23 | 98.52% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 12 | 86.67% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 88.11% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 72.45% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.06% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 62.39% | 97.86% | -35.47% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| rar | `general` | 0 | 71.39% | 100.00% | -28.61% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 77.67% | 99.16% | -21.49% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| 7z | `general` | 0 | 70.97% | 90.97% | -20.00% |
| tar | `general` | 0 | 76.00% | 93.33% | -17.33% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.74% | 53.29% | -3.55% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.84% | 84.31% | -1.47% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| elf | `filegroups/native` | 0 | 96.81% | 97.86% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 97.52% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 2 | 70.83% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 31.79% | 49.13% | -17.34% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 97.85% | -5.58% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| elf | `filegroups/native` | 3 | 98.91% | 99.17% | -0.27% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 11.38% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 60.73% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 19 | 94.28% | — | — |
| jpeg | `filegroups/media` | 1 | 14.96% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 26 | 98.70% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 12 | 86.67% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.50% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 73.77% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.48% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 62.39% | 97.86% | -35.47% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| rar | `general` | 0 | 74.49% | 100.00% | -25.51% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 81.33% | 99.16% | -17.84% |
| 7z | `general` | 0 | 75.75% | 90.97% | -15.22% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 59.55% | 66.56% | -7.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.75% | 53.29% | -3.54% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.84% | 84.31% | -1.47% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 24 | 98.55% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 76.26% | 74.64% | 1.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 31.79% | 49.13% | -17.34% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| cab | `general` | 0 | 51.72% | 62.07% | -10.34% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.27% | 97.85% | -5.58% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 4 | 99.22% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 11.38% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| javascript | `filetypes/javascript` | 22 | 94.38% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 27 | 98.73% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 15 | 87.59% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.50% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 74.58% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.70% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 62.82% | 97.86% | -35.04% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| rar | `general` | 0 | 74.49% | 100.00% | -25.51% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 81.33% | 99.16% | -17.84% |
| 7z | `general` | 0 | 75.75% | 90.97% | -15.22% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 59.55% | 66.56% | -7.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.76% | 53.29% | -3.52% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.84% | 84.31% | -1.47% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 24 | 98.55% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 32.37% | 49.13% | -16.76% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 84.12% | 97.85% | -13.73% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 4 | 99.23% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 11.38% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 60.73% | — | — |
| javascript | `filetypes/javascript` | 22 | 94.44% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 29 | 98.77% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 17 | 87.64% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.50% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 75.01% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.79% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 0.00% | 62.07% | -62.07% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 63.25% | 97.86% | -34.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| rar | `general` | 0 | 74.49% | 100.00% | -25.51% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 81.33% | 99.16% | -17.84% |
| 7z | `general` | 0 | 75.75% | 90.97% | -15.22% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| tar | `general` | 0 | 81.33% | 93.33% | -12.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.78% | 53.29% | -3.51% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.84% | 84.31% | -1.47% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| elf | `filegroups/native` | 0 | 96.81% | 97.86% | -1.05% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 24 | 98.55% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 32.37% | 49.13% | -16.76% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 96.14% | 97.85% | -1.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 4 | 99.31% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 11.64% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 60.73% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 23 | 94.51% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 17 | 87.77% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 3 | 87.87% | 87.87% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 75.39% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.82% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 63.25% | 97.86% | -34.62% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.01% | 53.29% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 84.31% | -1.23% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 26.59% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.54% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 95.02% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 73.54% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 74.75% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 32.95% | 49.13% | -16.18% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 96.14% | 97.85% | -1.72% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 4 | 99.82% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 5 | 99.32% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 11.64% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 60.73% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 25 | 94.66% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 1 | 14.96% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 35 | 99.03% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 75.49% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 17 | 87.99% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 3 | 87.87% | 87.87% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 75.53% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 60.92% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.10% | 97.86% | -33.76% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 82.85% | 99.16% | -16.31% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 76.81% | 90.97% | -14.16% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| tar.gz | `general` | 0 | 62.58% | 66.56% | -3.98% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.01% | 53.29% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 84.31% | -1.23% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.97% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 76.26% | 74.64% | 1.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 81.78% | 100.00% | -18.22% |
| gz | `general` | 3 | 32.95% | 49.13% | -16.18% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.16% | -11.66% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 96.14% | 97.85% | -1.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 99.34% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 11.64% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 26 | 94.69% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 38 | 99.06% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 12 | 93.00% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 19 | 89.13% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 3 | 87.87% | 87.87% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 75.76% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 61.05% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.10% | 97.86% | -33.76% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 82.85% | 99.16% | -16.31% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 76.81% | 90.97% | -14.16% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 60.56% | 66.56% | -6.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.05% | 53.29% | -2.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 84.31% | -1.23% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 81.92% | 100.00% | -18.08% |
| gz | `general` | 3 | 32.95% | 49.13% | -16.18% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| zst | `general` | 0 | 86.74% | 99.16% | -12.42% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 96.14% | 97.85% | -1.72% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 4 | 99.84% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 5 | 99.32% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 11.64% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 28 | 94.89% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 1 | 14.96% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 40 | 99.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 12 | 93.00% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 19 | 89.13% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 4 | 87.87% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 76.17% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 2 | 85.65% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| zip | `general` | 1 | 61.47% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.53% | 97.86% | -33.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 82.85% | 99.16% | -16.31% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 76.81% | 90.97% | -14.16% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 60.56% | 66.56% | -6.00% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.05% | 53.29% | -2.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.72% | 84.31% | -1.59% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| elf | `filegroups/native` | 0 | 96.89% | 97.86% | -0.97% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 82.19% | 100.00% | -17.81% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 84.12% | 97.85% | -13.73% |
| zst | `general` | 0 | 87.04% | 99.16% | -12.12% |
| gz | `general` | 0 | 19.08% | 26.59% | -7.51% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| cab | `general` | 0 | 55.17% | 62.07% | -6.90% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| tar | `general` | 0 | 88.67% | 93.33% | -4.67% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 6 | 99.38% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 12.40% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| javascript | `filetypes/javascript` | 29 | 94.92% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 7.80% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 41 | 99.22% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 82.10% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 8 | 83.55% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 4 | 87.87% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 77.58% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general` | 2 | 62.20% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| cab | `general` | 0 | 10.34% | 62.07% | -51.72% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| msi | `filetypes/msi` | 0 | 64.53% | 97.86% | -33.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| gz | `general` | 0 | 0.00% | 26.59% | -26.59% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| rar | `general` | 0 | 75.98% | 100.00% | -24.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 82.85% | 99.16% | -16.31% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 76.81% | 90.97% | -14.16% |
| tar | `general` | 0 | 82.00% | 93.33% | -11.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 60.56% | 66.56% | -6.00% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| zip | `general` | 0 | 51.05% | 53.29% | -2.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.21% | 84.31% | -1.10% |
| elf | `filegroups/native` | 0 | 96.89% | 97.86% | -0.97% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 34 | 98.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 2 | 71.67% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| rar | `general` | 0 | 82.19% | 100.00% | -17.81% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 84.12% | 97.85% | -13.73% |
| zst | `general` | 0 | 87.04% | 99.16% | -12.12% |
| gz | `general` | 0 | 19.08% | 26.59% | -7.51% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| cab | `general` | 0 | 55.17% | 62.07% | -6.90% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.83% | 7.84% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `general,filegroups/native,filetypes/elf` | 7 | 99.41% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 12.40% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `filetypes/javascript` | 30 | 94.99% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 47 | 99.30% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 82.10% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 8 | 83.63% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 4 | 87.87% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 77.73% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general` | 2 | 62.31% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 20.69% | 62.07% | -41.38% |
| msi | `filetypes/msi` | 0 | 64.53% | 97.86% | -33.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 2.31% | 26.59% | -24.28% |
| rar | `general` | 0 | 77.19% | 100.00% | -22.81% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 83.69% | 99.16% | -15.47% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 78.41% | 90.97% | -12.57% |
| tar | `general` | 0 | 83.33% | 93.33% | -10.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 97.86% | -4.72% |
| tar.gz | `general` | 0 | 62.26% | 66.56% | -4.30% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 49.95% | 53.29% | -3.33% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.33% | 84.31% | -0.98% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 40 | 99.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| html | `general,filegroups/documents` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| rar | `general` | 0 | 82.19% | 100.00% | -17.81% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 84.12% | 97.85% | -13.73% |
| zst | `general` | 0 | 87.04% | 99.16% | -12.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| gz | `general` | 0 | 19.65% | 26.59% | -6.94% |
| cab | `general` | 0 | 55.17% | 62.07% | -6.90% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.83% | 7.84% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 6 | 99.39% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 5 | 12.49% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 30 | 95.13% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 4 | 97.85% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.58% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 49 | 99.32% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 82.10% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 8 | 83.77% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 5 | 88.60% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 78.07% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general` | 2 | 62.41% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 83.33% | -83.33% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| xlsx | `filegroups/documents` | 0 | 29.32% | 90.17% | -60.84% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 20.69% | 62.07% | -41.38% |
| msi | `filetypes/msi` | 0 | 64.96% | 97.86% | -32.91% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 68.67% | 97.85% | -29.18% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 2.31% | 26.59% | -24.28% |
| rar | `general` | 0 | 77.19% | 100.00% | -22.81% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.66% | 65.90% | -20.23% |
| zst | `general` | 0 | 83.69% | 99.16% | -15.47% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| 7z | `general` | 0 | 78.41% | 90.97% | -12.57% |
| tar | `general` | 0 | 83.33% | 93.33% | -10.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 3.74% | 12.85% | -9.12% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| tar.gz | `general` | 0 | 62.26% | 66.56% | -4.30% |
| jar | `filetypes/jar` | 0 | 56.54% | 60.21% | -3.66% |
| zip | `general` | 0 | 50.01% | 53.29% | -3.28% |
| lnk | `general,filetypes/lnk` | 0 | 49.04% | 51.72% | -2.68% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 94.77% | 96.99% | -2.22% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| elf | `filegroups/native` | 0 | 96.89% | 97.86% | -0.97% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.46% | 84.31% | -0.86% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| go | `general,filetypes/go` | 0 | 0.85% | 1.19% | -0.34% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 99.46% | 99.67% | -0.21% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 88.33% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 40 | 99.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.48% | 6.44% | 0.03% |
| package.json | `general,filegroups/config` | 0 | 91.68% | 91.59% | 0.09% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.15% | 0.00% | 0.15% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 73.58% | 72.99% | 0.59% |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 60.05% | 59.30% | 0.75% |
| vbs | `general,filetypes/vbs` | 0 | 27.71% | 26.84% | 0.87% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 89.69% | 87.79% | 1.91% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 39.69% | 35.80% | 3.89% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 70.45% | 52.27% | 18.18% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 72.41% | -72.41% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 83.33% | -50.00% |
| crx | `general` | 0 | 57.14% | 100.00% | -42.86% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| doc | `general,filegroups/documents` | 0 | 72.18% | 99.61% | -27.43% |
| rar | `general` | 0 | 82.32% | 100.00% | -17.68% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 85.71% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 84.12% | 97.85% | -13.73% |
| zst | `general` | 0 | 87.12% | 99.16% | -12.04% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.52% | 24.79% | -7.26% |
| gz | `general` | 0 | 19.65% | 26.59% | -6.94% |
| c | `general,filetypes/c` | 0 | 7.02% | 12.85% | -5.83% |
| 7z | `general` | 0 | 87.26% | 90.97% | -3.72% |
| jpeg | `general,filegroups/media` | 0 | 12.60% | 14.17% | -1.57% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| tar | `general` | 0 | 92.67% | 93.33% | -0.67% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| pkg-info | `filetypes/pkg-info` | 0 | 98.43% | 98.75% | -0.31% |
| unknown | `general` | 0 | 0.00% | 0.22% | -0.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 96.85% | 96.99% | -0.14% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 7.83% | 7.84% | -0.01% |
| batch | `general,filegroups/scripts,filetypes/batch` | 1 | 99.72% | — | — |
| cab | `general` | 1 | 62.07% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 79.55% | — | — |
| elf | `filegroups/native` | 7 | 99.39% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 10 | 22.43% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `filetypes/jar` | 1 | 59.16% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 50.87% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 31 | 95.13% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 95.42% | — | — |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| msi | `general,filetypes/msi` | 0 | 97.86% | 97.86% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 97.32% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 51 | 99.40% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 92.59% | 92.59% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 89.24% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 82.10% | — | — |
| pptx | `filegroups/documents` | 0 | 22.73% | 22.73% | 0.00% |
| python | `filegroups/scripts` | 8 | 83.99% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `filegroups/scripts` | 5 | 88.60% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 2 | 78.71% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 33.77% | — | — |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 12 | 100.00% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.74% | 2.74% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general` | 2 | 62.62% | — | — |
| xls | `general,filegroups/documents` | 0 | 96.07% | 95.37% | 0.69% |
| png | `general,filegroups/media,filetypes/png` | 0 | 6.24% | 0.00% | 6.24% |
| lnk | `general,filetypes/lnk` | 0 | 69.73% | 51.72% | 18.01% |
