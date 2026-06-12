# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 924639 (314123 malware, 610516 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 164925 | 20260 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 57.23% | 0 | 50.93% | -6.30% | filegroups/native: 62.92% | 1.000 | 1.000 |
| elf | 22552 | 22610 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 94.20% | 0 | 94.44% | 0.23% | filetypes/elf: 97.00% | 1.000 | 0.999 |
| pdf | 22502 | 2976 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 7.63% | 0 | 7.87% | 0.24% | filetypes/pdf: 73.79% | 0.992 | 0.992 |
| batch | 22107 | 689 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 2.41% | 0 | 1.55% | -0.86% | filetypes/batch: 2.41% | 0.980 | 0.980 |
| javascript | 14888 | 81081 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 61.57% | 0 | 45.69% | -15.87% | filegroups/scripts: 65.46% | 0.950 | 0.947 |
| zip | 12722 | 1543 | `general,filetypes/zip` | general: 36.77% | 0 | 34.33% | -2.44% | general: 39.64% | 0.975 | 0.973 |
| xlsx | 7500 | 201 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.03% | 0 | 30.13% | -0.89% | filegroups/documents: 31.05% | 0.995 | 0.995 |
| xls | 4697 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.78% | 0 | 93.76% | -1.02% | filetypes/xls: 95.06% | 0.997 | 0.997 |
| doc | 3983 | 7 | `general,filegroups/documents` | filegroups/documents: 96.79% | — | — | — | filegroups/documents: 98.90% | — | 1.000 |
| kotlin | 3949 | 6907 | `general,filegroups/source,filetypes/kotlin` | filegroups/source: 52.57% | 0 | 52.67% | 0.10% | filegroups/source: 56.98% | 0.894 | 0.878 |
| python | 2824 | 27179 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 45.33% | 0 | 48.94% | 3.61% | filetypes/python: 57.01% | 0.786 | 0.789 |
| tar | 2806 | 3396 | `general,filetypes/tar` | filetypes/tar: 85.14% | 0 | 71.88% | -13.26% | filetypes/tar: 88.28% | 0.994 | 0.988 |
| rar | 2579 | 1 | `general` | general: 99.22% | 0 | 30.17% | -69.06% | general: 100.00% | — | 1.000 |
| package.json | 2267 | 2923 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 87.16% | 0 | 89.24% | 2.07% | general: 91.93% | 0.996 | 0.996 |
| c | 2143 | 97740 | `general,filegroups/source,filetypes/c` | general: 7.42% | 0 | 4.53% | -2.89% | filegroups/source: 8.73% | 0.214 | 0.252 |
| unknown | 2103 | 6685 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.62% | — | 0.740 |
| shell | 1950 | 8082 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 73.13% | 0 | 73.23% | 0.10% | filetypes/shell: 75.28% | 0.966 | 0.966 |
| vbs | 1457 | 428 | `general,filetypes/vbs` | filetypes/vbs: 22.99% | 0 | 26.29% | 3.29% | filetypes/vbs: 43.58% | 0.989 | 0.990 |
| go | 1396 | 16015 | `general,filegroups/source,filetypes/go` | filetypes/go: 4.30% | 0 | 4.51% | 0.21% | filetypes/go: 4.94% | 0.194 | 0.209 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 12.78% | -74.98% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 289 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.46% | 0 | 95.69% | 0.23% | general: 97.02% | 0.998 | 0.998 |
| 7z | 1071 | 14 | `general` | general: 90.29% | 0 | 28.48% | -61.81% | general: 91.78% | — | 0.999 |
| png | 1053 | 22769 | `general,filegroups/media,filetypes/png` | filegroups/media: 5.03% | 0 | 2.66% | -2.37% | general: 5.60% | 0.157 | 0.157 |
| ole | 813 | 799 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 82.41% | 0 | 81.67% | -0.74% | filetypes/ole: 83.15% | 0.989 | 0.989 |
| rtf | 791 | 55 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.36% | 0 | 98.10% | -0.25% | filetypes/rtf: 98.36% | 0.999 | 0.999 |
| php | 713 | 19535 | `general,filegroups/scripts,filetypes/php` | general: 50.35% | 0 | 48.25% | -2.10% | filegroups/scripts: 55.54% | 0.765 | 0.766 |
| powershell | 677 | 312 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 49.48% | 0 | 50.81% | 1.33% | filetypes/powershell: 55.39% | 0.983 | 0.979 |
| text | 598 | 13216 | `general,filetypes/text` | filetypes/text: 4.68% | 0 | 4.52% | -0.17% | general: 4.68% | 0.122 | 0.114 |
| docx | 569 | 59 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 83.48% | 0 | 74.34% | -9.14% | filegroups/documents: 83.48% | 0.989 | 0.989 |
| msi | 561 | 15 | `general,filetypes/msi` | filetypes/msi: 76.83% | 0 | 65.78% | -11.05% | filetypes/msi: 81.82% | 0.997 | 0.996 |
| lnk | 547 | 132 | `general,filetypes/lnk` | filetypes/lnk: 83.55% | 0 | 70.75% | -12.80% | filetypes/lnk: 83.55% | 0.991 | 0.990 |
| gz | 532 | 9116 | `general` | general: 44.17% | 0 | 0.00% | -44.17% | general: 44.92% | — | 0.695 |
| xml | 507 | 28364 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.56% | 0 | 1.78% | -0.79% | filegroups/config: 2.56% | 0.122 | 0.094 |
| jar | 459 | 489 | `general,filetypes/jar` | filetypes/jar: 58.61% | 0 | 58.61% | 0.00% | filetypes/jar: 60.13% | 0.958 | 0.951 |
| csharp | 418 | 9682 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 15.55% | 0 | 13.88% | -1.67% | filegroups/source: 18.42% | 0.362 | 0.363 |
| python-bytecode | 415 | 24307 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 83.61% | 0 | 77.59% | -6.02% | filetypes/python-bytecode: 83.86% | 0.862 | 0.866 |
| java | 361 | 9905 | `general,filegroups/source,filetypes/java` | general: 1.94% | 0 | 1.66% | -0.28% | filegroups/source: 2.22% | 0.138 | 0.168 |
| macho | 341 | 1570 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 79.77% | 0 | 80.94% | 1.17% | filetypes/macho: 92.38% | 0.990 | 0.985 |
| java_class | 240 | 98272 | `general,filegroups/portable,filetypes/java_class` | general: 59.58% | 0 | 45.00% | -14.58% | filegroups/portable: 72.08% | 0.871 | 0.872 |
| rust | 228 | 11902 | `general,filegroups/source,filetypes/rust` | general: 2.19% | 0 | 0.88% | -1.32% | general: 2.19% | 0.024 | 0.024 |
| crx | 177 | 10 | `general,filetypes/crx` | filetypes/crx: 97.74% | 0 | 28.81% | -68.93% | filetypes/crx: 97.74% | 0.999 | 0.999 |
| jpeg | 176 | 3849 | `general,filegroups/media,filetypes/jpeg` | general: 10.23% | 0 | 10.23% | 0.00% | general: 10.23% | 0.195 | 0.226 |
| json | 134 | 6384 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.017 |
| cab | 99 | 11 | `general` | general: 38.38% | 0 | 0.00% | -38.38% | general: 82.83% | — | 0.988 |
| makefile | 88 | 3996 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.026 | 0.026 |
| plist | 82 | 1623 | `general,filegroups/config,filetypes/plist` | filegroups/config: 4.88% | 0 | 2.44% | -2.44% | general: 4.88% | 0.112 | 0.112 |
| pptx | 73 | 22 | `general,filegroups/documents` | filegroups/documents: 9.59% | — | — | — | filegroups/documents: 43.84% | — | 0.821 |
| deb | 51 | 965 | `general,filetypes/deb` | general: 9.80% | 0 | 9.80% | 0.00% | general: 9.80% | 0.135 | 0.129 |
| perl | 41 | 5328 | `general,filegroups/scripts,filetypes/perl` | general: 56.10% | 0 | 56.10% | 0.00% | filetypes/perl: 65.85% | 0.797 | 0.800 |
| chm | 38 | 7 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 97.37% | — | 0.995 |
| data | 38 | 1388 | `general` | general: 18.42% | 0 | 0.00% | -18.42% | general: 28.95% | — | 0.438 |
| cargo.toml | 28 | 173 | `general,filetypes/cargo.toml` | general: 32.14% | 0 | 17.86% | -14.29% | general: 32.14% | 0.472 | 0.472 |
| applescript | 26 | 36 | `general,filetypes/applescript` | filetypes/applescript: 26.92% | 0 | 23.08% | -3.85% | general: 26.92% | 0.544 | 0.538 |
| whl | 25 | 113 | `general,filetypes/whl` | filetypes/whl: 60.00% | 0 | 60.00% | 0.00% | filetypes/whl: 68.00% | 0.878 | 0.856 |
| gem | 24 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| npm | 23 | 2 | `general` | general: 82.61% | 0 | 0.00% | -82.61% | general: 100.00% | — | 0.992 |
| ruby | 21 | 3474 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 38.10% | 0 | 42.86% | 4.76% | filetypes/ruby: 47.62% | 0.562 | 0.566 |
| asar | 18 | 1 | `general` | general: 88.89% | 0 | 0.00% | -88.89% | general: 100.00% | — | 0.994 |
| dockerfile | 18 | 273 | `general,filetypes/dockerfile` | filetypes/dockerfile: 5.56% | 0 | 5.56% | 0.00% | filetypes/dockerfile: 5.56% | 0.205 | 0.180 |
| groovy | 16 | 953 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.015 | 0.015 |
| html | 14 | 1991 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2388 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 38.46% | -30.77% | general: 69.23% | 0.681 | 0.712 |
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
| asar | `` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.90% | 99.22% | -69.33% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 29.93% | 99.22% | -69.29% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.01% | 99.22% | -69.21% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.09% | 99.22% | -69.14% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.55% | 87.76% | -75.21% |
| rar | `general` | 0 | 30.17% | 99.22% | -69.06% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.78% | 87.76% | -74.98% |
| rar | `general` | 0 | 30.17% | 99.22% | -69.06% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| rar | `general` | 0 | 30.21% | 99.22% | -69.02% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| rar | `general` | 0 | 30.24% | 99.22% | -68.98% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 12.86% | 87.76% | -74.90% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.40% | 99.22% | -68.83% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.48% | 90.29% | -61.81% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 13.09% | 87.76% | -74.67% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.48% | 99.22% | -68.75% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.57% | 90.29% | -61.72% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 13.17% | 87.76% | -74.59% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 30.48% | 99.22% | -68.75% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.66% | 90.29% | -61.62% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| zst | `general` | 0 | 14.11% | 87.76% | -73.66% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| rar | `general` | 0 | 32.30% | 99.22% | -66.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 29.69% | 90.29% | -60.60% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `` | 0 | 0.00% | 82.61% | -82.61% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| zst | `general` | 0 | 19.64% | 87.76% | -68.12% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.33% | 99.22% | -62.89% |
| 7z | `general` | 0 | 32.77% | 90.29% | -57.52% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.17% | -44.17% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 38.38% | -38.38% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `general` | 0 | 0.00% | 82.61% | -82.61% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 46.06% | 99.22% | -53.16% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 42.95% | 90.29% | -47.34% |
| zst | `general` | 0 | 41.62% | 87.76% | -46.14% |
| gz | `general` | 0 | 0.56% | 44.17% | -43.61% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 1.01% | 38.38% | -37.37% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `general` | 0 | 0.00% | 82.61% | -82.61% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 53.01% | 99.22% | -46.22% |
| 7z | `general` | 0 | 48.65% | 90.29% | -41.64% |
| gz | `general` | 0 | 2.82% | 44.17% | -41.35% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| cab | `general` | 0 | 2.02% | 38.38% | -36.36% |
| zst | `general` | 0 | 51.60% | 87.76% | -36.17% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `general` | 0 | 0.00% | 82.61% | -82.61% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 59.79% | 99.22% | -39.43% |
| gz | `general` | 0 | 5.26% | 44.17% | -38.91% |
| 7z | `general` | 0 | 54.90% | 90.29% | -35.39% |
| cab | `general` | 0 | 6.06% | 38.38% | -32.32% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| zst | `general` | 0 | 65.55% | 87.76% | -22.21% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.69% | 61.57% | -15.87% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 45.00% | 59.58% | -14.58% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| c | `general,filegroups/source` | 0 | 4.53% | 7.42% | -2.89% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| gem | `general` | 0 | 4.17% | 100.00% | -95.83% |
| asar | `general` | 0 | 0.00% | 88.89% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| crx | `general,filetypes/crx` | 0 | 28.81% | 97.74% | -68.93% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| npm | `general` | 0 | 17.39% | 82.61% | -65.22% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 65.30% | 99.22% | -33.93% |
| gz | `general` | 0 | 12.03% | 44.17% | -32.14% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| cab | `general` | 0 | 13.13% | 38.38% | -25.25% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| zst | `general` | 0 | 83.09% | 87.76% | -4.68% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| gem | `general` | 0 | 45.83% | 100.00% | -54.17% |
| markdown | `general` | 0 | 0.00% | 50.00% | -50.00% |
| npm | `general` | 0 | 39.13% | 82.61% | -43.48% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| rar | `general` | 0 | 68.28% | 99.22% | -30.94% |
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| gz | `general` | 0 | 16.35% | 44.17% | -27.82% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cab | `general` | 0 | 22.22% | 38.38% | -16.16% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| zst | `general` | 0 | 85.81% | 87.76% | -1.95% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| lua | `general,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| gem | `general` | 0 | 70.83% | 100.00% | -29.17% |
| rar | `general` | 0 | 70.18% | 99.22% | -29.04% |
| npm | `general` | 0 | 56.52% | 82.61% | -26.09% |
| gz | `general` | 0 | 19.17% | 44.17% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| cab | `general` | 0 | 26.26% | 38.38% | -12.12% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| xml | `filegroups/config` | 0 | 1.78% | 2.56% | -0.79% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.94% | 45.33% | 3.61% |
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
| npm | `general` | 0 | 56.52% | 82.61% | -26.09% |
| rar | `general` | 0 | 73.17% | 99.22% | -26.06% |
| gz | `general` | 0 | 21.99% | 44.17% | -22.18% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 0.00% | 18.42% | -18.42% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| gem | `general` | 0 | 87.50% | 100.00% | -12.50% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 50.93% | 57.23% | -6.30% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 77.59% | 83.61% | -6.02% |
| cab | `general` | 0 | 33.33% | 38.38% | -5.05% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.66% | 5.03% | -2.37% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.25% | 50.35% | -2.10% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| xml | `general,filegroups/config` | 0 | 2.17% | 2.56% | -0.39% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 57.86% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.44% | 94.20% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
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
| rar | `general` | 0 | 77.05% | 99.22% | -22.18% |
| npm | `general` | 0 | 60.87% | 82.61% | -21.74% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 26.69% | 44.17% | -17.48% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| gem | `general` | 0 | 91.67% | 100.00% | -8.33% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 50.91% | 55.54% | -4.63% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 59.83% | 62.92% | -3.09% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 1 | 3.23% | 5.60% | -2.37% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| rust | `general,filegroups/source` | 0 | 0.88% | 2.19% | -1.32% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 96.15% | 97.00% | -0.85% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| xml | `general,filegroups/config` | 0 | 2.17% | 2.56% | -0.39% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 83.37% | 83.61% | -0.24% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 57.86% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.51% | 4.30% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
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
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| rar | `general` | 0 | 81.19% | 99.22% | -18.03% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 2.63% | 18.42% | -15.79% |
| gz | `general` | 0 | 29.32% | 44.17% | -14.85% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 17.86% | 32.14% | -14.29% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| tar | `general,filetypes/tar` | 0 | 71.88% | 85.14% | -13.26% |
| npm | `general` | 0 | 69.57% | 82.61% | -13.04% |
| lnk | `general,filetypes/lnk` | 0 | 70.75% | 83.55% | -12.80% |
| java_class | `general,filetypes/java_class` | 1 | 59.58% | 72.08% | -12.50% |
| msi | `general,filetypes/msi` | 0 | 65.78% | 76.83% | -11.05% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 74.34% | 83.48% | -9.14% |
| gem | `general` | 0 | 91.67% | 100.00% | -8.33% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 50.91% | 55.54% | -4.63% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| pe | `general,filegroups/native,filetypes/pe` | 1 | 59.83% | 62.92% | -3.09% |
| plist | `filegroups/config` | 0 | 2.44% | 4.88% | -2.44% |
| zip | `general,filetypes/zip` | 0 | 34.33% | 36.77% | -2.44% |
| png | `general,filegroups/media,filetypes/png` | 1 | 3.23% | 5.60% | -2.37% |
| c | `general,filegroups/source` | 1 | 6.86% | 8.73% | -1.87% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.88% | 15.55% | -1.67% |
| xls | `filetypes/xls` | 0 | 93.76% | 94.78% | -1.02% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 30.13% | 31.03% | -0.89% |
| rust | `general,filegroups/source` | 0 | 1.32% | 2.19% | -0.88% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.55% | 2.41% | -0.86% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 96.15% | 97.00% | -0.85% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 81.67% | 82.41% | -0.74% |
| xml | `general,filegroups/config` | 0 | 2.17% | 2.56% | -0.39% |
| java | `general,filegroups/source` | 0 | 1.66% | 1.94% | -0.28% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.10% | 98.36% | -0.25% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 83.37% | 83.61% | -0.24% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 61.37% | 61.57% | -0.19% |
| text | `general,filetypes/text` | 0 | 4.52% | 4.68% | -0.17% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.80% | 9.80% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 5.56% | 5.56% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `filetypes/jar` | 0 | 58.61% | 58.61% | 0.00% |
| jpeg | `filegroups/media` | 0 | 10.23% | 10.23% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filetypes/perl` | 0 | 56.10% | 56.10% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| python | `general,filegroups/scripts,filetypes/python` | 2 | 57.86% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 60.00% | 60.00% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.67% | 52.57% | 0.10% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 73.23% | 73.13% | 0.10% |
| go | `general,filegroups/source,filetypes/go` | 1 | 5.09% | 4.94% | 0.14% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.69% | 95.46% | 0.23% |
| pdf | `general,filegroups/documents` | 0 | 7.87% | 7.63% | 0.24% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 80.94% | 79.77% | 1.17% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 50.81% | 49.48% | 1.33% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 89.24% | 87.16% | 2.07% |
| vbs | `general,filetypes/vbs` | 0 | 26.29% | 22.99% | 3.29% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 42.86% | 38.10% | 4.76% |
