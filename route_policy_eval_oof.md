# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 924639 (314123 malware, 610516 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 164925 | 20260 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 57.23% | 0 | 21.86% | -35.36% | filegroups/native: 62.92% | 1.000 | 1.000 |
| elf | 22552 | 22610 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 94.20% | 0 | 91.40% | -2.80% | filetypes/elf: 97.00% | 1.000 | 0.999 |
| pdf | 22502 | 2976 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 7.63% | 0 | 6.03% | -1.60% | filetypes/pdf: 73.79% | 0.992 | 0.992 |
| batch | 22107 | 689 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 2.41% | 0 | 0.94% | -1.47% | filetypes/batch: 2.41% | 0.980 | 0.980 |
| javascript | 14888 | 81081 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 61.57% | 0 | 20.82% | -40.75% | filegroups/scripts: 65.46% | 0.950 | 0.947 |
| zip | 12722 | 1543 | `general,filetypes/zip` | general: 36.77% | 0 | 26.68% | -10.09% | general: 39.64% | 0.975 | 0.973 |
| xlsx | 7500 | 201 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.03% | 0 | 29.88% | -1.15% | filegroups/documents: 31.05% | 0.995 | 0.995 |
| xls | 4697 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.78% | 0 | 82.63% | -12.16% | filetypes/xls: 95.06% | 0.997 | 0.997 |
| doc | 3983 | 7 | `general,filegroups/documents` | filegroups/documents: 96.79% | 0 | 78.89% | -17.90% | filegroups/documents: 98.90% | — | 1.000 |
| kotlin | 3949 | 6907 | `general,filegroups/source,filetypes/kotlin` | filegroups/source: 52.57% | 0 | 45.00% | -7.57% | filegroups/source: 56.98% | 0.894 | 0.878 |
| python | 2824 | 27179 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 45.33% | 0 | 42.92% | -2.41% | filetypes/python: 57.01% | 0.786 | 0.789 |
| tar | 2806 | 3396 | `general,filetypes/tar` | filetypes/tar: 85.14% | 0 | 76.51% | -8.62% | filetypes/tar: 88.28% | 0.994 | 0.988 |
| rar | 2579 | 1 | `general` | general: 99.22% | 0 | 10.90% | -88.33% | general: 100.00% | — | 1.000 |
| package.json | 2267 | 2923 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 87.16% | 0 | 71.72% | -15.44% | general: 91.93% | 0.996 | 0.996 |
| c | 2143 | 97740 | `general,filegroups/source,filetypes/c` | general: 7.42% | 0 | 6.91% | -0.51% | filegroups/source: 8.73% | 0.214 | 0.252 |
| unknown | 2103 | 6685 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.62% | — | 0.740 |
| shell | 1950 | 8082 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 73.13% | 0 | 9.08% | -64.05% | filetypes/shell: 75.28% | 0.966 | 0.966 |
| vbs | 1457 | 428 | `general,filetypes/vbs` | filetypes/vbs: 22.99% | 0 | 17.50% | -5.49% | filetypes/vbs: 43.58% | 0.989 | 0.990 |
| go | 1396 | 16015 | `general,filegroups/source,filetypes/go` | filetypes/go: 4.30% | 0 | 4.44% | 0.14% | filetypes/go: 4.94% | 0.194 | 0.209 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 0.00% | -87.76% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 289 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.46% | 0 | 71.57% | -23.88% | general: 97.02% | 0.998 | 0.998 |
| 7z | 1071 | 14 | `general` | general: 90.29% | 0 | 16.15% | -74.14% | general: 91.78% | — | 0.999 |
| png | 1053 | 22769 | `general,filegroups/media,filetypes/png` | filegroups/media: 5.03% | 0 | 0.09% | -4.94% | general: 5.60% | 0.157 | 0.157 |
| ole | 813 | 799 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 82.41% | 0 | 10.82% | -71.59% | filetypes/ole: 83.15% | 0.989 | 0.989 |
| rtf | 791 | 55 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.36% | 0 | 97.22% | -1.14% | filetypes/rtf: 98.36% | 0.999 | 0.999 |
| php | 713 | 19535 | `general,filegroups/scripts,filetypes/php` | general: 50.35% | 0 | 48.53% | -1.82% | filegroups/scripts: 55.54% | 0.765 | 0.766 |
| powershell | 677 | 312 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 49.48% | 0 | 33.53% | -15.95% | filetypes/powershell: 55.39% | 0.983 | 0.979 |
| text | 598 | 13216 | `general,filetypes/text` | filetypes/text: 4.68% | 0 | 3.01% | -1.67% | general: 4.68% | 0.122 | 0.114 |
| docx | 569 | 59 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 83.48% | 0 | 51.32% | -32.16% | filegroups/documents: 83.48% | 0.989 | 0.989 |
| msi | 561 | 15 | `general,filetypes/msi` | filetypes/msi: 92.52% | 0 | 52.41% | -40.12% | filetypes/msi: 95.33% | 0.999 | 0.996 |
| lnk | 547 | 132 | `general,filetypes/lnk` | filetypes/lnk: 83.55% | 0 | 68.01% | -15.54% | filetypes/lnk: 83.55% | 0.991 | 0.990 |
| gz | 532 | 9116 | `general` | general: 44.17% | 0 | 0.00% | -44.17% | general: 44.92% | — | 0.695 |
| xml | 507 | 28364 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.56% | 0 | 1.58% | -0.99% | filegroups/config: 2.56% | 0.122 | 0.094 |
| jar | 459 | 489 | `general,filetypes/jar` | filetypes/jar: 58.61% | 0 | 45.75% | -12.85% | filetypes/jar: 60.13% | 0.958 | 0.951 |
| csharp | 418 | 9682 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 15.55% | 0 | 15.79% | 0.24% | filegroups/source: 18.42% | 0.362 | 0.363 |
| python-bytecode | 415 | 24307 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 83.61% | 0 | 39.04% | -44.58% | filetypes/python-bytecode: 83.86% | 0.862 | 0.866 |
| java | 361 | 9905 | `general,filegroups/source,filetypes/java` | general: 1.94% | 0 | 1.66% | -0.28% | filegroups/source: 2.22% | 0.138 | 0.168 |
| macho | 341 | 1570 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 79.77% | 0 | 51.03% | -28.74% | filetypes/macho: 92.38% | 0.990 | 0.985 |
| java_class | 240 | 98272 | `general,filegroups/portable,filetypes/java_class` | general: 59.58% | 0 | 22.08% | -37.50% | filegroups/portable: 72.08% | 0.871 | 0.872 |
| rust | 228 | 11902 | `general,filegroups/source,filetypes/rust` | general: 2.19% | 0 | 1.32% | -0.88% | general: 2.19% | 0.024 | 0.024 |
| crx | 177 | 10 | `general,filetypes/crx` | filetypes/crx: 97.74% | 0 | 28.81% | -68.93% | filetypes/crx: 97.74% | 0.999 | 0.999 |
| jpeg | 176 | 3849 | `general,filegroups/media,filetypes/jpeg` | general: 10.23% | 0 | 1.14% | -9.09% | general: 10.23% | 0.195 | 0.226 |
| json | 134 | 6384 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.017 |
| cab | 99 | 11 | `general` | general: 38.38% | 0 | 0.00% | -38.38% | general: 82.83% | — | 0.988 |
| makefile | 88 | 3996 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.026 | 0.026 |
| plist | 82 | 1623 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.88% | 0 | 1.22% | -3.66% | general: 4.88% | 0.112 | 0.112 |
| pptx | 73 | 22 | `general,filegroups/documents` | filegroups/documents: 9.59% | 0 | 0.00% | -9.59% | filegroups/documents: 43.84% | — | 0.821 |
| deb | 51 | 965 | `general,filetypes/deb` | general: 9.80% | 0 | 9.80% | 0.00% | general: 9.80% | 0.135 | 0.129 |
| perl | 41 | 5328 | `general,filegroups/scripts,filetypes/perl` | general: 56.10% | 0 | 56.10% | 0.00% | filetypes/perl: 65.85% | 0.797 | 0.800 |
| chm | 38 | 7 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 97.37% | — | 0.995 |
| data | 38 | 1388 | `general` | general: 18.42% | 0 | 0.00% | -18.42% | general: 28.95% | — | 0.438 |
| cargo.toml | 28 | 173 | `general,filetypes/cargo.toml` | general: 32.14% | 0 | 17.86% | -14.29% | general: 32.14% | 0.472 | 0.472 |
| applescript | 26 | 36 | `general,filetypes/applescript` | filetypes/applescript: 26.92% | 0 | 23.08% | -3.85% | general: 26.92% | 0.544 | 0.538 |
| whl | 25 | 113 | `general,filetypes/whl` | filetypes/whl: 60.00% | 0 | 60.00% | 0.00% | filetypes/whl: 68.00% | 0.878 | 0.856 |
| gem | 24 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| npm | 23 | 2 | `general` | general: 82.61% | 0 | 0.00% | -82.61% | general: 100.00% | — | 0.992 |
| ruby | 21 | 3474 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 38.10% | 0 | 28.57% | -9.52% | filetypes/ruby: 47.62% | 0.562 | 0.566 |
| asar | 18 | 1 | `general` | general: 88.89% | 0 | 0.00% | -88.89% | general: 100.00% | — | 0.994 |
| dockerfile | 18 | 273 | `general,filetypes/dockerfile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 1.000 | 0.148 |
| groovy | 16 | 953 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.049 | 0.043 |
| html | 14 | 1991 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2388 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 30.77% | -38.46% | general: 69.23% | 0.681 | 0.712 |
| package-lock.json | 12 | 84 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.151 |
| apk_android | 11 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| markdown | 10 | 3652 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 0.943 |
| xz | 10 | 4902 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.494 |
| chrome-manifest | 8 | 56 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 62.50% | 0 | 62.50% | 0.00% | filetypes/chrome-manifest: 62.50% | 0.814 | 0.814 |
| clojure | 7 | 665 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.637 | 0.637 |
| pyproject.toml | 6 | 12 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 16.67% | — | 0.588 |
| objc | 5 | 2808 | `general,filetypes/objc` | general: 60.00% | 0 | 20.00% | -40.00% | general: 80.00% | 0.108 | 0.108 |
| zig | 5 | 21 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 40.00% | — | 0.530 |
| swift | 4 | 3919 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.084 |
| bz2 | 3 | 1429 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| desktop-entry | 3 | 479 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.670 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| systemd | 2 | 177 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.009 |
| composerjson | 1 | 9 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 1.000 |
| github-actions | 1 | 1017 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.200 |
| nupkg | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
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
| rar | `general` | 0 | 2.68% | 99.22% | -96.55% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 10.74% | 90.29% | -79.55% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 2.68% | 99.22% | -96.55% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 10.83% | 90.29% | -79.46% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 2.75% | 99.22% | -96.47% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 11.02% | 90.29% | -79.27% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 2.83% | 99.22% | -96.39% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 11.02% | 90.29% | -79.27% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 2.95% | 99.22% | -96.28% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 11.02% | 90.29% | -79.27% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 2.99% | 99.22% | -96.24% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 11.20% | 90.29% | -79.08% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 3.37% | 99.22% | -95.85% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 12.04% | 90.29% | -78.24% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 4.23% | 99.22% | -95.00% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 12.98% | 90.29% | -77.31% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 4.85% | 99.22% | -94.38% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 13.73% | 90.29% | -76.56% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.86% | 96.79% | -17.93% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 5.43% | 99.22% | -93.80% |
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 14.19% | 90.29% | -76.10% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 10.90% | 99.22% | -88.33% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| 7z | `general` | 0 | 16.15% | 90.29% | -74.14% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| rar | `general` | 0 | 16.17% | 99.22% | -83.06% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 5.77% | 87.76% | -82.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| 7z | `general` | 0 | 19.33% | 90.29% | -70.96% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 9.12% | 87.76% | -78.64% |
| rar | `general` | 0 | 22.37% | 99.22% | -76.85% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| 7z | `general` | 0 | 23.25% | 90.29% | -67.04% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.24% | 87.76% | -75.53% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| rar | `general` | 0 | 28.58% | 99.22% | -70.65% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| 7z | `general` | 0 | 27.64% | 90.29% | -62.65% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| rar | `general` | 0 | 29.74% | 99.22% | -69.48% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| 7z | `general` | 0 | 28.20% | 90.29% | -62.09% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.89% | 96.79% | -17.90% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 14.19% | 87.76% | -73.58% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 32.65% | 99.22% | -66.58% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| 7z | `general` | 0 | 29.88% | 90.29% | -60.41% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 78.99% | 96.79% | -17.80% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| zst | `general` | 0 | 19.25% | 87.76% | -68.51% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| rar | `general` | 0 | 36.22% | 99.22% | -63.01% |
| 7z | `general` | 0 | 32.68% | 90.29% | -57.61% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 79.01% | 96.79% | -17.78% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| zst | `general` | 0 | 27.83% | 87.76% | -59.94% |
| rar | `general` | 0 | 39.86% | 99.22% | -59.36% |
| 7z | `general` | 0 | 36.60% | 90.29% | -53.69% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 79.04% | 96.79% | -17.75% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `general` | 0 | 0.00% | 82.61% | -82.61% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 50.37% | 99.22% | -48.86% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| 7z | `general` | 0 | 46.50% | 90.29% | -43.79% |
| gz | `general` | 0 | 1.88% | 44.17% | -42.29% |
| zst | `general` | 0 | 46.92% | 87.76% | -40.84% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| cab | `general` | 0 | 1.01% | 38.38% | -37.37% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| doc | `general,filegroups/documents` | 0 | 79.29% | 96.79% | -17.50% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| npm | `general` | 0 | 0.00% | 82.61% | -82.61% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 20.82% | 61.57% | -40.75% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 59.40% | 99.22% | -39.82% |
| gz | `general` | 0 | 5.08% | 44.17% | -39.10% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| java_class | `general,filetypes/java_class` | 0 | 22.08% | 59.58% | -37.50% |
| 7z | `general` | 0 | 54.44% | 90.29% | -35.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| cab | `general` | 0 | 5.05% | 38.38% | -33.33% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| zst | `general` | 0 | 64.15% | 87.76% | -23.62% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| doc | `general,filegroups/documents` | 0 | 81.17% | 96.79% | -15.62% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.91% | 7.42% | -0.51% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| gem | `general` | 0 | 4.17% | 100.00% | -95.83% |
| asar | `general` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| npm | `general` | 0 | 17.39% | 82.61% | -65.22% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| rar | `general` | 0 | 65.65% | 99.22% | -33.58% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| gz | `general` | 0 | 12.22% | 44.17% | -31.95% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| cab | `general` | 0 | 13.13% | 38.38% | -25.25% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| doc | `general,filegroups/documents` | 0 | 84.38% | 96.79% | -12.40% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| zst | `general` | 0 | 83.24% | 87.76% | -4.52% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| gem | `general` | 0 | 58.33% | 100.00% | -41.67% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| npm | `general` | 0 | 52.17% | 82.61% | -30.43% |
| rar | `general` | 0 | 68.90% | 99.22% | -30.32% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| gz | `general` | 0 | 17.86% | 44.17% | -26.32% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| cab | `general` | 0 | 24.24% | 38.38% | -14.14% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| doc | `general,filegroups/documents` | 0 | 84.48% | 96.79% | -12.30% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| zst | `general` | 0 | 86.28% | 87.76% | -1.48% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| gem | `general` | 0 | 70.83% | 100.00% | -29.17% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| rar | `general` | 0 | 70.84% | 99.22% | -28.38% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| npm | `general` | 0 | 56.52% | 82.61% | -26.09% |
| gz | `general` | 0 | 19.92% | 44.17% | -24.25% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| doc | `general,filegroups/documents` | 0 | 84.86% | 96.79% | -11.93% |
| cab | `general` | 0 | 27.27% | 38.38% | -11.11% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| pptx | `general,filegroups/documents` | 0 | 0.00% | 9.59% | -9.59% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 42.92% | 45.33% | -2.41% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 1.58% | 2.56% | -0.99% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 7.89% | 86.84% | -78.95% |
| asar | `general` | 0 | 11.11% | 88.89% | -77.78% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 39.04% | 83.61% | -44.58% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 21.86% | 57.23% | -35.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| rar | `general` | 0 | 74.21% | 99.22% | -25.01% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| npm | `general` | 0 | 60.87% | 82.61% | -21.74% |
| gz | `general` | 0 | 23.50% | 44.17% | -20.68% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| gem | `general` | 0 | 91.67% | 100.00% | -8.33% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 9.59% | -8.22% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.09% | 5.03% | -4.94% |
| python | `general,filetypes/python` | 1 | 52.23% | 57.01% | -4.78% |
| doc | `general,filegroups/documents` | 0 | 92.17% | 96.79% | -4.62% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.40% | 94.20% | -2.80% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.53% | 50.35% | -1.82% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| xml | `general,filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| cab | `general` | 0 | 38.38% | 38.38% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |

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
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| chm | `general` | 0 | 23.68% | 86.84% | -63.16% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 33.23% | 57.23% | -23.99% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| rar | `general` | 0 | 77.70% | 99.22% | -21.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 26.88% | 44.17% | -17.29% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `general` | 0 | 69.57% | 82.61% | -13.04% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| gem | `general` | 0 | 91.67% | 100.00% | -8.33% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 9.59% | -8.22% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.90% | 83.61% | -7.71% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| python | `general,filetypes/python` | 1 | 52.23% | 57.01% | -4.78% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| png | `general,filegroups/media,filetypes/png` | 1 | 2.09% | 5.60% | -3.51% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| xml | `general,filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.32% | 94.20% | 0.12% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.44% | 4.30% | 0.14% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |
| php | `general,filetypes/php` | 0 | 50.63% | 50.35% | 0.28% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| nupkg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 88.89% | -77.78% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.82% | 82.41% | -71.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 9.08% | 73.13% | -64.05% |
| chm | `general` | 0 | 34.21% | 86.84% | -52.63% |
| msi | `general,filetypes/msi` | 0 | 52.41% | 92.52% | -40.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 30.77% | 69.23% | -38.46% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 51.32% | 83.48% | -32.16% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 51.03% | 79.77% | -28.74% |
| java_class | `general,filetypes/java_class` | 0 | 31.67% | 59.58% | -27.92% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 33.23% | 57.23% | -23.99% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 71.57% | 95.46% | -23.88% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 41.44% | 61.57% | -20.13% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| rar | `general` | 0 | 81.16% | 99.22% | -18.07% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 33.53% | 49.48% | -15.95% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| lnk | `general,filetypes/lnk` | 0 | 68.01% | 83.55% | -15.54% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 71.72% | 87.16% | -15.44% |
| gz | `general` | 0 | 29.32% | 44.17% | -14.85% |
| cargo.toml | `general` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `general` | 0 | 69.57% | 82.61% | -13.04% |
| jar | `general,filetypes/jar` | 0 | 45.75% | 58.61% | -12.85% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 82.63% | 94.78% | -12.16% |
| zip | `general,filetypes/zip` | 0 | 26.68% | 36.77% | -10.09% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 38.10% | -9.52% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 1.14% | 10.23% | -9.09% |
| tar | `general,filetypes/tar` | 0 | 76.51% | 85.14% | -8.62% |
| gem | `general` | 0 | 91.67% | 100.00% | -8.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.90% | 83.61% | -7.71% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 45.00% | 52.57% | -7.57% |
| vbs | `general,filetypes/vbs` | 0 | 17.50% | 22.99% | -5.49% |
| pptx | `general,filegroups/documents` | 0 | 4.11% | 9.59% | -5.48% |
| python | `general,filetypes/python` | 1 | 52.23% | 57.01% | -4.78% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 1.22% | 4.88% | -3.66% |
| png | `general,filegroups/media,filetypes/png` | 1 | 2.09% | 5.60% | -3.51% |
| text | `general,filetypes/text` | 0 | 3.01% | 4.68% | -1.67% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 6.03% | 7.63% | -1.60% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.94% | 2.41% | -1.47% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.88% | 31.03% | -1.15% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.22% | 98.36% | -1.14% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| xml | `general,filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.66% | 1.94% | -0.28% |
| c | `general,filegroups/source,filetypes/c` | 0 | 7.23% | 7.42% | -0.19% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general,filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.32% | 94.20% | 0.12% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 15.79% | 15.55% | 0.24% |
| php | `general,filetypes/php` | 0 | 50.63% | 50.35% | 0.28% |
