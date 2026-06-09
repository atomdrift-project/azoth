# Azoth Route Policy Eval

- Partition: `test`
- Score table: `/home/t/collimator/out/models/azoth-candidate-filetypes-c-9445b9b1b5c81388/score_table.npz`
- Route policies: `/home/t/collimator/out/models/azoth-candidate-filetypes-c-9445b9b1b5c81388/route_policies.json`
- Rows in partition: 905195 (312695 malware, 592500 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 164518 | 20130 | `general,filegroups/native,filetypes/pe` | filetypes/pe: 62.52% | 0 | 64.10% | 1.59% | filetypes/pe: 64.40% | 1.000 | 1.000 |
| pdf | 22502 | 2947 | `general,filegroups/documents,filetypes/pdf` | general: 4.10% | 0 | 4.08% | -0.02% | filetypes/pdf: 74.38% | 0.992 | 0.994 |
| elf | 22443 | 22231 | `general,filegroups/native,filetypes/elf` | filetypes/elf: 91.84% | 0 | 92.17% | 0.32% | filetypes/elf: 97.13% | 1.000 | 1.000 |
| batch | 22100 | 708 | `general,filegroups/scripts,filetypes/batch` | filetypes/batch: 1.94% | 0 | 2.22% | 0.28% | filetypes/batch: 2.68% | 0.998 | 0.995 |
| javascript | 14813 | 79726 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 63.15% | 0 | 55.49% | -7.66% | filetypes/javascript: 66.06% | 0.971 | 0.963 |
| zip | 12676 | 1501 | `general,filetypes/zip` | filetypes/zip: 37.61% | 0 | 29.53% | -8.09% | filetypes/zip: 43.83% | 0.995 | 0.986 |
| xlsx | 7472 | 201 | `general,filegroups/documents,filetypes/xlsx` | filegroups/documents: 31.80% | 0 | 30.37% | -1.43% | filegroups/documents: 31.80% | 0.995 | 0.985 |
| xls | 4671 | 2652 | `general,filegroups/documents,filetypes/xls` | filetypes/xls: 94.90% | 0 | 94.80% | -0.11% | filetypes/xls: 95.14% | 0.998 | 0.998 |
| doc | 3959 | 7 | `general,filegroups/documents` | filegroups/documents: 99.39% | — | — | — | filegroups/documents: 99.42% | — | 1.000 |
| kotlin | 3937 | 6848 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 52.65% | 0 | 50.44% | -2.21% | filegroups/source: 56.95% | 0.953 | 0.954 |
| tar | 2802 | 3332 | `general,filetypes/tar` | filetypes/tar: 83.80% | 0 | 84.19% | 0.39% | filetypes/tar: 85.55% | 0.995 | 0.987 |
| python | 2760 | 26860 | `general,filegroups/scripts,filetypes/python` | filegroups/scripts: 41.23% | 0 | 44.82% | 3.59% | filetypes/python: 61.09% | 0.829 | 0.828 |
| rar | 2569 | 0 | `general` | general: 100.00% | 0 | 15.26% | -84.74% | general: 100.00% | — | — |
| package.json | 2265 | 2939 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 79.60% | 0 | 85.70% | 6.09% | filetypes/package.json: 93.64% | 0.996 | 0.997 |
| c | 2106 | 95882 | `general,filegroups/source,filetypes/c` | filetypes/c: 11.06% | 0 | 9.31% | -1.76% | filetypes/c: 11.73% | 0.254 | 0.255 |
| unknown | 2101 | 6570 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.76% | — | 0.746 |
| shell | 1937 | 7925 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 76.65% | 0 | 69.70% | -6.96% | filetypes/shell: 82.28% | 0.981 | 0.979 |
| vbs | 1450 | 428 | `general,filetypes/vbs` | filetypes/vbs: 20.48% | 0 | 26.34% | 5.86% | general: 34.55% | 0.991 | 0.991 |
| go | 1377 | 15709 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.60% | 0 | 5.81% | 0.21% | filetypes/go: 5.60% | 0.651 | 0.640 |
| zst | 1283 | 2044 | `general` | general: 87.76% | 0 | 18.16% | -69.60% | general: 97.04% | — | 0.997 |
| pkg-info | 1277 | 290 | `general,filetypes/pkg-info` | filetypes/pkg-info: 95.61% | 0 | 95.85% | 0.23% | general: 97.02% | 0.998 | 0.997 |
| png | 1023 | 22239 | `general,filegroups/media,filetypes/png` | filetypes/png: 2.93% | 0 | 2.93% | 0.00% | filegroups/media: 5.77% | 0.122 | 0.120 |
| 7z | 1021 | 14 | `general` | general: 85.50% | 0 | 22.14% | -63.37% | general: 89.13% | — | 0.999 |
| ole | 809 | 792 | `general,filegroups/documents,filetypes/ole` | filetypes/ole: 82.82% | 0 | 82.08% | -0.74% | filegroups/documents: 92.71% | 0.992 | 0.994 |
| rtf | 790 | 54 | `general,filegroups/documents,filetypes/rtf` | filetypes/rtf: 97.34% | 0 | 97.47% | 0.13% | filetypes/rtf: 97.34% | 0.999 | 0.999 |
| php | 708 | 19409 | `general,filegroups/scripts,filetypes/php` | general: 50.28% | 0 | 46.89% | -3.39% | general: 52.68% | 0.787 | 0.782 |
| powershell | 670 | 312 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 44.03% | 0 | 45.22% | 1.19% | filegroups/scripts: 61.94% | 0.990 | 0.985 |
| docx | 568 | 58 | `general,filegroups/documents,filetypes/docx` | filegroups/documents: 83.80% | 0 | 79.05% | -4.75% | filegroups/documents: 85.39% | 0.989 | 0.992 |
| msi | 560 | 15 | `general,filetypes/msi` | filetypes/msi: 81.96% | 0 | 68.39% | -13.57% | filetypes/msi: 81.96% | 0.997 | 0.995 |
| lnk | 543 | 132 | `general,filetypes/lnk` | filetypes/lnk: 82.87% | 0 | 71.09% | -11.79% | filetypes/lnk: 82.87% | 0.991 | 0.989 |
| gz | 530 | 9083 | `general` | general: 31.51% | 0 | 0.00% | -31.51% | general: 36.23% | — | 0.689 |
| xml | 491 | 27109 | `general,filegroups/config,filetypes/xml` | filegroups/config: 14.87% | 0 | 13.65% | -1.22% | filegroups/config: 14.87% | 0.115 | 0.242 |
| jar | 458 | 481 | `general,filetypes/jar` | filetypes/jar: 57.42% | 0 | 55.46% | -1.97% | filetypes/jar: 57.42% | 0.958 | 0.950 |
| python-bytecode | 401 | 23635 | `general,filetypes/python-bytecode` | filetypes/python-bytecode: 86.28% | 0 | 81.80% | -4.49% | filetypes/python-bytecode: 86.28% | 0.882 | 0.883 |
| csharp | 392 | 8373 | `general,filegroups/source,filetypes/csharp` | general: 15.82% | 0 | 14.54% | -1.28% | filegroups/source: 20.41% | 0.426 | 0.426 |
| text | 381 | 13134 | `general,filetypes/text` | general: 6.56% | 0 | 5.51% | -1.05% | general: 8.14% | 0.115 | 0.122 |
| macho | 339 | 1575 | `general,filegroups/native,filetypes/macho` | general: 69.32% | 0 | 74.93% | 5.60% | filetypes/macho: 89.38% | 0.989 | 0.983 |
| java | 307 | 7146 | `general,filegroups/source,filetypes/java` | filetypes/java: 3.91% | 0 | 5.21% | 1.30% | filetypes/java: 8.47% | 0.276 | 0.274 |
| java_class | 238 | 93690 | `general,filegroups/portable,filetypes/java_class` | filegroups/portable: 71.43% | 0 | 63.03% | -8.40% | filegroups/portable: 75.21% | 0.888 | 0.886 |
| rust | 213 | 12612 | `general,filegroups/source,filetypes/rust` | filetypes/rust: 3.76% | 0 | 3.76% | 0.00% | filetypes/rust: 3.76% | 0.056 | 0.058 |
| jpeg | 168 | 3803 | `general,filegroups/media,filetypes/jpeg` | general: 10.71% | 0 | 8.93% | -1.79% | filetypes/jpeg: 13.10% | 0.244 | 0.267 |
| crx | 163 | 10 | `general,filetypes/crx` | filetypes/crx: 98.16% | 0 | 83.44% | -14.72% | filetypes/crx: 98.16% | 0.999 | 0.988 |
| json | 129 | 5421 | `general,filegroups/config` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.027 |
| cab | 99 | 11 | `general` | general: 23.23% | 0 | 0.00% | -23.23% | general: 46.46% | — | 0.978 |
| makefile | 85 | 3834 | `general,filegroups/source,filetypes/makefile` | filetypes/makefile: 1.18% | 0 | 0.00% | -1.18% | filetypes/makefile: 1.18% | 0.058 | 0.052 |
| plist | 77 | 1610 | `general,filegroups/config,filetypes/plist` | filetypes/plist: 2.60% | 0 | 2.60% | 0.00% | filegroups/config: 6.49% | 0.143 | 0.136 |
| pptx | 73 | 22 | `general,filegroups/documents` | filegroups/documents: 6.85% | — | — | — | filegroups/documents: 32.88% | — | 0.826 |
| deb | 50 | 947 | `general,filetypes/deb` | general: 10.00% | 0 | 10.00% | 0.00% | general: 10.00% | 0.140 | 0.129 |
| perl | 39 | 5403 | `general,filegroups/scripts,filetypes/perl` | general: 58.97% | 0 | 51.28% | -7.69% | filetypes/perl: 69.23% | 0.838 | 0.868 |
| chm | 38 | 6 | `general` | general: 86.84% | 0 | 0.00% | -86.84% | general: 86.84% | — | 0.992 |
| data | 37 | 1382 | `general` | general: 21.62% | 0 | 0.00% | -21.62% | general: 32.43% | — | 0.456 |
| applescript | 26 | 36 | `general,filetypes/applescript` | general: 26.92% | 0 | 19.23% | -7.69% | general: 26.92% | 0.538 | 0.538 |
| cargo.toml | 25 | 210 | `general,filetypes/cargo.toml` | general: 32.00% | 0 | 20.00% | -12.00% | general: 32.00% | 0.447 | 0.447 |
| whl | 25 | 109 | `general,filetypes/whl` | general: 52.00% | 0 | 40.00% | -12.00% | general: 52.00% | 0.144 | 0.757 |
| gem | 21 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| ruby | 21 | 3436 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 42.86% | 0 | 28.57% | -14.29% | general: 42.86% | 0.540 | 0.564 |
| asar | 18 | 2 | `general` | general: 94.44% | 0 | 0.00% | -94.44% | general: 94.44% | — | 0.994 |
| dockerfile | 16 | 278 | `general,filetypes/dockerfile` | filetypes/dockerfile: 6.25% | 0 | 6.25% | 0.00% | filetypes/dockerfile: 6.25% | 0.185 | 0.168 |
| groovy | 16 | 860 | `general,filetypes/groovy` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | 0.015 | 0.015 |
| html | 14 | 1393 | `general,filegroups/documents,filetypes/html` | general: 100.00% | 0 | 100.00% | 0.00% | general: 100.00% | 1.000 | 1.000 |
| lua | 13 | 2359 | `general,filegroups/scripts,filetypes/lua` | general: 69.23% | 0 | 46.15% | -23.08% | general: 69.23% | 0.688 | 0.758 |
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
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| doc | `general,filegroups/documents` | 0 | 98.64% | 99.39% | -0.76% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.00% | 31.51% | -31.51% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `general` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.19% | 31.51% | -31.32% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `general` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.19% | 31.51% | -31.32% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| cab | `general` | 0 | 0.00% | 23.23% | -23.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| gem | `general` | 0 | 0.00% | 100.00% | -100.00% |
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
| gz | `general` | 0 | 0.38% | 31.51% | -31.13% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| cab | `general` | 0 | 1.01% | 23.23% | -22.22% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| markdown | `general` | 0 | 0.00% | 100.00% | -100.00% |
| msg | `` | 0 | 0.00% | 100.00% | -100.00% |
| xlsm | `` | 0 | 0.00% | 100.00% | -100.00% |
| xpi | `general` | 0 | 0.00% | 100.00% | -100.00% |
| asar | `` | 0 | 0.00% | 94.44% | -94.44% |
| gem | `general` | 0 | 9.52% | 100.00% | -90.48% |
| chm | `` | 0 | 0.00% | 86.84% | -86.84% |
| bz2 | `general` | 0 | 0.00% | 66.67% | -66.67% |
| desktop-entry | `general` | 0 | 0.00% | 66.67% | -66.67% |
| rar | `general` | 0 | 36.36% | 100.00% | -63.64% |
| 7z | `general` | 0 | 41.43% | 85.50% | -44.07% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| gz | `general` | 0 | 0.57% | 31.51% | -30.94% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| zst | `general` | 0 | 57.91% | 87.76% | -29.85% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| cab | `general` | 0 | 1.01% | 23.23% | -22.22% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| gem | `general` | 0 | 42.86% | 100.00% | -57.14% |
| objc | `general` | 0 | 20.00% | 60.00% | -40.00% |
| 7z | `general` | 0 | 50.15% | 85.50% | -35.36% |
| xz | `general` | 0 | 0.00% | 30.00% | -30.00% |
| gz | `general` | 0 | 5.28% | 31.51% | -26.23% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| zst | `general` | 0 | 65.94% | 87.76% | -21.82% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| cab | `general` | 0 | 3.03% | 23.23% | -20.20% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 0 | 63.03% | 71.43% | -8.40% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 55.49% | 63.15% | -7.66% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| c | `general,filegroups/source,filetypes/c` | 0 | 9.31% | 11.06% | -1.76% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| 7z | `general` | 0 | 59.55% | 85.50% | -25.95% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| xz | `general` | 0 | 10.00% | 30.00% | -20.00% |
| gz | `general` | 0 | 13.40% | 31.51% | -18.11% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| cab | `general` | 0 | 13.13% | 23.23% | -10.10% |
| gem | `general` | 0 | 90.48% | 100.00% | -9.52% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| zst | `general` | 0 | 82.39% | 87.76% | -5.38% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| 7z | `general` | 0 | 63.08% | 85.50% | -22.43% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| gz | `general` | 0 | 16.98% | 31.51% | -14.53% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| gem | `general` | 0 | 95.24% | 100.00% | -4.76% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| cab | `general` | 0 | 19.19% | 23.23% | -4.04% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| zst | `general` | 0 | 85.42% | 87.76% | -2.34% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| 7z | `general` | 0 | 64.45% | 85.50% | -21.06% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| gz | `general` | 0 | 18.68% | 31.51% | -12.83% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| gem | `general` | 0 | 95.24% | 100.00% | -4.76% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| zst | `general` | 0 | 86.52% | 87.76% | -1.25% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| cab | `general` | 0 | 22.22% | 23.23% | -1.01% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| python | `general,filegroups/scripts,filetypes/python` | 0 | 44.82% | 41.23% | 3.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| data | `general` | 0 | 0.00% | 21.62% | -21.62% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| 7z | `general` | 0 | 66.11% | 85.50% | -19.39% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| gz | `general` | 0 | 19.62% | 31.51% | -11.89% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| gem | `general` | 0 | 95.24% | 100.00% | -4.76% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 81.80% | 86.28% | -4.49% |
| php | `general,filegroups/scripts,filetypes/php` | 0 | 46.89% | 50.28% | -3.39% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 59.64% | 61.09% | -1.45% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 0 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 0 | 2.93% | 2.93% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 92.17% | 91.84% | 0.32% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 64.10% | 62.52% | 1.59% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 2.70% | 21.62% | -18.92% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| gz | `general` | 0 | 20.38% | 31.51% | -11.13% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| gem | `general` | 0 | 95.24% | 100.00% | -4.76% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 59.64% | 61.09% | -1.45% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 85.79% | 86.28% | -0.50% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 2 | 49.15% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 1 | 5.77% | 5.77% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.15% | 97.13% | 0.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.81% | 5.60% | 0.21% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| pe | `filegroups/native,filetypes/pe` | 1 | 70.02% | 64.40% | 5.62% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |

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
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 46.15% | 69.23% | -23.08% |
| pyproject.toml | `general` | 0 | 0.00% | 20.00% | -20.00% |
| zig | `general` | 0 | 0.00% | 20.00% | -20.00% |
| data | `general` | 0 | 5.41% | 21.62% | -16.22% |
| crx | `general,filetypes/crx` | 0 | 83.44% | 98.16% | -14.72% |
| clojure | `general,filetypes/clojure` | 0 | 42.86% | 57.14% | -14.29% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 28.57% | 42.86% | -14.29% |
| msi | `general,filetypes/msi` | 0 | 68.39% | 81.96% | -13.57% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 20.00% | 32.00% | -12.00% |
| whl | `general` | 0 | 40.00% | 52.00% | -12.00% |
| lnk | `general,filetypes/lnk` | 0 | 71.09% | 82.87% | -11.79% |
| gz | `general` | 0 | 21.13% | 31.51% | -10.38% |
| zip | `general,filetypes/zip` | 0 | 29.53% | 37.61% | -8.09% |
| perl | `general,filegroups/scripts,filetypes/perl` | 0 | 51.28% | 58.97% | -7.69% |
| applescript | `general` | 0 | 19.23% | 26.92% | -7.69% |
| shell | `general,filegroups/scripts,filetypes/shell` | 0 | 69.70% | 76.65% | -6.96% |
| gem | `general` | 0 | 95.24% | 100.00% | -4.76% |
| docx | `general,filegroups/documents,filetypes/docx` | 0 | 79.05% | 83.80% | -4.75% |
| java_class | `general,filegroups/portable,filetypes/java_class` | 1 | 71.85% | 75.21% | -3.36% |
| kotlin | `general,filegroups/source` | 0 | 50.44% | 52.65% | -2.21% |
| jar | `filetypes/jar` | 0 | 55.46% | 57.42% | -1.97% |
| jpeg | `filegroups/media,filetypes/jpeg` | 0 | 8.93% | 10.71% | -1.79% |
| python | `general,filegroups/scripts,filetypes/python` | 1 | 59.64% | 61.09% | -1.45% |
| xlsx | `filegroups/documents,filetypes/xlsx` | 0 | 30.37% | 31.80% | -1.43% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 14.54% | 15.82% | -1.28% |
| xml | `general,filegroups/config,filetypes/xml` | 0 | 13.65% | 14.87% | -1.22% |
| makefile | `general,filetypes/makefile` | 0 | 0.00% | 1.18% | -1.18% |
| text | `general,filetypes/text` | 0 | 5.51% | 6.56% | -1.05% |
| ole | `filegroups/documents,filetypes/ole` | 0 | 82.08% | 82.82% | -0.74% |
| python-bytecode | `filetypes/python-bytecode` | 0 | 85.79% | 86.28% | -0.50% |
| c | `general,filegroups/source,filetypes/c` | 0 | 10.87% | 11.06% | -0.19% |
| xls | `filegroups/documents,filetypes/xls` | 0 | 94.80% | 94.90% | -0.11% |
| pdf | `general,filegroups/documents,filetypes/pdf` | 0 | 4.08% | 4.10% | -0.02% |
| chrome-manifest | `general,filetypes/chrome-manifest` | 0 | 37.50% | 37.50% | 0.00% |
| composerjson | `general` | 0 | 0.00% | 0.00% | 0.00% |
| deb | `filetypes/deb` | 0 | 10.00% | 10.00% | 0.00% |
| dockerfile | `general,filetypes/dockerfile` | 0 | 6.25% | 6.25% | 0.00% |
| github-actions | `general` | 0 | 0.00% | 0.00% | 0.00% |
| groovy | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| json | `general,filegroups/config` | 1 | 0.00% | 0.00% | 0.00% |
| ooxml | `general` | 0 | 0.00% | 0.00% | 0.00% |
| package-lock.json | `general` | 0 | 0.00% | 0.00% | 0.00% |
| php | `general,filegroups/scripts,filetypes/php` | 2 | 49.15% | — | — |
| pkg | `` | 0 | 0.00% | 0.00% | 0.00% |
| plist | `filegroups/config,filetypes/plist` | 0 | 2.60% | 2.60% | 0.00% |
| png | `filetypes/png` | 1 | 5.77% | 5.77% | 0.00% |
| rust | `general,filegroups/source,filetypes/rust` | 0 | 3.76% | 3.76% | 0.00% |
| swift | `general,filegroups/source` | 0 | 0.00% | 0.00% | 0.00% |
| systemd | `general` | 0 | 0.00% | 0.00% | 0.00% |
| unknown | `general` | 0 | 0.00% | 0.00% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 1 | 97.15% | 97.13% | 0.02% |
| javascript | `general,filegroups/scripts,filetypes/javascript` | 0 | 63.20% | 63.15% | 0.05% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.47% | 97.34% | 0.13% |
| pkg-info | `general,filetypes/pkg-info` | 0 | 95.85% | 95.61% | 0.23% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 2.22% | 1.94% | 0.28% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.95% | 5.60% | 0.36% |
| tar | `general,filetypes/tar` | 0 | 84.19% | 83.80% | 0.39% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 45.22% | 44.03% | 1.19% |
| java | `general,filegroups/source,filetypes/java` | 0 | 5.21% | 3.91% | 1.30% |
| macho | `general,filegroups/native,filetypes/macho` | 0 | 74.93% | 69.32% | 5.60% |
| pe | `filegroups/native,filetypes/pe` | 1 | 70.02% | 64.40% | 5.62% |
| vbs | `general,filetypes/vbs` | 0 | 26.34% | 20.48% | 5.86% |
| package.json | `general,filegroups/config,filetypes/package.json` | 0 | 85.70% | 79.60% | 6.09% |
