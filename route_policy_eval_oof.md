# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 821686 (296586 malware, 525100 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 158293 | 19912 | `general,filegroups/native,filetypes/pe` | filegroups/native: 50.57% | 0 | 53.46% | 2.89% | filetypes/pe: 59.68% | 1.000 | 1.000 |
| pdf | 22473 | 2714 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 73.72% | 0 | 43.33% | -30.39% | filetypes/pdf: 73.73% | 0.999 | 0.999 |
| batch | 22011 | 520 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 98.47% | 0 | 98.06% | -0.41% | filetypes/batch: 98.47% | 1.000 | 1.000 |
| elf | 20140 | 20699 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 90.89% | 0 | 88.91% | -1.98% | filetypes/elf: 91.17% | 1.000 | 0.999 |
| javascript | 12513 | 70685 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 66.74% | 0 | 55.45% | -11.29% | filetypes/javascript: 67.27% | 0.972 | 0.965 |
| zip | 12168 | 1238 | `general,filetypes/zip` | filetypes/zip: 33.40% | 0 | 20.33% | -13.07% | filetypes/zip: 39.56% | 0.987 | 0.986 |
| xlsx | 6526 | 169 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 53.08% | 0 | 44.58% | -8.50% | filegroups/documents: 55.21% | 0.999 | 0.999 |
| xls | 4076 | 2651 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.11% | 0 | 92.74% | -1.37% | filegroups/documents: 95.22% | 0.999 | 0.996 |
| kotlin | 4037 | 6300 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 49.69% | 0 | 46.97% | -2.72% | filetypes/kotlin: 49.69% | 0.974 | 0.967 |
| tar.gz | 3662 | 1937 | `general,filetypes/tar.gz` | filetypes/tar.gz: 81.87% | 0 | 75.86% | -6.01% | filetypes/tar.gz: 83.78% | 0.999 | 0.999 |
| doc | 3449 | 7 | `general,filegroups/documents` | filegroups/documents: 99.33% | 0 | 99.04% | -0.29% | filegroups/documents: 99.57% | — | 1.000 |
| unknown | 2681 | 32957 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 1.16% | — | 0.347 |
| python | 2345 | 20509 | `general,filegroups/scripts,filetypes/python` | general: 44.82% | 0 | 43.97% | -0.85% | filetypes/python: 63.37% | 0.972 | 0.963 |
| rar | 2239 | 0 | `general` | general: 100.00% | 0 | 39.08% | -60.92% | general: 100.00% | — | — |
| package.json | 2223 | 2136 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 87.45% | 0 | 90.28% | 2.83% | filegroups/config: 93.12% | 0.999 | 0.999 |
| c | 1780 | 74226 | `general,filegroups/source,filetypes/c` | filetypes/c: 10.28% | 0 | 4.38% | -5.90% | filegroups/source: 10.96% | 0.381 | 0.366 |
| shell | 1608 | 6762 | `general,filegroups/scripts,filetypes/shell` | general: 68.72% | 0 | 75.12% | 6.41% | filetypes/shell: 74.75% | 0.989 | 0.978 |
| zst | 1312 | 2046 | `general` | general: 97.41% | 0 | 28.96% | -68.45% | general: 98.78% | — | 1.000 |
| pkg-info | 1277 | 172 | `general,filetypes/pkg-info` | general: 78.54% | 0 | 82.07% | 3.52% | filetypes/pkg-info: 99.92% | 1.000 | 1.000 |
| vbs | 1257 | 427 | `general,filetypes/vbs` | filetypes/vbs: 60.94% | 0 | 64.84% | 3.90% | filetypes/vbs: 68.89% | 0.997 | 0.997 |
| go | 1182 | 13714 | `general,filegroups/source,filetypes/go` | filetypes/go: 1.69% | 0 | 1.27% | -0.42% | filegroups/source: 2.37% | 0.469 | 0.491 |
| 7z | 743 | 16 | `general` | general: 89.37% | 0 | 73.49% | -15.88% | general: 90.17% | — | 0.999 |
| ole | 708 | 737 | `general,filegroups/documents,filetypes/ole` | filegroups/documents: 94.63% | 0 | 17.37% | -77.26% | filegroups/documents: 94.77% | 0.998 | 0.998 |
| rtf | 691 | 51 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 98.70% | 0 | 98.70% | 0.00% | filetypes/rtf: 98.70% | 1.000 | 1.000 |
| png | 673 | 18998 | `general,filegroups/media,filetypes/png` | filegroups/media: 1.49% | 0 | 1.63% | 0.15% | filetypes/png: 8.62% | 0.134 | 0.135 |
| msi | 591 | 16 | `general` | general: 56.01% | 0 | 0.51% | -55.50% | general: 66.16% | — | 0.995 |
| powershell | 580 | 299 | `general,filegroups/scripts,filetypes/powershell` | filetypes/powershell: 31.55% | 0 | 48.97% | 17.41% | filetypes/powershell: 52.07% | 0.991 | 0.985 |
| php | 554 | 15055 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 64.44% | 0 | 42.42% | -22.02% | filetypes/php: 64.98% | 0.915 | 0.906 |
| docx | 501 | 58 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 88.82% | 0 | 81.64% | -7.19% | filetypes/docx: 89.82% | 0.995 | 0.992 |
| lnk | 500 | 131 | `general,filetypes/lnk` | filetypes/lnk: 82.80% | 0 | 67.80% | -15.00% | filetypes/lnk: 83.00% | 0.994 | 0.992 |
| gz | 487 | 8136 | `general` | general: 23.20% | 0 | 0.00% | -23.20% | general: 28.34% | — | 0.705 |
| xml | 381 | 22297 | `general,filegroups/config,filetypes/xml` | general: 2.89% | 0 | 4.72% | 1.84% | general: 3.15% | 0.128 | 0.302 |
| jar | 379 | 432 | `general,filetypes/jar` | filetypes/jar: 56.46% | 0 | 56.99% | 0.53% | filetypes/jar: 60.16% | 0.988 | 0.982 |
| python-bytecode | 343 | 9233 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.96% | 0 | 92.13% | -5.83% | filetypes/python-bytecode: 97.96% | 0.982 | 0.982 |
| macho | 327 | 1462 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 81.65% | 0 | 46.79% | -34.86% | filetypes/macho: 82.26% | 0.986 | 0.940 |
| csharp | 241 | 8112 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 31.54% | 0 | 22.41% | -9.13% | filegroups/source: 31.54% | 0.612 | 0.581 |
| java_class | 219 | 83812 | `general,filegroups/portable,filetypes/java_class` | general: 47.03% | 0 | 15.53% | -31.51% | general: 69.41% | 0.001 | 0.053 |
| tar | 182 | 63 | `general,filetypes/tar` | filetypes/tar: 97.80% | 0 | 95.05% | -2.75% | filetypes/tar: 97.80% | 0.996 | 0.995 |
| text | 170 | 8772 | `general,filetypes/text` | general: 14.12% | 0 | 10.59% | -3.53% | general: 14.71% | 0.204 | 0.236 |
| rust | 166 | 10346 | `general,filegroups/source,filetypes/rust` | general: 2.41% | 0 | 1.81% | -0.60% | filetypes/rust: 3.01% | 0.116 | 0.086 |
| jpeg | 149 | 3363 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 14.09% | 0 | 9.40% | -4.70% | filetypes/jpeg: 14.09% | 0.259 | 0.258 |
| json | 93 | 3931 | `general,filegroups/config,filetypes/json` | filegroups/config: 4.30% | 0 | 4.30% | 0.00% | filegroups/config: 4.30% | 0.045 | 0.090 |
| cab | 85 | 12 | `general` | general: 21.18% | 0 | 0.00% | -21.18% | general: 51.76% | — | 0.973 |
| plist | 66 | 1581 | `general,filegroups/config,filetypes/plist` | filegroups/config: 6.06% | 0 | 6.06% | 0.00% | general: 6.06% | 0.116 | 0.128 |
| pptx | 65 | 21 | `general,filegroups/documents,filetypes/pptx` | filetypes/pptx: 66.15% | 0 | 38.46% | -27.69% | filetypes/pptx: 75.38% | 0.936 | 0.897 |
| makefile | 60 | 2952 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.024 | 0.028 |
| deb | 43 | 824 | `general,filetypes/deb` | general: 4.65% | — | — | — | filetypes/deb: 11.63% | 0.607 | 0.585 |
| markdown | 41 | 7657 | `general,filetypes/markdown` | general: 9.76% | 0 | 2.44% | -7.32% | general: 9.76% | 0.007 | 0.060 |
| crx | 39 | 12 | `general,filetypes/crx` | filetypes/crx: 92.31% | 0 | 76.92% | -15.38% | filetypes/crx: 94.87% | 0.993 | 0.982 |
| perl | 34 | 4192 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 70.59% | 0 | 70.59% | 0.00% | filetypes/perl: 91.18% | 0.930 | 0.933 |
| data | 32 | 1201 | `general` | general: 28.12% | 0 | 0.00% | -28.12% | general: 34.38% | — | 0.498 |
| chm | 30 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| html | 25 | 3226 | `general,filegroups/documents,filetypes/html` | filetypes/html: 68.00% | 0 | 68.00% | 0.00% | filegroups/documents: 68.00% | 0.853 | 0.852 |
| asar | 17 | 1 | `general` | general: 94.12% | 0 | 0.00% | -94.12% | general: 100.00% | — | 0.997 |
| groovy | 15 | 791 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.065 | 0.081 |
| lua | 13 | 2296 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 53.85% | -15.38% | filegroups/scripts: 76.92% | 0.788 | 0.775 |
| ruby | 12 | 2981 | `general,filegroups/scripts,filetypes/ruby` | general: 83.33% | 0 | 0.00% | -83.33% | general: 83.33% | 0.935 | 0.942 |
| java | 10 | 4459 | `general,filegroups/source,filetypes/java` | filegroups/source: 60.00% | 0 | 40.00% | -20.00% | filetypes/java: 70.00% | 0.852 | 0.828 |
| package-lock.json | 8 | 75 | `general,filetypes/package-lock.json` | general: 0.00% | — | — | — | general: 0.00% | 0.184 | 0.177 |
| clojure | 7 | 340 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 57.14% | 0.00% | general: 57.14% | 0.687 | 0.687 |
| chrome-manifest | 6 | 54 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 33.33% | 0 | 33.33% | 0.00% | filetypes/chrome-manifest: 50.00% | 0.677 | 0.683 |
| dockerfile | 6 | 214 | `general,filetypes/dockerfile` | general: 0.00% | — | — | — | general: 0.00% | 0.366 | 0.107 |
| objc | 5 | 2580 | `general` | general: 60.00% | 0 | 20.00% | -40.00% | general: 60.00% | — | 0.609 |
| zig | 5 | 17 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.691 |
| xz | 4 | 3922 | `general` | general: 25.00% | 0 | 0.00% | -25.00% | general: 25.00% | — | 0.350 |
| applescript | 3 | 35 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.810 |
| bz2 | 3 | 1425 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| pkg | 3 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 100.00% | — | 0.639 |
| swift | 3 | 3871 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.048 |
| whl | 3 | 32 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.189 |
| cargo.toml | 2 | 21 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.090 |
| pyproject.toml | 2 | 2 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 100.00% | — | 1.000 |
| desktop-entry | 1 | 65 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| github-actions | 1 | 832 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.125 |
| ooxml | 1 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| systemd | 1 | 159 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.009 |
| tar.bz2 | 1 | 29 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| xpi | 1 | 5 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| doc | `` | 0 | 0.00% | 99.33% | -99.33% |
| zst | `` | 0 | 0.00% | 97.41% | -97.41% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| 7z | `` | 0 | 0.00% | 89.37% | -89.37% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 8.33% | 83.33% | -75.00% |
| applescript | `` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `` | 0 | 0.00% | 60.00% | -60.00% |
| msi | `` | 0 | 0.00% | 56.01% | -56.01% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `` | 0 | 0.00% | 40.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| lnk | `general,filetypes/lnk` | 0 | 74.60% | 82.80% | -8.20% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| deb | `` | 0 | 0.00% | 4.65% | -4.65% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.37% | 81.65% | -4.28% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.74% | 14.09% | -3.36% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| cargo.toml | `` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| dockerfile | `` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general,filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 89.82% | 88.82% | 1.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.12% | 50.57% | 5.55% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 26.07% | 97.41% | -71.34% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.95% | 100.00% | -61.05% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `filetypes/javascript` | 0 | 55.00% | 66.74% | -11.74% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| lnk | `general,filetypes/lnk` | 0 | 74.60% | 82.80% | -8.20% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.37% | 81.65% | -4.28% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.71% | 50.57% | 4.14% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 26.07% | 97.41% | -71.34% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.95% | 100.00% | -61.05% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `filetypes/javascript` | 0 | 55.04% | 66.74% | -11.70% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| lnk | `general,filetypes/lnk` | 0 | 74.60% | 82.80% | -8.20% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.37% | 81.65% | -4.28% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.73% | 50.57% | 4.16% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 26.07% | 97.41% | -71.34% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.95% | 100.00% | -61.05% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| lnk | `filetypes/lnk` | 0 | 42.40% | 82.80% | -40.40% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| bz2 | `general` | 0 | 33.33% | 66.67% | -33.33% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.21% | 66.74% | -11.53% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.37% | 81.65% | -4.28% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.74% | 50.57% | 4.17% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 26.07% | 97.41% | -71.34% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.99% | 100.00% | -61.01% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| lnk | `filetypes/lnk` | 0 | 60.80% | 82.80% | -22.00% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.27% | 66.74% | -11.47% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 77.37% | 81.65% | -4.28% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| bz2 | `general` | 0 | 66.67% | 66.67% | 0.00% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.76% | 50.57% | 4.19% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| pdf | `filetypes/pdf` | 0 | 0.00% | 73.72% | -73.72% |
| macho | `filetypes/macho` | 0 | 8.87% | 81.65% | -72.78% |
| zst | `general` | 0 | 26.14% | 97.41% | -71.27% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.99% | 100.00% | -61.01% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| lnk | `filetypes/lnk` | 0 | 64.20% | 82.80% | -18.60% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `filetypes/javascript` | 0 | 55.24% | 66.74% | -11.50% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| bz2 | `general` | 0 | 66.67% | 66.67% | 0.00% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.84% | 50.57% | 4.27% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 26.60% | 97.41% | -70.81% |
| pdf | `filetypes/pdf` | 0 | 3.81% | 73.72% | -69.91% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.99% | 100.00% | -61.01% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| macho | `filetypes/macho` | 0 | 37.00% | 81.65% | -44.65% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| lnk | `filetypes/lnk` | 0 | 65.80% | 82.80% | -17.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| bz2 | `general` | 0 | 66.67% | 66.67% | 0.00% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 54.93% | 50.57% | 4.36% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| pdf | `filetypes/pdf` | 0 | 3.83% | 73.72% | -69.89% |
| zst | `general` | 0 | 27.59% | 97.41% | -69.82% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 38.99% | 100.00% | -61.01% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| macho | `filetypes/macho` | 0 | 42.20% | 81.65% | -39.45% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| lnk | `filetypes/lnk` | 0 | 67.00% | 82.80% | -15.80% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| docx | `filetypes/docx` | 0 | 81.44% | 88.82% | -7.39% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 55.03% | 50.57% | 4.45% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 27.82% | 97.41% | -69.59% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.04% | 100.00% | -60.96% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| pdf | `filetypes/pdf` | 0 | 27.86% | 73.72% | -45.86% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| macho | `filetypes/macho` | 0 | 43.12% | 81.65% | -38.53% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 67.60% | 82.80% | -15.20% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 55.09% | 50.57% | 4.52% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 28.96% | 97.41% | -68.45% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.08% | 100.00% | -60.92% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| macho | `filetypes/macho` | 0 | 46.79% | 81.65% | -34.86% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| pdf | `filetypes/pdf` | 0 | 43.33% | 73.72% | -30.39% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 67.80% | 82.80% | -15.00% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.46% | 50.57% | 2.89% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 29.19% | 97.41% | -68.22% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.08% | 100.00% | -60.92% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| macho | `filetypes/macho` | 0 | 49.54% | 81.65% | -32.11% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| pdf | `filetypes/pdf` | 0 | 51.65% | 73.72% | -22.07% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 68.20% | 82.80% | -14.60% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.51% | 50.57% | 2.94% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 29.73% | 97.41% | -67.68% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.08% | 100.00% | -60.92% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| macho | `filetypes/macho` | 0 | 53.82% | 81.65% | -27.83% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| pdf | `filetypes/pdf` | 0 | 54.85% | 73.72% | -18.87% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 68.20% | 82.80% | -14.60% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.55% | 50.57% | 2.98% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| zst | `general` | 0 | 30.03% | 97.41% | -67.38% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.08% | 100.00% | -60.92% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| macho | `filetypes/macho` | 0 | 54.74% | 81.65% | -26.91% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 68.20% | 82.80% | -14.60% |
| pdf | `filetypes/pdf` | 0 | 60.46% | 73.72% | -13.26% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.59% | 50.57% | 3.02% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| zst | `general` | 0 | 31.48% | 97.41% | -65.93% |
| rar | `general` | 0 | 39.08% | 100.00% | -60.92% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| macho | `filetypes/macho` | 0 | 56.27% | 81.65% | -25.38% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 68.40% | 82.80% | -14.40% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| pdf | `filetypes/pdf` | 0 | 60.88% | 73.72% | -12.84% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.62% | 50.57% | 3.05% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| zst | `general` | 0 | 31.86% | 97.41% | -65.55% |
| rar | `general` | 0 | 39.12% | 100.00% | -60.88% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| macho | `filetypes/macho` | 0 | 56.57% | 81.65% | -25.08% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| lnk | `filetypes/lnk` | 0 | 68.40% | 82.80% | -14.40% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| pdf | `filetypes/pdf` | 0 | 62.09% | 73.72% | -11.63% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.64% | 88.82% | -7.19% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.66% | 50.57% | 3.09% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 40.42% | 100.00% | -59.58% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 48.25% | 97.41% | -49.16% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| macho | `filetypes/macho` | 0 | 60.24% | 81.65% | -21.41% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| lnk | `filetypes/lnk` | 0 | 71.80% | 82.80% | -11.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.84% | 88.82% | -6.99% |
| pdf | `filetypes/pdf` | 0 | 66.83% | 73.72% | -6.89% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 53.98% | 50.57% | 3.40% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 40.42% | 100.00% | -59.58% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 48.25% | 97.41% | -49.16% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| macho | `filetypes/macho` | 0 | 63.30% | 81.65% | -18.35% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| lnk | `filetypes/lnk` | 0 | 72.40% | 82.80% | -10.40% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.84% | 88.82% | -6.99% |
| pdf | `filetypes/pdf` | 0 | 67.63% | 73.72% | -6.09% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| pe | `filetypes/pe` | 0 | 45.63% | 50.57% | -4.94% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 9.40% | 14.09% | -4.70% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ruby | `filetypes/ruby` | 0 | 0.00% | 83.33% | -83.33% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 40.73% | 100.00% | -59.27% |
| msi | `general` | 0 | 0.51% | 56.01% | -55.50% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 52.29% | 97.41% | -45.12% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| macho | `filetypes/macho` | 0 | 66.97% | 81.65% | -14.68% |
| zip | `general,filetypes/zip` | 0 | 20.33% | 33.40% | -13.07% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| lnk | `filetypes/lnk` | 0 | 72.80% | 82.80% | -10.00% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.84% | 88.82% | -6.99% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| pdf | `filetypes/pdf` | 0 | 68.22% | 73.72% | -5.50% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.07% | 14.09% | -4.03% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 1.81% | 2.41% | -0.60% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.12% | 50.57% | 5.55% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| chm | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| tar.bz2 | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.12% | -94.12% |
| ole | `general,filegroups/documents` | 0 | 17.37% | 94.63% | -77.26% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 8.33% | 83.33% | -75.00% |
| applescript | `general` | 0 | 0.00% | 66.67% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 41.89% | 100.00% | -58.11% |
| msi | `general` | 0 | 1.35% | 56.01% | -54.65% |
| pyproject.toml | `` | 0 | 0.00% | 50.00% | -50.00% |
| zig | `general` | 0 | 0.00% | 40.00% | -40.00% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| zst | `general` | 0 | 61.81% | 97.41% | -35.59% |
| zip | `filetypes/zip` | 0 | 0.18% | 33.40% | -33.22% |
| java_class | `general` | 0 | 15.53% | 47.03% | -31.51% |
| data | `general` | 0 | 0.00% | 28.12% | -28.12% |
| pptx | `filegroups/documents,filetypes/pptx` | 0 | 38.46% | 66.15% | -27.69% |
| xz | `general` | 0 | 0.00% | 25.00% | -25.00% |
| gz | `general` | 0 | 0.00% | 23.20% | -23.20% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 42.42% | 64.44% | -22.02% |
| cab | `general` | 0 | 0.00% | 21.18% | -21.18% |
| java | `filegroups/source` | 0 | 40.00% | 60.00% | -20.00% |
| 7z | `general` | 0 | 73.49% | 89.37% | -15.88% |
| crx | `general,filetypes/crx` | 0 | 76.92% | 92.31% | -15.38% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.45% | 66.74% | -11.29% |
| macho | `filetypes/macho` | 0 | 71.25% | 81.65% | -10.40% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 22.41% | 31.54% | -9.13% |
| lnk | `filetypes/lnk` | 0 | 73.80% | 82.80% | -9.00% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 44.58% | 53.08% | -8.50% |
| markdown | `general,filetypes/markdown` | 0 | 2.44% | 9.76% | -7.32% |
| docx | `filetypes/docx` | 0 | 81.84% | 88.82% | -6.99% |
| tar.gz | `general,filetypes/tar.gz` | 0 | 75.86% | 81.87% | -6.01% |
| c | `general,filegroups/source,filetypes/c` | 0 | 4.38% | 10.28% | -5.90% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 92.13% | 97.96% | -5.83% |
| text | `general` | 0 | 10.59% | 14.12% | -3.53% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 10.74% | 14.09% | -3.36% |
| tar | `general,filetypes/tar` | 0 | 95.05% | 97.80% | -2.75% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 46.97% | 49.69% | -2.72% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 71.16% | 73.72% | -2.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 88.91% | 90.89% | -1.98% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 92.74% | 94.11% | -1.37% |
| rust | `filetypes/rust` | 0 | 1.20% | 2.41% | -1.20% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 43.97% | 44.82% | -0.85% |
| go | `general,filegroups/source,filetypes/go` | 0 | 1.27% | 1.69% | -0.42% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 98.06% | 98.47% | -0.41% |
| doc | `general,filegroups/documents` | 0 | 99.04% | 99.33% | -0.29% |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 33.33% | 33.33% | 0.00% |
| clojure | `filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 68.00% | 68.00% | 0.00% |
| json | `filegroups/config` | 0 | 4.30% | 4.30% | 0.00% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 70.59% | 70.59% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 6.06% | 6.06% | 0.00% |
| rtf | `general,filegroups/documents,filetypes/rtf` | 0 | 98.70% | 98.70% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| png | `general,filegroups/media,filetypes/png` | 0 | 1.63% | 1.49% | 0.15% |
| jar | `general,filetypes/jar` | 0 | 56.99% | 56.46% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 4.72% | 2.89% | 1.84% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 90.28% | 87.45% | 2.83% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 82.07% | 78.54% | 3.52% |
| vbs | `general,filetypes/vbs` | 0 | 64.84% | 60.94% | 3.90% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 56.12% | 50.57% | 5.55% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 75.12% | 68.72% | 6.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 48.97% | 31.55% | 17.41% |
