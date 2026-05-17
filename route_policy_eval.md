# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 530207 (185983 malware, 344224 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@3FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 101848 | 18512 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 61.37% | 2 | 67.91% | — | general: 73.03% | 1.000 | 1.000 |
| pdf | 18189 | 1731 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 8.02% | 0 | 6.55% | -1.47% | filetypes/pdf: 9.18% | 0.996 | 0.994 |
| batch | 17345 | 263 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 98.94% | 0 | 93.70% | -5.23% | filetypes/batch: 99.56% | 1.000 | 1.000 |
| javascript | 9626 | 55042 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 68.55% | 1 | 68.73% | — | filetypes/javascript: 78.17% | 0.988 | 0.984 |
| zip | 6832 | 751 | `general,filegroups/archive,filetypes/zip` | filegroups/archive: 62.63% | 0 | 56.15% | -6.48% | general: 69.42% | 0.994 | 0.994 |
| elf | 4439 | 15507 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 93.51% | 2 | 94.03% | — | filetypes/elf: 96.22% | 1.000 | 1.000 |
| tar.gz | 3426 | 1614 | `general,filegroups/archive,filetypes/tar.gz` | filegroups/archive: 86.25% | 0 | 76.91% | -9.34% | general: 90.34% | 0.999 | 0.998 |
| kotlin | 2391 | 5048 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 54.62% | 1 | 58.93% | — | filetypes/kotlin: 72.48% | 0.987 | 0.983 |
| python | 2239 | 15453 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 48.10% | 1 | 61.59% | — | filetypes/python: 67.22% | 0.980 | 0.969 |
| xlsx | 2181 | 8 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 91.29% | 0 | 29.25% | -62.04% | filegroups/documents: 92.53% | 0.981 | 0.996 |
| package.json | 2153 | 1189 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 93.27% | 0 | 93.03% | -0.23% | filegroups/config: 99.58% | 1.000 | 1.000 |
| c | 1756 | 64237 | `general,filegroups/source,filetypes/c` | filetypes/c: 12.13% | — | — | — | filetypes/c: 13.61% | 0.495 | 0.481 |
| zst | 1312 | 2034 | `general,filegroups/archive,filetypes/zst` | filegroups/archive: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | 1.000 | 1.000 |
| doc | 1283 | 3 | `general,filegroups/documents` | general: 99.69% | 0 | 0.00% | -99.69% | general: 100.00% | — | 1.000 |
| pkg-info | 1275 | 107 | `general,filetypes/pkg-info` | filetypes/pkg-info: 97.10% | 0 | 97.10% | 0.00% | filetypes/pkg-info: 98.82% | 1.000 | 1.000 |
| xls | 1258 | 6 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 99.52% | 0 | 0.00% | -99.52% | filegroups/documents: 99.84% | 0.980 | 0.999 |
| go | 1177 | 11772 | `general,filegroups/source,filetypes/go` | filetypes/go: 1.53% | 0 | 0.00% | -1.53% | filetypes/go: 4.16% | 0.447 | 0.523 |
| unknown | 1125 | 1993 | `general,filetypes/unknown` | general: 0.18% | 0 | 0.00% | -0.18% | filetypes/unknown: 57.96% | 0.768 | 0.768 |
| png | 648 | 13138 | `general,filegroups/media,filetypes/png` | filegroups/media: 0.15% | 0 | 0.00% | -0.15% | general: 9.26% | 0.181 | 0.181 |
| rar | 630 | 0 | `general,filegroups/archive` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| 7z | 531 | 10 | `general,filegroups/archive,filetypes/7z` | general: 90.21% | 0 | 86.82% | -3.39% | general: 91.34% | 0.976 | 0.999 |
| php | 495 | 7725 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 66.46% | 0 | 33.94% | -32.53% | filetypes/php: 72.93% | 0.926 | 0.906 |
| shell | 406 | 5407 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 71.18% | 0 | 61.82% | -9.36% | filetypes/shell: 77.34% | 0.953 | 0.932 |
| xml | 253 | 16756 | `general,filegroups/config,filetypes/xml` | general: 1.58% | 0 | 0.00% | -1.58% | general: 3.56% | 0.191 | 0.203 |
| vbs | 235 | 417 | `general,filetypes/vbs` | filetypes/vbs: 32.34% | — | — | — | general: 46.81% | 0.968 | 0.968 |
| csharp | 230 | 7556 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 30.87% | 0 | 0.00% | -30.87% | filegroups/source: 31.74% | 0.578 | 0.572 |
| ole | 219 | 659 | `general,filegroups/documents,filetypes/ole` | general: 91.32% | 0 | 0.00% | -91.32% | filetypes/ole: 96.80% | 0.992 | 0.992 |
| macho | 205 | 1087 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 80.00% | 0 | 47.32% | -32.68% | filetypes/macho: 80.49% | 0.990 | 0.926 |
| python-bytecode | 198 | 2667 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.47% | 0 | 0.00% | -97.47% | filetypes/python-bytecode: 97.47% | 0.995 | 0.995 |
| rtf | 196 | 50 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.45% | — | — | — | filetypes/rtf: 100.00% | 1.000 | 1.000 |
| lnk | 168 | 94 | `general,filetypes/lnk` | filetypes/lnk: 51.79% | — | — | — | filetypes/lnk: 63.10% | 0.964 | 0.961 |
| rust | 163 | 9550 | `general,filegroups/source,filetypes/rust` | general: 1.84% | 0 | 0.00% | -1.84% | filegroups/source: 3.07% | 0.111 | 0.080 |
| gz | 162 | 5559 | `general,filegroups/archive,filetypes/gz` | filetypes/gz: 68.52% | 0 | 0.00% | -68.52% | filetypes/gz: 68.52% | 0.703 | 0.704 |
| jar | 161 | 216 | `general,filegroups/portable,filetypes/jar` | general: 59.01% | — | — | — | filegroups/portable: 72.05% | 0.975 | 0.979 |
| docx | 158 | 31 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 60.13% | — | — | — | general: 84.18% | 0.972 | 0.969 |
| text | 154 | 7706 | `general,filetypes/text` | general: 12.34% | 0 | 0.00% | -12.34% | filetypes/text: 17.53% | 0.304 | 0.303 |
| tar | 149 | 47 | `general,filegroups/archive,filetypes/tar` | filetypes/tar: 97.99% | — | — | — | filetypes/tar: 97.99% | 0.996 | 0.995 |
| java_class | 134 | 34023 | `general,filegroups/portable,filetypes/java_class` | general: 73.88% | — | — | — | filegroups/portable: 85.82% | 0.946 | 0.948 |
| powershell | 119 | 261 | `general,filegroups/scripts,filetypes/powershell` | general: 42.02% | — | — | — | filegroups/scripts: 67.23% | 0.946 | 0.950 |
| jpeg | 116 | 1282 | `general,filegroups/media,filetypes/jpeg` | general: 11.21% | 0 | 10.34% | -0.86% | filegroups/media: 12.07% | 0.272 | 0.276 |
| msi | 115 | 12 | `general,filegroups/archive,filetypes/msi` | filetypes/msi: 88.70% | — | — | — | filetypes/msi: 98.26% | 0.998 | 0.999 |
| plist | 68 | 1522 | `general,filegroups/config,filetypes/plist` | general: 1.47% | 0 | 0.00% | -1.47% | general: 5.88% | 0.122 | 0.111 |
| data | 58 | 1152 | `general,filetypes/data` | filetypes/data: 77.59% | 0 | 60.34% | -17.24% | filetypes/data: 77.59% | 0.895 | 0.898 |
| perl | 26 | 3781 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 88.46% | 0 | 0.00% | -88.46% | filetypes/perl: 92.31% | 0.950 | 0.949 |
| cab | 25 | 12 | `general,filegroups/archive,filetypes/cab` | filegroups/archive: 60.00% | — | — | — | general: 100.00% | 0.980 | 0.981 |
| pptx | 22 | 21 | `general,filegroups/documents,filetypes/pptx` | filetypes/pptx: 31.82% | — | — | — | general: 31.82% | 0.596 | 0.584 |
| makefile | 17 | 2695 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 5.88% | 0.025 | 0.025 |
| groovy | 13 | 639 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | filetypes/groovy: 7.69% | 0.051 | 0.051 |
| deb | 7 | 636 | `general,filegroups/archive` | filegroups/archive: 42.86% | 0 | 0.00% | -42.86% | general: 71.43% | — | 0.596 |
| ruby | 7 | 2821 | `general,filegroups/scripts,filetypes/ruby` | general: 85.71% | 0 | 0.00% | -85.71% | general: 100.00% | 0.903 | 0.928 |
| chm | 6 | 4 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| crx | 6 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| lua | 5 | 1608 | `general,filegroups/scripts` | general: 40.00% | 0 | 0.00% | -40.00% | filegroups/scripts: 60.00% | — | 0.591 |
| java | 4 | 4121 | `general,filegroups/source` | filegroups/source: 75.00% | 0 | 0.00% | -75.00% | general: 75.00% | — | 0.753 |
| xz | 4 | 2884 | `general,filegroups/archive,filetypes/xz` | filegroups/archive: 50.00% | 0 | 25.00% | -25.00% | general: 50.00% | 0.251 | 0.251 |
| html | 3 | 984 | `general,filegroups/documents` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| package-lock.json | 3 | 57 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.038 |
| applescript | 2 | 32 | `general` | general: 100.00% | — | — | — | general: 100.00% | — | 1.000 |
| chrome-manifest | 2 | 29 | `general` | general: 0.00% | — | — | — | general: 50.00% | — | 0.267 |
| github-actions | 1 | 656 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 100.00% | — | 0.250 |
| msg | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| objc | 1 | 2292 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 122 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.012 |
| tar.bz2 | 1 | 19 | `general` | general: 100.00% | — | — | — | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| batch | `` | 0 | 0.00% | 98.94% | -98.94% |
| tar | `` | 0 | 0.00% | 97.99% | -97.99% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| rtf | `` | 0 | 0.00% | 97.45% | -97.45% |
| pkg-info | `` | 0 | 0.00% | 97.10% | -97.10% |
| elf | `` | 0 | 0.00% | 93.51% | -93.51% |
| package.json | `` | 0 | 0.00% | 93.27% | -93.27% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| xlsx | `` | 0 | 0.00% | 91.29% | -91.29% |
| 7z | `` | 0 | 0.00% | 90.21% | -90.21% |
| msi | `` | 0 | 0.00% | 88.70% | -88.70% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| tar.gz | `` | 0 | 0.00% | 86.25% | -86.25% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| macho | `` | 0 | 0.00% | 80.00% | -80.00% |
| data | `` | 0 | 0.00% | 77.59% | -77.59% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| java_class | `` | 0 | 0.00% | 73.88% | -73.88% |
| shell | `` | 0 | 0.00% | 71.18% | -71.18% |
| javascript | `` | 0 | 0.00% | 68.55% | -68.55% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| zip | `` | 0 | 0.00% | 62.63% | -62.63% |
| pe | `` | 0 | 0.00% | 61.37% | -61.37% |
| docx | `` | 0 | 0.00% | 60.13% | -60.13% |
| cab | `` | 0 | 0.00% | 60.00% | -60.00% |
| jar | `` | 0 | 0.00% | 59.01% | -59.01% |
| kotlin | `` | 0 | 0.00% | 54.62% | -54.62% |
| lnk | `` | 0 | 0.00% | 51.79% | -51.79% |
| xz | `` | 0 | 0.00% | 50.00% | -50.00% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `` | 0 | 0.00% | 42.86% | -42.86% |
| powershell | `` | 0 | 0.00% | 42.02% | -42.02% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| vbs | `` | 0 | 0.00% | 32.34% | -32.34% |
| pptx | `` | 0 | 0.00% | 31.82% | -31.82% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| c | `` | 0 | 0.00% | 12.13% | -12.13% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| pdf | `` | 0 | 0.00% | 8.02% | -8.02% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| unknown | `` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| chrome-manifest | `` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |

## Deployed OR-rule at L0 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| php | `filegroups/scripts` | 0 | 33.94% | 66.46% | -32.53% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| data | `filetypes/data` | 0 | 60.34% | 77.59% | -17.24% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| shell | `filetypes/shell` | 0 | 61.82% | 71.18% | -9.36% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 56.09% | 62.63% | -6.54% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| jpeg | `filegroups/media` | 0 | 9.48% | 11.21% | -1.72% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| package.json | `general,filegroups/config` | 0 | 92.99% | 93.27% | -0.28% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native` | 1 | 84.05% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.73% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.80% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 67.91% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 49.13% | — | — |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| package.json | `` | 0 | 0.00% | 93.27% | -93.27% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `` | 0 | 0.00% | 77.59% | -77.59% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| java_class | `` | 0 | 0.00% | 73.88% | -73.88% |
| javascript | `` | 0 | 0.00% | 68.55% | -68.55% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| kotlin | `` | 0 | 0.00% | 54.62% | -54.62% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| c | `` | 0 | 0.00% | 12.13% | -12.13% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| shell | `filetypes/shell` | 0 | 60.59% | 71.18% | -10.59% |
| zip | `filegroups/archive` | 0 | 55.91% | 62.63% | -6.72% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| pe | `filetypes/pe` | 0 | 59.39% | 61.37% | -1.98% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| elf | `filetypes/elf` | 0 | 93.35% | 93.51% | -0.16% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filetypes/perl` | 0 | 88.46% | 88.46% | 0.00% |

## Deployed OR-rule at L1 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| php | `filegroups/scripts` | 0 | 35.15% | 66.46% | -31.31% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| data | `filetypes/data` | 0 | 68.97% | 77.59% | -8.62% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.00% | 86.25% | -5.25% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| zip | `general,filegroups/archive` | 0 | 58.58% | 62.63% | -4.05% |
| shell | `filetypes/shell` | 0 | 67.24% | 71.18% | -3.94% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.65% | 8.02% | -1.37% |
| jpeg | `filegroups/media` | 0 | 10.34% | 11.21% | -0.86% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| elf | `filetypes/elf` | 2 | 94.03% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 71.85% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 60.02% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 1 | 93.27% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 4 | 71.92% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 61.59% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| package.json | `` | 0 | 0.00% | 93.27% | -93.27% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `` | 0 | 0.00% | 77.59% | -77.59% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| java_class | `` | 0 | 0.00% | 73.88% | -73.88% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| javascript | `filegroups/scripts` | 0 | 42.43% | 68.55% | -26.13% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| shell | `filetypes/shell` | 0 | 60.59% | 71.18% | -10.59% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 55.93% | 62.63% | -6.70% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| kotlin | `filetypes/kotlin` | 0 | 52.61% | 54.62% | -2.01% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| pe | `filetypes/pe` | 0 | 59.72% | 61.37% | -1.65% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native,filetypes/elf` | 1 | 93.76% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filetypes/perl` | 0 | 88.46% | 88.46% | 0.00% |

## Deployed OR-rule at L2 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| ole | `filegroups/documents` | 0 | 17.81% | 91.32% | -73.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| vbs | `filetypes/vbs` | 0 | 20.43% | 32.34% | -11.91% |
| macho | `filetypes/macho` | 0 | 69.27% | 80.00% | -10.73% |
| csharp | `filegroups/source` | 0 | 20.43% | 30.87% | -10.43% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| shell | `filetypes/shell` | 0 | 62.32% | 71.18% | -8.87% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.06% | 86.25% | -5.20% |
| data | `filetypes/data` | 0 | 72.41% | 77.59% | -5.17% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| javascript | `filetypes/javascript` | 3 | 74.23% | 78.17% | -3.95% |
| zip | `general,filegroups/archive` | 0 | 58.77% | 62.63% | -3.86% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| php | `filetypes/php` | 0 | 63.84% | 66.46% | -2.63% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.85% | 8.02% | -1.17% |
| jpeg | `filegroups/media` | 0 | 10.34% | 11.21% | -0.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| elf | `filetypes/elf` | 2 | 94.19% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 60.60% | — | — |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 93.40% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 73.49% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 62.97% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| package.json | `` | 0 | 0.00% | 93.27% | -93.27% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `` | 0 | 0.00% | 77.59% | -77.59% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| java_class | `` | 0 | 0.00% | 73.88% | -73.88% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| kotlin | `` | 0 | 0.00% | 54.62% | -54.62% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| shell | `filetypes/shell` | 0 | 61.08% | 71.18% | -10.10% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 55.96% | 62.63% | -6.67% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| javascript | `filetypes/javascript` | 0 | 66.79% | 68.55% | -1.77% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native,filetypes/elf` | 1 | 93.99% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 66.36% | 61.37% | 4.98% |

## Deployed OR-rule at L3 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| vbs | `filetypes/vbs` | 0 | 20.43% | 32.34% | -11.91% |
| csharp | `filegroups/source` | 0 | 20.43% | 30.87% | -10.43% |
| macho | `filetypes/macho` | 0 | 69.76% | 80.00% | -10.24% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| shell | `filetypes/shell` | 0 | 62.32% | 71.18% | -8.87% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.12% | 86.25% | -5.14% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| zip | `general,filegroups/archive` | 0 | 58.91% | 62.63% | -3.72% |
| ole | `filegroups/documents` | 0 | 87.67% | 91.32% | -3.65% |
| data | `filetypes/data` | 0 | 74.14% | 77.59% | -3.45% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| php | `filetypes/php` | 0 | 63.84% | 66.46% | -2.63% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.87% | 8.02% | -1.15% |
| jpeg | `filegroups/media` | 0 | 10.34% | 11.21% | -0.86% |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| elf | `filetypes/elf` | 2 | 94.28% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 4 | 76.53% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 59.22% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 93.68% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 5 | 76.26% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 64.18% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| shell | `filetypes/shell` | 0 | 61.08% | 71.18% | -10.10% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 55.97% | 62.63% | -6.66% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| javascript | `filetypes/javascript` | 0 | 66.79% | 68.55% | -1.77% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| package.json | `general,filegroups/config` | 0 | 92.80% | 93.27% | -0.46% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native,filetypes/elf` | 1 | 94.17% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| kotlin | `filetypes/kotlin` | 1 | 57.30% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 66.66% | 61.37% | 5.28% |

## Deployed OR-rule at L4 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| zst | `general` | 0 | 87.50% | 100.00% | -12.50% |
| vbs | `filetypes/vbs` | 0 | 20.43% | 32.34% | -11.91% |
| macho | `filetypes/macho` | 0 | 69.76% | 80.00% | -10.24% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| shell | `filetypes/shell` | 0 | 62.32% | 71.18% | -8.87% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.23% | 86.25% | -5.02% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 87.67% | 91.32% | -3.65% |
| zip | `general,filegroups/archive` | 0 | 59.06% | 62.63% | -3.57% |
| data | `filetypes/data` | 0 | 74.14% | 77.59% | -3.45% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| php | `filetypes/php` | 0 | 64.04% | 66.46% | -2.42% |
| elf | `filetypes/elf` | 3 | 94.55% | 96.22% | -1.67% |
| javascript | `filetypes/javascript` | 3 | 76.63% | 78.17% | -1.55% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.92% | 8.02% | -1.10% |
| c | `filetypes/c` | 1 | 13.04% | — | — |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jpeg | `filegroups/media` | 0 | 11.21% | 11.21% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.48% | — | — |
| makefile | `filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 94.71% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 6 | 79.93% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 2 | 65.30% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| python | `` | 0 | 0.00% | 48.10% | -48.10% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| jpeg | `filegroups/media` | 0 | 0.00% | 11.21% | -11.21% |
| shell | `filetypes/shell` | 0 | 61.58% | 71.18% | -9.61% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 56.02% | 62.63% | -6.62% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| package.json | `general,filegroups/config` | 0 | 92.85% | 93.27% | -0.42% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native` | 1 | 83.98% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.55% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.13% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 66.98% | 61.37% | 5.61% |

## Deployed OR-rule at L5 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| zst | `general` | 0 | 87.50% | 100.00% | -12.50% |
| vbs | `filetypes/vbs` | 0 | 20.43% | 32.34% | -11.91% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 86.36% | 97.47% | -11.11% |
| macho | `filetypes/macho` | 0 | 69.76% | 80.00% | -10.24% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| csharp | `filegroups/source` | 0 | 21.30% | 30.87% | -9.57% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.32% | 86.25% | -4.93% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| data | `filetypes/data` | 0 | 74.14% | 77.59% | -3.45% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| zip | `general,filegroups/archive` | 0 | 59.35% | 62.63% | -3.28% |
| shell | `filetypes/shell` | 0 | 68.47% | 71.18% | -2.71% |
| php | `filetypes/php` | 0 | 64.04% | 66.46% | -2.42% |
| elf | `filetypes/elf` | 3 | 94.64% | 96.22% | -1.58% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| javascript | `filetypes/javascript` | 3 | 76.88% | 78.17% | -1.30% |
| pdf | `general` | 0 | 6.93% | 8.02% | -1.09% |
| c | `filetypes/c` | 1 | 13.27% | — | — |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jpeg | `filegroups/media` | 0 | 11.21% | 11.21% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 61.48% | — | — |
| ole | `filegroups/documents,filetypes/ole` | 0 | 91.32% | 91.32% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 95.08% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 8 | 81.49% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 2 | 65.92% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L6 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| data | `filetypes/data` | 0 | 1.72% | 77.59% | -75.86% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| shell | `filetypes/shell` | 0 | 61.58% | 71.18% | -9.61% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| jpeg | `filegroups/media` | 0 | 2.59% | 11.21% | -8.62% |
| zip | `filegroups/archive` | 0 | 56.02% | 62.63% | -6.62% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| rust | `general` | 0 | 0.61% | 1.84% | -1.23% |
| package.json | `general,filegroups/config` | 0 | 92.85% | 93.27% | -0.42% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native` | 1 | 84.03% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.55% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.30% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 48.77% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 67.29% | 61.37% | 5.92% |

## Deployed OR-rule at L6 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| zst | `general` | 0 | 87.50% | 100.00% | -12.50% |
| vbs | `filetypes/vbs` | 0 | 20.43% | 32.34% | -11.91% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 86.36% | 97.47% | -11.11% |
| macho | `filetypes/macho` | 0 | 69.76% | 80.00% | -10.24% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.38% | 86.25% | -4.87% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| data | `filetypes/data` | 0 | 74.14% | 77.59% | -3.45% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| zip | `general,filegroups/archive,filetypes/zip` | 0 | 59.56% | 62.63% | -3.07% |
| shell | `filetypes/shell` | 0 | 68.47% | 71.18% | -2.71% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| elf | `filetypes/elf` | 3 | 95.11% | 96.22% | -1.10% |
| pdf | `general` | 0 | 6.94% | 8.02% | -1.08% |
| php | `filetypes/php` | 0 | 65.66% | 66.46% | -0.81% |
| javascript | `filetypes/javascript` | 3 | 77.65% | 78.17% | -0.52% |
| c | `filetypes/c` | 1 | 13.27% | — | — |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `filetypes/kotlin` | 1 | 60.60% | — | — |
| ole | `filegroups/documents,filetypes/ole` | 0 | 91.32% | 91.32% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 95.59% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 11 | 81.98% | — | — |
| perl | `filetypes/perl` | 0 | 88.46% | 88.46% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 2 | 66.41% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |

## Deployed OR-rule at L7 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| php | `` | 0 | 0.00% | 66.46% | -66.46% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| data | `filetypes/data` | 0 | 60.34% | 77.59% | -17.24% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| shell | `filetypes/shell` | 0 | 61.82% | 71.18% | -9.36% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| jpeg | `filegroups/media` | 0 | 2.59% | 11.21% | -8.62% |
| zip | `filegroups/archive` | 0 | 56.06% | 62.63% | -6.57% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| xml | `` | 0 | 0.00% | 1.58% | -1.58% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| rust | `general` | 0 | 1.23% | 1.84% | -0.61% |
| package.json | `general,filegroups/config` | 0 | 92.94% | 93.27% | -0.33% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native` | 1 | 84.05% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.73% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.64% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 67.91% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 48.91% | — | — |

## Deployed OR-rule at L7 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 86.36% | 97.47% | -11.11% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| vbs | `general,filetypes/vbs` | 0 | 22.55% | 32.34% | -9.79% |
| macho | `filetypes/macho` | 0 | 70.24% | 80.00% | -9.76% |
| csharp | `filegroups/source` | 0 | 21.30% | 30.87% | -9.57% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.38% | 86.25% | -4.87% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| data | `filetypes/data` | 0 | 74.14% | 77.59% | -3.45% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| shell | `filetypes/shell` | 0 | 68.47% | 71.18% | -2.71% |
| zip | `general,filegroups/archive,filetypes/zip` | 0 | 59.94% | 62.63% | -2.69% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.98% | 8.02% | -1.04% |
| php | `filetypes/php` | 0 | 65.66% | 66.46% | -0.81% |
| elf | `filetypes/elf` | 3 | 95.45% | 96.22% | -0.77% |
| javascript | `filetypes/javascript` | 3 | 77.99% | 78.17% | -0.19% |
| c | `filetypes/c` | 1 | 13.38% | — | — |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| jpeg | `filegroups/media` | 1 | 11.21% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.74% | — | — |
| ole | `filegroups/documents,filetypes/ole` | 0 | 91.32% | 91.32% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 96.05% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 11 | 82.33% | — | — |
| perl | `filetypes/perl` | 0 | 88.46% | 88.46% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 31.82% | 31.82% | 0.00% |
| python | `filetypes/python` | 2 | 66.86% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| zst | `general,filegroups/archive,filetypes/zst` | 0 | 100.00% | 100.00% | 0.00% |

## Deployed OR-rule at L8 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| php | `filegroups/scripts` | 0 | 33.94% | 66.46% | -32.53% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| data | `filetypes/data` | 0 | 60.34% | 77.59% | -17.24% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| macho | `filetypes/macho` | 0 | 68.78% | 80.00% | -11.22% |
| shell | `filetypes/shell` | 0 | 61.82% | 71.18% | -9.36% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 56.09% | 62.63% | -6.54% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| rust | `` | 0 | 0.00% | 1.84% | -1.84% |
| jpeg | `filegroups/media` | 0 | 9.48% | 11.21% | -1.72% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| package.json | `general,filegroups/config` | 0 | 92.99% | 93.27% | -0.28% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filegroups/native` | 1 | 84.05% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.73% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.80% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 67.91% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 49.13% | — | — |

## Deployed OR-rule at L8 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| jpeg | `` | 0 | 0.00% | 11.21% | -11.21% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 86.36% | 97.47% | -11.11% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| vbs | `general,filetypes/vbs` | 0 | 22.55% | 32.34% | -9.79% |
| macho | `filetypes/macho` | 0 | 70.24% | 80.00% | -9.76% |
| csharp | `filegroups/source` | 0 | 21.30% | 30.87% | -9.57% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.49% | 86.25% | -4.76% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| zip | `general,filegroups/archive,filetypes/zip` | 0 | 60.25% | 62.63% | -2.39% |
| data | `filetypes/data` | 0 | 75.86% | 77.59% | -1.72% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.98% | 8.02% | -1.04% |
| php | `filetypes/php` | 0 | 65.66% | 66.46% | -0.81% |
| shell | `filetypes/shell` | 0 | 70.69% | 71.18% | -0.49% |
| elf | `filetypes/elf` | 3 | 95.88% | 96.22% | -0.34% |
| python | `filetypes/python` | 3 | 67.04% | 67.22% | -0.18% |
| c | `filetypes/c` | 3 | 13.50% | 13.61% | -0.11% |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 4 | 78.57% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 62.74% | — | — |
| ole | `filegroups/documents,filetypes/ole` | 0 | 91.32% | 91.32% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 96.19% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 12 | 82.49% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| png | `filegroups/media` | 2 | 9.10% | — | — |
| pptx | `general,filegroups/documents,filetypes/pptx` | 0 | 31.82% | 31.82% | 0.00% |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| zst | `general,filegroups/archive,filetypes/zst` | 0 | 100.00% | 100.00% | 0.00% |

## Deployed OR-rule at L9 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| html | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| objc | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| python-bytecode | `` | 0 | 0.00% | 97.47% | -97.47% |
| ole | `` | 0 | 0.00% | 91.32% | -91.32% |
| perl | `` | 0 | 0.00% | 88.46% | -88.46% |
| ruby | `` | 0 | 0.00% | 85.71% | -85.71% |
| java | `` | 0 | 0.00% | 75.00% | -75.00% |
| gz | `` | 0 | 0.00% | 68.52% | -68.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| lua | `` | 0 | 0.00% | 40.00% | -40.00% |
| macho | `general` | 0 | 47.32% | 80.00% | -32.68% |
| php | `filegroups/scripts` | 0 | 33.94% | 66.46% | -32.53% |
| csharp | `` | 0 | 0.00% | 30.87% | -30.87% |
| xz | `filetypes/xz` | 0 | 25.00% | 50.00% | -25.00% |
| data | `filetypes/data` | 0 | 60.34% | 77.59% | -17.24% |
| text | `` | 0 | 0.00% | 12.34% | -12.34% |
| shell | `filetypes/shell` | 0 | 61.82% | 71.18% | -9.36% |
| tar.gz | `filetypes/tar.gz` | 0 | 76.91% | 86.25% | -9.34% |
| zip | `filegroups/archive` | 0 | 56.15% | 62.63% | -6.48% |
| batch | `filetypes/batch` | 0 | 93.70% | 98.94% | -5.23% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| go | `` | 0 | 0.00% | 1.53% | -1.53% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| pdf | `general` | 0 | 6.55% | 8.02% | -1.47% |
| jpeg | `filegroups/media` | 0 | 10.34% | 11.21% | -0.86% |
| package.json | `general,filegroups/config` | 0 | 93.03% | 93.27% | -0.23% |
| unknown | `filetypes/unknown` | 0 | 0.00% | 0.18% | -0.18% |
| png | `` | 0 | 0.00% | 0.15% | -0.15% |
| elf | `filetypes/elf` | 2 | 94.03% | — | — |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `filetypes/javascript` | 1 | 68.73% | — | — |
| kotlin | `filetypes/kotlin` | 1 | 58.93% | — | — |
| makefile | `` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 67.91% | — | — |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| python | `filetypes/python` | 1 | 61.59% | — | — |

## Deployed OR-rule at L9 suspicious

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.69% | -99.69% |
| xls | `` | 0 | 0.00% | 99.52% | -99.52% |
| xlsx | `filegroups/documents` | 0 | 29.25% | 91.29% | -62.04% |
| deb | `general,filegroups/archive` | 0 | 0.00% | 42.86% | -42.86% |
| msi | `filetypes/msi` | 0 | 66.96% | 88.70% | -21.74% |
| lnk | `filetypes/lnk` | 0 | 35.71% | 51.79% | -16.07% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 86.36% | 97.47% | -11.11% |
| jar | `filegroups/portable` | 0 | 49.07% | 59.01% | -9.94% |
| vbs | `general,filetypes/vbs` | 0 | 22.55% | 32.34% | -9.79% |
| macho | `filetypes/macho` | 0 | 70.24% | 80.00% | -9.76% |
| csharp | `filegroups/source` | 0 | 21.30% | 30.87% | -9.57% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 93.85% | 98.94% | -5.09% |
| tar.gz | `general,filegroups/archive,filetypes/tar.gz` | 0 | 81.58% | 86.25% | -4.67% |
| powershell | `general` | 0 | 37.82% | 42.02% | -4.20% |
| 7z | `filegroups/archive` | 0 | 86.82% | 90.21% | -3.39% |
| tar | `filetypes/tar` | 0 | 94.63% | 97.99% | -3.36% |
| zip | `general,filegroups/archive,filetypes/zip` | 0 | 60.52% | 62.63% | -2.11% |
| data | `filetypes/data` | 0 | 75.86% | 77.59% | -1.72% |
| plist | `` | 0 | 0.00% | 1.47% | -1.47% |
| php | `filetypes/php` | 0 | 65.66% | 66.46% | -0.81% |
| shell | `filetypes/shell` | 0 | 70.69% | 71.18% | -0.49% |
| elf | `filetypes/elf` | 3 | 95.90% | 96.22% | -0.32% |
| python | `filetypes/python` | 3 | 67.13% | 67.22% | -0.09% |
| c | `filetypes/c` | 4 | 13.61% | — | — |
| cab | `general,filegroups/archive,filetypes/cab` | 1 | 76.00% | — | — |
| docx | `general,filegroups/documents,filetypes/docx` | 1 | 68.35% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| gz | `filetypes/gz` | 1 | 68.52% | — | — |
| html | `general,filegroups/documents` | 0 | 100.00% | 100.00% | 0.00% |
| javascript | `filetypes/javascript` | 5 | 79.19% | — | — |
| jpeg | `filegroups/media` | 1 | 11.21% | — | — |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 63.66% | — | — |
| ole | `filegroups/documents,filetypes/ole` | 0 | 91.32% | 91.32% | 0.00% |
| package.json | `general,filegroups/config` | 2 | 96.70% | — | — |
| pdf | `general,filegroups/documents,filetypes/pdf` | 1 | 8.66% | — | — |
| pe | `general,filegroups/native,filetypes/pe` | 13 | 82.61% | — | — |
| perl | `filetypes/perl` | 0 | 88.46% | 88.46% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 97.10% | 97.10% | 0.00% |
| png | `general` | 2 | 9.10% | — | — |
| rtf | `filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| zst | `general,filegroups/archive,filetypes/zst` | 0 | 100.00% | 100.00% | 0.00% |
