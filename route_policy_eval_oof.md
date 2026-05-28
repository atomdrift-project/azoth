# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 633178 (221078 malware, 412100 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 115270 | 19127 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 52.99% | 1 | 69.26% | — | general: 71.93% | 1.000 | 1.000 |
| pdf | 22312 | 1743 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 7.59% | 0 | 7.30% | -0.29% | filetypes/pdf: 45.55% | 0.999 | 0.997 |
| batch | 21695 | 457 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 98.79% | 0 | 94.04% | -4.75% | filegroups/scripts: 98.94% | 1.000 | 1.000 |
| javascript | 11503 | 65282 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 71.17% | 3 | 77.99% | 0.00% | filetypes/javascript: 77.99% | 0.980 | 0.973 |
| elf | 10129 | 18869 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 86.75% | 1 | 94.16% | — | filetypes/elf: 96.01% | 1.000 | 1.000 |
| zip | 7619 | 975 | `general,filetypes/zip` | filetypes/zip: 53.79% | 0 | 52.33% | -1.46% | general: 64.56% | 0.991 | 0.990 |
| kotlin | 3992 | 5617 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 51.55% | 1 | 55.31% | — | filegroups/source: 79.76% | 0.982 | 0.973 |
| tar.gz | 3566 | 1758 | `general,filetypes/tar.gz` | filetypes/tar.gz: 82.19% | 0 | 69.27% | -12.93% | general: 86.32% | 0.999 | 0.998 |
| python | 2297 | 16990 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 38.35% | 3 | 67.22% | 0.04% | filetypes/python: 67.17% | 0.974 | 0.969 |
| xlsx | 2243 | 22 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 91.22% | 0 | 33.48% | -57.74% | filegroups/documents: 91.62% | 0.981 | 0.996 |
| package.json | 2201 | 1563 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 89.10% | 1 | 90.41% | — | filegroups/config: 99.55% | 1.000 | 0.999 |
| unknown | 1897 | 2038 | `general` | general: 47.23% | 0 | 0.00% | -47.23% | general: 47.23% | — | 0.849 |
| c | 1767 | 68272 | `general,filegroups/source,filetypes/c` | filetypes/c: 13.75% | 0 | 13.70% | -0.06% | filetypes/c: 13.98% | 0.280 | 0.279 |
| zst | 1312 | 2041 | `general` | general: 99.09% | 0 | 87.50% | -11.59% | general: 100.00% | — | 1.000 |
| xls | 1302 | 2646 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 96.16% | 0 | 95.16% | -1.00% | filetypes/xls: 96.54% | 0.999 | 0.999 |
| doc | 1287 | 4 | `general,filegroups/documents` | filegroups/documents: 72.57% | 0 | 72.26% | -0.31% | general: 100.00% | — | 1.000 |
| pkg-info | 1276 | 133 | `general,filetypes/pkg-info` | filetypes/pkg-info: 97.10% | 0 | 97.02% | -0.08% | filetypes/pkg-info: 99.84% | 1.000 | 1.000 |
| go | 1177 | 12102 | `general,filegroups/source,filetypes/go` | filetypes/go: 4.93% | 1 | 5.10% | — | filetypes/go: 7.14% | 0.742 | 0.736 |
| shell | 958 | 5959 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 83.72% | 2 | 86.43% | — | filetypes/shell: 87.58% | 0.984 | 0.977 |
| rar | 767 | 0 | `general` | general: 100.00% | 0 | 73.92% | -26.08% | general: 100.00% | — | — |
| png | 660 | 14991 | `general,filegroups/media,filetypes/png` | filegroups/media: 0.45% | 2 | 9.09% | — | general: 9.09% | 0.146 | 0.143 |
| 7z | 580 | 12 | `general,filetypes/7z` | general: 88.62% | 0 | 87.59% | -1.03% | general: 94.14% | 0.976 | 0.998 |
| vbs | 555 | 426 | `general,filetypes/vbs` | filetypes/vbs: 17.12% | 0 | 17.66% | 0.54% | filetypes/vbs: 44.86% | 0.981 | 0.981 |
| php | 530 | 13349 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 68.11% | 0 | 68.30% | 0.19% | filetypes/php: 74.72% | 0.913 | 0.910 |
| powershell | 374 | 284 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 24.06% | 0 | 25.13% | 1.07% | filetypes/powershell: 72.19% | 0.976 | 0.968 |
| xml | 307 | 19746 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.93% | 0 | 8.79% | 5.86% | filegroups/config: 6.19% | 0.163 | 0.194 |
| lnk | 297 | 131 | `general,filetypes/lnk` | filetypes/lnk: 72.39% | 0 | 71.38% | -1.01% | filetypes/lnk: 73.40% | 0.982 | 0.978 |
| msi | 285 | 14 | `general,filetypes/msi` | filetypes/msi: 76.49% | 0 | 44.21% | -32.28% | filetypes/msi: 98.60% | 0.999 | 0.997 |
| macho | 274 | 1403 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 79.20% | 0 | 75.55% | -3.65% | filetypes/macho: 87.59% | 0.992 | 0.958 |
| python-bytecode | 259 | 6750 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 98.07% | 0 | 92.28% | -5.79% | filetypes/python-bytecode: 98.07% | 0.996 | 0.996 |
| csharp | 236 | 7613 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 29.66% | 0 | 24.58% | -5.08% | filetypes/csharp: 32.63% | 0.608 | 0.598 |
| ole | 229 | 702 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 92.14% | 0 | 91.27% | -0.87% | filetypes/ole: 96.51% | 0.990 | 0.989 |
| rtf | 216 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.69% | 0 | 97.69% | 0.00% | filetypes/rtf: 97.69% | 0.999 | 0.999 |
| jar | 205 | 305 | `general,filetypes/jar` | general: 56.59% | 0 | 54.63% | -1.95% | filetypes/jar: 79.02% | 0.983 | 0.976 |
| docx | 183 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 54.64% | 0 | 72.68% | 18.03% | filegroups/documents: 86.34% | 0.976 | 0.973 |
| gz | 181 | 7139 | `general` | general: 28.73% | 1 | 28.73% | — | general: 32.60% | — | 0.637 |
| java_class | 177 | 55387 | `general,filegroups/portable,filetypes/java_class` | filetypes/java_class: 67.23% | 3 | 84.18% | -2.82% | filegroups/portable: 87.01% | 0.961 | 0.959 |
| rust | 164 | 10209 | `general,filegroups/source,filetypes/rust` | general: 1.83% | 0 | 1.22% | -0.61% | filetypes/rust: 4.88% | 0.105 | 0.075 |
| text | 163 | 8144 | `general,filetypes/text` | general: 12.27% | 0 | 12.27% | 0.00% | general: 14.72% | 0.172 | 0.203 |
| tar | 152 | 54 | `general,filetypes/tar` | filetypes/tar: 96.71% | 0 | 97.37% | 0.66% | filetypes/tar: 98.03% | 0.996 | 0.995 |
| jpeg | 131 | 1344 | `general,filegroups/media,filetypes/jpeg` | general: 14.50% | 0 | 10.69% | -3.82% | filetypes/jpeg: 19.08% | 0.585 | 0.535 |
| plist | 68 | 1555 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.41% | 0 | 4.41% | 0.00% | general: 5.88% | 0.204 | 0.129 |
| data | 58 | 1168 | `general` | general: 74.14% | 0 | 0.00% | -74.14% | general: 82.76% | — | 0.838 |
| crx | 37 | 5 | `general` | general: 67.57% | 0 | 10.81% | -56.76% | general: 78.38% | — | 0.973 |
| cab | 30 | 12 | `general,filetypes/cab` | general: 50.00% | 0 | 50.00% | 0.00% | general: 100.00% | 0.894 | 0.975 |
| perl | 28 | 4002 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 89.29% | 0 | 89.29% | 0.00% | filetypes/perl: 89.29% | 0.956 | 0.956 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | general: 9.09% | 0 | 4.55% | -4.55% | general: 31.82% | 0.328 | 0.557 |
| makefile | 17 | 2792 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.018 | 0.016 |
| groovy | 15 | 771 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.042 | 0.042 |
| chm | 10 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| deb | 7 | 748 | `general` | general: 28.57% | 0 | 0.00% | -28.57% | general: 71.43% | — | 0.593 |
| dockerfile | 7 | 153 | `general,filetypes/dockerfile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.962 | 0.725 |
| html | 7 | 984 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 0.982 | 0.982 |
| ruby | 7 | 2968 | `general,filegroups/scripts,filetypes/ruby` | general: 100.00% | 0 | 28.57% | -71.43% | general: 100.00% | 0.776 | 0.781 |
| chrome-manifest | 6 | 51 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 66.67% | 0 | 66.67% | 0.00% | general: 66.67% | 0.802 | 0.808 |
| lua | 6 | 2131 | `general,filegroups/scripts` | general: 50.00% | 0 | 33.33% | -16.67% | filegroups/scripts: 66.67% | — | 0.629 |
| java | 4 | 4331 | `general,filegroups/source` | filegroups/source: 75.00% | 0 | 50.00% | -25.00% | filegroups/source: 75.00% | — | 0.751 |
| xz | 4 | 3908 | `general` | general: 25.00% | 0 | 25.00% | 0.00% | general: 25.00% | — | 0.328 |
| applescript | 3 | 35 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.810 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| package-lock.json | 3 | 69 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.038 |
| bz2 | 2 | 1408 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.501 |
| pyproject.toml | 2 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| github-actions | 1 | 750 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.143 |
| objc | 1 | 2532 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 147 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.011 |
| tar.bz2 | 1 | 27 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 75.00% | -75.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `` | 0 | 0.00% | 47.23% | -47.23% |
| gz | `general` | 0 | 0.00% | 28.73% | -28.73% |
| deb | `` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.92% | 100.00% | -26.08% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 81.78% | 99.09% | -17.30% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.58% | 13.75% | -6.17% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 62.71% | 67.23% | -4.52% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 63.77% | 68.11% | -4.34% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 68.60% | 71.17% | -2.57% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.08% | 4.93% | -0.85% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 83.72% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| xml | `general,filegroups/config` | 0 | 2.61% | 2.93% | -0.33% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 86.99% | 86.75% | 0.24% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.76% | 0.45% | 0.30% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| zip | `general,filetypes/zip` | 0 | 54.68% | 53.79% | 0.89% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| msi | `general,filetypes/msi` | 0 | 80.00% | 76.49% | 3.51% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.30% | 52.99% | 4.31% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 46.67% | 38.35% | 8.32% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 44.21% | 76.49% | -32.28% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.92% | 100.00% | -26.08% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 82.49% | 87.01% | -4.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| macho | `filetypes/macho` | 0 | 75.55% | 79.20% | -3.65% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.29% | 53.79% | -1.50% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.96% | 13.75% | -0.79% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.94% | 97.10% | -0.16% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 77.99% | 77.99% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `filegroups/config` | 1 | 89.96% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 75.00% | -75.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 37.54% | 76.49% | -38.95% |
| gz | `general` | 0 | 0.00% | 28.73% | -28.73% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 71.71% | 100.00% | -28.29% |
| zst | `general` | 0 | 73.48% | 99.09% | -25.61% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| macho | `filetypes/macho` | 0 | 68.98% | 79.20% | -10.22% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 63.77% | 68.11% | -4.34% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| zip | `filetypes/zip` | 0 | 51.74% | 53.79% | -2.05% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.28% | 13.75% | -1.47% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.08% | 4.93% | -0.85% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 83.72% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| xml | `general,filegroups/config` | 0 | 2.61% | 2.93% | -0.33% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.19% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 74.95% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 86.99% | 86.75% | 0.24% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.76% | 0.45% | 0.30% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.30% | 52.99% | 4.31% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 46.67% | 38.35% | 8.32% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.37% | 76.49% | -29.12% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.49% | 100.00% | -24.51% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.35% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 80.18% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| java | `general,filegroups/source` | 0 | 0.00% | 75.00% | -75.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 40.35% | 76.49% | -36.14% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 71.84% | 100.00% | -28.16% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 76.60% | 99.09% | -22.48% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| macho | `filetypes/macho` | 0 | 70.44% | 79.20% | -8.76% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 64.91% | 68.11% | -3.21% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 51.84% | 53.79% | -1.94% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.28% | 13.75% | -1.47% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.08% | 4.93% | -0.85% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 83.72% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.87% | 97.10% | -0.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 72.88% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 75.68% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 58.29% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 86.99% | 86.75% | 0.24% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.76% | 0.45% | 0.30% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `filetypes/msi` | 0 | 49.12% | 76.49% | -27.37% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.88% | 100.00% | -24.12% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.92% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.93% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 3 | 7.14% | 7.14% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 9 | 80.91% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 1 | 10.69% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.25% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 7.50% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 71.25% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 70.38% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.68% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 40.35% | 76.49% | -36.14% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.36% | 100.00% | -27.64% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 78.58% | 99.09% | -20.50% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| macho | `filetypes/macho` | 0 | 72.99% | 79.20% | -6.20% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.23% | 68.11% | -1.89% |
| zip | `filetypes/zip` | 0 | 51.99% | 53.79% | -1.80% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.28% | 13.75% | -1.47% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 83.72% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.87% | 97.10% | -0.24% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.76% | 4.93% | -0.17% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.45% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 72.88% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 76.28% | — | — |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 59.25% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `filetypes/msi` | 0 | 49.47% | 76.49% | -27.02% |
| rar | `general` | 0 | 78.49% | 100.00% | -21.51% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.66% | 98.07% | -5.41% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 13.98% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.95% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.31% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 12 | 82.25% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 2 | 12.21% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.30% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 71.38% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 71.64% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 70.38% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| python | `general,filetypes/python` | 4 | 68.22% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.68% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| vbs | `general,filetypes/vbs` | 1 | 28.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 90.96% | 87.01% | 3.95% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 41.75% | 76.49% | -34.74% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 72.36% | 100.00% | -27.64% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| zst | `general` | 0 | 78.58% | 99.09% | -20.50% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| macho | `filetypes/macho` | 0 | 73.36% | 79.20% | -5.84% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.23% | 68.11% | -1.89% |
| zip | `filetypes/zip` | 0 | 52.01% | 53.79% | -1.77% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.45% | 13.75% | -1.30% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 83.09% | 83.72% | -0.63% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.87% | 97.10% | -0.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.45% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 72.88% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 76.28% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 59.25% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `filetypes/msi` | 0 | 50.53% | 76.49% | -25.96% |
| rar | `general` | 0 | 78.75% | 100.00% | -21.25% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.66% | 98.07% | -5.41% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 25.42% | 29.66% | -4.24% |
| text | `general,filetypes/text` | 3 | 12.27% | 14.72% | -2.45% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 12.39% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.95% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filetypes/go` | 4 | 8.24% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 1 | 50.00% | — | — |
| java_class | `general,filegroups/portable,filetypes/java_class` | 5 | 93.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 14 | 82.65% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.30% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 71.38% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 73.51% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 70.38% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 6 | 70.13% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 42.86% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 87.68% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| vbs | `general,filetypes/vbs` | 1 | 28.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| lua | `general,filegroups/scripts` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 42.46% | 76.49% | -34.04% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.14% | 100.00% | -26.86% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| zst | `general` | 0 | 81.25% | 99.09% | -17.84% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 85.71% | 98.07% | -12.36% |
| macho | `filetypes/macho` | 0 | 74.09% | 79.20% | -5.11% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 66.23% | 68.11% | -1.89% |
| zip | `filetypes/zip` | 0 | 52.08% | 53.79% | -1.71% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.45% | 13.75% | -1.30% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.87% | 97.10% | -0.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.45% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 72.88% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 76.28% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 59.25% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.39% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `filetypes/msi` | 0 | 51.23% | 76.49% | -25.26% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 78.88% | 100.00% | -21.12% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 100.00% | -14.29% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.66% | 98.07% | -5.41% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.27% | 14.72% | -2.45% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.54% | 29.66% | -2.12% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| png | `general,filegroups/media,filetypes/png` | 3 | 8.94% | 9.09% | -0.15% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 12.39% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 8.33% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 6 | 93.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 15 | 82.94% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.52% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 71.38% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 73.67% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 71.32% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 6 | 70.13% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| vbs | `general,filetypes/vbs` | 1 | 28.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 87.68% | 87.58% | 0.10% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 43.86% | 76.49% | -32.63% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.14% | 100.00% | -26.86% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| zst | `general` | 0 | 81.25% | 99.09% | -17.84% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| macho | `filetypes/macho` | 0 | 74.82% | 79.20% | -4.38% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.19% | 53.79% | -1.60% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.79% | 13.75% | -0.96% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 67.74% | 68.11% | -0.38% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.87% | 97.10% | -0.24% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 51.53% | 51.55% | -0.03% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.68% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 72.88% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 76.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 59.25% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 1 | 85.39% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 52.98% | 76.49% | -23.51% |
| rar | `general` | 0 | 79.27% | 100.00% | -20.73% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 85.71% | 100.00% | -14.29% |
| zst | `general` | 0 | 85.98% | 99.09% | -13.11% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.66% | 98.07% | -5.41% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.27% | 14.72% | -2.45% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.97% | 29.66% | -1.69% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 12.39% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 8.50% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.83% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 6 | 93.22% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 83.79% | — | — |
| jpeg | `filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.52% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 71.38% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 80.47% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 71.32% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 6 | 70.13% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| vbs | `general,filetypes/vbs` | 1 | 28.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| shell | `general,filegroups/scripts,filetypes/shell` | 3 | 87.68% | 87.58% | 0.10% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 43.86% | 76.49% | -32.63% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.14% | 100.00% | -26.86% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 82.49% | 87.01% | -4.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| macho | `filetypes/macho` | 0 | 75.55% | 79.20% | -3.65% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.24% | 53.79% | -1.55% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.79% | 13.75% | -0.96% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.94% | 97.10% | -0.16% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 76.88% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 10.00% | 100.00% | -90.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| msi | `filetypes/msi` | 0 | 52.98% | 76.49% | -23.51% |
| rar | `general` | 0 | 79.40% | 100.00% | -20.60% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.66% | 98.07% | -5.41% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.27% | 14.72% | -2.45% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 28.39% | 29.66% | -1.27% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 12.39% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.98% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 8.58% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.83% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general` | 1 | 50.00% | — | — |
| java_class | `filegroups/portable,filetypes/java_class` | 11 | 94.92% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 84.37% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.52% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 71.38% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 7 | 75.82% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 71.51% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 77.32% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| vbs | `general,filetypes/vbs` | 2 | 36.22% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 44.21% | 76.49% | -32.28% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.92% | 100.00% | -26.08% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 82.49% | 87.01% | -4.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| macho | `filetypes/macho` | 0 | 75.55% | 79.20% | -3.65% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.29% | 53.79% | -1.50% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| c | `general,filegroups/source,filetypes/c` | 0 | 12.96% | 13.75% | -0.79% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.94% | 97.10% | -0.16% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 77.99% | 77.99% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `filegroups/config` | 1 | 89.96% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 8.79% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.10% | 4.93% | 0.17% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| tar | `filetypes/tar` | 0 | 67.11% | 96.71% | -29.61% |
| msi | `filetypes/msi` | 0 | 52.98% | 76.49% | -23.51% |
| rar | `general` | 0 | 80.18% | 100.00% | -19.82% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.27% | 14.72% | -2.45% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 28.81% | 29.66% | -0.85% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 1 | 12.39% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.01% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.01% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 31.49% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general` | 1 | 50.00% | — | — |
| java_class | `filegroups/portable,filetypes/java_class` | 12 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 20 | 84.64% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.52% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 92.14% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 82.49% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `filetypes/php` | 1 | 71.89% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 77.32% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| vbs | `general,filetypes/vbs` | 2 | 36.22% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.84% | 98.79% | 0.05% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 82.59% | 82.19% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `general` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 44.21% | 76.49% | -32.28% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 73.92% | 100.00% | -26.08% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| batch | `filetypes/batch` | 0 | 94.04% | 98.79% | -4.75% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| macho | `filetypes/macho` | 0 | 75.55% | 79.20% | -3.65% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 84.18% | 87.01% | -2.82% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.33% | 53.79% | -1.46% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 95.16% | 96.16% | -1.00% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 5.10% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 3 | 77.99% | 77.99% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.31% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `filegroups/config` | 1 | 90.41% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 89.29% | 89.29% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| msi | `filetypes/msi` | 0 | 54.39% | 76.49% | -22.11% |
| rar | `general` | 0 | 80.44% | 100.00% | -19.56% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 88.16% | 96.71% | -8.55% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 28.81% | 29.66% | -0.85% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 11 | 16.13% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 93.08% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.60% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 31.49% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general` | 1 | 50.00% | — | — |
| java_class | `filegroups/portable,filetypes/java_class` | 12 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 21 | 84.85% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.52% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 92.14% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 83.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 2 | 89.29% | — | — |
| php | `general,filetypes/php` | 2 | 73.58% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 1 | 4.41% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 77.32% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 36.22% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 1 | 60.15% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 0.00% | 74.14% | -74.14% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 45.61% | 76.49% | -30.88% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.71% | 100.00% | -25.29% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 84.18% | 87.01% | -2.82% |
| batch | `filetypes/batch` | 0 | 96.68% | 98.79% | -2.11% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.40% | 53.79% | -1.39% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 5.18% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 4 | 78.27% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.31% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `filegroups/config` | 1 | 90.73% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `general,filetypes/text` | 1 | 12.88% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L10 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| applescript | `general` | 0 | 33.33% | 66.67% | -33.33% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 54.39% | 76.49% | -22.11% |
| rar | `general` | 0 | 80.83% | 100.00% | -19.17% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 88.82% | 96.71% | -7.89% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 2 | 16.98% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 29.66% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.44% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 13 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 23 | 84.98% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 12.98% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.07% | — | — |
| macho | `general,filetypes/macho` | 1 | 81.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 92.14% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 14 | 83.10% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 5 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.58% | — | — |
| plist | `filegroups/config,filetypes/plist` | 1 | 5.88% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 77.32% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| vbs | `general,filetypes/vbs` | 2 | 36.22% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L11 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 45.96% | 76.49% | -30.53% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.71% | 100.00% | -25.29% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 84.18% | 87.01% | -2.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.43% | 53.79% | -1.35% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 5.10% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 4 | 78.27% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `filegroups/config` | 1 | 90.87% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L11 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 54.74% | 76.49% | -21.75% |
| rar | `general` | 0 | 81.10% | 100.00% | -18.90% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 88.82% | 96.71% | -7.89% |
| macho | `general,filetypes/macho` | 3 | 82.48% | 87.59% | -5.11% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 2 | 17.20% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.08% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 14 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 26 | 85.13% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.07% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 92.14% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 15 | 83.24% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.58% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 5.88% | — | — |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.09% | 9.09% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 79.41% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| elf | `general,filegroups/native,filetypes/elf` | 3 | 96.28% | 96.01% | 0.27% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L12 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 10.81% | 67.57% | -56.76% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 46.67% | 76.49% | -29.82% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| rar | `general` | 0 | 74.71% | 100.00% | -25.29% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.28% | 98.07% | -5.79% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 84.18% | 87.01% | -2.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| zip | `filetypes/zip` | 0 | 52.50% | 53.79% | -1.29% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 1 | 5.18% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 5 | 78.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L12 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 54.74% | 76.49% | -21.75% |
| rar | `general` | 0 | 81.36% | 100.00% | -18.64% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 89.47% | 96.71% | -7.24% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 15 | 18.45% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.93% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 96.36% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 29 | 85.40% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.07% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filetypes/ole` | 1 | 92.14% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 83.30% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.77% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 5.88% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 79.41% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.31% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.24% | 9.09% | 0.15% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L13 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.37% | 76.49% | -29.12% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.23% | 100.00% | -24.77% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 84.18% | 87.01% | -2.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 94.16% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.35% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 5 | 78.63% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.88% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 69.26% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L13 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 55.44% | 76.49% | -21.05% |
| rar | `general` | 0 | 81.62% | 100.00% | -18.38% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 90.13% | 96.71% | -6.58% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 15 | 18.73% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.93% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 4 | 96.36% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 31 | 85.56% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.40% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 92.14% | 92.14% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 83.75% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.77% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 5.88% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 7 | 79.41% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filetypes/ruby` | 1 | 100.00% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.52% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| png | `general,filegroups/media,filetypes/png` | 3 | 9.24% | 9.09% | 0.15% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L14 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.37% | 76.49% | -29.12% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.23% | 100.00% | -24.77% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 69.27% | 82.19% | -12.93% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 85.31% | 87.01% | -1.69% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.70% | 13.75% | -0.06% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.35% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 79.52% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L14 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 55.79% | 76.49% | -20.70% |
| rar | `general` | 0 | 81.62% | 100.00% | -18.38% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 90.79% | 96.71% | -5.92% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.22% | 1.83% | -0.61% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 16 | 18.96% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.93% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 8 | 97.45% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 32 | 85.86% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.40% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `general,filegroups/source,filetypes/makefile` | 1 | 0.00% | — | — |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 92.14% | 92.14% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 83.77% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.77% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 5.88% | — | — |
| png | `general,filegroups/media,filetypes/png` | 4 | 9.24% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 79.89% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 5 | 88.52% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 1 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L15 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.37% | 76.49% | -29.12% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.49% | 100.00% | -24.51% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 85.31% | 87.01% | -1.69% |
| text | `general,filetypes/text` | 0 | 11.04% | 12.27% | -1.23% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.35% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 79.52% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.02% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| package.json | `general,filegroups/config` | 0 | 89.28% | 89.10% | 0.18% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L15 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 55.79% | 76.49% | -20.70% |
| rar | `general` | 0 | 81.88% | 100.00% | -18.12% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 90.79% | 96.71% | -5.92% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 17 | 19.07% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.93% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 9 | 97.82% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 32 | 85.98% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.07% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 92.14% | 92.14% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 4 | 99.55% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 16 | 83.88% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.77% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 2 | 5.88% | — | — |
| png | `general,filegroups/media,filetypes/png` | 5 | 9.24% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 79.89% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 2 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.73% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L16 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 100.00% | -71.43% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.37% | 76.49% | -29.12% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.49% | 100.00% | -24.51% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.69% | 98.79% | -2.10% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.35% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 80.18% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L16 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 55.79% | 76.49% | -20.70% |
| rar | `general` | 0 | 82.01% | 100.00% | -17.99% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| tar | `filetypes/tar` | 0 | 90.79% | 96.71% | -5.92% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 17 | 19.13% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 30.93% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 10 | 97.84% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 34 | 86.27% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.55% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 92.14% | 92.14% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 84.30% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.96% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 3 | 5.88% | 5.88% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 5 | 9.24% | — | — |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 2 | 59.09% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 79.89% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.73% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L17 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.72% | 76.49% | -28.77% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 100.00% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.88% | 100.00% | -24.12% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.70% | 98.79% | -2.09% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.69% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 1 | 28.73% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 80.18% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L17 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 56.49% | 76.49% | -20.00% |
| rar | `general` | 0 | 82.14% | 100.00% | -17.86% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 3 | 62.03% | 72.19% | -10.16% |
| tar | `filetypes/tar` | 0 | 90.79% | 96.71% | -5.92% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.68% | 98.07% | -0.39% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 17 | 19.19% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 2 | 31.78% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 10 | 97.86% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 36 | 86.38% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 63.60% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 1 | 96.07% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.93% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 17 | 84.56% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 2 | 73.96% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 3 | 5.88% | 5.88% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 5 | 9.24% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 79.89% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.73% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 1 | 83.76% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L18 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 47.72% | 76.49% | -28.77% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 100.00% | -28.57% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.88% | 100.00% | -24.12% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.70% | 98.79% | -2.09% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.69% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 80.37% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| php | `general,filetypes/php` | 0 | 68.30% | 68.11% | 0.19% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L18 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 20.00% | 100.00% | -80.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 56.49% | 76.49% | -20.00% |
| rar | `general` | 0 | 82.14% | 100.00% | -17.86% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 3 | 62.03% | 72.19% | -10.16% |
| tar | `filetypes/tar` | 0 | 91.45% | 96.71% | -5.26% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 17 | 19.35% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filetypes/csharp` | 2 | 31.78% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 11 | 97.90% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 3 | 32.60% | 32.60% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 15 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 40 | 86.53% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 63.60% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 1 | 96.07% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 2 | 98.82% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.93% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 18 | 84.98% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 3 | 5.88% | 5.88% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 5 | 9.24% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 80.37% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 1 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.83% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 2 | 84.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| php | `general,filetypes/php` | 3 | 75.09% | 74.72% | 0.38% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L19 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 100.00% | -28.57% |
| msi | `filetypes/msi` | 0 | 48.07% | 76.49% | -28.42% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.88% | 100.00% | -24.12% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.69% | 14.50% | -3.82% |
| batch | `filetypes/batch` | 0 | 96.70% | 98.79% | -2.08% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.69% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filetypes/javascript` | 6 | 80.37% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 69.04% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 70.38% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L19 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| chm | `general` | 0 | 30.00% | 100.00% | -70.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 56.49% | 76.49% | -20.00% |
| rar | `general` | 0 | 82.14% | 100.00% | -17.86% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 3 | 62.03% | 72.19% | -10.16% |
| tar | `filetypes/tar` | 0 | 91.45% | 96.71% | -5.26% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| package.json | `general,filegroups/config,filetypes/package.json` | 3 | 98.82% | 99.55% | -0.73% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 17 | 19.58% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filetypes/csharp` | 2 | 31.78% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 11 | 97.96% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filegroups/source,filetypes/go` | 4 | 9.35% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 4 | 32.60% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `filegroups/portable,filetypes/java_class` | 18 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 42 | 86.60% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 63.60% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 1 | 96.07% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.93% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 18 | 84.99% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 3 | 5.88% | 5.88% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 5 | 9.24% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 8 | 80.37% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 2 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.83% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 2 | 84.83% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| php | `general,filetypes/php` | 3 | 75.09% | 74.72% | 0.38% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| data | `general` | 0 | 1.72% | 74.14% | -72.41% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 13.51% | 67.57% | -54.05% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| deb | `general` | 0 | 0.00% | 28.57% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 71.43% | 100.00% | -28.57% |
| msi | `filetypes/msi` | 0 | 48.07% | 76.49% | -28.42% |
| java | `general,filegroups/source` | 0 | 50.00% | 75.00% | -25.00% |
| rar | `general` | 0 | 75.88% | 100.00% | -24.12% |
| lua | `general,filegroups/scripts` | 0 | 33.33% | 50.00% | -16.67% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 24.58% | 29.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 93.05% | 98.07% | -5.02% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 77.82% | 82.19% | -4.37% |
| batch | `filetypes/batch` | 0 | 96.71% | 98.79% | -2.08% |
| jar | `general,filetypes/jar` | 0 | 54.63% | 56.59% | -1.95% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| ole | `general,filetypes/ole` | 0 | 91.27% | 92.14% | -0.87% |
| doc | `general,filegroups/documents` | 0 | 72.26% | 72.57% | -0.31% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 7.30% | 7.59% | -0.29% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 92.88% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 5.69% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 2 | 29.28% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 6 | 80.52% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 1 | 10.69% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 58.17% | — | — |
| makefile | `general,filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 94.82% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 71.25% | — | — |
| perl | `filegroups/scripts,filetypes/perl` | 1 | 89.29% | — | — |
| php | `general,filetypes/php` | 1 | 70.38% | — | — |
| plist | `filegroups/config,filetypes/plist` | 0 | 4.41% | 4.41% | 0.00% |
| png | `general,filetypes/png` | 2 | 9.09% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.83% | 1.83% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 86.43% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 12.27% | 12.27% | 0.00% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 96.16% | 96.16% | 0.00% |
| xz | `general` | 0 | 25.00% | 25.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 3 | 67.22% | 67.17% | 0.04% |
| c | `general,filegroups/source,filetypes/c` | 0 | 13.81% | 13.75% | 0.06% |
| vbs | `general,filetypes/vbs` | 0 | 17.66% | 17.12% | 0.54% |
| tar | `general,filetypes/tar` | 0 | 97.37% | 96.71% | 0.66% |
| macho | `general,filetypes/macho` | 0 | 79.93% | 79.20% | 0.73% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 25.13% | 24.06% | 1.07% |
| zip | `general,filetypes/zip` | 0 | 56.39% | 53.79% | 2.60% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 3 | 91.53% | 87.01% | 4.52% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |

## Deployed OR-rule at L20 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| pyproject.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 72.57% | -72.57% |
| data | `general` | 0 | 3.45% | 74.14% | -70.69% |
| chm | `general` | 0 | 30.00% | 100.00% | -70.00% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 33.48% | 91.22% | -57.74% |
| crx | `general` | 0 | 16.22% | 67.57% | -51.35% |
| unknown | `general` | 0 | 0.00% | 47.23% | -47.23% |
| msi | `filetypes/msi` | 0 | 56.84% | 76.49% | -19.65% |
| rar | `general` | 0 | 82.27% | 100.00% | -17.73% |
| zst | `general` | 0 | 87.50% | 99.09% | -11.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 3 | 62.03% | 72.19% | -10.16% |
| tar | `filetypes/tar` | 0 | 92.11% | 96.71% | -4.61% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 4.55% | 9.09% | -4.55% |
| text | `general,filetypes/text` | 3 | 12.88% | 14.72% | -1.84% |
| 7z | `general` | 0 | 87.59% | 88.62% | -1.03% |
| lnk | `general,filetypes/lnk` | 0 | 71.38% | 72.39% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 97.30% | 98.07% | -0.77% |
| package.json | `general,filegroups/config,filetypes/package.json` | 3 | 98.82% | 99.55% | -0.73% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 97.02% | 97.10% | -0.08% |
| applescript | `general` | 0 | 66.67% | 66.67% | 0.00% |
| bz2 | `general` | 0 | 50.00% | 50.00% | 0.00% |
| c | `general,filetypes/c` | 17 | 19.58% | — | — |
| cab | `general` | 0 | 50.00% | 50.00% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 66.67% | 66.67% | 0.00% |
| csharp | `general,filetypes/csharp` | 2 | 31.78% | — | — |
| deb | `general` | 0 | 28.57% | 28.57% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 11 | 98.01% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `filetypes/go` | 5 | 10.11% | — | — |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `general` | 4 | 32.60% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 1 | 57.07% | — | — |
| java | `general,filegroups/source` | 0 | 75.00% | 75.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 17 | 95.48% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 45 | 86.80% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 2 | 14.50% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 63.60% | — | — |
| lua | `general,filegroups/scripts` | 0 | 50.00% | 50.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| objc | `general` | 0 | 100.00% | 100.00% | 0.00% |
| ole | `filegroups/documents,filetypes/ole` | 1 | 96.07% | — | — |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 2 | 71.93% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 19 | 85.04% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 1 | 92.86% | — | — |
| php | `general,filetypes/php` | 4 | 75.85% | — | — |
| plist | `general,filegroups/config,filetypes/plist` | 3 | 5.88% | 5.88% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 6 | 9.24% | — | — |
| python | `general,filegroups/scripts,filetypes/python` | 9 | 80.41% | — | — |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 97.69% | 97.69% | 0.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 1 | 100.00% | — | — |
| rust | `general,filegroups/source,filetypes/rust` | 2 | 3.66% | — | — |
| shell | `general,filegroups/scripts,filetypes/shell` | 6 | 88.83% | — | — |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| tar.bz2 | `general` | 0 | 100.00% | 100.00% | 0.00% |
| tar.gz | `general,filetypes/tar.gz` | 5 | 87.24% | — | — |
| xls | `general,filegroups/documents,filetypes/xls` | 1 | 96.31% | — | — |
| xz | `general` | 2 | 25.00% | — | — |
| zip | `general,filetypes/zip` | 2 | 61.02% | — | — |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.88% | 98.79% | 0.10% |
| vbs | `general,filetypes/vbs` | 3 | 45.05% | 44.86% | 0.18% |
| macho | `general,filegroups/native,filetypes/macho` | 3 | 89.78% | 87.59% | 2.19% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 8.79% | 2.93% | 5.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 72.68% | 54.64% | 18.03% |
