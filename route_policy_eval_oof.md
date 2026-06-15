# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 991247 (326734 malware, 664513 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 171362 | 20600 | `general,filegroups/native,filetypes/pe` | filegroups/native: 55.45% | 0 | 57.35% | 1.90% | filegroups/native: 65.38% | 0.999 | 0.999 |
| elf | 23343 | 24158 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 92.79% | 0 | 93.05% | 0.26% | filetypes/elf: 95.83% | 1.000 | 1.000 |
| pdf | 22519 | 3088 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 71.58% | 0 | 71.61% | 0.03% | filetypes/pdf: 73.38% | 0.994 | 0.993 |
| batch | 22130 | 745 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 2.09% | 0 | 2.06% | -0.03% | filegroups/scripts: 2.35% | 0.998 | 0.994 |
| javascript | 15966 | 85276 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 66.77% | 0 | 38.29% | -28.47% | filetypes/javascript: 67.57% | 0.943 | 0.932 |
| zip | 12966 | 2079 | `general,filetypes/zip` | filetypes/zip: 40.36% | 0 | 36.43% | -3.93% | filetypes/zip: 40.59% | 0.969 | 0.967 |
| xlsx | 7860 | 210 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 30.97% | 0 | 30.45% | -0.53% | filegroups/documents: 30.97% | 0.995 | 0.995 |
| xls | 4944 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.24% | 0 | 93.83% | -0.40% | filegroups/documents: 94.42% | 0.995 | 0.995 |
| doc | 4189 | 7 | `general,filegroups/documents` | filegroups/documents: 96.32% | — | — | — | filegroups/documents: 98.73% | — | 1.000 |
| kotlin | 4023 | 7339 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 55.64% | 0 | 53.62% | -2.02% | filetypes/kotlin: 58.50% | 0.910 | 0.910 |
| tar | 3856 | 5156 | `general,filetypes/tar` | filetypes/tar: 91.31% | 0 | 91.44% | 0.13% | filetypes/tar: 93.70% | 0.995 | 0.992 |
| python | 2922 | 29621 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 41.17% | 0 | 45.04% | 3.87% | general: 53.49% | 0.805 | 0.804 |
| rar | 2684 | 1 | `general` | general: 99.11% | 0 | 21.61% | -77.50% | general: 100.00% | — | 1.000 |
| unknown | 2362 | 12480 | `general` | general: 0.04% | 0 | 0.00% | -0.04% | general: 0.34% | — | 0.387 |
| package.json | 2339 | 3126 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 88.41% | 0 | 91.83% | 3.42% | filegroups/config: 95.90% | 0.996 | 0.996 |
| c | 2205 | 104725 | `general,filegroups/source` | general: 7.48% | — | — | — | general: 10.25% | — | 0.261 |
| shell | 1906 | 8489 | `general,filegroups/scripts,filetypes/shell` | filegroups/scripts: 71.88% | 0 | 48.11% | -23.77% | filegroups/scripts: 71.98% | 0.962 | 0.962 |
| vbs | 1534 | 429 | `general,filetypes/vbs` | filetypes/vbs: 35.42% | 0 | 42.31% | 6.89% | filetypes/vbs: 64.91% | 0.993 | 0.993 |
| go | 1432 | 16708 | `general,filegroups/source,filetypes/go` | filetypes/go: 4.89% | 0 | 4.54% | -0.35% | filetypes/go: 6.22% | 0.260 | 0.226 |
| zst | 1312 | 2784 | `general` | general: 97.41% | 0 | 3.89% | -93.52% | general: 97.41% | — | 0.991 |
| pkg-info | 1278 | 321 | `general,filetypes/pkg-info` | filetypes/pkg-info: 96.71% | 0 | 96.71% | 0.00% | general: 96.95% | 0.998 | 0.998 |
| 7z | 1117 | 16 | `general` | general: 91.76% | 0 | 24.44% | -67.32% | general: 91.76% | — | 0.999 |
| png | 1115 | 24068 | `general,filegroups/media,filetypes/png` | filegroups/media: 1.61% | 0 | 2.69% | 1.08% | filetypes/png: 5.29% | 0.119 | 0.124 |
| ole | 866 | 817 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 78.84% | 0 | 78.18% | -0.67% | filetypes/ole: 78.96% | 0.991 | 0.991 |
| rtf | 829 | 55 | `general,filegroups/documents,filetypes/rtf` | general: 97.23% | 0 | 97.10% | -0.12% | general: 97.23% | 0.999 | 0.999 |
| text | 744 | 15124 | `general` | general: 3.36% | 0 | 0.00% | -3.36% | general: 3.90% | — | 0.130 |
| php | 735 | 20767 | `general,filegroups/scripts,filetypes/php` | general: 47.48% | 0 | 45.71% | -1.77% | general: 55.37% | 0.789 | 0.775 |
| powershell | 716 | 331 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 46.37% | 0 | 47.77% | 1.40% | filetypes/powershell: 61.31% | 0.987 | 0.982 |
| msi | 693 | 20 | `general,filetypes/msi` | filetypes/msi: 83.26% | 0 | 81.39% | -1.88% | filetypes/msi: 83.55% | 0.997 | 0.996 |
| docx | 595 | 62 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 79.33% | 0 | 73.61% | -5.71% | filegroups/documents: 80.50% | 0.991 | 0.991 |
| lnk | 570 | 132 | `general,filetypes/lnk` | filetypes/lnk: 73.16% | 0 | 70.88% | -2.28% | filetypes/lnk: 73.16% | 0.988 | 0.987 |
| gz | 559 | 9823 | `general` | general: 41.50% | 0 | 0.00% | -41.50% | general: 43.11% | — | 0.694 |
| xml | 537 | 33302 | `general,filegroups/config,filetypes/xml` | filetypes/xml: 4.47% | 0 | 5.77% | 1.30% | filetypes/xml: 6.33% | 0.103 | 0.124 |
| jar | 462 | 548 | `general,filetypes/jar` | filetypes/jar: 58.66% | 0 | 57.36% | -1.30% | filetypes/jar: 58.66% | 0.977 | 0.968 |
| csharp | 458 | 9815 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 13.60% | 0 | 13.76% | 0.16% | filegroups/source: 15.79% | 0.350 | 0.356 |
| java | 447 | 10298 | `general,filegroups/source` | general: 1.34% | 0 | 0.00% | -1.34% | filegroups/source: 1.57% | — | 0.171 |
| python-bytecode | 443 | 33989 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 79.91% | 0 | 75.85% | -4.06% | filetypes/python-bytecode: 80.59% | 0.834 | 0.832 |
| macho | 343 | 1623 | `general,filegroups/native,filetypes/macho` | filegroups/native: 69.10% | 0 | 71.14% | 2.04% | filetypes/macho: 91.25% | 0.990 | 0.988 |
| apk_android | 335 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| java_class | 262 | 99313 | `general,filegroups/portable,filetypes/java_class` | filegroups/portable: 72.90% | 0 | 61.45% | -11.45% | filetypes/java_class: 76.72% | 0.880 | 0.878 |
| rust | 243 | 12565 | `general,filegroups/source` | general: 1.65% | 0 | 0.82% | -0.82% | general: 2.06% | — | 0.076 |
| jpeg | 183 | 3996 | `general,filegroups/media` | general: 6.01% | — | — | — | filegroups/media: 13.66% | — | 0.239 |
| npm | 158 | 11 | `general,filetypes/npm` | filetypes/npm: 84.21% | 0 | 71.52% | -12.69% | filetypes/npm: 85.53% | 0.996 | 0.993 |
| json | 146 | 7802 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.047 |
| cab | 104 | 13 | `general` | general: 31.73% | 0 | 0.00% | -31.73% | general: 74.04% | — | 0.984 |
| whl | 104 | 559 | `general,filetypes/whl` | filetypes/whl: 65.66% | 0 | 60.58% | -5.08% | filetypes/whl: 80.81% | 0.934 | 0.911 |
| crx | 102 | 13 | `general,filetypes/crx` | general: 52.94% | 0 | 65.69% | 12.75% | filetypes/crx: 75.49% | 0.987 | 0.984 |
| makefile | 94 | 4264 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.037 |
| plist | 83 | 1637 | `general,filegroups/config,filetypes/plist` | general: 2.41% | 0 | 2.41% | 0.00% | filegroups/config: 4.82% | 0.121 | 0.121 |
| pptx | 80 | 23 | `general,filegroups/documents` | filegroups/documents: 10.00% | — | — | — | filegroups/documents: 50.00% | — | 0.853 |
| deb | 55 | 965 | `general,filetypes/deb` | filetypes/deb: 10.91% | 0 | 10.91% | 0.00% | filetypes/deb: 10.91% | 0.148 | 0.142 |
| data | 42 | 1405 | `general` | general: 23.81% | 0 | 0.00% | -23.81% | general: 33.33% | — | 0.462 |
| perl | 41 | 5435 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 60.98% | 0 | 63.41% | 2.44% | filetypes/perl: 68.29% | 0.804 | 0.802 |
| chm | 35 | 7 | `general` | general: 77.14% | 0 | 0.00% | -77.14% | general: 80.00% | — | 0.984 |
| gem | 32 | 62 | `general,filetypes/gem` | filetypes/gem: 96.67% | 0 | 90.62% | -6.04% | filetypes/gem: 96.67% | 0.991 | 0.979 |
| cargo.toml | 30 | 242 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 33.33% | — | 0.432 |
| applescript | 26 | 40 | `general,filetypes/applescript` | filetypes/applescript: 26.92% | 0 | 23.08% | -3.85% | general: 26.92% | 0.498 | 0.498 |
| ruby | 25 | 3513 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 40.00% | 0 | 44.00% | 4.00% | filetypes/ruby: 40.00% | 0.483 | 0.492 |
| dockerfile | 22 | 296 | `general,filetypes/dockerfile` | filetypes/dockerfile: 4.55% | 0 | 4.55% | 0.00% | filetypes/dockerfile: 4.55% | 0.195 | 0.167 |
| asar | 19 | 1 | `general` | general: 84.21% | 0 | 0.00% | -84.21% | general: 100.00% | — | 0.992 |
| groovy | 16 | 986 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.053 | 0.048 |
| html | 15 | 1991 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| package-lock.json | 14 | 89 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.304 |
| lua | 13 | 2408 | `general,filegroups/scripts` | general: 69.23% | 0 | 7.69% | -61.54% | general: 69.23% | — | 0.725 |
| chrome-manifest | 11 | 57 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 72.73% | 0 | 72.73% | 0.00% | filetypes/chrome-manifest: 72.73% | 0.906 | 0.905 |
| markdown | 10 | 4670 | `general` | general: 70.00% | 0 | 0.00% | -70.00% | general: 100.00% | — | 0.970 |
| xz | 10 | 5154 | `general` | general: 10.00% | 0 | 0.00% | -10.00% | general: 10.00% | — | 0.276 |
| clojure | 7 | 715 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.625 | 0.625 |
| nupkg | 6 | 7 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 66.67% | — | 0.780 |
| pyproject.toml | 6 | 14 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 33.33% | — | 0.727 |
| swift | 6 | 4097 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.056 |
| zig | 6 | 21 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 33.33% | — | 0.475 |
| bz2 | 5 | 1424 | `general` | general: 60.00% | 0 | 0.00% | -60.00% | general: 60.00% | — | 0.681 |
| objc | 5 | 2847 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 80.00% | — | 0.713 |
| composerjson | 3 | 24 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.324 |
| desktop-entry | 3 | 516 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.669 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| pkg | 3 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.319 |
| crate | 2 | 159 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.567 |
| systemd | 2 | 192 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.011 |
| github-actions | 1 | 1104 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| odf | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| ooxml | 1 | 7 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.125 |
| vsix | 1 | 111 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.016 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 10 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.75% | 99.11% | -78.35% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.55% | 91.76% | -68.22% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.75% | 99.11% | -78.35% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.55% | 91.76% | -68.22% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.79% | 99.11% | -78.32% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.63% | 91.76% | -68.13% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.83% | 99.11% | -78.28% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.63% | 91.76% | -68.13% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.86% | 99.11% | -78.24% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.63% | 91.76% | -68.13% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.90% | 99.11% | -78.20% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.63% | 91.76% | -68.13% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.66% | 97.41% | -93.75% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 20.90% | 99.11% | -78.20% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.90% | 91.76% | -67.86% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 21.05% | 99.11% | -78.06% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.90% | 91.76% | -67.86% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 21.24% | 99.11% | -77.87% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 23.90% | 91.76% | -67.86% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 21.39% | 99.11% | -77.72% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.35% | 91.76% | -67.41% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 21.61% | 99.11% | -77.50% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.44% | 91.76% | -67.32% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| rar | `general` | 0 | 21.83% | 99.11% | -77.27% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.44% | 91.76% | -67.32% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 22.06% | 99.11% | -77.05% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.53% | 91.76% | -67.23% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.89% | 97.41% | -93.52% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 22.17% | 99.11% | -76.94% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.53% | 91.76% | -67.23% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 3.96% | 97.41% | -93.45% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 22.28% | 99.11% | -76.83% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.62% | 91.76% | -67.14% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 4.04% | 97.41% | -93.37% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 22.43% | 99.11% | -76.68% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| 7z | `general` | 0 | 24.62% | 91.76% | -67.14% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 4.34% | 97.41% | -93.06% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 24.18% | 99.11% | -74.93% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 26.32% | 91.76% | -65.44% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| zst | `general` | 0 | 6.33% | 97.41% | -91.08% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| rar | `general` | 0 | 25.75% | 99.11% | -73.36% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 27.84% | 91.76% | -63.92% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 41.50% | -41.50% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.00% | 3.36% | -3.36% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| java | `general,filegroups/source` | 0 | 0.00% | 1.34% | -1.34% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| zst | `general` | 0 | 34.68% | 97.41% | -62.73% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 40.80% | 99.11% | -58.31% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 43.51% | 91.76% | -48.25% |
| gz | `general` | 0 | 0.36% | 41.50% | -41.14% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 0.00% | 31.73% | -31.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 0.40% | 3.36% | -2.96% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| java | `general,filegroups/source` | 0 | 0.22% | 1.34% | -1.12% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `general` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 48.73% | 99.11% | -50.37% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| 7z | `general` | 0 | 52.19% | 91.76% | -39.57% |
| gz | `general` | 0 | 3.58% | 41.50% | -37.92% |
| zst | `general` | 0 | 59.76% | 97.41% | -37.65% |
| cab | `general` | 0 | 2.88% | 31.73% | -28.85% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| text | `general` | 0 | 1.08% | 3.36% | -2.28% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| java | `general,filegroups/source` | 0 | 0.22% | 1.34% | -1.12% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 84.21% | -84.21% |
| chm | `general` | 0 | 0.00% | 77.14% | -77.14% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| lua | `general,filegroups/scripts` | 0 | 7.69% | 69.23% | -61.54% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 55.51% | 99.11% | -43.59% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| gz | `general` | 0 | 6.08% | 41.50% | -35.42% |
| 7z | `general` | 0 | 59.27% | 91.76% | -32.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 38.29% | 66.77% | -28.47% |
| cab | `general` | 0 | 6.73% | 31.73% | -25.00% |
| zst | `general` | 0 | 72.79% | 97.41% | -24.62% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| nupkg | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 61.45% | 72.90% | -11.45% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| text | `general` | 0 | 1.48% | 3.36% | -1.88% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| rust | `general,filegroups/source` | 0 | 0.82% | 1.65% | -0.82% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 10.00% | 10.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 2.86% | 77.14% | -74.29% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 64.64% | 99.11% | -34.46% |
| lua | `general,filegroups/scripts` | 0 | 38.46% | 69.23% | -30.77% |
| gz | `general` | 0 | 15.21% | 41.50% | -26.30% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| zst | `general` | 0 | 84.07% | 97.41% | -13.34% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| cab | `general` | 0 | 24.04% | 31.73% | -7.69% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.15% | 3.36% | -1.21% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 16.67% | 16.67% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 10.00% | 10.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 2.86% | 77.14% | -74.29% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 67.06% | 99.11% | -32.04% |
| lua | `general,filegroups/scripts` | 0 | 38.46% | 69.23% | -30.77% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| gz | `general` | 0 | 19.32% | 41.50% | -22.18% |
| cargo.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| zst | `general` | 0 | 85.44% | 97.41% | -11.97% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.28% | 3.36% | -1.08% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 16.67% | 16.67% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 10.00% | 10.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 2.86% | 77.14% | -74.29% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| lua | `general,filegroups/scripts` | 0 | 38.46% | 69.23% | -30.77% |
| rar | `general` | 0 | 68.82% | 99.11% | -30.29% |
| data | `general` | 0 | 0.00% | 23.81% | -23.81% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| gz | `general` | 0 | 20.93% | 41.50% | -20.57% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| zst | `general` | 0 | 86.51% | 97.41% | -10.90% |
| cargo.toml | `general` | 0 | 6.67% | 16.67% | -10.00% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 75.85% | 79.91% | -4.06% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.28% | 3.36% | -1.08% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 16.67% | 16.67% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xz | `general` | 0 | 10.00% | 10.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 45.04% | 41.17% | 3.87% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 11.64% | 100.00% | -88.36% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| markdown | `general` | 0 | 0.00% | 70.00% | -70.00% |
| chm | `general` | 0 | 11.43% | 77.14% | -65.71% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crate | `general` | 0 | 0.00% | 50.00% | -50.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| rar | `general` | 0 | 71.61% | 99.11% | -27.50% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| data | `general` | 0 | 2.38% | 23.81% | -21.43% |
| gz | `general` | 0 | 22.54% | 41.50% | -18.96% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| zst | `general` | 0 | 87.04% | 97.41% | -10.37% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| cargo.toml | `general` | 0 | 13.33% | 16.67% | -3.33% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 45.71% | 47.48% | -1.77% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.42% | 3.36% | -0.94% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 79.46% | 79.91% | -0.45% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 16.67% | 16.67% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.05% | 92.79% | 0.26% |
| python | `general,filetypes/python` | 1 | 54.38% | 53.49% | 0.89% |
| png | `general,filegroups/media,filetypes/png` | 0 | 2.69% | 1.61% | 1.08% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 57.35% | 55.45% | 1.90% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 11.64% | 100.00% | -88.36% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| markdown | `general` | 0 | 10.00% | 70.00% | -60.00% |
| objc | `general` | 0 | 0.00% | 40.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| rar | `general` | 0 | 73.40% | 99.11% | -25.71% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| data | `general` | 0 | 4.76% | 23.81% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| gz | `general` | 0 | 25.04% | 41.50% | -16.46% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| zst | `general` | 0 | 87.50% | 97.41% | -9.91% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| cargo.toml | `general` | 0 | 13.33% | 16.67% | -3.33% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.42% | 3.36% | -0.94% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 79.46% | 79.91% | -0.45% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.54% | 4.89% | -0.35% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 96.73% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 60.71% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 2 | 49.52% | — | — |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 5.29% | 5.29% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| python | `general,filetypes/python` | 1 | 54.38% | 53.49% | 0.89% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 11.64% | 100.00% | -88.36% |
| chm | `` | 0 | 0.00% | 77.14% | -77.14% |
| asar | `general` | 0 | 10.53% | 84.21% | -73.68% |
| bz2 | `general` | 0 | 0.00% | 60.00% | -60.00% |
| markdown | `general` | 0 | 10.00% | 70.00% | -60.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| rar | `general` | 0 | 74.81% | 99.11% | -24.29% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 48.11% | 71.88% | -23.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| data | `general` | 0 | 4.76% | 23.81% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| gz | `general` | 0 | 26.48% | 41.50% | -15.03% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| npm | `filetypes/npm` | 0 | 71.52% | 84.21% | -12.69% |
| javascript | `filetypes/javascript` | 0 | 59.41% | 66.77% | -7.36% |
| gem | `filetypes/gem` | 0 | 90.62% | 96.67% | -6.04% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 73.61% | 79.33% | -5.71% |
| whl | `filetypes/whl` | 0 | 60.58% | 65.66% | -5.08% |
| zip | `general,filetypes/zip` | 0 | 36.43% | 40.36% | -3.93% |
| applescript | `general,filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| cargo.toml | `general` | 0 | 13.33% | 16.67% | -3.33% |
| lnk | `general,filetypes/lnk` | 0 | 70.88% | 73.16% | -2.28% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 53.62% | 55.64% | -2.02% |
| msi | `general,filetypes/msi` | 0 | 81.39% | 83.26% | -1.88% |
| jar | `general,filetypes/jar` | 0 | 57.36% | 58.66% | -1.30% |
| text | `general` | 0 | 2.55% | 3.36% | -0.81% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 78.18% | 78.84% | -0.67% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.45% | 30.97% | -0.53% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 79.46% | 79.91% | -0.45% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 93.83% | 94.24% | -0.40% |
| go | `general,filegroups/source,filetypes/go` | 1 | 6.08% | 6.22% | -0.14% |
| rtf | `general,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| unknown | `general` | 0 | 0.00% | 0.04% | -0.04% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 2.09% | -0.03% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 50.00% | 50.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.91% | 10.91% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 96.73% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 72.90% | 72.90% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 60.71% | — | — |
| php | `general,filegroups/scripts,filetypes/php` | 2 | 49.52% | — | — |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `general,filegroups/config,filetypes/plist` | 0 | 2.41% | 2.41% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 1 | 5.29% | 5.29% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| xz | `general` | 0 | 10.00% | 10.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.61% | 71.58% | 0.03% |
| tar | `general,filetypes/tar` | 0 | 91.44% | 91.31% | 0.13% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.76% | 13.60% | 0.16% |
| python | `general,filetypes/python` | 1 | 54.38% | 53.49% | 0.89% |
| xml | `filegroups/config,filetypes/xml` | 0 | 5.77% | 4.47% | 1.30% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 47.77% | 46.37% | 1.40% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 71.14% | 69.10% | 2.04% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 63.41% | 60.98% | 2.44% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 91.83% | 88.41% | 3.42% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 44.00% | 40.00% | 4.00% |
| vbs | `general,filetypes/vbs` | 0 | 42.31% | 35.42% | 6.89% |
| crx | `general,filetypes/crx` | 0 | 65.69% | 52.94% | 12.75% |
