# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 924639 (314123 malware, 610516 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 164925 | 20260 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 52.93% | 0 | 56.71% | 3.79% | filetypes/pe: 63.83% | 1.000 | 1.000 |
| elf | 22552 | 22610 | `general,filegroups/native,filetypes/elf` | filegroups/native: 92.84% | 0 | 92.62% | -0.22% | filetypes/elf: 97.80% | 1.000 | 1.000 |
| pdf | 22502 | 2976 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 6.54% | 0 | 5.60% | -0.94% | filetypes/pdf: 73.79% | 0.992 | 0.997 |
| batch | 22107 | 689 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 2.41% | 0 | 1.55% | -0.86% | filetypes/batch: 2.41% | 0.980 | 0.980 |
| javascript | 14889 | 81081 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 62.74% | 0 | 60.60% | -2.14% | filegroups/scripts: 65.46% | 0.969 | 0.963 |
| zip | 12591 | 1530 | `general,filetypes/zip` | general: 37.12% | 0 | 31.84% | -5.28% | filetypes/zip: 41.16% | 0.994 | 0.991 |
| xlsx | 7500 | 201 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.39% | 0 | 30.27% | -1.12% | filegroups/documents: 31.63% | 0.995 | 0.984 |
| xls | 4697 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.78% | 0 | 94.04% | -0.75% | filetypes/xls: 95.06% | 0.997 | 0.997 |
| doc | 3983 | 7 | `general,filegroups/documents` | filegroups/documents: 98.97% | — | — | — | filegroups/documents: 99.52% | — | 1.000 |
| kotlin | 3948 | 6907 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 51.98% | 0 | 52.36% | 0.38% | filetypes/kotlin: 55.42% | 0.893 | 0.916 |
| python | 2824 | 27179 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 45.33% | 0 | 48.37% | 3.05% | filetypes/python: 58.25% | 0.826 | 0.824 |
| tar | 2777 | 3395 | `general,filetypes/tar` | filetypes/tar: 86.03% | 0 | 72.63% | -13.40% | filetypes/tar: 89.20% | 0.996 | 0.991 |
| rar | 2579 | 1 | `general` | general: 99.22% | 0 | 30.17% | -69.06% | general: 100.00% | — | 1.000 |
| package.json | 2267 | 2923 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 87.16% | 0 | 89.28% | 2.12% | filegroups/config: 94.18% | 0.996 | 0.997 |
| c | 2143 | 97740 | `general,filegroups/source,filetypes/c` | filetypes/c: 10.36% | 0 | 9.29% | -1.07% | filegroups/source: 11.15% | 0.269 | 0.272 |
| unknown | 2103 | 6685 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.62% | — | 0.740 |
| shell | 1950 | 8082 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 78.97% | 0 | 70.15% | -8.82% | filetypes/shell: 80.92% | 0.982 | 0.977 |
| vbs | 1457 | 428 | `general,filetypes/vbs` | filetypes/vbs: 61.50% | 0 | 62.87% | 1.37% | filetypes/vbs: 62.73% | 0.994 | 0.994 |
| go | 1396 | 16015 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.87% | 0 | 5.87% | 0.00% | filetypes/go: 6.30% | 0.655 | 0.650 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 12.78% | -74.98% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 289 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.46% | 0 | 95.69% | 0.23% | general: 97.02% | 0.998 | 0.998 |
| 7z | 1071 | 14 | `general` | general: 90.29% | 0 | 28.48% | -61.81% | general: 91.78% | — | 0.999 |
| png | 1053 | 22769 | `general,filegroups/media,filetypes/png` | filegroups/media: 5.03% | 0 | 2.66% | -2.37% | general: 5.60% | 0.157 | 0.157 |
| ole | 813 | 799 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 92.50% | 0 | 81.67% | -10.82% | filegroups/documents: 93.23% | 0.989 | 0.994 |
| rtf | 791 | 55 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.36% | 0 | 98.10% | -0.25% | filetypes/rtf: 98.36% | 0.999 | 1.000 |
| php | 713 | 19535 | `general,filegroups/scripts,filetypes/php` | general: 50.35% | 0 | 47.69% | -2.66% | filegroups/scripts: 55.54% | 0.789 | 0.782 |
| powershell | 677 | 312 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 49.48% | 0 | 50.81% | 1.33% | filegroups/scripts: 54.51% | 0.986 | 0.981 |
| text | 598 | 13216 | `general,filetypes/text` | filetypes/text: 4.68% | 0 | 4.52% | -0.17% | general: 4.68% | 0.122 | 0.114 |
| docx | 569 | 59 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 85.94% | 0 | 75.04% | -10.90% | filegroups/documents: 86.64% | 0.989 | 0.993 |
| msi | 561 | 15 | `general,filetypes/msi` | filetypes/msi: 76.83% | 0 | 65.78% | -11.05% | filetypes/msi: 81.82% | 0.997 | 0.996 |
| lnk | 547 | 132 | `general,filetypes/lnk` | filetypes/lnk: 83.55% | 0 | 70.75% | -12.80% | filetypes/lnk: 83.55% | 0.991 | 0.990 |
| gz | 532 | 9116 | `general` | general: 44.17% | 0 | 0.00% | -44.17% | general: 44.92% | — | 0.695 |
| xml | 507 | 28364 | `general,filegroups/config,filetypes/xml` | filegroups/config: 9.66% | 0 | 9.47% | -0.20% | filegroups/config: 11.05% | 0.122 | 0.134 |
| jar | 459 | 489 | `general,filetypes/jar` | filetypes/jar: 64.49% | 0 | 64.49% | 0.00% | filetypes/jar: 71.24% | 0.977 | 0.978 |
| csharp | 418 | 9682 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 17.70% | 0 | 14.59% | -3.11% | filegroups/source: 17.94% | 0.362 | 0.329 |
| python-bytecode | 415 | 24307 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 83.61% | 0 | 77.59% | -6.02% | filetypes/python-bytecode: 83.86% | 0.862 | 0.866 |
| java | 361 | 9905 | `general,filegroups/source,filetypes/java` | filetypes/java: 4.43% | 0 | 3.32% | -1.11% | filetypes/java: 6.09% | 0.225 | 0.235 |
| macho | 341 | 1570 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 85.04% | 0 | 75.66% | -9.38% | filetypes/macho: 86.22% | 0.991 | 0.985 |
| java_class | 240 | 98272 | `general,filegroups/portable,filetypes/java_class` | filetypes/java_class: 67.50% | 0 | 59.17% | -8.33% | filetypes/java_class: 78.33% | 0.821 | 0.854 |
| rust | 228 | 11902 | `general,filegroups/source,filetypes/rust` | general: 2.19% | 0 | 1.32% | -0.88% | general: 2.19% | 0.024 | 0.031 |
| crx | 177 | 10 | `general,filetypes/crx` | filetypes/crx: 97.74% | 0 | 28.81% | -68.93% | filetypes/crx: 97.74% | 0.999 | 0.999 |
| jpeg | 176 | 3849 | `general,filegroups/media,filetypes/jpeg` | general: 10.23% | 0 | 10.23% | 0.00% | general: 10.23% | 0.195 | 0.226 |
| json | 134 | 6384 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.021 |
| apk_android | 127 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| cab | 99 | 11 | `general` | general: 38.38% | 0 | 0.00% | -38.38% | general: 82.83% | — | 0.988 |
| makefile | 88 | 3996 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.026 | 0.029 |
| plist | 82 | 1623 | `general,filegroups/config,filetypes/plist` | filetypes/plist: 2.44% | 0 | 2.44% | 0.00% | general: 4.88% | 0.112 | 0.108 |
| pptx | 73 | 22 | `general,filegroups/documents` | filegroups/documents: 5.48% | — | — | — | filegroups/documents: 36.99% | — | 0.825 |
| deb | 51 | 965 | `general,filetypes/deb` | general: 9.80% | 0 | 9.80% | 0.00% | general: 9.80% | 0.135 | 0.129 |
| npm | 50 | 2 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 0.987 |
| perl | 41 | 5328 | `general,filegroups/scripts,filetypes/perl` | general: 56.10% | 0 | 56.10% | 0.00% | filetypes/perl: 65.85% | 0.797 | 0.800 |
| whl | 40 | 113 | `general,filetypes/whl` | filetypes/whl: 60.00% | 0 | 37.50% | -22.50% | filetypes/whl: 68.00% | 0.878 | 0.863 |
| chm | 38 | 7 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 97.37% | — | 0.995 |
| data | 38 | 1388 | `general` | general: 18.42% | 0 | 0.00% | -18.42% | general: 28.95% | — | 0.438 |
| cargo.toml | 28 | 173 | `general,filetypes/cargo.toml` | general: 32.14% | 0 | 17.86% | -14.29% | general: 32.14% | 0.472 | 0.472 |
| applescript | 26 | 36 | `general,filetypes/applescript` | filetypes/applescript: 26.92% | 0 | 23.08% | -3.85% | general: 26.92% | 0.544 | 0.538 |
| gem | 26 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| ruby | 21 | 3474 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 38.10% | 0 | 42.86% | 4.76% | filetypes/ruby: 47.62% | 0.562 | 0.566 |
| asar | 18 | 1 | `general` | general: 88.89% | 0 | 0.00% | -88.89% | general: 100.00% | — | 0.994 |
| dockerfile | 18 | 273 | `general,filetypes/dockerfile` | filetypes/dockerfile: 5.56% | 0 | 5.56% | 0.00% | filetypes/dockerfile: 5.56% | 0.205 | 0.180 |
| groovy | 16 | 953 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.015 | 0.015 |
| html | 14 | 1991 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2388 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 38.46% | -30.77% | general: 69.23% | 0.681 | 0.712 |
| package-lock.json | 12 | 84 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.151 |
| markdown | 10 | 3652 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 0.943 |
| xz | 10 | 4902 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.494 |
| chrome-manifest | 8 | 56 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 62.50% | 0 | 62.50% | 0.00% | filetypes/chrome-manifest: 62.50% | 0.814 | 0.814 |
| clojure | 7 | 665 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.637 | 0.637 |
| pyproject.toml | 6 | 12 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 16.67% | — | 0.588 |
| objc | 5 | 2808 | `general,filetypes/objc` | general: 60.00% | 0 | 20.00% | -40.00% | general: 80.00% | 0.108 | 0.108 |
| zig | 5 | 21 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 40.00% | — | 0.530 |
| swift | 4 | 3919 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.001 |
| bz2 | 3 | 1429 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| desktop-entry | 3 | 479 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.670 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| systemd | 2 | 177 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.009 |
| composerjson | 1 | 9 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 1.000 |
| github-actions | 1 | 1017 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.200 |
| nupkg | 1 | 1 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| ooxml | 1 | 7 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.125 |
| pkg | 1 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 8 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.44% | 98.97% | -0.53% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.93% | 99.22% | -69.29% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.69% | 98.97% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.01% | 99.22% | -69.21% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.09% | 99.22% | -69.14% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.17% | 99.22% | -69.06% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.78% | 87.76% | -74.98% |
| rar | `general` | 0 | 30.17% | 99.22% | -69.06% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| rar | `general` | 0 | 30.21% | 99.22% | -69.02% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| rar | `general` | 0 | 30.24% | 99.22% | -68.98% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.40% | 99.22% | -68.83% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 13.09% | 87.76% | -74.67% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.48% | 99.22% | -68.75% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.57% | 90.29% | -61.72% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 13.17% | 87.76% | -74.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.48% | 99.22% | -68.75% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.66% | 90.29% | -61.62% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 14.11% | 87.76% | -73.66% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 32.30% | 99.22% | -66.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 29.69% | 90.29% | -60.60% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| zst | `general` | 0 | 19.64% | 87.76% | -68.12% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.33% | 99.22% | -62.89% |
| 7z | `general` | 0 | 32.77% | 90.29% | -57.52% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 46.06% | 99.22% | -53.16% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 42.95% | 90.29% | -47.34% |
| zst | `general` | 0 | 41.62% | 87.76% | -46.14% |
| gz | `general` | 0 | 0.56% | 44.17% | -43.61% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 1.01% | 38.38% | -37.37% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 53.01% | 99.22% | -46.22% |
| 7z | `general` | 0 | 48.65% | 90.29% | -41.64% |
| gz | `general` | 0 | 2.82% | 44.17% | -41.35% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 2.02% | 38.38% | -36.36% |
| zst | `general` | 0 | 51.60% | 87.76% | -36.17% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 59.79% | 99.22% | -39.43% |
| gz | `general` | 0 | 5.26% | 44.17% | -38.91% |
| 7z | `general` | 0 | 54.90% | 90.29% | -35.39% |
| cab | `general` | 0 | 6.06% | 38.38% | -32.32% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zst | `general` | 0 | 65.55% | 87.76% | -22.21% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 59.17% | 67.50% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 60.60% | 62.74% | -2.14% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.29% | 10.36% | -1.07% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `general` | 0 | 3.85% | 100.00% | -96.15% |
| asar | `general` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `general` | 0 | 8.00% | 50.00% | -42.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 65.30% | 99.22% | -33.93% |
| gz | `general` | 0 | 12.03% | 44.17% | -32.14% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| cab | `general` | 0 | 13.13% | 38.38% | -25.25% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| zst | `general` | 0 | 83.09% | 87.76% | -4.68% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 5.56% | 88.89% | -83.33% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| gem | `general` | 0 | 42.31% | 100.00% | -57.69% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| npm | `general` | 0 | 18.00% | 50.00% | -32.00% |
| rar | `general` | 0 | 68.28% | 99.22% | -30.94% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| gz | `general` | 0 | 16.35% | 44.17% | -27.82% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cab | `general` | 0 | 22.22% | 38.38% | -16.16% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| zst | `general` | 0 | 85.81% | 87.76% | -1.95% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 5.56% | 88.89% | -83.33% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| gem | `general` | 0 | 65.38% | 100.00% | -34.62% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| rar | `general` | 0 | 70.18% | 99.22% | -29.04% |
| gz | `general` | 0 | 19.17% | 44.17% | -25.00% |
| npm | `general` | 0 | 26.00% | 50.00% | -24.00% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| cab | `general` | 0 | 26.26% | 38.38% | -12.12% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.37% | 45.33% | 3.05% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| asar | `general` | 0 | 11.11% | 88.89% | -77.78% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| rar | `general` | 0 | 73.17% | 99.22% | -26.06% |
| npm | `general` | 0 | 26.00% | 50.00% | -24.00% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| gz | `general` | 0 | 21.99% | 44.17% | -22.18% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gem | `general` | 0 | 80.77% | 100.00% | -19.23% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| cab | `general` | 0 | 33.33% | 38.38% | -5.05% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.69% | 50.35% | -2.66% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 56.94% | 58.25% | -1.31% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| doc | `general,filegroups/documents` | 0 | 98.69% | 98.97% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.62% | 92.84% | -0.22% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.71% | 52.93% | 3.79% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 88.89% | -77.78% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| chm | `general` | 0 | 23.68% | 86.84% | -63.16% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| rar | `general` | 0 | 77.05% | 99.22% | -22.18% |
| npm | `general` | 0 | 28.00% | 50.00% | -22.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 26.69% | 44.17% | -17.48% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| gem | `general` | 0 | 84.62% | 100.00% | -15.38% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 49.65% | 55.54% | -5.89% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| png | `general,filegroups/media,filetypes/png` | 1 | 3.23% | 5.60% | -2.37% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 56.94% | 58.25% | -1.31% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 83.37% | 83.61% | -0.24% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.87% | 5.87% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 70.42% | — | — |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.81% | 97.80% | 0.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 88.89% | -77.78% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| chm | `general` | 0 | 34.21% | 86.84% | -52.63% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| whl | `filetypes/whl` | 0 | 37.50% | 60.00% | -22.50% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| rar | `general` | 0 | 81.19% | 99.22% | -18.03% |
| npm | `general` | 0 | 32.00% | 50.00% | -18.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| gem | `general` | 0 | 84.62% | 100.00% | -15.38% |
| gz | `general` | 0 | 29.32% | 44.17% | -14.85% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 72.63% | 86.03% | -13.40% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 75.04% | 85.94% | -10.90% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 81.67% | 92.50% | -10.82% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 75.66% | 85.04% | -9.38% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 70.15% | 78.97% | -8.82% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 49.65% | 55.54% | -5.89% |
| zip | `general,filetypes/zip` | 0 | 31.84% | 37.12% | -5.28% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.59% | 17.70% | -3.11% |
| png | `general,filegroups/media,filetypes/png` | 1 | 3.23% | 5.60% | -2.37% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 56.94% | 58.25% | -1.31% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.27% | 31.39% | -1.12% |
| java | `general,filegroups/source,filetypes/java` | 0 | 3.32% | 4.43% | -1.11% |
| pdf | `general,filegroups/documents` | 0 | 5.60% | 6.54% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.04% | 94.78% | -0.75% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 83.37% | 83.61% | -0.24% |
| xml | `general,filegroups/config` | 0 | 9.47% | 9.66% | -0.20% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 64.49% | 64.49% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 70.42% | — | — |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.44% | 2.44% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.81% | 97.80% | 0.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.55% | 10.36% | 0.19% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 6.23% | 5.87% | 0.36% |
| kotlin | `general,filetypes/kotlin` | 0 | 52.36% | 51.98% | 0.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 62.74% | 0.46% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 68.75% | 67.50% | 1.25% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| vbs | `general,filetypes/vbs` | 0 | 62.87% | 61.50% | 1.37% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.28% | 87.16% | 2.12% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |
