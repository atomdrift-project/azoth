# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 592885 (213106 malware, 379779 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 113044 | 18905 | `general,filegroups/native,filetypes/pe` | general: 44.89% | 1 | 64.13% | — | general: 66.90% | 1.000 | 1.000 |
| pdf | 21804 | 1734 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 6.67% | 0 | 6.41% | -0.26% | filetypes/pdf: 96.53% | 1.000 | 0.999 |
| batch | 21129 | 427 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 98.76% | 0 | 98.83% | 0.07% | filegroups/scripts: 99.01% | 1.000 | 1.000 |
| javascript | 10627 | 59718 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 58.38% | 8 | 76.34% | — | filegroups/scripts: 75.73% | 0.985 | 0.982 |
| elf | 8986 | 17158 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 91.69% | 2 | 93.46% | — | filetypes/elf: 93.40% | 1.000 | 1.000 |
| zip | 7409 | 870 | `general` | general: 48.31% | 0 | 40.61% | -7.69% | general: 65.78% | — | 0.990 |
| tar.gz | 3466 | 1676 | `general` | general: 61.57% | 1 | 61.57% | — | general: 80.32% | — | 0.996 |
| kotlin | 2903 | 5360 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 48.67% | 1 | 59.94% | — | filegroups/source: 72.06% | 0.970 | 0.970 |
| python | 2273 | 16343 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 48.44% | 2 | 65.33% | — | filetypes/python: 68.37% | 0.979 | 0.971 |
| xlsx | 2237 | 12 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 91.10% | 0 | 29.01% | -62.09% | general: 91.69% | 0.981 | 0.996 |
| package.json | 2163 | 1440 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 92.05% | 0 | 86.78% | -5.27% | general: 99.31% | 1.000 | 1.000 |
| c | 1766 | 66650 | `general,filegroups/source,filetypes/c` | filegroups/source: 11.38% | 1 | 13.08% | — | filetypes/c: 13.53% | 0.419 | 0.311 |
| unknown | 1354 | 2020 | `general` | general: 2.95% | 0 | 0.00% | -2.95% | general: 20.90% | — | 0.770 |
| zst | 1312 | 2034 | `general` | general: 99.24% | 0 | 87.50% | -11.74% | general: 100.00% | — | 1.000 |
| xls | 1297 | 48 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 95.84% | 0 | 92.44% | -3.39% | filegroups/documents: 96.53% | 1.000 | 1.000 |
| doc | 1287 | 3 | `general,filegroups/documents` | general: 99.69% | 0 | 90.99% | -8.70% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 114 | `general,filetypes/pkg-info` | general: 97.02% | 0 | 97.02% | 0.00% | filetypes/pkg-info: 99.69% | 1.000 | 1.000 |
| go | 1177 | 11867 | `general,filegroups/source,filetypes/go` | filegroups/source: 1.70% | 0 | 1.78% | 0.08% | filetypes/go: 4.84% | 0.369 | 0.630 |
| shell | 819 | 5696 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 81.32% | 1 | 85.10% | — | filetypes/shell: 86.32% | 0.983 | 0.968 |
| rar | 741 | 0 | `general` | general: 100.00% | 0 | 72.20% | -27.80% | general: 100.00% | — | — |
| png | 657 | 14393 | `general,filegroups/media,filetypes/png` | filegroups/media: 1.07% | 1 | 1.07% | — | general: 8.98% | 0.163 | 0.185 |
| 7z | 565 | 12 | `general` | general: 89.56% | 0 | 75.04% | -14.51% | general: 90.80% | — | 0.999 |
| php | 512 | 10870 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 70.12% | 0 | 68.95% | -1.17% | filetypes/php: 72.66% | 0.917 | 0.911 |
| vbs | 463 | 423 | `general,filetypes/vbs` | filetypes/vbs: 25.27% | 0 | 25.70% | 0.43% | filetypes/vbs: 48.16% | 0.977 | 0.977 |
| xml | 292 | 18398 | `general,filegroups/config,filetypes/xml` | filegroups/config: 3.42% | 2 | 3.08% | — | general: 5.14% | 0.153 | 0.164 |
| macho | 262 | 1383 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 88.17% | 0 | 87.02% | -1.15% | filetypes/macho: 93.89% | 0.997 | 0.989 |
| lnk | 261 | 127 | `general,filetypes/lnk` | filetypes/lnk: 52.11% | 0 | 48.66% | -3.45% | filetypes/lnk: 70.50% | 0.975 | 0.975 |
| powershell | 260 | 274 | `general,filegroups/scripts,filetypes/powershell` | general: 24.23% | 0 | 29.62% | 5.38% | filetypes/powershell: 74.62% | 0.974 | 0.968 |
| msi | 235 | 13 | `general,filetypes/msi` | filetypes/msi: 97.45% | 0 | 76.17% | -21.28% | filetypes/msi: 97.87% | 1.000 | 0.997 |
| csharp | 234 | 7572 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 31.20% | 0 | 27.78% | -3.42% | filegroups/source: 32.05% | 0.607 | 0.596 |
| python-bytecode | 233 | 3910 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.85% | 0 | 93.56% | -4.29% | filetypes/python-bytecode: 97.85% | 0.995 | 0.995 |
| ole | 229 | 665 | `general,filegroups/documents,filetypes/ole` | general: 91.27% | 0 | 91.27% | 0.00% | general: 95.63% | 0.993 | 0.993 |
| rtf | 215 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.67% | 0 | 97.67% | 0.00% | general: 98.14% | 1.000 | 1.000 |
| jar | 192 | 249 | `general,filetypes/jar` | general: 57.81% | 0 | 57.29% | -0.52% | filetypes/jar: 77.08% | 0.979 | 0.974 |
| docx | 176 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 54.55% | 0 | 71.59% | 17.05% | general: 85.80% | 0.976 | 0.974 |
| gz | 173 | 6467 | `general` | general: 29.48% | 0 | 28.32% | -1.16% | general: 38.73% | — | 0.662 |
| java_class | 173 | 47394 | `general,filegroups/portable,filetypes/java_class` | general: 65.32% | 3 | 73.41% | -9.83% | filegroups/portable: 83.24% | 0.946 | 0.946 |
| rust | 164 | 9604 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 2.44% | 0 | 2.44% | 0.00% | filegroups/source: 3.05% | 0.119 | 0.065 |
| text | 160 | 7993 | `general,filetypes/text` | general: 11.88% | 0 | 12.50% | 0.63% | filetypes/text: 15.62% | 0.253 | 0.235 |
| tar | 150 | 51 | `general` | general: 94.00% | 0 | 68.67% | -25.33% | general: 95.33% | — | 0.994 |
| jpeg | 128 | 1319 | `general,filegroups/media,filetypes/jpeg` | general: 14.06% | 0 | 13.28% | -0.78% | filegroups/media: 18.75% | 0.321 | 0.334 |
| plist | 68 | 1544 | `general,filegroups/config,filetypes/plist` | general: 2.94% | 0 | 2.94% | 0.00% | general: 5.88% | 0.118 | 0.180 |
| data | 58 | 1157 | `general` | general: 68.97% | 0 | 0.00% | -68.97% | general: 81.03% | — | 0.823 |
| cab | 29 | 12 | `general` | general: 34.48% | 0 | 3.45% | -31.03% | general: 100.00% | — | 0.950 |
| perl | 27 | 3960 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 81.48% | 1 | 81.48% | — | filegroups/scripts: 85.19% | 0.921 | 0.925 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filegroups/documents: 22.73% | 0 | 9.09% | -13.64% | general: 31.82% | 0.328 | 0.591 |
| makefile | 17 | 2741 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 5.88% | 0.058 | 0.055 |
| groovy | 15 | 648 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.038 | 0.037 |
| chm | 9 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| crx | 7 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 709 | `general` | general: 28.57% | 0 | 0.00% | -28.57% | general: 71.43% | — | 0.586 |
| ruby | 7 | 2945 | `general,filegroups/scripts,filetypes/ruby` | general: 85.71% | 0 | 28.57% | -57.14% | general: 100.00% | 0.831 | 0.831 |
| html | 6 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 16.67% | -83.33% | general: 100.00% | — | 1.000 |
| lua | 6 | 1919 | `general,filegroups/scripts` | general: 50.00% | 0 | 33.33% | -16.67% | filegroups/scripts: 66.67% | — | 0.661 |
| java | 4 | 4192 | `general,filegroups/source` | general: 50.00% | 0 | 50.00% | 0.00% | filegroups/source: 75.00% | — | 0.690 |
| xz | 4 | 3478 | `general` | general: 25.00% | 0 | 25.00% | 0.00% | general: 50.00% | — | 0.406 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 65 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.050 |
| applescript | 2 | 32 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 2 | 1405 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.501 |
| chrome-manifest | 2 | 46 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.643 |
| github-actions | 1 | 707 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 100.00% | — | 0.250 |
| objc | 1 | 2308 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 134 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.008 |
| tar.bz2 | 1 | 21 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| chrome-manifest | `` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `` | 0 | 0.00% | 50.00% | -50.00% |
| zip | `` | 0 | 0.00% | 48.31% | -48.31% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| gz | `general` | 0 | 0.00% | 29.48% | -29.48% |
| deb | `` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| zst | `general` | 0 | 79.42% | 99.24% | -19.82% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.59% | 70.12% | -19.53% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.21% | 31.20% | -5.98% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 60.69% | 65.32% | -4.62% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.85% | 11.38% | -4.53% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| tar.gz | `general` | 0 | 57.99% | 61.57% | -3.58% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| unknown | `` | 0 | 0.00% | 2.95% | -2.95% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.78% | 91.69% | -1.90% |
| plist | `filegroups/config,filetypes/plist` | 0 | 1.47% | 2.94% | -1.47% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| xls | `general,filegroups/documents` | 0 | 95.14% | 95.84% | -0.69% |
| xml | `general,filegroups/config` | 0 | 2.74% | 3.42% | -0.68% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 57.74% | 58.38% | -0.64% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.36% | 1.70% | -0.34% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.07% | 1.07% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 98.51% | 97.02% | 1.49% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 49.37% | 44.89% | 4.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 55.04% | 48.44% | 6.60% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

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
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.41% | 70.12% | -3.71% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general` | 2 | 8.98% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 65.33% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.55% | 11.38% | 0.17% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| tar | `general` | 0 | 44.00% | 94.00% | -50.00% |
| cab | `general` | 0 | 0.00% | 34.48% | -34.48% |
| rar | `general` | 0 | 66.26% | 100.00% | -33.74% |
| gz | `general` | 0 | 0.00% | 29.48% | -29.48% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| zst | `general` | 0 | 70.73% | 99.24% | -28.51% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| 7z | `general` | 0 | 69.20% | 89.56% | -20.35% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.59% | 70.12% | -19.53% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zip | `general` | 0 | 38.86% | 48.31% | -9.45% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| tar.gz | `general` | 0 | 55.14% | 61.57% | -6.43% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.21% | 31.20% | -5.98% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.78% | 91.69% | -1.90% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.02% | 11.38% | -1.36% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| xml | `general,filegroups/config` | 0 | 2.74% | 3.42% | -0.68% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.36% | 1.70% | -0.34% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 66.47% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.75% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.07% | 1.07% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 49.37% | 44.89% | 4.49% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 55.04% | 48.44% | 6.60% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.22% | 100.00% | -25.78% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 76.00% | 94.00% | -18.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 77.35% | 89.56% | -12.21% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| zip | `general` | 0 | 44.82% | 48.31% | -3.48% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 84.39% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.51% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.84% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| tar | `general` | 0 | 50.67% | 94.00% | -43.33% |
| rar | `general` | 0 | 66.94% | 100.00% | -33.06% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| zst | `general` | 0 | 72.87% | 99.24% | -26.37% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 50.59% | 70.12% | -19.53% |
| 7z | `general` | 0 | 71.15% | 89.56% | -18.41% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| jpeg | `filetypes/jpeg` | 0 | 1.56% | 14.06% | -12.50% |
| zip | `general` | 0 | 39.26% | 48.31% | -9.04% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.21% | 31.20% | -5.98% |
| tar.gz | `general` | 0 | 55.77% | 61.57% | -5.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.02% | 11.38% | -1.36% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| xml | `general,filegroups/config` | 0 | 2.74% | 3.42% | -0.68% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.36% | 1.70% | -0.34% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.71% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 2 | 69.94% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.75% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 61.96% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.07% | 1.07% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 64.06% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 14.29% | 100.00% | -85.71% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| cab | `general` | 0 | 6.90% | 34.48% | -27.59% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 78.81% | 100.00% | -21.19% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| tar | `general` | 0 | 82.00% | 94.00% | -12.00% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 79.82% | 89.56% | -9.73% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.77% | 31.20% | -0.43% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.53% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 2.63% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 29.48% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 5 | 86.13% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 77.16% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.66% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 61.96% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 70.90% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `filegroups/scripts,filetypes/python` | 7 | 70.48% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.57% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| elf | `general,filegroups/native,filetypes/elf` | 3 | 93.52% | 93.40% | 0.12% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.76% | 92.05% | 1.71% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| tar | `general` | 0 | 62.00% | 94.00% | -32.00% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 76.60% | 99.24% | -22.64% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| 7z | `general` | 0 | 72.74% | 89.56% | -16.81% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| jpeg | `filetypes/jpeg` | 0 | 1.56% | 14.06% | -12.50% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 66.20% | 75.73% | -9.53% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 62.11% | 70.12% | -8.01% |
| zip | `general` | 0 | 40.61% | 48.31% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.21% | 31.20% | -5.98% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| tar.gz | `general` | 0 | 56.69% | 61.57% | -4.88% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.02% | 11.38% | -1.36% |
| rust | `general,filetypes/rust` | 0 | 1.22% | 2.44% | -1.22% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| xml | `general,filegroups/config` | 0 | 2.74% | 3.42% | -0.68% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.36% | 1.70% | -0.34% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.79% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 61.96% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.07% | 1.07% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 64.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 11.11% | 100.00% | -88.89% |
| crx | `general` | 0 | 28.57% | 100.00% | -71.43% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| powershell | `filetypes/powershell` | 0 | 0.00% | 24.23% | -24.23% |
| cab | `general` | 0 | 10.34% | 34.48% | -24.14% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 80.57% | 100.00% | -19.43% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 80.53% | 89.56% | -9.03% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| tar | `general` | 0 | 85.33% | 94.00% | -8.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| zip | `general` | 0 | 45.13% | 48.31% | -3.17% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.77% | 31.20% | -0.43% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 93.69% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 3.14% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 29.48% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 5 | 89.60% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 77.16% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.66% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 89.69% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.13% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 64.76% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 70.90% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `filegroups/scripts,filetypes/python` | 8 | 71.62% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.57% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| c | `general,filegroups/source,filetypes/c` | 3 | 13.65% | 13.53% | 0.11% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| tar | `general` | 0 | 62.00% | 94.00% | -32.00% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| zst | `general` | 0 | 76.60% | 99.24% | -22.64% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| 7z | `general` | 0 | 72.74% | 89.56% | -16.81% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| jpeg | `filetypes/jpeg` | 0 | 1.56% | 14.06% | -12.50% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 66.20% | 75.73% | -9.53% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| zip | `general` | 0 | 40.61% | 48.31% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.21% | 31.20% | -5.98% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 64.84% | 70.12% | -5.27% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| tar.gz | `general` | 0 | 56.69% | 61.57% | -4.88% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.31% | 11.38% | -1.08% |
| text | `general,filetypes/text` | 0 | 11.25% | 11.88% | -0.62% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.79% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 61.96% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.07% | 1.07% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 64.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general` | 1 | 2.74% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 22.22% | 100.00% | -77.78% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 57.14% | 85.71% | -28.57% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 81.65% | 100.00% | -18.35% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 81.42% | 89.56% | -8.14% |
| tar | `general` | 0 | 86.00% | 94.00% | -8.00% |
| cab | `general` | 0 | 27.59% | 34.48% | -6.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| zip | `general` | 0 | 45.32% | 48.31% | -2.98% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.77% | 31.20% | -0.43% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 5 | 13.82% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 5 | 94.18% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 4 | 6.12% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 30.06% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 89.60% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 9 | 77.42% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.66% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.13% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 69.69% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.09% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 77.96% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `filetypes/rust` | 1 | 2.44% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.57% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.60% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| tar | `general` | 0 | 62.00% | 94.00% | -32.00% |
| rar | `general` | 0 | 68.15% | 100.00% | -31.85% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| zst | `general` | 0 | 76.60% | 99.24% | -22.64% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| 7z | `general` | 0 | 72.74% | 89.56% | -16.81% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| jpeg | `filetypes/jpeg` | 0 | 1.56% | 14.06% | -12.50% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| zip | `general` | 0 | 40.61% | 48.31% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 64.84% | 70.12% | -5.27% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| tar.gz | `general` | 0 | 56.69% | 61.57% | -4.88% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 65.29% | 68.37% | -3.08% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.31% | 11.38% | -1.08% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 4 | 69.59% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 62.95% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 11.88% | 11.88% | 0.00% |
| xml | `general` | 1 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 82.78% | 81.32% | 1.47% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 82.19% | 100.00% | -17.81% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 81.77% | 89.56% | -7.79% |
| tar | `general` | 0 | 87.33% | 94.00% | -6.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| cab | `general` | 0 | 31.03% | 34.48% | -3.45% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| zip | `general` | 0 | 45.90% | 48.31% | -2.40% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 7 | 17.16% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 31.20% | 31.20% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 5 | 94.28% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 30.06% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 6 | 90.17% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 77.75% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 5 | 61.45% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.13% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 71.69% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.09% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 2 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 77.96% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 1 | 2.44% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 4 | 87.06% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.60% | — | — |
| text | `general,filetypes/text` | 1 | 11.88% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| zst | `general` | 0 | 79.42% | 99.24% | -19.82% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.99% | 97.85% | -6.87% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 64.84% | 70.12% | -5.27% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| zip | `general` | 0 | 43.81% | 48.31% | -4.49% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 77.78% | 81.48% | -3.70% |
| tar.gz | `general` | 0 | 57.99% | 61.57% | -3.58% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 65.29% | 68.37% | -3.08% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.99% | 11.38% | -0.40% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 62.95% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 82.78% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 11.88% | 11.88% | 0.00% |
| xml | `general` | 1 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 48.67% | 4.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 82.32% | 100.00% | -17.68% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 81.77% | 89.56% | -7.79% |
| tar | `general` | 0 | 87.33% | 94.00% | -6.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| zip | `general` | 0 | 46.12% | 48.31% | -2.19% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 7 | 14.33% | — | — |
| cab | `general` | 0 | 34.48% | 34.48% | 0.00% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 31.20% | 31.20% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 94.57% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 6 | 6.71% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 30.06% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 6 | 90.17% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 77.95% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 60.66% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.13% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 73.20% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.09% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 6 | 8.83% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 78.35% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 4 | 87.06% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.63% | — | — |
| text | `general,filetypes/text` | 1 | 11.88% | — | — |
| xml | `general` | 2 | 4.45% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| zip | `general` | 0 | 43.81% | 48.31% | -4.49% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.41% | 70.12% | -3.71% |
| tar.gz | `general` | 0 | 57.99% | 61.57% | -3.58% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 65.29% | 68.37% | -3.08% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.99% | 11.38% | -0.40% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 57.46% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| rar | `general` | 0 | 82.32% | 100.00% | -17.68% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 81.77% | 89.56% | -7.79% |
| tar | `general` | 0 | 87.33% | 94.00% | -6.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| zip | `general` | 0 | 46.28% | 48.31% | -2.02% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 8 | 14.38% | — | — |
| cab | `general` | 0 | 34.48% | 34.48% | 0.00% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 94.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 6 | 6.97% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 31.79% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 6 | 90.17% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 78.06% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 60.66% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.13% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 32.31% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 74.07% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.09% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 6 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 78.93% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 4 | 87.06% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.63% | — | — |
| text | `general,filetypes/text` | 2 | 12.50% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 32.61% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 31.62% | 31.20% | 0.43% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

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
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.41% | 70.12% | -3.71% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `filetypes/macho` | 0 | 86.64% | 88.17% | -1.53% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general` | 2 | 8.98% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 65.33% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.55% | 11.38% | 0.17% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 0.43% | 97.45% | -97.02% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| rar | `general` | 0 | 82.32% | 100.00% | -17.68% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 82.30% | 89.56% | -7.26% |
| tar | `general` | 0 | 87.33% | 94.00% | -6.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| zip | `general` | 0 | 46.52% | 48.31% | -1.78% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source,filetypes/c` | 9 | 14.44% | — | — |
| cab | `general` | 0 | 34.48% | 34.48% | 0.00% |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 95.03% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 6 | 6.97% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 31.79% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 7 | 90.75% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 15 | 78.73% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 95.70% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 74.72% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.09% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 7 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 78.93% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 1 | 2.44% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.63% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 32.61% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 87.42% | 86.32% | 1.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

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
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 68.95% | 70.12% | -1.17% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 65.33% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 0.85% | 97.45% | -96.60% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| chm | `general` | 0 | 33.33% | 100.00% | -66.67% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| rar | `general` | 0 | 82.86% | 100.00% | -17.14% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 82.48% | 89.56% | -7.08% |
| tar | `general` | 0 | 88.00% | 94.00% | -6.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| gz | `general` | 3 | 35.26% | 38.73% | -3.47% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| zip | `general` | 0 | 47.71% | 48.31% | -0.59% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source,filetypes/c` | 13 | 14.44% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 95.05% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 7 | 7.65% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 9 | 90.75% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 15 | 79.01% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 9 | 76.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.29% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 7 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 78.93% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 2.44% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 32.61% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 87.42% | 86.32% | 1.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

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
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.20% | 100.00% | -27.80% |
| tar | `general` | 0 | 68.67% | 94.00% | -25.33% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| 7z | `general` | 0 | 75.04% | 89.56% | -14.51% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 73.41% | 83.24% | -9.83% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.34% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 65.33% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `filetypes/rust` | 0 | 2.44% | 2.44% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 7.23% | 97.45% | -90.21% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| chm | `general` | 0 | 44.44% | 100.00% | -55.56% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| rar | `general` | 0 | 83.13% | 100.00% | -16.87% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 82.83% | 89.56% | -6.73% |
| tar | `general` | 0 | 88.00% | 94.00% | -6.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| gz | `general` | 3 | 35.26% | 38.73% | -3.47% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| zip | `general` | 0 | 47.83% | 48.31% | -0.47% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source,filetypes/c` | 13 | 14.50% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 6 | 95.14% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `filetypes/java_class` | 6 | 90.75% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 79.54% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 1 | 13.28% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 1 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 96.72% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 10 | 76.33% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 71.29% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 7 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 10 | 78.93% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 32.61% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.82% | 100.00% | -26.18% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 75.33% | 94.00% | -18.67% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 76.46% | 89.56% | -13.10% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.78% | 31.20% | -3.42% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 82.66% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.09% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 2.44% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 12.77% | 97.45% | -84.68% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 83.27% | 100.00% | -16.73% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 82.83% | 89.56% | -6.73% |
| tar | `general` | 0 | 88.00% | 94.00% | -6.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| gz | `general` | 3 | 35.26% | 38.73% | -3.47% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| zip | `general` | 0 | 48.01% | 48.31% | -0.30% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source,filetypes/c` | 15 | 14.84% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 8 | 95.33% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filetypes/java_class` | 9 | 91.33% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 79.54% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.35% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 10 | 76.59% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 12 | 79.10% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `general,filegroups/documents` | 0 | 16.67% | 100.00% | -83.33% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 85.71% | -57.14% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.82% | 100.00% | -26.18% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 75.33% | 94.00% | -18.67% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 76.46% | 89.56% | -13.10% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 82.66% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.13% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 2.44% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 3.08% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 20.00% | 97.45% | -77.45% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| rar | `general` | 0 | 83.54% | 100.00% | -16.46% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.01% | 89.56% | -6.55% |
| tar | `general` | 0 | 88.67% | 94.00% | -5.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| xml | `general` | 3 | 4.45% | 5.14% | -0.68% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| zip | `general` | 0 | 48.08% | 48.31% | -0.23% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filegroups/source,filetypes/c` | 15 | 14.84% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 8 | 95.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `filegroups/portable,filetypes/java_class` | 9 | 91.91% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 79.60% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.35% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 11 | 76.94% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 13 | 79.19% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.82% | 100.00% | -26.18% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 75.33% | 94.00% | -18.67% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 76.46% | 89.56% | -13.10% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 82.66% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 64.13% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 23.83% | 97.45% | -73.62% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| rar | `general` | 0 | 83.54% | 100.00% | -16.46% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.01% | 89.56% | -6.55% |
| tar | `general` | 0 | 88.67% | 94.00% | -5.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| xml | `general` | 3 | 4.79% | 5.14% | -0.34% |
| zip | `general` | 0 | 48.20% | 48.31% | -0.11% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 17 | 16.93% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 8 | 95.95% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 11 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 79.62% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.35% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 12 | 78.38% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 13 | 79.19% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.82% | 100.00% | -26.18% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 75.33% | 94.00% | -18.67% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 76.64% | 89.56% | -12.92% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| zip | `general` | 0 | 44.81% | 48.31% | -3.50% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.41% | 6.67% | -0.26% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.46% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.20% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 83.82% | 83.24% | 0.58% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| msi | `filetypes/msi` | 0 | 25.96% | 97.45% | -71.49% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| rar | `general` | 0 | 83.67% | 100.00% | -16.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.19% | 89.56% | -6.37% |
| tar | `general` | 0 | 88.67% | 94.00% | -5.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.56% | 97.85% | -4.29% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| text | `general,filetypes/text` | 3 | 15.00% | 15.62% | -0.63% |
| xml | `general` | 3 | 4.79% | 5.14% | -0.34% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 18 | 17.38% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 9 | 96.09% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 12 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 25 | 80.85% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.39% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 12 | 78.63% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 13 | 79.19% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 48.47% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.82% | 100.00% | -26.18% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 75.33% | 94.00% | -18.67% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 76.64% | 89.56% | -12.92% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| zip | `general` | 0 | 44.82% | 48.31% | -3.48% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.31% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.21% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 83.82% | 83.24% | 0.58% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| msi | `filetypes/msi` | 0 | 30.21% | 97.45% | -67.23% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| rar | `general` | 0 | 83.67% | 100.00% | -16.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.54% | 89.56% | -6.02% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 18 | 17.38% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 11 | 96.27% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 25 | 80.93% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.39% | — | — |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 13 | 79.02% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 14 | 79.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 2 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.03% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 48.68% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.22% | 100.00% | -25.78% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 76.00% | 94.00% | -18.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 77.35% | 89.56% | -12.21% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| zip | `general` | 0 | 44.82% | 48.31% | -3.48% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 84.39% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.51% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| msi | `filetypes/msi` | 0 | 33.62% | 97.45% | -63.83% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 83.67% | 100.00% | -16.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.54% | 89.56% | -6.02% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 19 | 18.06% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 11 | 96.55% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 1 | 57.81% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 25 | 81.20% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.39% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 13 | 79.90% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 4 | 72.46% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 14 | 79.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `filetypes/rust` | 3 | 3.05% | 3.05% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 87.67% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 1 | 61.94% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.22% | 100.00% | -25.78% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 76.00% | 94.00% | -18.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 77.35% | 89.56% | -12.21% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 86.78% | 92.05% | -5.27% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| zip | `general` | 0 | 44.82% | 48.31% | -3.48% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.34% | 31.20% | -0.85% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.08% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 84.39% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| msi | `filetypes/msi` | 0 | 35.74% | 97.45% | -61.70% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 83.67% | 100.00% | -16.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 83.89% | 89.56% | -5.66% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| zip | `general` | 0 | 44.96% | 48.31% | -3.35% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `filetypes/c` | 19 | 18.06% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 11 | 96.57% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 2 | 58.33% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 25 | 81.35% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.63% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 13 | 80.39% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 6 | 73.83% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 15 | 79.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 4 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 87.67% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 32.05% | 31.20% | 0.85% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.22% | 100.00% | -25.78% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| tar | `general` | 0 | 76.00% | 94.00% | -18.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| 7z | `general` | 0 | 77.35% | 89.56% | -12.21% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| zip | `general` | 0 | 44.88% | 48.31% | -3.43% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 29.06% | 31.20% | -2.14% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.53% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 84.39% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.76% | 92.05% | 1.71% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| msi | `filetypes/msi` | 0 | 36.60% | 97.45% | -60.85% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 83.67% | 100.00% | -16.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 84.07% | 89.56% | -5.49% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 18.69% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 12 | 96.59% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 2 | 58.33% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 26 | 81.49% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 60.66% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 80.72% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 6 | 73.83% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 8 | 9.13% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 74.62% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 15 | 79.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 4 | 3.05% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 87.67% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 62.29% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.34% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 75.03% | 100.00% | -24.97% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar | `general` | 0 | 78.67% | 94.00% | -15.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 77.88% | 89.56% | -11.68% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| zip | `general` | 0 | 44.90% | 48.31% | -3.40% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| gz | `general` | 0 | 28.32% | 29.48% | -1.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 69.34% | 70.12% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.77% | 31.20% | -0.43% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.53% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 4 | 84.97% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 76.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 66.58% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 5 | 69.38% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.76% | 92.05% | 1.71% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| msi | `filetypes/msi` | 0 | 38.72% | 97.45% | -58.72% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 83.94% | 100.00% | -16.06% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 84.25% | 89.56% | -5.31% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 94.42% | 97.85% | -3.43% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 18.69% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 13 | 96.66% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 5 | 6.29% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 2 | 58.33% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 28 | 81.61% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 61.01% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 80.88% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 6 | 73.83% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 9 | 9.13% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 74.62% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 15 | 79.28% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 2 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 87.91% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 63.16% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.45% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 68.97% | -68.97% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| cab | `general` | 0 | 3.45% | 34.48% | -31.03% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 75.03% | 100.00% | -24.97% |
| msi | `general,filetypes/msi` | 0 | 76.17% | 97.45% | -21.28% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar | `general` | 0 | 78.67% | 94.00% | -15.33% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| 7z | `general` | 0 | 77.88% | 89.56% | -11.68% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.99% | 97.85% | -3.86% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| zip | `general` | 0 | 44.90% | 48.31% | -3.40% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| unknown | `general` | 0 | 0.00% | 2.95% | -2.95% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 87.02% | 88.17% | -1.15% |
| jpeg | `filegroups/media` | 0 | 13.28% | 14.06% | -0.78% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 2.44% | -0.61% |
| jar | `general,filetypes/jar` | 0 | 57.29% | 57.81% | -0.52% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 30.77% | 31.20% | -0.43% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.53% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 93.50% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 29.48% | — | — |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| java | `general,filegroups/source` | 0 | 50.00% | 50.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 4 | 84.97% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 8 | 77.16% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 59.94% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 91.27% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.89% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 61.96% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 81.48% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 70.90% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.94% | 2.94% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 1.07% | — | — |
| python | `filegroups/scripts,filetypes/python` | 7 | 70.48% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.10% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 61.57% | — | — |
| xml | `general,filegroups/config,filetypes/xml` | 2 | 4.11% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.78% | 1.70% | 0.08% |
| vbs | `general,filetypes/vbs` | 0 | 25.70% | 25.27% | 0.43% |
| text | `general,filetypes/text` | 0 | 12.50% | 11.88% | 0.63% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 93.76% | 92.05% | 1.71% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 29.62% | 24.23% | 5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 68.97% | -67.24% |
| xlsx | `filegroups/documents` | 0 | 29.01% | 91.10% | -62.09% |
| msi | `filetypes/msi` | 0 | 39.15% | 97.45% | -58.30% |
| crx | `general` | 0 | 42.86% | 100.00% | -57.14% |
| applescript | `general` | 0 | 50.00% | 100.00% | -50.00% |
| chm | `general` | 0 | 55.56% | 100.00% | -44.44% |
| rar | `general` | 0 | 84.08% | 100.00% | -15.92% |
| pptx | `filegroups/documents` | 0 | 9.09% | 22.73% | -13.64% |
| zst | `general` | 0 | 87.50% | 99.24% | -11.74% |
| doc | `general,filegroups/documents` | 0 | 90.99% | 99.69% | -8.70% |
| 7z | `general` | 0 | 84.25% | 89.56% | -5.31% |
| tar | `general` | 0 | 89.33% | 94.00% | -4.67% |
| lnk | `general,filetypes/lnk` | 0 | 48.66% | 52.11% | -3.45% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 94.42% | 97.85% | -3.43% |
| xls | `general,filegroups/documents` | 0 | 92.44% | 95.84% | -3.39% |
| text | `general,filetypes/text` | 3 | 12.50% | 15.62% | -3.12% |
| gz | `general` | 3 | 35.84% | 38.73% | -2.89% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 3 | 95.86% | 96.53% | -0.67% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 20 | 18.69% | — | — |
| chrome-manifest | `general` | 0 | 50.00% | 50.00% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 2 | 32.05% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 13 | 96.66% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filetypes/go` | 7 | 8.07% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents` | 1 | 100.00% | — | — |
| jar | `general,filetypes/jar` | 2 | 58.33% | — | — |
| java | `general,filegroups/source` | 1 | 75.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 13 | 93.06% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 30 | 81.76% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.06% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 2 | 61.11% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filegroups/native,filetypes/macho` | 2 | 92.37% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 91.27% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filetypes/package.json` | 2 | 96.35% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 81.20% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 85.19% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 6 | 73.83% | — | — |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.02% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 9 | 9.13% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 74.62% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 16 | 79.32% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.67% | 97.67% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 85.71% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 2 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 87.91% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general` | 1 | 63.16% | — | — |
| unknown | `general` | 1 | 2.95% | — | — |
| vbs | `general,filetypes/vbs` | 1 | 35.85% | — | — |
| xml | `general` | 3 | 5.14% | 5.14% | 0.00% |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general` | 2 | 62.61% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.83% | 98.76% | 0.07% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 71.59% | 54.55% | 17.05% |
