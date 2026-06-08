# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 860189 (310056 malware, 550133 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 163879 | 19967 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 52.68% | 0 | 56.49% | 3.81% | filetypes/pe: 63.59% | 0.999 | 0.999 |
| pdf | 22501 | 2934 | `general,filegroups/documents,filetypes/pdf` | general: 5.04% | 0 | 4.48% | -0.56% | filetypes/pdf: 70.77% | 0.994 | 0.995 |
| elf | 22304 | 21532 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 93.79% | 0 | 93.97% | 0.18% | filetypes/elf: 97.44% | 1.000 | 1.000 |
| batch | 22089 | 596 | `general,filegroups/scripts,filetypes/batch` | general: 1.58% | 0 | 0.96% | -0.61% | filetypes/batch: 2.68% | 0.998 | 0.995 |
| javascript | 14609 | 76386 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 64.62% | 0 | 63.33% | -1.29% | filetypes/javascript: 64.93% | 0.973 | 0.964 |
| zip | 12628 | 1457 | `general,filetypes/zip` | filetypes/zip: 34.82% | 0 | 34.10% | -0.72% | filetypes/zip: 47.14% | 0.996 | 0.985 |
| xlsx | 7425 | 198 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.37% | 0 | 30.46% | -0.90% | filegroups/documents: 37.08% | 0.996 | 0.987 |
| xls | 4647 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.99% | 0 | 94.40% | -0.58% | filetypes/xls: 95.07% | 0.998 | 0.998 |
| doc | 3930 | 7 | `general,filegroups/documents` | filegroups/documents: 99.44% | — | — | — | filegroups/documents: 99.47% | — | 1.000 |
| kotlin | 3917 | 6462 | `general,filegroups/source,filetypes/kotlin` | filegroups/source: 52.54% | 0 | 52.03% | -0.51% | filegroups/source: 57.72% | 0.897 | 0.902 |
| tar | 2774 | 3015 | `general,filetypes/tar` | filetypes/tar: 86.19% | 0 | 86.30% | 0.11% | filetypes/tar: 88.43% | 0.995 | 0.988 |
| python | 2596 | 24934 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 47.19% | 0 | 48.46% | 1.27% | filetypes/python: 63.06% | 0.835 | 0.832 |
| rar | 2551 | 0 | `general` | general: 100.00% | 0 | 33.95% | -66.05% | general: 100.00% | — | — |
| package.json | 2246 | 2728 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 86.51% | 0 | 85.89% | -0.62% | filegroups/config: 95.77% | 0.997 | 0.997 |
| unknown | 2099 | 6203 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.33% | — | 0.784 |
| c | 1934 | 88499 | `general,filegroups/source,filetypes/c` | filetypes/c: 11.89% | 0 | 9.98% | -1.91% | filetypes/c: 12.20% | 0.253 | 0.258 |
| shell | 1893 | 7497 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 76.23% | 0 | 72.05% | -4.17% | filetypes/shell: 80.88% | 0.985 | 0.977 |
| vbs | 1436 | 426 | `general,filetypes/vbs` | filetypes/vbs: 68.66% | 0 | 56.69% | -11.98% | filetypes/vbs: 69.71% | 0.996 | 0.996 |
| go | 1305 | 15232 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.82% | 0 | 5.06% | -0.77% | filetypes/go: 6.21% | 0.658 | 0.645 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 36.63% | -51.13% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 243 | `general,filetypes/pkg-info` | filetypes/pkg-info: 94.44% | 0 | 94.75% | 0.31% | general: 97.02% | 0.998 | 0.998 |
| png | 905 | 21709 | `general,filegroups/media,filetypes/png` | filetypes/png: 5.52% | 0 | 5.52% | 0.00% | filetypes/png: 6.19% | 0.119 | 0.127 |
| 7z | 885 | 14 | `general` | general: 89.72% | 0 | 30.17% | -59.55% | general: 91.19% | — | 0.999 |
| ole | 801 | 782 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 89.89% | 0 | 80.90% | -8.99% | filegroups/documents: 92.88% | 0.977 | 0.993 |
| rtf | 785 | 54 | `general,filegroups/documents,filetypes/rtf` | general: 97.45% | 0 | 97.58% | 0.13% | general: 97.45% | 1.000 | 1.000 |
| php | 671 | 18441 | `general,filegroups/scripts,filetypes/php` | general: 51.12% | 0 | 43.22% | -7.90% | general: 52.61% | 0.775 | 0.767 |
| powershell | 650 | 308 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 51.69% | 0 | 53.08% | 1.38% | filegroups/scripts: 51.85% | 0.990 | 0.986 |
| docx | 563 | 58 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 84.19% | 0 | 79.57% | -4.62% | filegroups/documents: 84.37% | 0.989 | 0.994 |
| msi | 554 | 13 | `general,filetypes/msi` | filetypes/msi: 82.31% | 0 | 68.95% | -13.36% | filetypes/msi: 82.49% | 0.997 | 0.996 |
| lnk | 542 | 131 | `general,filetypes/lnk` | filetypes/lnk: 80.81% | 0 | 70.66% | -10.15% | filetypes/lnk: 80.81% | 0.992 | 0.990 |
| gz | 526 | 8678 | `general` | general: 42.21% | 0 | 0.19% | -42.02% | general: 43.16% | — | 0.688 |
| jar | 454 | 456 | `general,filetypes/jar` | filetypes/jar: 54.41% | 0 | 55.51% | 1.10% | filetypes/jar: 56.61% | 0.974 | 0.973 |
| xml | 437 | 26007 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.52% | 0 | 2.52% | 0.00% | filetypes/xml: 2.75% | 0.295 | 0.331 |
| python-bytecode | 378 | 15284 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 90.74% | 0 | 83.07% | -7.67% | filetypes/python-bytecode: 91.01% | 0.923 | 0.922 |
| macho | 335 | 1507 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 75.52% | 0 | 77.91% | 2.39% | filetypes/macho: 86.87% | 0.992 | 0.986 |
| csharp | 316 | 8367 | `general,filegroups/source,filetypes/csharp` | general: 17.09% | 0 | 17.09% | 0.00% | filegroups/source: 25.00% | 0.402 | 0.402 |
| text | 288 | 11093 | `general,filetypes/text` | general: 8.68% | 0 | 7.64% | -1.04% | general: 10.76% | 0.142 | 0.161 |
| java_class | 230 | 88106 | `general,filegroups/portable,filetypes/java_class` | filegroups/portable: 71.30% | 0 | 62.61% | -8.70% | filegroups/portable: 77.83% | 0.903 | 0.901 |
| rust | 188 | 11023 | `general,filegroups/source,filetypes/rust` | general: 2.66% | 0 | 1.60% | -1.06% | general: 4.79% | 0.010 | 0.067 |
| jpeg | 156 | 3741 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 11.54% | 0 | 3.85% | -7.69% | filetypes/jpeg: 12.82% | 0.278 | 0.246 |
| crx | 146 | 10 | `general,filetypes/crx` | filetypes/crx: 95.89% | 0 | 68.49% | -27.40% | filetypes/crx: 95.89% | 0.998 | 0.968 |
| java | 142 | 5222 | `general,filegroups/source,filetypes/java` | filetypes/java: 10.56% | 0 | 4.93% | -5.63% | filetypes/java: 10.56% | 0.293 | 0.297 |
| json | 113 | 4504 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.041 |
| cab | 96 | 11 | `general` | general: 47.92% | 0 | 1.04% | -46.88% | general: 68.75% | — | 0.987 |
| makefile | 75 | 3434 | `general,filegroups/source,filetypes/makefile` | filetypes/makefile: 2.67% | 0 | 0.00% | -2.67% | filetypes/makefile: 2.67% | 0.055 | 0.055 |
| plist | 75 | 1600 | `general,filegroups/config,filetypes/plist` | filegroups/config: 5.33% | 0 | 5.33% | 0.00% | filegroups/config: 5.33% | 0.076 | 0.076 |
| pptx | 73 | 21 | `general,filegroups/documents` | filegroups/documents: 4.11% | — | — | — | filegroups/documents: 34.25% | — | 0.829 |
| deb | 50 | 903 | `general,filetypes/deb` | general: 10.00% | 0 | 10.00% | 0.00% | general: 10.00% | 0.137 | 0.131 |
| perl | 39 | 4975 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 51.28% | 0 | 51.28% | 0.00% | filetypes/perl: 76.92% | 0.847 | 0.843 |
| chm | 38 | 6 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 97.37% | — | 0.995 |
| data | 34 | 1355 | `general` | general: 32.35% | 0 | 0.00% | -32.35% | general: 32.35% | — | 0.463 |
| asar | 18 | 1 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| cargo.toml | 18 | 87 | `general,filetypes/cargo.toml` | general: 22.22% | 0 | 22.22% | 0.00% | general: 27.78% | 0.433 | 0.433 |
| ruby | 17 | 3110 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 41.18% | 0 | 41.18% | 0.00% | filetypes/ruby: 58.82% | 0.692 | 0.690 |
| html | 14 | 1393 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| groovy | 13 | 858 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.015 | 0.015 |
| lua | 13 | 2337 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 69.23% | 0.00% | general: 69.23% | 0.696 | 0.710 |
| dockerfile | 11 | 243 | `general,filetypes/dockerfile` | filetypes/dockerfile: 9.09% | 0 | 0.00% | -9.09% | filetypes/dockerfile: 9.09% | 0.174 | 0.159 |
| package-lock.json | 10 | 81 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.159 |
| xz | 10 | 4445 | `general` | general: 10.00% | 0 | 0.00% | -10.00% | general: 20.00% | — | 0.369 |
| markdown | 9 | 2745 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| chrome-manifest | 8 | 55 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 62.50% | 0 | 62.50% | 0.00% | filetypes/chrome-manifest: 62.50% | 0.844 | 0.810 |
| clojure | 7 | 636 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.640 | 0.640 |
| objc | 5 | 2791 | `general` | general: 60.00% | 0 | 0.00% | -60.00% | general: 60.00% | — | 0.625 |
| zig | 5 | 21 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 60.00% | — | 0.616 |
| pyproject.toml | 4 | 9 | `general` | general: 25.00% | 0 | 0.00% | -25.00% | general: 25.00% | — | 0.747 |
| swift | 4 | 3911 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.095 |
| applescript | 3 | 36 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 3 | 1429 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| desktop-entry | 3 | 93 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.694 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| whl | 3 | 89 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.062 |
| systemd | 2 | 174 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.010 |
| github-actions | 1 | 932 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.333 |
| ooxml | 1 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| pkg | 1 | 4 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.500 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 7 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.87% | 100.00% | -66.13% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 29.94% | 89.72% | -59.77% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| doc | `general,filegroups/documents` | 0 | 98.65% | 99.44% | -0.79% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.91% | 100.00% | -66.09% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.06% | 89.72% | -59.66% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| doc | `general,filegroups/documents` | 0 | 98.96% | 99.44% | -0.48% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.91% | 100.00% | -66.09% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.06% | 89.72% | -59.66% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.91% | 100.00% | -66.09% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.17% | 89.72% | -59.55% |
| zst | `general` | 0 | 36.55% | 87.76% | -51.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.95% | 100.00% | -66.05% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.17% | 89.72% | -59.55% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.95% | 100.00% | -66.05% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.17% | 89.72% | -59.55% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.99% | 100.00% | -66.01% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.17% | 89.72% | -59.55% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.99% | 100.00% | -66.01% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.40% | 89.72% | -59.32% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 33.99% | 100.00% | -66.01% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.40% | 89.72% | -59.32% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 34.03% | 100.00% | -65.97% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.40% | 89.72% | -59.32% |
| zst | `general` | 0 | 36.63% | 87.76% | -51.13% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 34.03% | 100.00% | -65.97% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.51% | 89.72% | -59.21% |
| zst | `general` | 0 | 37.41% | 87.76% | -50.35% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 34.93% | 100.00% | -65.07% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.96% | 89.72% | -58.76% |
| zst | `general` | 0 | 38.58% | 87.76% | -49.18% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.46% | 100.00% | -61.54% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 34.24% | 89.72% | -55.48% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.57% | 42.21% | -41.63% |
| zst | `general` | 0 | 46.30% | 87.76% | -41.47% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 46.61% | 100.00% | -53.39% |
| 7z | `general` | 0 | 38.64% | 89.72% | -51.07% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.76% | 42.21% | -41.44% |
| zst | `general` | 0 | 54.01% | 87.76% | -33.75% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 43.73% | 89.72% | -45.99% |
| cab | `general` | 0 | 2.08% | 47.92% | -45.83% |
| rar | `general` | 0 | 56.45% | 100.00% | -43.55% |
| gz | `general` | 0 | 2.66% | 42.21% | -39.54% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| zst | `general` | 0 | 59.78% | 87.76% | -27.98% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| cab | `general` | 0 | 4.17% | 47.92% | -43.75% |
| 7z | `general` | 0 | 50.85% | 89.72% | -38.87% |
| gz | `general` | 0 | 3.61% | 42.21% | -38.59% |
| rar | `general` | 0 | 61.98% | 100.00% | -38.02% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zst | `general` | 0 | 64.93% | 87.76% | -22.84% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| java_class | `general,filetypes/java_class` | 0 | 62.61% | 71.30% | -8.70% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.98% | 11.89% | -1.91% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.33% | 64.62% | -1.29% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 2.63% | 86.84% | -84.21% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| cab | `general` | 0 | 11.46% | 47.92% | -36.46% |
| rar | `general` | 0 | 67.31% | 100.00% | -32.69% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| gz | `general` | 0 | 13.69% | 42.21% | -28.52% |
| 7z | `general` | 0 | 62.26% | 89.72% | -27.46% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| zst | `general` | 0 | 75.68% | 87.76% | -12.08% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 5.56% | 100.00% | -94.44% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 69.38% | 100.00% | -30.62% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| cab | `general` | 0 | 20.83% | 47.92% | -27.08% |
| gz | `general` | 0 | 16.73% | 42.21% | -25.48% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| 7z | `general` | 0 | 66.33% | 89.72% | -23.39% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| zst | `general` | 0 | 85.27% | 87.76% | -2.49% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 100.00% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 70.13% | 100.00% | -29.87% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| cab | `general` | 0 | 23.96% | 47.92% | -23.96% |
| gz | `general` | 0 | 18.44% | 42.21% | -23.76% |
| 7z | `general` | 0 | 68.70% | 89.72% | -21.02% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| zst | `general` | 0 | 86.20% | 87.76% | -1.56% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 100.00% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| applescript | `general` | 0 | 66.67% | 100.00% | -33.33% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 70.68% | 100.00% | -29.32% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| cab | `general` | 0 | 25.00% | 47.92% | -22.92% |
| gz | `general` | 0 | 21.48% | 42.21% | -20.72% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| 7z | `general` | 0 | 71.19% | 89.72% | -18.53% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 0 | 5.52% | 5.52% | 0.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 93.97% | 93.79% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.46% | 47.19% | 1.27% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.49% | 52.68% | 3.81% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 100.00% | -88.89% |
| chm | `general` | 0 | 7.89% | 86.84% | -78.95% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 71.34% | 100.00% | -28.66% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 23.19% | 42.21% | -19.01% |
| 7z | `general` | 0 | 72.20% | 89.72% | -17.51% |
| cab | `general` | 0 | 31.25% | 47.92% | -16.67% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 43.22% | 51.12% | -7.90% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 83.07% | 90.74% | -7.67% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 60.32% | 63.06% | -2.73% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.06% | 5.82% | -0.77% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 97.65% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 65.79% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 2 | 6.41% | — | — |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 100.00% | -88.89% |
| markdown | `general` | 0 | 11.11% | 100.00% | -88.89% |
| chm | `general` | 0 | 10.53% | 86.84% | -76.32% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 71.74% | 100.00% | -28.26% |
| crx | `general,filetypes/crx` | 0 | 68.49% | 95.89% | -27.40% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| gz | `general` | 0 | 26.24% | 42.21% | -15.97% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.95% | 82.31% | -13.36% |
| vbs | `general,filetypes/vbs` | 0 | 56.69% | 68.66% | -11.98% |
| lnk | `general,filetypes/lnk` | 0 | 70.66% | 80.81% | -10.15% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 80.90% | 89.89% | -8.99% |
| cab | `general` | 0 | 39.58% | 47.92% | -8.33% |
| jpeg | `filetypes/jpeg` | 0 | 3.85% | 11.54% | -7.69% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.93% | 10.56% | -5.63% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.57% | 84.19% | -4.62% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 72.05% | 76.23% | -4.17% |
| java_class | `general,filetypes/java_class` | 1 | 74.35% | 77.83% | -3.48% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 60.32% | 63.06% | -2.73% |
| makefile | `filegroups/source,filetypes/makefile` | 0 | 0.00% | 2.67% | -2.67% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 51.42% | 52.61% | -1.19% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| text | `general,filetypes/text` | 0 | 7.64% | 8.68% | -1.04% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.46% | 31.37% | -0.90% |
| zip | `general,filetypes/zip` | 0 | 34.10% | 34.82% | -0.72% |
| package.json | `general,filegroups/config` | 0 | 85.89% | 86.51% | -0.62% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 0.96% | 1.58% | -0.61% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.40% | 94.99% | -0.58% |
| c | `general,filegroups/source,filetypes/c` | 0 | 11.32% | 11.89% | -0.57% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.48% | 5.04% | -0.56% |
| kotlin | `general,filegroups/source` | 0 | 52.03% | 52.54% | -0.51% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 90.48% | 90.74% | -0.26% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 62.50% | 62.50% | 0.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 17.09% | 17.09% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 97.65% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| lua | `filegroups/scripts,filetypes/lua` | 0 | 69.23% | 69.23% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 65.79% | — | — |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 51.28% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `general,filegroups/config` | 0 | 5.33% | 5.33% | 0.00% |
| png | `filetypes/png` | 2 | 6.41% | — | — |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `filegroups/config,filetypes/xml` | 0 | 2.52% | 2.52% | 0.00% |
| tar | `general,filetypes/tar` | 0 | 86.30% | 86.19% | 0.11% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 65.04% | 64.93% | 0.12% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.58% | 97.45% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 6.05% | 5.82% | 0.23% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 94.75% | 94.44% | 0.31% |
| jar | `general,filetypes/jar` | 0 | 55.51% | 54.41% | 1.10% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 53.08% | 51.69% | 1.38% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.91% | 75.52% | 2.39% |
