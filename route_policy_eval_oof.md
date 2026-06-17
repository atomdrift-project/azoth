# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 1000673 (323561 malware, 677112 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 168802 | 20889 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 60.47% | 0 | 54.44% | -6.03% | filetypes/pe: 62.15% | 0.999 | 0.999 |
| elf | 23425 | 24529 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 93.06% | 0 | 93.14% | 0.08% | filetypes/elf: 95.86% | 1.000 | 0.999 |
| pdf | 22516 | 3091 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 74.42% | 0 | 74.46% | 0.04% | filetypes/pdf: 74.54% | 0.989 | 0.989 |
| batch | 22130 | 751 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 1.41% | 0 | 2.06% | 0.65% | filegroups/scripts: 1.50% | 0.984 | 0.984 |
| javascript | 15559 | 85935 | `general,filegroups/scripts,filetypes/javascript` | filegroups/scripts: 58.38% | 0 | 51.48% | -6.90% | filegroups/scripts: 63.70% | 0.943 | 0.942 |
| zip | 13116 | 2211 | `general,filetypes/zip` | general: 39.54% | 0 | 32.99% | -6.55% | general: 40.19% | 0.968 | 0.965 |
| xlsx | 7861 | 210 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 30.96% | 0 | 30.64% | -0.32% | general: 30.96% | 0.996 | 0.996 |
| xls | 4945 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.76% | 0 | 93.73% | -1.03% | filetypes/xls: 94.86% | 0.996 | 0.996 |
| doc | 4189 | 7 | `general,filegroups/documents` | filegroups/documents: 96.30% | — | — | — | filegroups/documents: 98.47% | — | 1.000 |
| kotlin | 3901 | 7344 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 53.88% | 0 | 47.12% | -6.77% | filetypes/kotlin: 54.68% | 0.916 | 0.916 |
| python | 2922 | 29969 | `general,filegroups/scripts,filetypes/python` | general: 35.11% | 0 | 38.47% | 3.35% | filetypes/python: 54.55% | 0.777 | 0.781 |
| tar | 2807 | 5186 | `general,filetypes/tar` | filetypes/tar: 86.93% | 0 | 86.07% | -0.86% | filetypes/tar: 88.85% | 0.993 | 0.988 |
| rar | 2708 | 1 | `general` | general: 99.30% | 0 | 20.68% | -78.62% | general: 100.00% | — | 1.000 |
| unknown | 2363 | 12492 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.42% | — | 0.292 |
| package.json | 2344 | 3158 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 90.44% | 0 | 90.49% | 0.04% | filegroups/config: 94.45% | 0.996 | 0.996 |
| c | 2255 | 105462 | `general,filegroups/source,filetypes/c` | filegroups/source: 7.36% | 0 | 5.59% | -1.77% | filegroups/source: 10.55% | 0.202 | 0.207 |
| shell | 2039 | 8665 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 77.19% | 0 | 72.93% | -4.27% | filetypes/shell: 77.29% | 0.966 | 0.964 |
| go | 1937 | 16583 | `general,filegroups/source,filetypes/go` | filetypes/go: 3.98% | 0 | 4.28% | 0.31% | filetypes/go: 4.39% | 0.249 | 0.203 |
| vbs | 1531 | 429 | `general,filetypes/vbs` | filetypes/vbs: 24.69% | 0 | 37.95% | 13.26% | general: 38.08% | 0.995 | 0.995 |
| zst | 1283 | 2781 | `general` | general: 87.76% | 0 | 8.11% | -79.66% | general: 97.04% | — | 0.989 |
| pkg-info | 1278 | 338 | `general,filetypes/pkg-info` | filetypes/pkg-info: 96.71% | 0 | 96.71% | 0.00% | general: 96.95% | 0.998 | 0.997 |
| 7z | 1145 | 14 | `general` | general: 82.97% | 0 | 24.45% | -58.52% | general: 89.96% | — | 0.999 |
| png | 1116 | 24087 | `general,filegroups/media,filetypes/png` | filetypes/png: 2.96% | 0 | 3.14% | 0.18% | filetypes/png: 5.29% | 0.121 | 0.111 |
| ole | 858 | 822 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 78.44% | 0 | 40.56% | -37.88% | filetypes/ole: 78.67% | 0.989 | 0.989 |
| rtf | 829 | 55 | `general,filegroups/documents,filetypes/rtf` | filegroups/documents: 97.23% | 0 | 97.10% | -0.12% | filegroups/documents: 97.23% | 0.999 | 0.999 |
| text | 752 | 15564 | `general,filetypes/text` | general: 3.32% | 0 | 3.32% | 0.00% | general: 4.12% | 0.089 | 0.113 |
| php | 743 | 20913 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 52.22% | 0 | 48.32% | -3.90% | filetypes/php: 54.10% | 0.765 | 0.766 |
| powershell | 715 | 332 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 49.37% | 0 | 52.73% | 3.36% | filetypes/powershell: 60.14% | 0.982 | 0.978 |
| docx | 595 | 62 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 79.83% | 0 | 80.17% | 0.34% | filegroups/documents: 80.00% | 0.991 | 0.991 |
| msi | 586 | 15 | `general,filetypes/msi` | filetypes/msi: 80.55% | 0 | 76.96% | -3.58% | filetypes/msi: 80.55% | 0.996 | 0.995 |
| xml | 583 | 33471 | `general,filegroups/config,filetypes/xml` | filegroups/config: 1.89% | 0 | 1.89% | 0.00% | filegroups/config: 6.00% | 0.077 | 0.077 |
| lnk | 566 | 132 | `general,filetypes/lnk` | filetypes/lnk: 76.50% | 0 | 70.49% | -6.01% | filetypes/lnk: 76.50% | 0.987 | 0.986 |
| gz | 556 | 10172 | `general` | general: 44.06% | 0 | 0.00% | -44.06% | general: 44.60% | — | 0.693 |
| jar | 483 | 674 | `general,filetypes/jar` | filetypes/jar: 45.96% | 0 | 47.62% | 1.66% | filetypes/jar: 54.24% | 0.942 | 0.936 |
| csharp | 458 | 9814 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 17.03% | 0 | 13.32% | -3.71% | filetypes/csharp: 18.78% | 0.375 | 0.376 |
| java | 448 | 11425 | `general,filegroups/source,filetypes/java` | general: 1.34% | 0 | 1.34% | 0.00% | filetypes/java: 2.46% | 0.123 | 0.127 |
| python-bytecode | 443 | 37355 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 79.68% | 0 | 76.75% | -2.93% | filetypes/python-bytecode: 80.59% | 0.837 | 0.826 |
| macho | 342 | 1644 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 73.68% | 0 | 74.56% | 0.88% | filetypes/macho: 89.47% | 0.991 | 0.983 |
| java_class | 262 | 101848 | `general,filegroups/portable,filetypes/java_class` | general: 27.10% | 0 | 13.74% | -13.36% | general: 57.63% | 0.252 | 0.430 |
| rust | 244 | 12619 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 2.46% | 0 | 2.87% | 0.41% | filetypes/rust: 3.69% | 0.058 | 0.079 |
| apk_android | 228 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| crx | 208 | 24 | `general,filetypes/crx` | filetypes/crx: 91.83% | 0 | 25.00% | -66.83% | filetypes/crx: 92.79% | 0.997 | 0.996 |
| jpeg | 183 | 4001 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 10.93% | 0 | 4.37% | -6.56% | filetypes/jpeg: 11.48% | 0.233 | 0.257 |
| npm | 172 | 28 | `general,filetypes/npm` | filetypes/npm: 65.12% | 0 | 62.79% | -2.33% | filetypes/npm: 69.19% | 0.977 | 0.977 |
| json | 148 | 8085 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.022 |
| cab | 105 | 11 | `general` | general: 19.05% | 0 | 0.00% | -19.05% | general: 71.43% | — | 0.981 |
| whl | 104 | 607 | `general,filetypes/whl` | filetypes/whl: 52.88% | 0 | 52.88% | 0.00% | filetypes/whl: 65.38% | 0.887 | 0.881 |
| makefile | 101 | 4367 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.027 | 0.027 |
| plist | 83 | 1641 | `general,filegroups/config,filetypes/plist` | filegroups/config: 3.61% | 0 | 3.61% | 0.00% | filegroups/config: 4.82% | 0.182 | 0.182 |
| pptx | 80 | 23 | `general,filegroups/documents` | filegroups/documents: 10.00% | — | — | — | filegroups/documents: 51.25% | — | 0.851 |
| deb | 54 | 1023 | `general,filetypes/deb` | general: 9.26% | 0 | 9.26% | 0.00% | general: 9.26% | 0.132 | 0.124 |
| data | 42 | 1408 | `general` | general: 11.90% | 0 | 0.00% | -11.90% | general: 21.43% | — | 0.426 |
| chm | 41 | 7 | `general` | general: 87.80% | 0 | 0.00% | -87.80% | general: 97.56% | — | 0.995 |
| perl | 41 | 5536 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 60.98% | 0 | 60.98% | 0.00% | filetypes/perl: 73.17% | 0.804 | 0.804 |
| cargo.toml | 30 | 244 | `general,filetypes/cargo.toml` | general: 16.67% | 0 | 13.33% | -3.33% | general: 26.67% | 0.450 | 0.450 |
| gem | 29 | 97 | `general,filetypes/gem` | general: 89.66% | 0 | 89.66% | 0.00% | filetypes/gem: 96.55% | 0.992 | 0.986 |
| applescript | 26 | 40 | `general,filetypes/applescript` | filetypes/applescript: 26.92% | 0 | 23.08% | -3.85% | general: 26.92% | 0.498 | 0.498 |
| ruby | 25 | 3536 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 40.00% | 0 | 40.00% | 0.00% | filetypes/ruby: 40.00% | 0.470 | 0.498 |
| dockerfile | 22 | 300 | `general,filetypes/dockerfile` | filetypes/dockerfile: 4.55% | 0 | 4.55% | 0.00% | filetypes/dockerfile: 4.55% | 0.210 | 0.167 |
| asar | 21 | 1 | `general` | general: 90.48% | 0 | 0.00% | -90.48% | general: 100.00% | — | 0.996 |
| gomod | 19 | 1 | `general` | general: 5.26% | 0 | 0.00% | -5.26% | general: 100.00% | — | 1.000 |
| cargolock | 16 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 1.000 |
| groovy | 16 | 990 | `general` | general: 6.25% | 0 | 0.00% | -6.25% | general: 6.25% | — | 0.284 |
| html | 15 | 1991 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| package-lock.json | 14 | 90 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.123 |
| lua | 13 | 2418 | `general,filegroups/scripts,filetypes/lua` | filegroups/scripts: 76.92% | 0 | 46.15% | -30.77% | filegroups/scripts: 76.92% | 0.757 | 0.782 |
| chrome-manifest | 11 | 58 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 72.73% | 0 | 72.73% | 0.00% | filetypes/chrome-manifest: 72.73% | 0.908 | 0.912 |
| markdown | 10 | 4786 | `general` | general: 60.00% | 0 | 0.00% | -60.00% | general: 100.00% | — | 0.957 |
| xz | 10 | 5096 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 50.00% | — | 0.584 |
| clojure | 7 | 723 | `general,filetypes/clojure` | filetypes/clojure: 42.86% | 0 | 42.86% | 0.00% | filetypes/clojure: 57.14% | 0.607 | 0.607 |
| pyproject.toml | 6 | 14 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 16.67% | — | 0.504 |
| swift | 6 | 4097 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.080 |
| zig | 6 | 21 | `general` | general: 16.67% | 0 | 0.00% | -16.67% | general: 50.00% | — | 0.530 |
| gosum | 5 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| objc | 5 | 2847 | `general,filetypes/objc` | general: 40.00% | 0 | 20.00% | -20.00% | general: 80.00% | 0.234 | 0.234 |
| bz2 | 4 | 1429 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.525 |
| desktop-entry | 3 | 516 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.669 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| composerjson | 2 | 24 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.417 |
| crate | 2 | 316 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.025 |
| systemd | 2 | 192 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.013 |
| github-actions | 1 | 1120 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.143 |
| nupkg | 1 | 10 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.143 |
| odf | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| ooxml | 1 | 7 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.125 |
| pkg | 1 | 8 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| vsix | 1 | 84 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.333 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 12 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.68% | 99.30% | -79.62% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.79% | 99.30% | -79.51% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.83% | 99.30% | -79.47% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.83% | 99.30% | -79.47% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.83% | 99.30% | -79.47% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 19.87% | 99.30% | -79.43% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| pptx | `general,filegroups/documents` | 0 | 2.50% | 10.00% | -7.50% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| doc | `general,filegroups/documents` | 0 | 95.56% | 96.30% | -0.74% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 20.09% | 99.30% | -79.21% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 23.76% | 82.97% | -59.21% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.72% | 87.76% | -80.05% |
| rar | `general` | 0 | 20.27% | 99.30% | -79.03% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.10% | 82.97% | -58.86% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.87% | 87.76% | -79.89% |
| rar | `general` | 0 | 20.35% | 99.30% | -78.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.19% | 82.97% | -58.78% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 7.87% | 87.76% | -79.89% |
| rar | `general` | 0 | 20.53% | 99.30% | -78.77% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.45% | 82.97% | -58.52% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 8.11% | 87.76% | -79.66% |
| rar | `general` | 0 | 20.68% | 99.30% | -78.62% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.45% | 82.97% | -58.52% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 8.18% | 87.76% | -79.58% |
| rar | `general` | 0 | 20.79% | 99.30% | -78.51% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.63% | 82.97% | -58.34% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 8.34% | 87.76% | -79.42% |
| rar | `general` | 0 | 21.12% | 99.30% | -78.18% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 24.80% | 82.97% | -58.17% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 8.57% | 87.76% | -79.19% |
| rar | `general` | 0 | 21.23% | 99.30% | -78.06% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 25.07% | 82.97% | -57.90% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 8.65% | 87.76% | -79.11% |
| rar | `general` | 0 | 21.42% | 99.30% | -77.88% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 25.33% | 82.97% | -57.64% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 9.20% | 87.76% | -78.57% |
| rar | `general` | 0 | 21.75% | 99.30% | -77.55% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 25.33% | 82.97% | -57.64% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| zst | `general` | 0 | 15.67% | 87.76% | -72.10% |
| rar | `general` | 0 | 30.10% | 99.30% | -69.20% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.22% | 82.97% | -52.75% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 0.00% | 44.06% | -44.06% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 37.11% | 99.30% | -62.19% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| zst | `general` | 0 | 32.81% | 87.76% | -54.95% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 38.17% | 82.97% | -44.80% |
| gz | `general` | 0 | 0.18% | 44.06% | -43.88% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `` | 0 | 0.00% | 87.80% | -87.80% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 39.36% | 99.30% | -59.93% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 43.18% | 87.76% | -44.58% |
| gz | `general` | 0 | 0.72% | 44.06% | -43.35% |
| 7z | `general` | 0 | 41.05% | 82.97% | -41.92% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| cab | `general` | 0 | 0.00% | 19.05% | -19.05% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `general` | 0 | 0.00% | 87.80% | -87.80% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 43.21% | 99.30% | -56.09% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| gz | `general` | 0 | 3.06% | 44.06% | -41.01% |
| xz | `general` | 0 | 0.00% | 40.00% | -40.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| 7z | `general` | 0 | 48.73% | 82.97% | -34.24% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| zst | `general` | 0 | 57.29% | 87.76% | -30.48% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| cab | `general` | 0 | 2.86% | 19.05% | -16.19% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 90.48% | -90.48% |
| chm | `general` | 0 | 2.44% | 87.80% | -85.37% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 48.15% | 99.30% | -51.14% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| gz | `general` | 0 | 7.19% | 44.06% | -36.87% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| xz | `general` | 0 | 10.00% | 40.00% | -30.00% |
| 7z | `general` | 0 | 55.55% | 82.97% | -27.42% |
| zst | `general` | 0 | 66.41% | 87.76% | -21.36% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| java_class | `general` | 0 | 13.74% | 27.10% | -13.36% |
| cab | `general` | 0 | 5.71% | 19.05% | -13.33% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 51.48% | 58.38% | -6.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| c | `general,filegroups/source` | 0 | 5.59% | 7.36% | -1.77% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 4.88% | 87.80% | -82.93% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| rar | `general` | 0 | 57.35% | 99.30% | -41.95% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| gz | `general` | 0 | 14.57% | 44.06% | -29.50% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| 7z | `general` | 0 | 63.41% | 82.97% | -19.56% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| zst | `general` | 0 | 80.67% | 87.76% | -7.09% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| cab | `general` | 0 | 12.38% | 19.05% | -6.67% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 4.88% | 87.80% | -82.93% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| rar | `general` | 0 | 62.00% | 99.30% | -37.30% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| gz | `general` | 0 | 18.88% | 44.06% | -25.18% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 76.75% | 79.68% | -2.93% |
| zst | `general` | 0 | 85.19% | 87.76% | -2.57% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cab | `general` | 0 | 19.05% | 19.05% | 0.00% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| nupkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| apk_android | `` | 0 | 0.00% | 100.00% | -100.00% |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 99.30% | -99.30% |
| chm | `general` | 0 | 4.88% | 87.80% | -82.93% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| gz | `general` | 0 | 20.86% | 44.06% | -23.20% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| zst | `general` | 0 | 86.75% | 87.76% | -1.01% |
| python-bytecode | `filetypes/python-bytecode` | 1 | 79.68% | 80.59% | -0.90% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| vsix | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 38.47% | 35.11% | 3.35% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 0.44% | 100.00% | -99.56% |
| rar | `` | 0 | 0.00% | 99.30% | -99.30% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| chm | `general` | 0 | 14.63% | 87.80% | -73.17% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| gz | `general` | 0 | 23.02% | 44.06% | -21.04% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 0.00% | 11.90% | -11.90% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.44% | 60.47% | -6.03% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 48.32% | 52.22% | -3.90% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| python-bytecode | `filetypes/python-bytecode` | 1 | 79.68% | 80.59% | -0.90% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| zst | `general` | 0 | 87.37% | 87.76% | -0.39% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 54.52% | 54.55% | -0.03% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.14% | 93.06% | 0.08% |
| png | `filegroups/media,filetypes/png` | 0 | 3.14% | 2.96% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 0.44% | 100.00% | -99.56% |
| rar | `` | 0 | 0.00% | 99.30% | -99.30% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| chm | `general` | 0 | 24.39% | 87.80% | -63.41% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| gz | `general` | 0 | 24.82% | 44.06% | -19.24% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 2.38% | 11.90% | -9.52% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| python-bytecode | `filetypes/python-bytecode` | 1 | 79.68% | 80.59% | -0.90% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| zst | `general` | 0 | 87.45% | 87.76% | -0.31% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 54.52% | 54.55% | -0.03% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| png | `filegroups/media,filetypes/png` | 1 | 5.29% | 5.29% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 10.00% | 10.00% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| text | `filetypes/text` | 0 | 3.32% | 3.32% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 3 | 96.79% | 96.79% | 0.01% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 60.62% | 60.47% | 0.15% |
| go | `general,filegroups/source,filetypes/go` | 0 | 4.28% | 3.98% | 0.31% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 54.78% | 52.22% | 2.56% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gosum | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| apk_android | `general` | 0 | 0.44% | 100.00% | -99.56% |
| rar | `` | 0 | 0.00% | 99.30% | -99.30% |
| asar | `general` | 0 | 9.52% | 90.48% | -80.95% |
| crx | `general,filetypes/crx` | 0 | 25.00% | 91.83% | -66.83% |
| markdown | `general` | 0 | 0.00% | 60.00% | -60.00% |
| chm | `general` | 0 | 31.71% | 87.80% | -56.10% |
| bz2 | `general` | 0 | 0.00% | 50.00% | -50.00% |
| ole | `general,filegroups/documents` | 0 | 40.56% | 78.44% | -37.88% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 46.15% | 76.92% | -30.77% |
| objc | `general` | 0 | 20.00% | 40.00% | -20.00% |
| gz | `general` | 0 | 26.44% | 44.06% | -17.63% |
| pyproject.toml | `general` | 0 | 0.00% | 16.67% | -16.67% |
| zig | `general` | 0 | 0.00% | 16.67% | -16.67% |
| data | `general` | 0 | 4.76% | 11.90% | -7.14% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 47.12% | 53.88% | -6.77% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 4.37% | 10.93% | -6.56% |
| zip | `general,filetypes/zip` | 0 | 32.99% | 39.54% | -6.55% |
| groovy | `general` | 0 | 0.00% | 6.25% | -6.25% |
| lnk | `general,filetypes/lnk` | 0 | 70.49% | 76.50% | -6.01% |
| gomod | `general` | 0 | 0.00% | 5.26% | -5.26% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.93% | 77.19% | -4.27% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 59.69% | 63.70% | -4.01% |
| applescript | `filetypes/applescript` | 0 | 23.08% | 26.92% | -3.85% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 13.32% | 17.03% | -3.71% |
| msi | `general,filetypes/msi` | 0 | 76.96% | 80.55% | -3.58% |
| cargo.toml | `filetypes/cargo.toml` | 0 | 13.33% | 16.67% | -3.33% |
| c | `general,filegroups/source` | 1 | 8.16% | 10.55% | -2.39% |
| npm | `general,filetypes/npm` | 0 | 62.79% | 65.12% | -2.33% |
| xls | `general,filetypes/xls` | 0 | 93.73% | 94.76% | -1.03% |
| python-bytecode | `filetypes/python-bytecode` | 1 | 79.68% | 80.59% | -0.90% |
| tar | `general,filetypes/tar` | 0 | 86.07% | 86.93% | -0.86% |
| java_class | `general` | 0 | 26.34% | 27.10% | -0.76% |
| text | `general,filetypes/text` | 1 | 3.46% | 4.12% | -0.66% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.64% | 30.96% | -0.32% |
| zst | `general` | 0 | 87.53% | 87.76% | -0.23% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.10% | 97.23% | -0.12% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 54.52% | 54.55% | -0.03% |
| cargolock | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 72.73% | 72.73% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 42.86% | 42.86% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 9.26% | 9.26% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 4.55% | 4.55% | 0.00% |
| gem | `filetypes/gem` | 0 | 89.66% | 89.66% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 4.90% | — | — |
| html | `general,filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source,filetypes/java` | 0 | 1.34% | 1.34% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.98% | 60.98% | 0.00% |
| pkg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg-info | `filetypes/pkg-info` | 0 | 96.71% | 96.71% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 3.61% | 3.61% | 0.00% |
| png | `filegroups/media,filetypes/png` | 1 | 5.29% | 5.29% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 40.00% | 40.00% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 52.88% | 52.88% | 0.00% |
| xml | `filegroups/config` | 0 | 1.89% | 1.89% | 0.00% |
| xpi | `general` | 0 | 100.00% | 100.00% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 3 | 96.79% | 96.79% | 0.01% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 74.46% | 74.42% | 0.04% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.49% | 90.44% | 0.04% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 60.62% | 60.47% | 0.15% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 80.17% | 79.83% | 0.34% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 2.87% | 2.46% | 0.41% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.06% | 1.41% | 0.65% |
| macho | `filegroups/native,filetypes/macho` | 0 | 74.56% | 73.68% | 0.88% |
| jar | `general,filetypes/jar` | 0 | 47.62% | 45.96% | 1.66% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 54.78% | 52.22% | 2.56% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 52.73% | 49.37% | 3.36% |
| vbs | `general,filetypes/vbs` | 0 | 37.95% | 24.69% | 13.26% |
