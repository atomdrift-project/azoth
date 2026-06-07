# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 860189 (310056 malware, 550133 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 163879 | 19967 | `general,filegroups/native,filetypes/pe` | filegroups/native: 49.80% | 2 | 62.39% | — | filegroups/native: 59.16% | 0.999 | 0.999 |
| pdf | 22501 | 2934 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 7.18% | 0 | 5.79% | -1.40% | filetypes/pdf: 70.77% | 0.994 | 0.994 |
| elf | 22304 | 21532 | `general,filegroups/native,filetypes/elf` | filegroups/native: 94.38% | 0 | 91.42% | -2.95% | filetypes/elf: 97.44% | 1.000 | 0.999 |
| batch | 22089 | 596 | `general,filegroups/scripts,filetypes/batch` | general: 1.58% | 0 | 1.73% | 0.16% | general: 1.74% | 0.989 | 0.989 |
| javascript | 14609 | 76386 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 63.62% | 2 | 65.66% | — | filetypes/javascript: 65.06% | 0.956 | 0.951 |
| zip | 12628 | 1457 | `general,filetypes/zip` | filetypes/zip: 33.79% | 0 | 30.81% | -2.98% | filetypes/zip: 42.07% | 0.976 | 0.974 |
| xlsx | 7425 | 198 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.10% | 0 | 28.81% | -2.29% | filetypes/xlsx: 31.15% | 0.996 | 0.996 |
| xls | 4647 | 2652 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 94.88% | 0 | 86.87% | -8.01% | filegroups/documents: 94.88% | 0.995 | 0.995 |
| doc | 3930 | 7 | `general,filegroups/documents` | filegroups/documents: 96.87% | 0 | 84.05% | -12.82% | filegroups/documents: 99.39% | — | 1.000 |
| kotlin | 3917 | 6462 | `general,filegroups/source,filetypes/kotlin` | filegroups/source: 52.54% | 1 | 55.02% | -2.71% | filegroups/source: 57.72% | 0.889 | 0.890 |
| tar | 2774 | 3015 | `general,filetypes/tar` | filetypes/tar: 86.19% | 0 | 80.79% | -5.41% | filetypes/tar: 88.43% | 0.995 | 0.988 |
| python | 2596 | 24934 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 47.19% | 0 | 48.04% | 0.85% | filetypes/python: 60.40% | 0.818 | 0.812 |
| rar | 2551 | 0 | `general` | general: 100.00% | 0 | 17.05% | -82.95% | general: 100.00% | — | — |
| package.json | 2246 | 2728 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 90.25% | 0 | 87.22% | -3.03% | filegroups/config: 95.77% | 0.997 | 0.997 |
| unknown | 2099 | 6203 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.33% | — | 0.784 |
| c | 1934 | 88499 | `general,filegroups/source,filetypes/c` | filetypes/c: 11.89% | 1 | 11.89% | -0.31% | filetypes/c: 12.20% | 0.253 | 0.258 |
| shell | 1893 | 7497 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 56.52% | 0 | 38.51% | -18.01% | filetypes/shell: 63.55% | 0.974 | 0.974 |
| vbs | 1436 | 426 | `general,filetypes/vbs` | filetypes/vbs: 68.66% | 0 | 69.01% | 0.35% | filetypes/vbs: 69.71% | 0.996 | 0.996 |
| go | 1305 | 15232 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.67% | 2 | 6.82% | — | filetypes/go: 6.74% | 0.285 | 0.219 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 13.64% | -74.12% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 243 | `general,filetypes/pkg-info` | filetypes/pkg-info: 94.44% | 0 | 76.19% | -18.25% | general: 97.02% | 0.998 | 0.998 |
| png | 905 | 21709 | `general,filegroups/media,filetypes/png` | filetypes/png: 5.52% | — | — | — | filetypes/png: 6.19% | 0.119 | 0.127 |
| 7z | 885 | 14 | `general` | general: 89.72% | 0 | 21.13% | -68.59% | general: 91.19% | — | 0.999 |
| ole | 801 | 782 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 84.14% | 0 | 10.61% | -73.53% | filetypes/ole: 84.14% | 0.990 | 0.990 |
| rtf | 785 | 54 | `general,filegroups/documents,filetypes/rtf` | filegroups/documents: 97.58% | 2 | 97.58% | — | filegroups/documents: 97.58% | 0.999 | 0.999 |
| php | 671 | 18441 | `general,filegroups/scripts,filetypes/php` | general: 51.12% | 0 | 44.11% | -7.00% | general: 52.61% | 0.775 | 0.767 |
| powershell | 650 | 308 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 51.69% | 0 | 43.38% | -8.31% | filetypes/powershell: 60.15% | 0.986 | 0.985 |
| docx | 563 | 58 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 82.24% | 0 | 68.74% | -13.50% | filegroups/documents: 82.95% | 0.989 | 0.989 |
| msi | 554 | 13 | `general,filetypes/msi` | filetypes/msi: 82.31% | 0 | 45.31% | -37.00% | filetypes/msi: 82.49% | 0.997 | 0.996 |
| lnk | 542 | 131 | `general,filetypes/lnk` | filetypes/lnk: 83.95% | 0 | 64.76% | -19.19% | filetypes/lnk: 84.13% | 0.994 | 0.992 |
| gz | 526 | 8678 | `general` | general: 42.21% | 0 | 0.00% | -42.21% | general: 43.16% | — | 0.688 |
| jar | 454 | 456 | `general,filetypes/jar` | filetypes/jar: 50.66% | 8 | 80.40% | — | filetypes/jar: 51.32% | 0.963 | 0.952 |
| xml | 437 | 26007 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.52% | 0 | 2.29% | -0.23% | filetypes/xml: 2.97% | 0.101 | 0.154 |
| python-bytecode | 378 | 15284 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 90.74% | 0 | 41.53% | -49.21% | filetypes/python-bytecode: 91.01% | 0.923 | 0.922 |
| macho | 335 | 1507 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 75.52% | 0 | 69.25% | -6.27% | filetypes/macho: 86.87% | 0.992 | 0.985 |
| csharp | 316 | 8367 | `general,filegroups/source,filetypes/csharp` | general: 17.09% | 1 | 21.20% | -3.80% | filegroups/source: 25.00% | 0.402 | 0.402 |
| text | 288 | 11093 | `general,filetypes/text` | general: 8.68% | 0 | 5.90% | -2.78% | general: 10.76% | 0.142 | 0.161 |
| java_class | 230 | 88106 | `general,filegroups/portable,filetypes/java_class` | general: 44.78% | 0 | 6.52% | -38.26% | general: 49.57% | 0.534 | 0.859 |
| rust | 188 | 11023 | `general,filegroups/source,filetypes/rust` | general: 2.66% | 0 | 1.60% | -1.06% | general: 4.79% | 0.010 | 0.067 |
| jpeg | 156 | 3741 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 11.54% | 0 | 1.28% | -10.26% | filetypes/jpeg: 12.82% | 0.278 | 0.246 |
| crx | 146 | 10 | `general,filetypes/crx` | filetypes/crx: 95.89% | 0 | 0.68% | -95.21% | filetypes/crx: 95.89% | 0.998 | 0.968 |
| java | 142 | 5222 | `general,filegroups/source,filetypes/java` | filetypes/java: 10.56% | 0 | 2.82% | -7.75% | filetypes/java: 10.56% | 0.293 | 0.297 |
| json | 113 | 4504 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.041 |
| cab | 96 | 11 | `general` | general: 47.92% | 0 | 0.00% | -47.92% | general: 68.75% | — | 0.987 |
| makefile | 75 | 3434 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 1.33% | 0.019 | 0.019 |
| plist | 75 | 1600 | `general,filegroups/config,filetypes/plist` | filegroups/config: 5.33% | 0 | 1.33% | -4.00% | filegroups/config: 5.33% | 0.076 | 0.076 |
| pptx | 73 | 21 | `general,filegroups/documents` | filegroups/documents: 8.22% | 0 | 1.37% | -6.85% | filegroups/documents: 34.25% | — | 0.803 |
| deb | 50 | 903 | `general,filetypes/deb` | general: 10.00% | 0 | 10.00% | 0.00% | general: 10.00% | 0.137 | 0.131 |
| perl | 39 | 4975 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 51.28% | 3 | 76.92% | -7.69% | filetypes/perl: 76.92% | 0.847 | 0.843 |
| chm | 38 | 6 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 97.37% | — | 0.995 |
| data | 34 | 1355 | `general` | general: 32.35% | 0 | 0.00% | -32.35% | general: 32.35% | — | 0.463 |
| asar | 18 | 1 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| cargo.toml | 18 | 87 | `general,filetypes/cargo.toml` | general: 22.22% | 0 | 22.22% | 0.00% | general: 27.78% | 0.433 | 0.433 |
| ruby | 17 | 3110 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 41.18% | 0 | 41.18% | 0.00% | filetypes/ruby: 58.82% | 0.692 | 0.690 |
| html | 14 | 1393 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| groovy | 13 | 858 | `general,filetypes/groovy` | general: 0.00% | 2 | 0.00% | — | general: 0.00% | 0.015 | 0.015 |
| lua | 13 | 2337 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 46.15% | -23.08% | general: 69.23% | 0.696 | 0.710 |
| dockerfile | 11 | 243 | `general,filetypes/dockerfile` | filetypes/dockerfile: 9.09% | 0 | 0.00% | -9.09% | filetypes/dockerfile: 9.09% | 0.174 | 0.159 |
| package-lock.json | 10 | 81 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.159 |
| xz | 10 | 4445 | `general` | general: 10.00% | 0 | 0.00% | -10.00% | general: 20.00% | — | 0.369 |
| markdown | 9 | 2745 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| chrome-manifest | 8 | 55 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 62.50% | 1 | 62.50% | 0.00% | filetypes/chrome-manifest: 62.50% | 0.844 | 0.810 |
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
| rar | `general` | 0 | 1.25% | 100.00% | -98.75% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 8.59% | 89.72% | -81.13% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| rar | `general` | 0 | 1.69% | 100.00% | -98.31% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 9.15% | 89.72% | -80.56% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| rar | `general` | 0 | 2.27% | 100.00% | -97.73% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 9.38% | 89.72% | -80.34% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| rar | `general` | 0 | 2.59% | 100.00% | -97.41% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 9.72% | 89.72% | -80.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| rar | `general` | 0 | 2.98% | 100.00% | -97.02% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 10.17% | 89.72% | -79.55% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| rar | `general` | 0 | 3.21% | 100.00% | -96.79% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 11.07% | 89.72% | -78.64% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| rar | `general` | 0 | 5.45% | 100.00% | -94.55% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 5.69% | 87.76% | -82.07% |
| 7z | `general` | 0 | 13.22% | 89.72% | -76.50% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| rar | `general` | 0 | 10.31% | 100.00% | -89.69% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 9.98% | 87.76% | -77.79% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| 7z | `general` | 0 | 17.18% | 89.72% | -72.54% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.45% | 100.00% | -86.55% |
| zst | `general` | 0 | 11.93% | 87.76% | -75.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| 7z | `general` | 0 | 18.53% | 89.72% | -71.19% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 14.43% | 100.00% | -85.57% |
| zst | `general` | 0 | 12.70% | 87.76% | -75.06% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| 7z | `general` | 0 | 19.55% | 89.72% | -70.17% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 17.05% | 100.00% | -82.95% |
| zst | `general` | 0 | 13.64% | 87.76% | -74.12% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| 7z | `general` | 0 | 21.13% | 89.72% | -68.59% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 21.72% | 100.00% | -78.28% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| zst | `general` | 0 | 15.04% | 87.76% | -72.72% |
| 7z | `general` | 0 | 23.05% | 89.72% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 24.46% | 100.00% | -75.54% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| zst | `general` | 0 | 15.82% | 87.76% | -71.94% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 24.63% | 89.72% | -65.08% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 24.74% | 100.00% | -75.26% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| zst | `general` | 0 | 15.98% | 87.76% | -71.78% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 24.63% | 89.72% | -65.08% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 25.13% | 100.00% | -74.87% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| zst | `general` | 0 | 16.06% | 87.76% | -71.71% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 24.75% | 89.72% | -64.97% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 25.72% | 100.00% | -74.28% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| zst | `general` | 0 | 16.45% | 87.76% | -71.32% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 25.08% | 89.72% | -64.63% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.05% | 96.87% | -12.82% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| rar | `general` | 0 | 32.26% | 100.00% | -67.74% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.93% | 89.72% | -60.79% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| zst | `general` | 0 | 33.67% | 87.76% | -54.09% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 0.00% | 47.92% | -47.92% |
| gz | `general` | 0 | 0.00% | 42.21% | -42.21% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.76% | 96.87% | -12.11% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 34.54% | 100.00% | -65.46% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| 7z | `general` | 0 | 30.96% | 89.72% | -58.76% |
| zst | `general` | 0 | 38.35% | 87.76% | -49.42% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.19% | 42.21% | -42.02% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 84.86% | 96.87% | -12.01% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 41.83% | 100.00% | -58.17% |
| 7z | `general` | 0 | 35.93% | 89.72% | -53.79% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 1.04% | 47.92% | -46.88% |
| gz | `general` | 0 | 0.57% | 42.21% | -41.63% |
| zst | `general` | 0 | 49.49% | 87.76% | -38.27% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 85.04% | 96.87% | -11.83% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| 7z | `general` | 0 | 41.47% | 89.72% | -48.25% |
| rar | `general` | 0 | 53.78% | 100.00% | -46.22% |
| cab | `general` | 0 | 2.08% | 47.92% | -45.83% |
| gz | `general` | 0 | 2.28% | 42.21% | -39.92% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| zst | `general` | 0 | 57.68% | 87.76% | -30.09% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 85.11% | 96.87% | -11.76% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| cab | `general` | 0 | 4.17% | 47.92% | -43.75% |
| 7z | `general` | 0 | 50.40% | 89.72% | -39.32% |
| gz | `general` | 0 | 3.42% | 42.21% | -38.78% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 6.52% | 44.78% | -38.26% |
| rar | `general` | 0 | 61.78% | 100.00% | -38.22% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zst | `general` | 0 | 64.69% | 87.76% | -23.07% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| doc | `general,filegroups/documents` | 0 | 86.26% | 96.87% | -10.61% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 2 | 65.66% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

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
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| chm | `general` | 0 | 2.63% | 86.84% | -84.21% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| cab | `general` | 0 | 11.46% | 47.92% | -36.46% |
| rar | `general` | 0 | 67.54% | 100.00% | -32.46% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| gz | `general` | 0 | 14.64% | 42.21% | -27.57% |
| 7z | `general` | 0 | 62.94% | 89.72% | -26.78% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 43.09% | 63.62% | -20.53% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| zst | `general` | 0 | 76.15% | 87.76% | -11.61% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 34.35% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| asar | `general` | 0 | 5.56% | 100.00% | -94.44% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 69.38% | 100.00% | -30.62% |
| cab | `general` | 0 | 20.83% | 47.92% | -27.08% |
| gz | `general` | 0 | 16.92% | 42.21% | -25.29% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| 7z | `general` | 0 | 66.44% | 89.72% | -23.28% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 43.09% | 63.62% | -20.53% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| zst | `general` | 0 | 85.35% | 87.76% | -2.42% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 34.35% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| crx | `general,filetypes/crx` | 0 | 0.68% | 95.89% | -95.21% |
| asar | `general` | 0 | 11.11% | 100.00% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 10.61% | 84.14% | -73.53% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 41.53% | 90.74% | -49.21% |
| msi | `general,filetypes/msi` | 0 | 45.31% | 82.31% | -37.00% |
| data | `general` | 0 | 0.00% | 32.35% | -32.35% |
| rar | `general` | 0 | 69.93% | 100.00% | -30.07% |
| pyproject.toml | `general` | 0 | 0.00% | 25.00% | -25.00% |
| cab | `general` | 0 | 23.96% | 47.92% | -23.96% |
| gz | `general` | 0 | 18.25% | 42.21% | -23.95% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| 7z | `general` | 0 | 68.36% | 89.72% | -21.36% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 43.09% | 63.62% | -20.53% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 64.76% | 83.95% | -19.19% |
| pkg-info | `general` | 0 | 76.19% | 94.44% | -18.25% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 38.51% | 56.52% | -18.01% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 68.74% | 82.24% | -13.50% |
| jpeg | `general,filetypes/jpeg` | 0 | 1.28% | 11.54% | -10.26% |
| dockerfile | `general` | 0 | 0.00% | 9.09% | -9.09% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 43.38% | 51.69% | -8.31% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 86.87% | 94.88% | -8.01% |
| java | `general,filegroups/source` | 0 | 2.82% | 10.56% | -7.75% |
| perl | `general,filegroups/scripts,filetypes/perl` | 3 | 76.92% | 84.62% | -7.69% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 44.11% | 51.12% | -7.00% |
| pptx | `general,filegroups/documents` | 0 | 1.37% | 8.22% | -6.85% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 69.25% | 75.52% | -6.27% |
| tar | `general,filetypes/tar` | 0 | 80.79% | 86.19% | -5.41% |
| plist | `general,filetypes/plist` | 0 | 1.33% | 5.33% | -4.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 1 | 21.20% | 25.00% | -3.80% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.22% | 90.25% | -3.03% |
| zip | `general,filetypes/zip` | 0 | 30.81% | 33.79% | -2.98% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 91.42% | 94.38% | -2.95% |
| text | `general` | 0 | 5.90% | 8.68% | -2.78% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 55.02% | 57.72% | -2.71% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 28.81% | 31.10% | -2.29% |
| zst | `general` | 0 | 85.89% | 87.76% | -1.87% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.79% | 7.18% | -1.40% |
| rust | `general,filegroups/source` | 0 | 1.60% | 2.66% | -1.06% |
| c | `general,filegroups/source,filetypes/c` | 1 | 11.89% | 12.20% | -0.31% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.29% | 2.52% | -0.23% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 22.22% | 22.22% | 0.00% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 1 | 62.50% | 62.50% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 2 | 6.82% | — | — |
| groovy | `general,filetypes/groovy` | 2 | 0.00% | — | — |
| html | `general` | 0 | 100.00% | 100.00% | 0.00% |
| jar | `general,filetypes/jar` | 8 | 80.40% | — | — |
| java_class | `general,filetypes/java_class` | 2 | 34.35% | — | — |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 62.39% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 2 | 97.58% | — | — |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.18% | 41.18% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.73% | 1.58% | 0.16% |
| vbs | `general,filetypes/vbs` | 0 | 69.01% | 68.66% | 0.35% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.04% | 47.19% | 0.85% |
