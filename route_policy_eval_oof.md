# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 905195 (312695 malware, 592500 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 164518 | 20130 | `general,filegroups/native,filetypes/pe` | filegroups/native: 49.81% | 0 | 59.28% | 9.47% | filegroups/native: 59.89% | 0.999 | 1.000 |
| pdf | 22502 | 2947 | `general,filegroups/documents,filetypes/pdf` | filegroups/documents: 5.12% | 0 | 5.13% | 0.01% | filetypes/pdf: 74.38% | 0.992 | 0.992 |
| elf | 22443 | 22231 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 94.35% | 0 | 94.46% | 0.11% | filetypes/elf: 96.28% | 1.000 | 0.999 |
| batch | 22100 | 708 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 1.51% | 0 | 2.04% | 0.53% | filetypes/batch: 2.71% | 0.987 | 0.987 |
| javascript | 14813 | 79726 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 62.00% | 0 | 53.92% | -8.08% | filegroups/scripts: 63.27% | 0.952 | 0.950 |
| zip | 12698 | 1501 | `general,filetypes/zip` | general: 34.35% | 0 | 34.53% | 0.18% | general: 37.12% | 0.975 | 0.972 |
| xlsx | 7472 | 201 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.06% | 0 | 30.54% | -0.52% | filegroups/documents: 31.09% | 0.995 | 0.995 |
| xls | 4671 | 2652 | `general,filegroups/documents,filetypes/xls` | filegroups/documents: 94.75% | 0 | 94.16% | -0.60% | filegroups/documents: 94.86% | 0.995 | 0.995 |
| doc | 3959 | 7 | `general,filegroups/documents` | filegroups/documents: 96.82% | — | — | — | filegroups/documents: 98.99% | — | 1.000 |
| kotlin | 3937 | 6848 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 52.91% | 0 | 52.27% | -0.64% | filegroups/source: 56.95% | 0.860 | 0.861 |
| tar | 2823 | 3332 | `general,filetypes/tar` | filetypes/tar: 83.88% | 0 | 84.27% | 0.39% | filetypes/tar: 85.62% | 0.995 | 0.988 |
| python | 2760 | 26860 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 47.61% | 0 | 49.35% | 1.74% | filetypes/python: 58.04% | 0.790 | 0.795 |
| rar | 2569 | 0 | `general` | general: 100.00% | 0 | 15.26% | -84.74% | general: 100.00% | — | — |
| package.json | 2265 | 2939 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 83.36% | 0 | 87.24% | 3.89% | filetypes/package.json: 93.64% | 0.996 | 0.996 |
| c | 2106 | 95882 | `general,filegroups/source,filetypes/c` | filetypes/c: 9.88% | 0 | 6.70% | -3.18% | filegroups/source: 10.35% | 0.255 | 0.263 |
| unknown | 2101 | 6570 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.76% | — | 0.746 |
| shell | 1937 | 7925 | `general,filegroups/scripts,filetypes/shell` | general: 62.42% | 0 | 71.14% | 8.72% | general: 67.37% | 0.966 | 0.969 |
| vbs | 1450 | 428 | `general,filetypes/vbs` | filetypes/vbs: 34.76% | 0 | 39.38% | 4.62% | filetypes/vbs: 39.17% | 0.991 | 0.991 |
| go | 1377 | 15709 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.01% | 0 | 5.30% | 0.29% | filetypes/go: 6.17% | 0.266 | 0.214 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 18.16% | -69.60% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 290 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.61% | 0 | 95.85% | 0.23% | general: 97.02% | 0.998 | 0.997 |
| png | 1023 | 22239 | `general,filegroups/media,filetypes/png` | filegroups/media: 0.20% | 0 | 0.00% | -0.20% | filegroups/media: 5.77% | 0.102 | 0.104 |
| 7z | 1021 | 14 | `general` | general: 85.50% | 0 | 22.14% | -63.37% | general: 89.13% | — | 0.999 |
| ole | 809 | 792 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 82.69% | 0 | 50.93% | -31.77% | filetypes/ole: 82.82% | 0.976 | 0.976 |
| rtf | 790 | 54 | `general,filegroups/documents,filetypes/rtf` | filegroups/documents: 97.22% | 0 | 97.22% | 0.00% | filegroups/documents: 97.22% | 0.999 | 0.999 |
| php | 708 | 19409 | `general,filegroups/scripts,filetypes/php` | general: 50.28% | 0 | 46.05% | -4.24% | general: 52.68% | 0.771 | 0.765 |
| powershell | 670 | 312 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 42.99% | 0 | 46.57% | 3.58% | filegroups/scripts: 57.91% | 0.985 | 0.982 |
| docx | 568 | 58 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 82.04% | 0 | 82.39% | 0.35% | filegroups/documents: 82.04% | 0.989 | 0.988 |
| msi | 560 | 15 | `general,filetypes/msi` | filetypes/msi: 81.96% | 0 | 68.39% | -13.57% | filetypes/msi: 81.96% | 0.997 | 0.995 |
| lnk | 543 | 132 | `general,filetypes/lnk` | filetypes/lnk: 83.61% | 0 | 78.45% | -5.16% | filetypes/lnk: 83.61% | 0.992 | 0.990 |
| gz | 530 | 9083 | `general` | general: 31.51% | 0 | 0.00% | -31.51% | general: 36.23% | — | 0.689 |
| xml | 491 | 27109 | `general,filegroups/config,filetypes/xml` | general: 2.24% | 0 | 2.24% | 0.00% | filetypes/xml: 5.09% | 0.115 | 0.158 |
| jar | 458 | 481 | `general,filetypes/jar` | filetypes/jar: 57.42% | 0 | 55.46% | -1.97% | filetypes/jar: 57.42% | 0.958 | 0.950 |
| python-bytecode | 401 | 23635 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 86.28% | 0 | 81.80% | -4.49% | filetypes/python-bytecode: 86.28% | 0.882 | 0.883 |
| csharp | 392 | 8373 | `general,filegroups/source,filetypes/csharp` | general: 15.82% | 0 | 14.54% | -1.28% | filegroups/source: 20.41% | 0.426 | 0.426 |
| text | 381 | 13134 | `general,filetypes/text` | general: 6.56% | 0 | 5.51% | -1.05% | general: 8.14% | 0.115 | 0.122 |
| macho | 339 | 1575 | `general,filegroups/native,filetypes/macho` | general: 69.32% | 0 | 74.93% | 5.60% | filetypes/macho: 89.38% | 0.989 | 0.983 |
| java | 307 | 7146 | `general,filegroups/source,filetypes/java` | filetypes/java: 4.56% | 0 | 4.89% | 0.33% | filetypes/java: 8.14% | 0.201 | 0.201 |
| java_class | 238 | 93690 | `general,filegroups/portable,filetypes/java_class` | general: 63.87% | 0 | 46.64% | -17.23% | filegroups/portable: 76.89% | 0.876 | 0.878 |
| rust | 213 | 12612 | `general,filegroups/source,filetypes/rust` | general: 1.41% | 0 | 1.41% | 0.00% | filegroups/source: 2.35% | 0.032 | 0.051 |
| jpeg | 168 | 3803 | `general,filegroups/media,filetypes/jpeg` | general: 10.71% | 0 | 8.93% | -1.79% | filetypes/jpeg: 13.10% | 0.244 | 0.267 |
| crx | 163 | 10 | `general,filetypes/crx` | filetypes/crx: 98.16% | 0 | 83.44% | -14.72% | filetypes/crx: 98.16% | 0.999 | 0.988 |
| json | 129 | 5421 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.061 |
| cab | 99 | 11 | `general` | general: 23.23% | 0 | 0.00% | -23.23% | general: 46.46% | — | 0.978 |
| makefile | 85 | 3834 | `general,filegroups/source,filetypes/makefile` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.026 | 0.026 |
| plist | 77 | 1610 | `general,filegroups/config,filetypes/plist` | filegroups/config: 5.19% | 0 | 5.19% | 0.00% | filegroups/config: 5.19% | 0.143 | 0.143 |
| pptx | 73 | 22 | `general,filegroups/documents` | filegroups/documents: 9.59% | — | — | — | filegroups/documents: 41.10% | — | 0.811 |
| deb | 50 | 947 | `general,filetypes/deb` | general: 10.00% | 0 | 10.00% | 0.00% | general: 10.00% | 0.140 | 0.129 |
| perl | 39 | 5403 | `general,filegroups/scripts,filetypes/perl` | general: 58.97% | 0 | 56.41% | -2.56% | filegroups/scripts: 69.23% | 0.838 | 0.838 |
| chm | 38 | 6 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 86.84% | — | 0.992 |
| data | 37 | 1382 | `general` | general: 21.62% | 0 | 0.00% | -21.62% | general: 32.43% | — | 0.456 |
| applescript | 26 | 36 | `general,filetypes/applescript` | general: 26.92% | 0 | 19.23% | -7.69% | general: 26.92% | 0.538 | 0.538 |
| cargo.toml | 25 | 210 | `general,filetypes/cargo.toml` | general: 32.00% | 0 | 20.00% | -12.00% | general: 32.00% | 0.447 | 0.447 |
| ruby | 21 | 3436 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 42.86% | 0 | 33.33% | -9.52% | general: 42.86% | 0.540 | 0.567 |
| asar | 18 | 2 | `general` | general: 94.44% | 0 | 0.00% | -94.44% | general: 94.44% | — | 0.994 |
| dockerfile | 16 | 278 | `general,filetypes/dockerfile` | filetypes/dockerfile: 6.25% | 0 | 6.25% | 0.00% | filetypes/dockerfile: 6.25% | 0.185 | 0.168 |
| groovy | 16 | 860 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.015 | 0.015 |
| html | 14 | 1393 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2359 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 38.46% | -30.77% | general: 69.23% | 0.688 | 0.724 |
| package-lock.json | 11 | 102 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.119 |
| markdown | 10 | 3521 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |
| xz | 10 | 4552 | `general` | general: 30.00% | 0 | 0.00% | -30.00% | general: 30.00% | — | 0.504 |
| chrome-manifest | 8 | 56 | `general,filetypes/chrome-manifest` | filetypes/chrome-manifest: 37.50% | 0 | 37.50% | 0.00% | filetypes/chrome-manifest: 62.50% | 0.740 | 0.636 |
| clojure | 7 | 676 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 42.86% | -14.29% | general: 57.14% | 0.625 | 0.625 |
| objc | 5 | 2798 | `general,filetypes/objc` | general: 60.00% | 0 | 20.00% | -40.00% | general: 60.00% | 0.108 | 0.108 |
| pyproject.toml | 5 | 23 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 20.00% | — | 0.664 |
| zig | 5 | 21 | `general` | general: 20.00% | 0 | 0.00% | -20.00% | general: 40.00% | — | 0.492 |
| swift | 4 | 3928 | `general,filegroups/source` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.120 |
| bz2 | 3 | 1430 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.667 |
| desktop-entry | 3 | 270 | `general` | general: 66.67% | 0 | 0.00% | -66.67% | general: 66.67% | — | 0.672 |
| msg | 3 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| whl | 3 | 109 | `general,filetypes/whl` | general: 0.00% | — | — | — | general: 0.00% | 0.144 | 0.055 |
| systemd | 2 | 177 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.009 |
| composerjson | 1 | 9 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 1.000 |
| github-actions | 1 | 1038 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| ooxml | 1 | 6 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| pkg | 1 | 5 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.250 |
| xlsm | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| xpi | 1 | 8 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | 1.000 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| rar | `general` | 0 | 13.12% | 100.00% | -86.88% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| zst | `general` | 0 | 15.28% | 87.76% | -72.49% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.08% | 85.50% | -65.43% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.20% | 100.00% | -86.80% |
| zst | `general` | 0 | 15.43% | 87.76% | -72.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.18% | 85.50% | -65.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.23% | 100.00% | -86.77% |
| zst | `general` | 0 | 15.43% | 87.76% | -72.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.18% | 85.50% | -65.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.23% | 100.00% | -86.77% |
| zst | `general` | 0 | 15.43% | 87.76% | -72.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.18% | 85.50% | -65.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.31% | 100.00% | -86.69% |
| zst | `general` | 0 | 15.43% | 87.76% | -72.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.18% | 85.50% | -65.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.35% | 100.00% | -86.65% |
| zst | `general` | 0 | 15.51% | 87.76% | -72.25% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.18% | 85.50% | -65.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| pptx | `general,filegroups/documents` | 0 | 9.59% | 9.59% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.51% | 100.00% | -86.49% |
| zst | `general` | 0 | 15.82% | 87.76% | -71.94% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.37% | 85.50% | -65.13% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 13.97% | 100.00% | -86.03% |
| zst | `general` | 0 | 16.13% | 87.76% | -71.63% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.86% | 85.50% | -64.64% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 14.25% | 100.00% | -85.75% |
| zst | `general` | 0 | 16.45% | 87.76% | -71.32% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 20.96% | 85.50% | -64.54% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 14.64% | 100.00% | -85.36% |
| zst | `general` | 0 | 17.61% | 87.76% | -70.15% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 21.74% | 85.50% | -63.76% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 15.26% | 100.00% | -84.74% |
| zst | `general` | 0 | 18.16% | 87.76% | -69.60% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 22.14% | 85.50% | -63.37% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 16.08% | 100.00% | -83.92% |
| zst | `general` | 0 | 18.39% | 87.76% | -69.37% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 22.43% | 85.50% | -63.08% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 16.70% | 100.00% | -83.30% |
| zst | `general` | 0 | 18.47% | 87.76% | -69.29% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 22.72% | 85.50% | -62.78% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 16.93% | 100.00% | -83.07% |
| zst | `general` | 0 | 18.55% | 87.76% | -69.21% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 22.92% | 85.50% | -62.59% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 17.36% | 100.00% | -82.64% |
| zst | `general` | 0 | 18.78% | 87.76% | -68.98% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 23.21% | 85.50% | -62.29% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 17.56% | 100.00% | -82.44% |
| zst | `general` | 0 | 19.56% | 87.76% | -68.20% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 23.41% | 85.50% | -62.10% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 23.51% | 100.00% | -76.49% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 28.01% | 85.50% | -57.49% |
| zst | `general` | 0 | 33.67% | 87.76% | -54.09% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.19% | 31.51% | -31.32% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| rar | `general` | 0 | 29.12% | 100.00% | -70.88% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| 7z | `general` | 0 | 33.20% | 85.50% | -52.30% |
| zst | `general` | 0 | 46.38% | 87.76% | -41.39% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.19% | 31.51% | -31.32% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 34.60% | 100.00% | -65.40% |
| 7z | `general` | 0 | 37.90% | 85.50% | -47.60% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| zst | `general` | 0 | 53.94% | 87.76% | -33.83% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.38% | 31.51% | -31.13% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 1.01% | 23.23% | -22.22% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.36% | 100.00% | -63.64% |
| 7z | `general` | 0 | 41.43% | 85.50% | -44.07% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| gz | `general` | 0 | 0.57% | 31.51% | -30.94% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| zst | `general` | 0 | 57.91% | 87.76% | -29.85% |
| cab | `general` | 0 | 1.01% | 23.23% | -22.22% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `general` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 39.12% | 100.00% | -60.88% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| 7z | `general` | 0 | 50.15% | 85.50% | -35.36% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| gz | `general` | 0 | 5.28% | 31.51% | -26.23% |
| zst | `general` | 0 | 65.94% | 87.76% | -21.82% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| cab | `general` | 0 | 3.03% | 23.23% | -20.20% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 0 | 46.64% | 63.87% | -17.23% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 53.92% | 62.00% | -8.08% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| c | `general,filegroups/source,filetypes/c` | 0 | 6.70% | 9.88% | -3.18% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 0.00% | 94.44% | -94.44% |
| chm | `general` | 0 | 2.63% | 86.84% | -84.21% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 41.30% | 100.00% | -58.70% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| 7z | `general` | 0 | 59.55% | 85.50% | -25.95% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| xz | `general` | 0 | 10.00% | 30.00% | -20.00% |
| gz | `general` | 0 | 13.40% | 31.51% | -18.11% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| cab | `general` | 0 | 13.13% | 23.23% | -10.10% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| zst | `general` | 0 | 82.39% | 87.76% | -5.38% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 5.56% | 94.44% | -88.89% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 42.12% | 100.00% | -57.88% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| 7z | `general` | 0 | 63.08% | 85.50% | -22.43% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| gz | `general` | 0 | 16.98% | 31.51% | -14.53% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| cab | `general` | 0 | 19.19% | 23.23% | -4.04% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| zst | `general` | 0 | 85.42% | 87.76% | -2.34% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 94.44% | -83.33% |
| chm | `general` | 0 | 5.26% | 86.84% | -81.58% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 42.43% | 100.00% | -57.57% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| 7z | `general` | 0 | 64.45% | 85.50% | -21.06% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| gz | `general` | 0 | 18.68% | 31.51% | -12.83% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| zst | `general` | 0 | 86.52% | 87.76% | -1.25% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| cab | `general` | 0 | 22.22% | 23.23% | -1.01% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 2.24% | 2.24% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 49.35% | 47.61% | 1.74% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `general` | 0 | 11.11% | 94.44% | -83.33% |
| chm | `general` | 0 | 7.89% | 86.84% | -78.95% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 42.86% | 100.00% | -57.14% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| 7z | `general` | 0 | 66.11% | 85.50% | -19.39% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| gz | `general` | 0 | 19.62% | 31.51% | -11.89% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.05% | 50.28% | -4.24% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| png | `filetypes/png` | 0 | 0.00% | 0.20% | -0.20% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 94.46% | 94.35% | 0.11% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 3.05% | 2.24% | 0.81% |
| python | `general,filetypes/python` | 1 | 59.46% | 58.04% | 1.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
| pe | `filegroups/native,filetypes/pe` | 0 | 59.28% | 49.81% | 9.47% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 10.00% | 100.00% | -90.00% |
| asar | `general` | 0 | 11.11% | 94.44% | -83.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| chm | `general` | 0 | 23.68% | 86.84% | -63.16% |
| rar | `general` | 0 | 43.67% | 100.00% | -56.33% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 2.70% | 21.62% | -18.92% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| gz | `general` | 0 | 20.38% | 31.51% | -11.13% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 48.59% | 52.68% | -4.10% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 85.79% | 86.28% | -0.50% |
| png | `general,filegroups/media` | 1 | 5.67% | 5.77% | -0.10% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 96.92% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `filegroups/native,filetypes/pe` | 2 | 67.82% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.30% | 5.01% | 0.29% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 3.05% | 2.24% | 0.81% |
| python | `general,filetypes/python` | 1 | 59.46% | 58.04% | 1.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| markdown | `general` | 0 | 10.00% | 100.00% | -90.00% |
| asar | `general` | 0 | 11.11% | 94.44% | -83.33% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| chm | `general` | 0 | 28.95% | 86.84% | -57.89% |
| rar | `general` | 0 | 44.88% | 100.00% | -55.12% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| desktop-entry | `general` | 0 | 33.33% | 66.67% | -33.33% |
| ole | `general,filegroups/documents,filetypes/ole` | 0 | 50.93% | 82.69% | -31.77% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 38.46% | 69.23% | -30.77% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 5.41% | 21.62% | -16.22% |
| java_class | `general,filetypes/java_class` | 1 | 60.92% | 76.89% | -15.97% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| gz | `general` | 0 | 21.13% | 31.51% | -10.38% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 33.33% | 42.86% | -9.52% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| lnk | `general,filetypes/lnk` | 0 | 78.45% | 83.61% | -5.16% |
| php | `general,filegroups/scripts,filetypes/php` | 1 | 48.59% | 52.68% | -4.10% |
| perl | `general,filetypes/perl` | 0 | 56.41% | 58.97% | -2.56% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| kotlin | `general,filegroups/source,filetypes/kotlin` | 0 | 52.27% | 52.91% | -0.64% |
| xls | `filetypes/xls` | 0 | 94.16% | 94.75% | -0.60% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.54% | 31.06% | -0.52% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 85.79% | 86.28% | -0.50% |
| png | `general,filegroups/media` | 1 | 5.67% | 5.77% | -0.10% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 1 | 63.22% | 63.27% | -0.05% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 96.92% | — | — |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 1 | 0.00% | 0.00% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pe | `filegroups/native,filetypes/pe` | 2 | 67.82% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 5.19% | 5.19% | 0.00% |
| rtf | `general,filetypes/rtf` | 0 | 97.22% | 97.22% | 0.00% |
| rust | `general,filegroups/source` | 0 | 1.41% | 1.41% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 5.13% | 5.12% | 0.01% |
| zip | `general,filetypes/zip` | 0 | 34.53% | 34.35% | 0.18% |
| go | `general,filegroups/source,filetypes/go` | 1 | 6.39% | 6.17% | 0.22% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| java | `general,filegroups/source,filetypes/java` | 0 | 4.89% | 4.56% | 0.33% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.21% | 9.88% | 0.33% |
| docx | `filegroups/documents,filetypes/docx` | 0 | 82.39% | 82.04% | 0.35% |
| tar | `general,filetypes/tar` | 0 | 84.27% | 83.88% | 0.39% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.04% | 1.51% | 0.53% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 3.05% | 2.24% | 0.81% |
| python | `general,filetypes/python` | 1 | 59.46% | 58.04% | 1.41% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 46.57% | 42.99% | 3.58% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 87.24% | 83.36% | 3.89% |
| vbs | `general,filetypes/vbs` | 0 | 39.38% | 34.76% | 4.62% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 71.14% | 62.42% | 8.72% |
