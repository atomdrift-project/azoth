# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 812235 (292108 malware, 520127 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 155698 | 19907 | `general,filegroups/native,filetypes/pe` | filegroups/native: 43.52% | 0 | 40.72% | -2.80% | filegroups/native: 47.25% | 0.999 | 0.999 |
| pdf | 22466 | 2673 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 7.94% | 0 | 8.11% | 0.18% | filetypes/pdf: 17.85% | 0.999 | 0.997 |
| batch | 21995 | 517 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 97.84% | 0 | 98.13% | 0.29% | filetypes/batch: 98.11% | 1.000 | 1.000 |
| elf | 19602 | 20507 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 90.37% | 0 | 89.33% | -1.05% | filetypes/elf: 90.70% | 0.999 | 1.000 |
| javascript | 12395 | 69938 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 60.52% | 0 | 47.39% | -13.13% | filetypes/javascript: 63.78% | 0.971 | 0.963 |
| zip | 11859 | 1231 | `general,filetypes/zip` | filetypes/zip: 39.07% | 0 | 26.89% | -12.18% | filetypes/zip: 39.56% | 0.986 | 0.986 |
| xlsx | 6279 | 164 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 52.17% | 0 | 29.29% | -22.89% | filegroups/documents: 52.17% | 0.999 | 0.999 |
| kotlin | 4034 | 6277 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 44.03% | 0 | 46.93% | 2.90% | filetypes/kotlin: 47.60% | 0.973 | 0.976 |
| xls | 3911 | 2651 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.17% | 0 | 92.02% | -2.15% | filegroups/documents: 94.73% | 0.998 | 0.998 |
| tar.gz | 3660 | 1915 | `general,filetypes/tar.gz` | filetypes/tar.gz: 80.25% | 0 | 57.92% | -22.32% | filetypes/tar.gz: 82.19% | 0.999 | 0.999 |
| doc | 3334 | 7 | `general,filegroups/documents` | filegroups/documents: 99.55% | 0 | 99.31% | -0.24% | filegroups/documents: 99.64% | — | 1.000 |
| unknown | 2679 | 32951 | `general` | general: 2.09% | 0 | 0.00% | -2.09% | general: 2.50% | — | 0.516 |
| python | 2344 | 20184 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 45.61% | 0 | 48.21% | 2.60% | filetypes/python: 62.71% | 0.968 | 0.960 |
| package.json | 2222 | 2056 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 88.97% | 0 | 90.46% | 1.49% | filegroups/config: 94.69% | 0.999 | 0.999 |
| rar | 2161 | 0 | `general` | general: 100.00% | 0 | 36.74% | -63.26% | general: 100.00% | — | — |
| c | 1779 | 73290 | `general,filegroups/source,filetypes/c` | filetypes/c: 9.27% | 0 | 2.98% | -6.30% | filetypes/c: 9.56% | 0.351 | 0.319 |
| shell | 1561 | 6645 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 75.40% | 0 | 18.83% | -56.57% | filetypes/shell: 77.07% | 0.988 | 0.976 |
| zst | 1312 | 2046 | `general` | general: 97.41% | 0 | 29.27% | -68.14% | general: 98.40% | — | 1.000 |
| pkg-info | 1277 | 169 | `general,filetypes/pkg-info` | general: 82.46% | 0 | 83.95% | 1.49% | filetypes/pkg-info: 99.92% | 1.000 | 1.000 |
| vbs | 1207 | 427 | `general,filetypes/vbs` | filetypes/vbs: 56.84% | 0 | 62.30% | 5.47% | filetypes/vbs: 64.46% | 0.997 | 0.997 |
| go | 1182 | 13310 | `general,filegroups/source,filetypes/go` | filetypes/go: 1.86% | 0 | 1.35% | -0.51% | filetypes/go: 1.86% | 0.450 | 0.605 |
| 7z | 729 | 16 | `general` | general: 88.75% | 0 | 36.76% | -51.99% | general: 90.26% | — | 0.999 |
| ole | 678 | 730 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 94.84% | 0 | 44.84% | -50.00% | filegroups/documents: 94.84% | 0.997 | 0.997 |
| png | 672 | 18697 | `general,filegroups/media,filetypes/png` | general: 0.00% | 0 | 0.00% | 0.00% | filetypes/png: 2.83% | 0.130 | 0.154 |
| rtf | 668 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.65% | 0 | 98.65% | 0.00% | filetypes/rtf: 98.65% | 1.000 | 1.000 |
| msi | 574 | 16 | `general` | general: 54.18% | 0 | 0.00% | -54.18% | general: 71.95% | — | 0.995 |
| powershell | 570 | 290 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 42.81% | 0 | 51.40% | 8.60% | filegroups/scripts: 62.63% | 0.988 | 0.988 |
| php | 554 | 14765 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 60.83% | 0 | 40.97% | -19.86% | filetypes/php: 66.79% | 0.907 | 0.902 |
| lnk | 488 | 131 | `general,filetypes/lnk` | filetypes/lnk: 82.58% | 0 | 72.34% | -10.25% | filetypes/lnk: 82.58% | 0.992 | 0.991 |
| docx | 482 | 57 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 89.42% | 0 | 86.31% | -3.11% | filetypes/docx: 90.46% | 0.995 | 0.991 |
| gz | 473 | 8121 | `general` | general: 22.62% | 0 | 0.00% | -22.62% | general: 32.14% | — | 0.701 |
| xml | 374 | 22164 | `general,filegroups/config,filetypes/xml` | general: 2.67% | 0 | 2.67% | 0.00% | filegroups/config: 3.21% | 0.250 | 0.329 |
| jar | 370 | 430 | `general,filetypes/jar` | filetypes/jar: 64.05% | 0 | 64.05% | 0.00% | filetypes/jar: 64.59% | 0.989 | 0.981 |
| python-bytecode | 339 | 9150 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.35% | 0 | 90.27% | -7.08% | filetypes/python-bytecode: 97.64% | 0.981 | 0.981 |
| macho | 319 | 1454 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 65.20% | 0 | 67.08% | 1.88% | filetypes/macho: 86.83% | 0.992 | 0.943 |
| csharp | 241 | 8112 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 29.88% | 0 | 27.80% | -2.07% | filegroups/source: 31.54% | 0.614 | 0.601 |
| java_class | 218 | 83138 | `general,filegroups/portable,filetypes/java_class` | general: 53.67% | 0 | 57.80% | 4.13% | general: 61.93% | 0.004 | 0.387 |
| tar | 182 | 63 | `general,filetypes/tar` | filetypes/tar: 97.80% | 0 | 95.05% | -2.75% | filetypes/tar: 97.80% | 0.995 | 0.995 |
| text | 169 | 8705 | `general,filetypes/text` | general: 13.61% | 0 | 12.43% | -1.18% | general: 14.79% | 0.197 | 0.204 |
| rust | 166 | 10339 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 3.01% | 0 | 2.41% | -0.60% | filetypes/rust: 4.22% | 0.110 | 0.089 |
| jpeg | 148 | 3284 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 12.84% | 0 | 1.35% | -11.49% | filetypes/jpeg: 12.84% | 0.301 | 0.286 |
| json | 92 | 3861 | `general,filegroups/config,filetypes/json` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.047 | 0.047 |
| cab | 80 | 12 | `general` | general: 8.75% | 0 | 0.00% | -8.75% | general: 75.00% | — | 0.966 |
| plist | 66 | 1576 | `general,filegroups/config,filetypes/plist` | filegroups/config: 6.06% | 0 | 6.06% | 0.00% | general: 6.06% | 0.128 | 0.150 |
| pptx | 64 | 21 | `general,filegroups/documents,filetypes/pptx` | filetypes/pptx: 65.62% | 0 | 39.06% | -26.56% | filetypes/pptx: 65.62% | 0.932 | 0.895 |
| makefile | 59 | 2913 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.097 | 0.024 |
| deb | 43 | 820 | `general,filetypes/deb` | filetypes/deb: 11.63% | 0 | 11.63% | 0.00% | filetypes/deb: 11.63% | 0.658 | 0.560 |
| markdown | 41 | 7507 | `general,filetypes/markdown` | general: 9.76% | 0 | 2.44% | -7.32% | general: 9.76% | 0.007 | 0.050 |
| crx | 39 | 12 | `general,filetypes/crx` | filetypes/crx: 92.31% | 0 | 87.18% | -5.13% | filetypes/crx: 92.31% | 0.992 | 0.987 |
| perl | 34 | 4172 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 76.47% | 0 | 70.59% | -5.88% | filetypes/perl: 91.18% | 0.960 | 0.958 |
| data | 31 | 1196 | `general` | general: 35.48% | 0 | 0.00% | -35.48% | general: 35.48% | — | 0.500 |
| chm | 29 | 5 | `general` | general: 93.10% | 0 | 0.00% | -93.10% | general: 93.10% | — | 0.993 |
| html | 25 | 3226 | `general,filegroups/documents,filetypes/html` | filegroups/documents: 68.00% | 0 | 68.00% | 0.00% | filegroups/documents: 72.00% | 0.842 | 0.842 |
| asar | 16 | 1 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| groovy | 15 | 791 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.065 | 0.077 |
| lua | 13 | 2292 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 61.54% | -7.69% | filegroups/scripts: 76.92% | 0.783 | 0.774 |
| ruby | 11 | 2981 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 72.73% | 0 | 0.00% | -72.73% | filegroups/scripts: 81.82% | 0.924 | 0.932 |
| java | 10 | 4459 | `general,filegroups/source,filetypes/java` | filegroups/source: 50.00% | 0 | 30.00% | -20.00% | filegroups/source: 60.00% | 0.370 | 0.513 |
| package-lock.json | 8 | 75 | `general,filetypes/package-lock.json` | general: 0.00% | — | — | — | general: 0.00% | 0.068 | 0.068 |
| clojure | 7 | 330 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 57.14% | 0.00% | filetypes/clojure: 57.14% | 0.631 | 0.631 |
| chrome-manifest | 6 | 54 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 50.00% | 0 | 0.00% | -50.00% | filetypes/chrome-manifest: 50.00% | 0.691 | 0.691 |
| dockerfile | 6 | 198 | `general,filetypes/dockerfile` | general: 0.00% | — | — | — | general: 0.00% | 0.422 | 0.283 |
| objc | 5 | 2568 | `general` | general: 80.00% | 0 | 0.00% | -80.00% | general: 80.00% | — | 0.803 |
| zig | 5 | 17 | `general` | general: 40.00% | 0 | 20.00% | -20.00% | general: 40.00% | — | 0.631 |
| xz | 4 | 3920 | `general` | general: 25.00% | 0 | 0.00% | -25.00% | general: 25.00% | — | 0.366 |
| applescript | 3 | 35 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.792 |
| bz2 | 3 | 1424 | `general` | general: 66.67% | 0 | 33.33% | -33.33% | general: 66.67% | — | 0.667 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| pkg | 3 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 100.00% | — | 0.639 |
| swift | 3 | 3871 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.062 |
| whl | 3 | 26 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.184 |
| cargo.toml | 2 | 21 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| pyproject.toml | 2 | 2 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 1.000 |
| desktop-entry | 1 | 65 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| github-actions | 1 | 824 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.125 |
| ooxml | 1 | 6 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| systemd | 1 | 154 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.008 |
| tar.bz2 | 1 | 29 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| xpi | 1 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.55% | -99.55% |
| zst | `` | 0 | 0.00% | 97.41% | -97.41% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| 7z | `` | 0 | 0.00% | 88.75% | -88.75% |
| objc | `` | 0 | 0.00% | 80.00% | -80.00% |
| applescript | `` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `` | 0 | 0.00% | 66.67% | -66.67% |
| msi | `` | 0 | 0.00% | 54.18% | -54.18% |
| chrome-manifest | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 27.27% | 72.73% | -45.45% |
| zig | `` | 0 | 0.00% | 40.00% | -40.00% |
| data | `` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| cab | `` | 0 | 0.00% | 8.75% | -8.75% |
| lnk | `general,filetypes/lnk` | 0 | 74.80% | 82.58% | -7.79% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 12.16% | 12.84% | -0.68% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| dockerfile | `` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 48.01% | 43.52% | 4.49% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.12% | 97.41% | -68.29% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.01% | 60.52% | -13.51% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 39.62% | 43.52% | -3.90% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.12% | 97.41% | -68.29% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.08% | 60.52% | -13.43% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 39.68% | 43.52% | -3.83% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.12% | 97.41% | -68.29% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.12% | 60.52% | -13.39% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 39.72% | 43.52% | -3.80% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.12% | 97.41% | -68.29% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.20% | 60.52% | -13.31% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 39.80% | 43.52% | -3.72% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.12% | 97.41% | -68.29% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 39.94% | 43.52% | -3.57% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.19% | 97.41% | -68.22% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.13% | 82.58% | -10.45% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 40.19% | 43.52% | -3.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| shell | `general,filetypes/shell` | 0 | 77.07% | 75.40% | 1.67% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| shell | `filetypes/shell` | 0 | 3.65% | 75.40% | -71.75% |
| zst | `general` | 0 | 29.19% | 97.41% | -68.22% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.70% | 100.00% | -63.30% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.34% | 82.58% | -10.25% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 40.42% | 43.52% | -3.09% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.27% | 97.41% | -68.14% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `filetypes/shell` | 0 | 9.22% | 75.40% | -66.18% |
| rar | `general` | 0 | 36.74% | 100.00% | -63.26% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 0.68% | 12.84% | -12.16% |
| lnk | `filetypes/lnk` | 0 | 72.34% | 82.58% | -10.25% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 40.57% | 43.52% | -2.95% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.27% | 97.41% | -68.14% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.74% | 100.00% | -63.26% |
| shell | `filetypes/shell` | 0 | 18.83% | 75.40% | -56.57% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 36.76% | 88.75% | -51.99% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| jpeg | `filetypes/jpeg` | 0 | 1.35% | 12.84% | -11.49% |
| lnk | `filetypes/lnk` | 0 | 72.34% | 82.58% | -10.25% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 40.72% | 43.52% | -2.80% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.27% | 97.41% | -68.14% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.74% | 100.00% | -63.26% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 37.04% | 88.75% | -51.71% |
| shell | `filetypes/shell` | 0 | 23.96% | 75.40% | -51.44% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| lnk | `filetypes/lnk` | 0 | 72.34% | 82.58% | -10.25% |
| jpeg | `filetypes/jpeg` | 0 | 2.70% | 12.84% | -10.14% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 35.89% | 43.52% | -7.62% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.27% | 97.41% | -68.14% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.79% | 100.00% | -63.21% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 37.04% | 88.75% | -51.71% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| shell | `filetypes/shell` | 0 | 26.46% | 75.40% | -48.94% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| pe | `filetypes/pe` | 0 | 19.56% | 43.52% | -23.95% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| lnk | `filetypes/lnk` | 0 | 72.34% | 82.58% | -10.25% |
| jpeg | `filetypes/jpeg` | 0 | 2.70% | 12.84% | -10.14% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.27% | 97.41% | -68.14% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.83% | 100.00% | -63.17% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 37.04% | 88.75% | -51.71% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| shell | `filetypes/shell` | 0 | 29.47% | 75.40% | -45.93% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| lnk | `filetypes/lnk` | 0 | 72.75% | 82.58% | -9.84% |
| jpeg | `filetypes/jpeg` | 0 | 3.38% | 12.84% | -9.46% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 48.01% | 43.52% | 4.49% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.34% | 97.41% | -68.06% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.83% | 100.00% | -63.17% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 37.04% | 88.75% | -51.71% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| shell | `filetypes/shell` | 0 | 31.39% | 75.40% | -44.01% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| lnk | `filetypes/lnk` | 0 | 72.75% | 82.58% | -9.84% |
| jpeg | `filetypes/jpeg` | 0 | 3.38% | 12.84% | -9.46% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 48.01% | 43.52% | 4.49% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| cargo.toml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| ooxml | `general` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 93.10% | -93.10% |
| objc | `general` | 0 | 0.00% | 80.00% | -80.00% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 72.73% | -72.73% |
| zst | `general` | 0 | 29.42% | 97.41% | -67.99% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.93% | 100.00% | -63.07% |
| msi | `general` | 0 | 0.00% | 54.18% | -54.18% |
| 7z | `general` | 0 | 37.04% | 88.75% | -51.71% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 44.84% | 94.84% | -50.00% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| shell | `filetypes/shell` | 0 | 34.59% | 75.40% | -40.81% |
| data | `general` | 0 | 0.00% | 35.48% | -35.48% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 39.06% | 65.62% | -26.56% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 29.29% | 52.17% | -22.89% |
| gz | `general` | 0 | 0.00% | 22.62% | -22.62% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 57.92% | 80.25% | -22.32% |
| java | `general,filegroups/source` | 0 | 30.00% | 50.00% | -20.00% |
| zig | `general` | 0 | 20.00% | 40.00% | -20.00% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 40.97% | 60.83% | -19.86% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 47.39% | 60.52% | -13.13% |
| zip | `general,filetypes/zip` | 0 | 26.89% | 39.07% | -12.18% |
| lnk | `filetypes/lnk` | 0 | 72.75% | 82.58% | -9.84% |
| jpeg | `filetypes/jpeg` | 0 | 4.05% | 12.84% | -8.78% |
| cab | `general` | 0 | 0.00% | 8.75% | -8.75% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 61.54% | 69.23% | -7.69% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 90.27% | 97.35% | -7.08% |
| c | `general,filegroups/source,filetypes/c` | 0 | 2.98% | 9.27% | -6.30% |
| perl | `filetypes/perl` | 0 | 70.59% | 76.47% | -5.88% |
| crx | `general,filetypes/crx` | 0 | 87.18% | 92.31% | -5.13% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 86.31% | 89.42% | -3.11% |
| tar | `filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.02% | 94.17% | -2.15% |
| unknown | `general` | 0 | 0.00% | 2.09% | -2.09% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 27.80% | 29.88% | -2.07% |
| text | `general,filetypes/text` | 0 | 12.43% | 13.61% | -1.18% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.33% | 90.37% | -1.05% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.41% | 3.01% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.35% | 1.86% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 99.31% | 99.55% | -0.24% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.63% | 11.63% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| jar | `general,filetypes/jar` | 0 | 64.05% | 64.05% | 0.00% |
| json | `filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.65% | 98.65% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config` | 0 | 2.67% | 2.67% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 8.11% | 7.94% | 0.18% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.13% | 97.84% | 0.29% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.46% | 88.97% | 1.49% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 83.95% | 82.46% | 1.49% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 67.08% | 65.20% | 1.88% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.21% | 45.61% | 2.60% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.93% | 44.03% | 2.90% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 57.80% | 53.67% | 4.13% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 48.01% | 43.52% | 4.49% |
| vbs | `general,filetypes/vbs` | 0 | 62.30% | 56.84% | 5.47% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 51.40% | 42.81% | 8.60% |
