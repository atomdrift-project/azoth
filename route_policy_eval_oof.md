# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 837332 (308082 malware, 529250 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 163459 | 19929 | `general,filegroups/native,filetypes/pe` | filegroups/native: 48.92% | 0 | 41.69% | -7.24% | filegroups/native: 63.20% | 0.999 | 1.000 |
| pdf | 22499 | 2923 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 6.84% | 0 | 4.25% | -2.59% | filetypes/pdf: 74.44% | 0.992 | 0.992 |
| elf | 22216 | 20670 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 93.58% | 0 | 92.64% | -0.94% | filetypes/elf: 95.09% | 1.000 | 0.999 |
| batch | 22079 | 556 | `general,filegroups/scripts,filetypes/batch` | general: 1.36% | 0 | 1.24% | -0.13% | filetypes/batch: 1.93% | 0.993 | 0.992 |
| javascript | 14438 | 73486 | `general,filegroups/scripts,filetypes/javascript` | filegroups/scripts: 61.32% | 0 | 37.28% | -24.05% | filetypes/javascript: 63.22% | 0.957 | 0.955 |
| zip | 12586 | 1429 | `general,filetypes/zip` | general: 37.42% | 0 | 35.17% | -2.25% | filetypes/zip: 41.09% | 0.976 | 0.975 |
| xlsx | 7394 | 198 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.15% | 0 | 29.09% | -2.06% | filetypes/xlsx: 31.17% | 0.997 | 0.997 |
| xls | 4629 | 2652 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 94.73% | 0 | 90.97% | -3.76% | filegroups/documents: 94.86% | 0.994 | 0.994 |
| doc | 3923 | 7 | `general,filegroups/documents` | filegroups/documents: 96.86% | 0 | 66.38% | -30.49% | filegroups/documents: 99.03% | — | 1.000 |
| kotlin | 3901 | 6364 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 51.42% | 1 | 54.55% | -3.28% | filetypes/kotlin: 57.83% | 0.898 | 0.898 |
| tar | 2762 | 2835 | `general,filetypes/tar` | filetypes/tar: 86.86% | 0 | 81.54% | -5.32% | filetypes/tar: 87.76% | 0.995 | 0.988 |
| rar | 2545 | 0 | `general` | general: 100.00% | 0 | 5.34% | -94.66% | general: 100.00% | — | — |
| python | 2432 | 22754 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 42.97% | 0 | 48.19% | 5.22% | general: 64.27% | 0.825 | 0.824 |
| package.json | 2244 | 2581 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 88.95% | 1 | 92.51% | -0.58% | filetypes/package.json: 93.09% | 0.997 | 0.997 |
| unknown | 2097 | 6196 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.76% | — | 0.726 |
| shell | 1872 | 7344 | `general,filegroups/scripts,filetypes/shell` | filegroups/scripts: 59.99% | 2 | 68.11% | — | filegroups/scripts: 75.11% | 0.977 | 0.977 |
| c | 1793 | 83253 | `general,filegroups/source,filetypes/c` | filetypes/c: 12.10% | 4 | 13.33% | — | filetypes/c: 13.33% | 0.263 | 0.256 |
| vbs | 1428 | 426 | `general,filetypes/vbs` | filetypes/vbs: 47.20% | 3 | 70.59% | -1.68% | filetypes/vbs: 56.65% | 0.994 | 0.993 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 8.26% | -79.50% | general: 97.04% | — | 0.995 |
| pkg-info | 1277 | 230 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.46% | 0 | 65.47% | -29.99% | general: 97.02% | 0.998 | 0.998 |
| go | 1238 | 15176 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.33% | 4 | 7.27% | — | filetypes/go: 5.33% | 0.277 | 0.221 |
| png | 811 | 21106 | `general,filegroups/media,filetypes/png` | filetypes/png: 3.08% | 0 | 0.12% | -2.96% | filetypes/png: 7.27% | 0.123 | 0.141 |
| ole | 792 | 778 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 83.96% | 0 | 50.88% | -33.08% | filetypes/ole: 84.22% | 0.982 | 0.982 |
| rtf | 784 | 53 | `general,filegroups/documents,filetypes/rtf` | general: 97.45% | 0 | 97.45% | 0.00% | general: 97.45% | 0.999 | 0.999 |
| 7z | 776 | 14 | `general` | general: 92.14% | 0 | 12.63% | -79.51% | general: 93.56% | — | 0.999 |
| php | 640 | 18231 | `general,filegroups/scripts,filetypes/php` | general: 55.16% | 0 | 47.03% | -8.12% | general: 55.31% | 0.783 | 0.775 |
| powershell | 636 | 306 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 55.19% | 0 | 56.45% | 1.26% | filegroups/scripts: 56.76% | 0.982 | 0.985 |
| docx | 562 | 58 | `general,filegroups/documents,filetypes/docx` | filetypes/docx: 80.07% | 0 | 44.66% | -35.41% | filegroups/documents: 82.74% | 0.989 | 0.989 |
| msi | 553 | 11 | `general,filetypes/msi` | filetypes/msi: 92.52% | 0 | 38.34% | -54.19% | filetypes/msi: 95.33% | 0.999 | 0.997 |
| lnk | 538 | 131 | `general,filetypes/lnk` | filetypes/lnk: 83.46% | 0 | 66.73% | -16.73% | filetypes/lnk: 83.46% | 0.991 | 0.990 |
| gz | 524 | 8636 | `general` | general: 27.10% | 0 | 0.00% | -27.10% | general: 40.84% | — | 0.688 |
| jar | 445 | 452 | `general,filetypes/jar` | filetypes/jar: 54.83% | 0 | 46.97% | -7.87% | filetypes/jar: 55.51% | 0.967 | 0.953 |
| xml | 393 | 25634 | `general,filegroups/config,filetypes/xml` | general: 2.54% | 1 | 3.56% | -2.29% | filegroups/config: 5.85% | 0.123 | 0.180 |
| python-bytecode | 354 | 10858 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 97.18% | 0 | 88.14% | -9.04% | filetypes/python-bytecode: 97.18% | 0.980 | 0.980 |
| macho | 334 | 1486 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 74.85% | 0 | 68.26% | -6.59% | filetypes/macho: 91.02% | 0.993 | 0.960 |
| csharp | 242 | 8141 | `general,filegroups/source,filetypes/csharp` | filetypes/csharp: 26.03% | 0 | 19.42% | -6.61% | filegroups/source: 31.40% | 0.460 | 0.460 |
| java_class | 221 | 88047 | `general,filegroups/portable,filetypes/java_class` | general: 71.49% | 16 | 90.05% | — | general: 72.40% | 0.902 | 0.898 |
| text | 214 | 10483 | `general,filetypes/text` | general: 12.15% | 0 | 8.41% | -3.74% | general: 14.49% | 0.175 | 0.186 |
| rust | 167 | 10881 | `general,filegroups/source,filetypes/rust` | general: 2.40% | 0 | 1.80% | -0.60% | filegroups/source: 5.39% | 0.038 | 0.052 |
| jpeg | 151 | 3720 | `general,filegroups/media,filetypes/jpeg` | filetypes/jpeg: 11.92% | 0 | 11.92% | 0.00% | filetypes/jpeg: 13.91% | 0.262 | 0.279 |
| crx | 129 | 10 | `general,filetypes/crx` | filetypes/crx: 96.90% | 0 | 40.31% | -56.59% | filetypes/crx: 96.90% | 0.999 | 0.995 |
| json | 103 | 3859 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.038 |
| cab | 96 | 11 | `general` | general: 23.96% | 0 | 0.00% | -23.96% | general: 33.33% | — | 0.974 |
| pptx | 72 | 21 | `general,filegroups/documents` | filegroups/documents: 6.94% | 0 | 1.39% | -5.56% | filegroups/documents: 40.28% | — | 0.808 |
| makefile | 68 | 3263 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 2.94% | 0.028 | 0.028 |
| plist | 66 | 1584 | `general,filegroups/config,filetypes/plist` | filegroups/config: 3.03% | 2 | 6.06% | — | filegroups/config: 6.06% | 0.131 | 0.131 |
| deb | 45 | 872 | `general,filetypes/deb` | general: 11.11% | 0 | 11.11% | 0.00% | general: 11.11% | 0.145 | 0.140 |
| chm | 38 | 6 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 86.84% | — | 0.987 |
| perl | 36 | 4913 | `general,filegroups/scripts,filetypes/perl` | filegroups/scripts: 72.22% | 0 | 69.44% | -2.78% | filetypes/perl: 83.33% | 0.913 | 0.923 |
| data | 32 | 1337 | `general` | general: 31.25% | 0 | 0.00% | -31.25% | general: 34.38% | — | 0.481 |
| asar | 17 | 1 | `general` | general: 88.24% | 0 | 0.00% | -88.24% | general: 100.00% | — | 0.993 |
| html | 14 | 1371 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| groovy | 13 | 787 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.049 | 0.049 |
| lua | 13 | 2321 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 53.85% | -15.38% | general: 69.23% | 0.707 | 0.714 |
| ruby | 12 | 3020 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 66.67% | 0 | 41.67% | -25.00% | filetypes/ruby: 75.00% | 0.937 | 0.937 |
| java | 10 | 5213 | `general,filegroups/source,filetypes/java` | filegroups/source: 30.00% | 0 | 30.00% | 0.00% | filegroups/source: 60.00% | 0.162 | 0.162 |
| xz | 10 | 3943 | `general` | general: 10.00% | 0 | 0.00% | -10.00% | general: 10.00% | — | 0.376 |
| package-lock.json | 9 | 79 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.136 |
| markdown | 8 | 2411 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| chrome-manifest | 7 | 55 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 71.43% | 0 | 42.86% | -28.57% | filetypes/chrome-manifest: 71.43% | 0.855 | 0.742 |
| clojure | 7 | 614 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.630 | 0.630 |
| dockerfile | 6 | 230 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.038 |
| objc | 5 | 2770 | `general` | general: 60.00% | 0 | 0.00% | -60.00% | general: 60.00% | — | 0.620 |
| zig | 5 | 21 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 40.00% | — | 0.473 |
| cargo.toml | 4 | 67 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.040 |
| swift | 4 | 3872 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.083 |
| applescript | 3 | 36 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| bz2 | 3 | 1429 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| whl | 3 | 78 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.078 |
| pyproject.toml | 2 | 6 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.667 |
| desktop-entry | 1 | 90 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| github-actions | 1 | 895 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.167 |
| ooxml | 1 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| pkg | 1 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| systemd | 1 | 172 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.009 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 6 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| 7z | `general` | 0 | 0.64% | 92.14% | -91.49% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| zst | `general` | 0 | 0.00% | 87.76% | -87.76% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 4.64% | 100.00% | -95.36% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 11.86% | 92.14% | -80.28% |
| zst | `general` | 0 | 7.87% | 87.76% | -79.89% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 4.64% | 100.00% | -95.36% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 11.86% | 92.14% | -80.28% |
| zst | `general` | 0 | 7.87% | 87.76% | -79.89% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 5.34% | 100.00% | -94.66% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 12.63% | 92.14% | -79.51% |
| zst | `general` | 0 | 8.26% | 87.76% | -79.50% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 5.34% | 100.00% | -94.66% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 12.63% | 92.14% | -79.51% |
| zst | `general` | 0 | 8.26% | 87.76% | -79.50% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 5.34% | 100.00% | -94.66% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 12.63% | 92.14% | -79.51% |
| zst | `general` | 0 | 8.26% | 87.76% | -79.50% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 10.84% | 100.00% | -89.16% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 15.98% | 92.14% | -76.16% |
| zst | `general` | 0 | 11.85% | 87.76% | -75.92% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| rar | `general` | 0 | 10.84% | 100.00% | -89.16% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| 7z | `general` | 0 | 15.98% | 92.14% | -76.16% |
| zst | `general` | 0 | 11.85% | 87.76% | -75.92% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| rar | `general` | 0 | 12.77% | 100.00% | -87.23% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 13.09% | 87.76% | -74.67% |
| 7z | `general` | 0 | 18.43% | 92.14% | -73.71% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 19.76% | 100.00% | -80.24% |
| 7z | `general` | 0 | 23.71% | 92.14% | -68.43% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| zst | `general` | 0 | 25.49% | 87.76% | -62.28% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.00% | 27.10% | -27.10% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 0.00% | 23.96% | -23.96% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 26.52% | 100.00% | -73.48% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 30.67% | 92.14% | -61.47% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 41.62% | 87.76% | -46.14% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.19% | 27.10% | -26.91% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 1.04% | 23.96% | -22.92% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 32.30% | 100.00% | -67.70% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| 7z | `general` | 0 | 36.73% | 92.14% | -55.41% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| zst | `general` | 0 | 48.79% | 87.76% | -38.97% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| gz | `general` | 0 | 0.76% | 27.10% | -26.34% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 1.04% | 23.96% | -22.92% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.82% | 100.00% | -63.18% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 42.78% | 92.14% | -49.36% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| zst | `general` | 0 | 56.04% | 87.76% | -31.72% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| doc | `general,filegroups/documents` | 0 | 66.38% | 96.86% | -30.49% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| gz | `general` | 0 | 2.48% | 27.10% | -24.62% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| cab | `general` | 0 | 1.04% | 23.96% | -22.92% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 88.24% | -88.24% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.45% | 100.00% | -60.55% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| 7z | `general` | 0 | 48.45% | 92.14% | -43.69% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| zst | `general` | 0 | 64.61% | 87.76% | -23.15% |
| doc | `general,filegroups/documents` | 0 | 73.80% | 96.86% | -23.07% |
| gz | `general` | 0 | 5.53% | 27.10% | -21.56% |
| cab | `general` | 0 | 3.12% | 23.96% | -20.83% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| xz | `general` | 0 | 0.00% | 10.00% | -10.00% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 4 | 13.33% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 16 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| applescript | `general` | 0 | 0.00% | 100.00% | -100.00% |
| desktop-entry | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 2.63% | 86.84% | -84.21% |
| asar | `general` | 0 | 5.88% | 88.24% | -82.35% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 41.49% | 100.00% | -58.51% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| 7z | `general` | 0 | 59.66% | 92.14% | -32.47% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 37.28% | 61.32% | -24.05% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| doc | `general,filegroups/documents` | 0 | 77.62% | 96.86% | -19.25% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| gz | `general` | 0 | 15.27% | 27.10% | -11.83% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| cab | `general` | 0 | 15.62% | 23.96% | -8.33% |
| zst | `general` | 0 | 79.58% | 87.76% | -8.18% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 8 | 13.83% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 24 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| asar | `general` | 0 | 11.76% | 88.24% | -76.47% |
| applescript | `general` | 0 | 33.33% | 100.00% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 42.12% | 100.00% | -57.88% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| 7z | `general` | 0 | 62.63% | 92.14% | -29.51% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| doc | `general,filegroups/documents` | 0 | 78.51% | 96.86% | -18.35% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.44% | 61.32% | -15.89% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| gz | `general` | 0 | 17.75% | 27.10% | -9.35% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| cab | `general` | 0 | 18.75% | 23.96% | -5.21% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| zst | `general` | 0 | 85.35% | 87.76% | -2.42% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 8 | 13.83% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| desktop-entry | `general` | 0 | 100.00% | 100.00% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 24 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| asar | `general` | 0 | 11.76% | 88.24% | -76.47% |
| applescript | `general` | 0 | 33.33% | 100.00% | -66.67% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| objc | `general` | 0 | 0.00% | 60.00% | -60.00% |
| rar | `general` | 0 | 42.51% | 100.00% | -57.49% |
| crx | `general,filetypes/crx` | 0 | 40.31% | 96.90% | -56.59% |
| msi | `general,filetypes/msi` | 0 | 38.34% | 92.52% | -54.19% |
| pyproject.toml | `general` | 0 | 0.00% | 50.00% | -50.00% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 44.66% | 80.07% | -35.41% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.88% | 83.96% | -33.08% |
| data | `general` | 0 | 0.00% | 31.25% | -31.25% |
| pkg-info | `general` | 0 | 65.47% | 95.46% | -29.99% |
| chrome-manifest | `filetypes/chrome-manifest` | 0 | 42.86% | 71.43% | -28.57% |
| 7z | `general` | 0 | 64.82% | 92.14% | -27.32% |
| ruby | `general,filegroups/scripts,filetypes/ruby` | 0 | 41.67% | 66.67% | -25.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| lnk | `general,filetypes/lnk` | 0 | 66.73% | 83.46% | -16.73% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 45.44% | 61.32% | -15.89% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 53.85% | 69.23% | -15.38% |
| doc | `general,filegroups/documents` | 0 | 81.72% | 96.86% | -15.14% |
| clojure | `general` | 0 | 42.86% | 57.14% | -14.29% |
| python-bytecode | `general,filetypes/python-bytecode` | 0 | 88.14% | 97.18% | -9.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 47.03% | 55.16% | -8.12% |
| jar | `general,filetypes/jar` | 0 | 46.97% | 54.83% | -7.87% |
| gz | `general` | 0 | 19.27% | 27.10% | -7.82% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 41.69% | 48.92% | -7.24% |
| csharp | `general,filegroups/source,filetypes/csharp` | 0 | 19.42% | 26.03% | -6.61% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 68.26% | 74.85% | -6.59% |
| pptx | `general,filegroups/documents` | 0 | 1.39% | 6.94% | -5.56% |
| tar | `general,filetypes/tar` | 0 | 81.54% | 86.86% | -5.32% |
| xls | `general,filegroups/documents,filetypes/xls` | 0 | 90.97% | 94.73% | -3.76% |
| text | `general,filetypes/text` | 0 | 8.41% | 12.15% | -3.74% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 1 | 54.55% | 57.83% | -3.28% |
| cab | `general` | 0 | 20.83% | 23.96% | -3.12% |
| png | `general,filegroups/media,filetypes/png` | 0 | 0.12% | 3.08% | -2.96% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 69.44% | 72.22% | -2.78% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.25% | 6.84% | -2.59% |
| xml | `filegroups/config,filetypes/xml` | 1 | 3.56% | 5.85% | -2.29% |
| zip | `general,filetypes/zip` | 0 | 35.17% | 37.42% | -2.25% |
| xlsx | `general,filegroups/documents,filetypes/xlsx` | 0 | 29.09% | 31.15% | -2.06% |
| vbs | `general,filetypes/vbs` | 3 | 70.59% | 72.27% | -1.68% |
| zst | `general` | 0 | 86.20% | 87.76% | -1.56% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.64% | 93.58% | -0.94% |
| rust | `general,filegroups/source` | 0 | 1.80% | 2.40% | -0.60% |
| package.json | `general,filegroups/config,filetypes/package.json` | 1 | 92.51% | 93.09% | -0.58% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 1.24% | 1.36% | -0.13% |
| c | `general,filegroups/source,filetypes/c` | 8 | 13.83% | — | — |
| cargo.toml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `general,filetypes/deb` | 0 | 11.11% | 11.11% | 0.00% |
| desktop-entry | `general` | 0 | 100.00% | 100.00% | 0.00% |
| dockerfile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| go | `general,filegroups/source,filetypes/go` | 4 | 7.27% | — | — |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `general,filegroups/source` | 0 | 30.00% | 30.00% | 0.00% |
| java_class | `general,filetypes/java_class` | 24 | 90.05% | — | — |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 11.92% | 11.92% | 0.00% |
| json | `general,filegroups/config` | 1 | 0.00% | 0.00% | 0.00% |
| makefile | `general` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 2 | 6.06% | — | — |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.45% | 97.45% | 0.00% |
| shell | `general,filegroups/scripts,filetypes/shell` | 2 | 68.11% | — | — |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| whl | `general` | 0 | 0.00% | 0.00% | 0.00% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 56.45% | 55.19% | 1.26% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 48.19% | 42.97% | 5.22% |
