# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 1553012 (325391 malware, 1227621 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 169093 | 23240 | `general,filegroups/native,filetypes/pe` | filegroups/native: 52.11% | 0 | 46.68% | -5.43% | filegroups/native: 55.01% | 1.000 | 0.975 |
| elf | 23575 | 47787 | `general,filegroups/native,filetypes/elf` | filegroups/native: 89.55% | 0 | 89.75% | 0.20% | filetypes/elf: 92.73% | 0.999 | 0.978 |
| pdf | 22517 | 3412 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 73.32% | 0 | 73.28% | -0.04% | filetypes/pdf: 73.99% | 0.993 | 0.984 |
| batch | 22133 | 951 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 7.92% | 0 | 8.38% | 0.46% | filegroups/scripts: 8.83% | 0.991 | 0.969 |
| javascript | 16603 | 143012 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 41.38% | 0 | 35.54% | -5.85% | filetypes/javascript: 43.03% | 0.921 | 0.692 |
| zip | 12956 | 2452 | `general,filetypes/zip` | filetypes/zip: 36.26% | 0 | 36.26% | 0.00% | filetypes/zip: 38.82% | 0.955 | 0.853 |
| ole_doc | 10602 | 3864 | `general,filetypes/ole_doc` | filetypes/ole_doc: 88.79% | 0 | 81.63% | -7.17% | filetypes/ole_doc: 91.05% | 0.995 | 0.990 |
| ooxml | 8556 | 350 | `general,filetypes/ooxml` | filetypes/ooxml: 15.96% | 0 | 15.95% | -0.00% | filetypes/ooxml: 34.38% | 0.989 | 0.966 |
| kotlin | 3903 | 9520 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 55.34% | 0 | 55.47% | 0.13% | filetypes/kotlin: 57.49% | 0.910 | 0.872 |
| python | 2846 | 60048 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 50.56% | 0 | 51.19% | 0.63% | filetypes/python: 50.60% | 0.802 | 0.567 |
| tar | 2802 | 6748 | `general,filetypes/tar` | filetypes/tar: 82.62% | 0 | 82.48% | -0.15% | filetypes/tar: 83.30% | 0.991 | 0.556 |
| rar | 2719 | 2 | `general` | general: 80.18% | 0 | 55.90% | -24.27% | general: 99.08% | — | 1.000 |
| package.json | 2478 | 4914 | `general,filegroups/config,filetypes/package.json` | filetypes/package.json: 72.28% | 0 | 75.99% | 3.71% | filegroups/config: 90.40% | 0.996 | 0.985 |
| shell | 2300 | 15779 | `general,filegroups/scripts,filetypes/shell` | filegroups/scripts: 37.22% | 0 | 46.22% | 9.00% | filegroups/scripts: 43.70% | 0.940 | 0.626 |
| c | 2298 | 166076 | `general,filegroups/source,filetypes/c` | filegroups/source: 7.79% | 0 | 7.14% | -0.65% | filegroups/source: 7.96% | 0.014 | 0.067 |
| go | 2113 | 26188 | `general,filegroups/source,filetypes/go` | filetypes/go: 5.21% | 0 | 4.40% | -0.80% | filegroups/source: 7.29% | 0.250 | 0.157 |
| unknown | 1787 | 5941 | `general` | general: 0.00% | — | — | — | general: 0.17% | — | 0.758 |
| vbs | 1556 | 445 | `general,filetypes/vbs` | filetypes/vbs: 28.98% | 0 | 24.55% | -4.43% | filetypes/vbs: 35.80% | 0.986 | 0.963 |
| zst | 1283 | 19125 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.877 |
| pkg_info | 1270 | 1299 | `general,filetypes/pkg_info` | filetypes/pkg_info: 96.14% | 0 | 96.06% | -0.08% | filetypes/pkg_info: 96.30% | 0.985 | 0.990 |
| 7z | 1163 | 17 | `general` | general: 16.34% | — | — | — | general: 20.81% | — | 0.994 |
| png | 1091 | 38786 | `general,filegroups/media,filetypes/png` | filetypes/png: 5.41% | 0 | 1.19% | -4.22% | filetypes/png: 5.50% | 0.098 | 0.107 |
| rtf | 830 | 94 | `general,filegroups/documents,filetypes/rtf` | filegroups/documents: 97.23% | 0 | 97.23% | 0.00% | filegroups/documents: 97.23% | 0.999 | 0.999 |
| php | 797 | 66969 | `general,filegroups/scripts,filetypes/php` | filegroups/scripts: 42.28% | 0 | 33.63% | -8.66% | filegroups/scripts: 43.41% | 0.694 | 0.365 |
| powershell | 721 | 565 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 42.72% | 0 | 41.61% | -1.11% | filegroups/scripts: 46.60% | 0.965 | 0.925 |
| lnk | 568 | 132 | `general,filetypes/lnk` | filetypes/lnk: 73.77% | 0 | 61.27% | -12.50% | filetypes/lnk: 73.77% | 0.992 | 0.986 |
| gz | 560 | 16710 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.359 |
| xml | 505 | 52291 | `general,filegroups/config,filetypes/xml` | filegroups/config: 2.18% | 0 | 2.38% | 0.20% | filegroups/config: 7.72% | 0.044 | 0.053 |
| text | 498 | 28597 | `general,filetypes/text` | filetypes/text: 4.02% | 0 | 2.21% | -1.81% | filetypes/text: 5.82% | 0.089 | 0.067 |
| jar | 491 | 1480 | `general,filetypes/jar` | filetypes/jar: 66.19% | 0 | 56.42% | -9.78% | filetypes/jar: 67.21% | 0.922 | 0.651 |
| csharp | 466 | 11018 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 13.95% | 0 | 15.67% | 1.72% | filegroups/source: 18.03% | 0.377 | 0.250 |
| python_bytecode | 461 | 71510 | `general,filetypes/python_bytecode` | filetypes/python_bytecode: 57.70% | 0 | 57.70% | 0.00% | filetypes/python_bytecode: 67.90% | 0.764 | 0.653 |
| java | 459 | 19246 | `general,filegroups/source,filetypes/java` | filegroups/source: 0.65% | 0 | 0.65% | 0.00% | filegroups/source: 0.65% | 0.028 | 0.030 |
| macho | 356 | 2572 | `general,filegroups/native,filetypes/macho` | filetypes/macho: 50.84% | 0 | 49.72% | -1.12% | filetypes/macho: 60.67% | 0.963 | 0.329 |
| whl | 356 | 665 | `general,filetypes/whl` | filetypes/whl: 39.89% | 0 | 39.89% | 0.00% | filetypes/whl: 39.89% | 0.936 | 0.678 |
| npm | 318 | 390 | `general,filetypes/npm` | filetypes/npm: 48.74% | 0 | 44.97% | -3.77% | filetypes/npm: 59.12% | 0.930 | 0.735 |
| java_class | 274 | 184533 | `general,filegroups/portable,filetypes/java_class` | general: 2.19% | 0 | 2.19% | 0.00% | general: 2.55% | 0.001 | 0.448 |
| rust | 257 | 39565 | `general,filegroups/source,filetypes/rust` | filegroups/source: 1.95% | 0 | 1.95% | 0.00% | filegroups/source: 3.89% | 0.004 | 0.017 |
| apk_android | 245 | 15 | `general` | general: 0.41% | 0 | 0.00% | -0.41% | general: 0.41% | — | 0.901 |
| crx | 209 | 111 | `general,filetypes/crx` | filetypes/crx: 7.66% | 0 | 11.00% | 3.35% | filetypes/crx: 87.56% | 0.986 | 0.889 |
| json | 199 | 17425 | `general,filegroups/config,filetypes/json` | filegroups/config: 7.04% | 0 | 7.04% | 0.00% | filegroups/config: 7.04% | 0.106 | 0.081 |
| jpeg | 180 | 5384 | `general,filegroups/media,filetypes/jpeg` | general: 2.78% | 0 | 3.89% | 1.11% | filetypes/jpeg: 13.33% | 0.198 | 0.213 |
| cab | 106 | 10 | `general` | general: 75.47% | 0 | 50.94% | -24.53% | general: 88.68% | — | 0.993 |
| makefile | 102 | 7366 | `general,filegroups/source,filetypes/makefile` | filegroups/source: 0.98% | 0 | 0.98% | 0.00% | filegroups/source: 0.98% | 0.020 | 0.026 |
| plist | 84 | 11901 | `general,filegroups/config,filetypes/plist` | filegroups/config: 3.57% | 0 | 3.57% | 0.00% | filegroups/config: 3.57% | 0.058 | 0.036 |
| gem | 82 | 225 | `general,filetypes/gem` | filetypes/gem: 98.78% | 0 | 96.34% | -2.44% | filetypes/gem: 98.78% | 0.994 | 0.625 |
| data | 78 | 7285 | `general` | general: 3.85% | — | — | — | general: 3.85% | — | 0.236 |
| deb | 55 | 2258 | `general,filetypes/deb` | general: 0.00% | — | — | — | general: 0.00% | 0.069 | 0.067 |
| cargo.toml | 50 | 790 | `general,filetypes/cargo.toml` | filetypes/cargo.toml: 14.00% | 0 | 12.00% | -2.00% | general: 28.00% | 0.605 | 0.391 |
| perl | 46 | 8052 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 67.39% | 0 | 60.87% | -6.52% | filetypes/perl: 67.39% | 0.820 | 0.281 |
| registry | 42 | 4160 | `general,filetypes/registry` | filetypes/registry: 42.86% | 0 | 42.86% | 0.00% | general: 42.86% | 0.786 | 0.777 |
| chm | 40 | 5 | `general` | general: 85.00% | 0 | 47.50% | -37.50% | general: 85.00% | — | 0.986 |
| ruby | 35 | 20712 | `general,filegroups/scripts,filetypes/ruby` | filetypes/ruby: 22.86% | 0 | 8.57% | -14.29% | filetypes/ruby: 25.71% | 0.362 | 0.233 |
| html | 31 | 2010 | `general,filegroups/documents,filetypes/html` | filegroups/documents: 100.00% | 0 | 100.00% | 0.00% | filegroups/documents: 100.00% | 1.000 | 1.000 |
| dockerfile | 25 | 517 | `general,filetypes/dockerfile` | general: 0.00% | — | — | — | general: 8.00% | 0.118 | 0.154 |
| asar | 21 | 3 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.722 |
| groovy | 17 | 1248 | `general,filetypes/groovy` | general: 11.76% | 0 | 11.76% | 0.00% | general: 17.65% | 0.187 | 0.218 |
| go.mod | 16 | 50 | `general` | general: 18.75% | 0 | 6.25% | -12.50% | general: 18.75% | — | 0.482 |
| lua | 14 | 3185 | `general,filegroups/scripts,filetypes/lua` | filegroups/scripts: 71.43% | 0 | 57.14% | -14.29% | filegroups/scripts: 71.43% | 0.838 | 0.346 |
| package-lock.json | 14 | 154 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.090 |
| xz | 14 | 5458 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.071 |
| chrome_manifest | 12 | 117 | `general,filetypes/chrome_manifest` | general: 50.00% | 0 | 50.00% | 0.00% | filetypes/chrome_manifest: 66.67% | 0.851 | 0.708 |
| markdown | 12 | 9530 | `general,filetypes/markdown` | general: 25.00% | 0 | 25.00% | 0.00% | general: 41.67% | 0.676 | 0.676 |
| applescript | 9 | 46 | `general,filetypes/applescript` | general: 88.89% | 0 | 88.89% | 0.00% | general: 88.89% | 0.908 | 0.908 |
| cargo.lock | 9 | 84 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.104 |
| github_actions | 8 | 1976 | `general,filetypes/github_actions` | general: 0.00% | — | — | — | general: 0.00% | 0.068 | 0.089 |
| swift | 8 | 4583 | `general,filegroups/source,filetypes/swift` | filegroups/source: 25.00% | 0 | 25.00% | 0.00% | filegroups/source: 25.00% | 0.068 | 0.084 |
| clojure | 7 | 977 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 57.14% | 0.00% | filetypes/clojure: 57.14% | 0.724 | 0.608 |
| pyproject.toml | 7 | 32 | `general` | general: 14.29% | 0 | 0.00% | -14.29% | general: 14.29% | — | 0.295 |
| vsix | 6 | 153 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.039 |
| zig | 6 | 160 | `general` | general: 0.00% | — | — | — | general: 16.67% | — | 0.159 |
| go.sum | 5 | 39 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.766 |
| nupkg | 5 | 269 | `general,filetypes/nupkg` | general: 0.00% | — | — | — | filetypes/nupkg: 20.00% | 0.303 | 0.229 |
| objective_c | 5 | 3188 | `general,filetypes/objective_c` | general: 0.00% | — | — | — | general: 0.00% | 0.029 | 0.064 |
| bz2 | 4 | 1648 | `general` | general: 50.00% | — | — | — | general: 100.00% | — | 0.887 |
| crate | 4 | 629 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.167 |
| composer.json | 3 | 254 | `general` | general: 33.33% | 0 | 33.33% | 0.00% | general: 33.33% | — | 0.348 |
| desktop_entry | 3 | 623 | `general` | general: 33.33% | 0 | 33.33% | 0.00% | general: 33.33% | — | 0.358 |
| dmg | 2 | 17 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.350 |
| svg | 2 | 16371 | `general,filegroups/media` | general: 0.00% | — | — | — | general: 0.00% | — | 0.000 |
| systemd_service | 2 | 382 | `general` | general: 50.00% | 0 | 0.00% | -50.00% | general: 50.00% | — | 0.503 |
| composer.lock | 1 | 20 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.048 |
| conda | 1 | 170 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.036 |
| gyp | 1 | 60 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.053 |
| odf | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| pkg_macos | 1 | 9 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.125 |
| xpi | 1 | 35 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.250 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| chm | `general` | 0 | 40.00% | 85.00% | -45.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 53.11% | 80.18% | -27.07% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 45.00% | 85.00% | -40.00% |
| rar | `general` | 0 | 53.11% | 80.18% | -27.07% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 45.00% | 85.00% | -40.00% |
| rar | `general` | 0 | 53.14% | 80.18% | -27.03% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 45.00% | 85.00% | -40.00% |
| rar | `general` | 0 | 53.18% | 80.18% | -27.00% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 45.00% | 85.00% | -40.00% |
| rar | `general` | 0 | 53.22% | 80.18% | -26.96% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| rar | `general` | 0 | 53.29% | 80.18% | -26.88% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| rar | `general` | 0 | 53.51% | 80.18% | -26.66% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| rar | `general` | 0 | 53.73% | 80.18% | -26.44% |
| cab | `general` | 0 | 50.00% | 75.47% | -25.47% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| rar | `general` | 0 | 55.24% | 80.18% | -24.94% |
| cab | `general` | 0 | 50.94% | 75.47% | -24.53% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| rar | `general` | 0 | 55.57% | 80.18% | -24.60% |
| cab | `general` | 0 | 50.94% | 75.47% | -24.53% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 50.94% | 75.47% | -24.53% |
| rar | `general` | 0 | 55.90% | 80.18% | -24.27% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| systemd_service | `general` | 0 | 0.00% | 50.00% | -50.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 59.76% | 80.18% | -20.41% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.21% | 80.18% | -19.97% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.32% | 80.18% | -19.86% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.76% | 80.18% | -19.42% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.76% | 80.18% | -19.42% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.90% | 80.18% | -19.27% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 47.50% | 85.00% | -37.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 60.98% | 80.18% | -19.20% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 52.50% | 85.00% | -32.50% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 61.13% | 80.18% | -19.05% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 51.89% | 75.47% | -23.58% |
| rar | `general` | 0 | 63.15% | 80.18% | -17.03% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| chm | `general` | 0 | 82.50% | 85.00% | -2.50% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 53.77% | 75.47% | -21.70% |
| rar | `general` | 0 | 64.99% | 80.18% | -15.19% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| javascript | `general,filetypes/javascript` | 0 | 35.54% | 41.38% | -5.85% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| c | `filegroups/source,filetypes/c` | 0 | 7.14% | 7.79% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.06% | 80.18% | -15.12% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| php | `filegroups/scripts,filetypes/php` | 0 | 33.63% | 42.28% | -8.66% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| png | `general,filegroups/media` | 0 | 1.19% | 5.41% | -4.22% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 57.70% | 57.70% | 0.00% |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| xml | `general,filegroups/config` | 0 | 2.38% | 2.18% | 0.20% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| python | `filegroups/scripts,filetypes/python` | 0 | 51.19% | 50.56% | 0.63% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.06% | 80.18% | -15.12% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| php | `filegroups/scripts,filetypes/php` | 1 | 40.15% | 43.41% | -3.26% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 67.25% | 67.90% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| xml | `filegroups/config` | 1 | 7.33% | 7.72% | -0.40% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| png | `general,filetypes/png` | 1 | 5.50% | 5.50% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 2 | 52.99% | — | — |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 89.75% | 89.55% | 0.20% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.10% | 80.18% | -15.08% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| php | `filegroups/scripts,filetypes/php` | 1 | 40.15% | 43.41% | -3.26% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| text | `general,filetypes/text` | 0 | 2.21% | 4.02% | -1.81% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| go | `filegroups/source,filetypes/go` | 0 | 4.40% | 5.21% | -0.80% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 67.25% | 67.90% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| xml | `filegroups/config` | 1 | 7.33% | 7.72% | -0.40% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 95.41% | — | — |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| png | `general,filetypes/png` | 1 | 5.50% | 5.50% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 2 | 52.99% | — | — |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| ruby | `filegroups/scripts` | 0 | 8.57% | 22.86% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 46.68% | 52.11% | -5.43% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| php | `filegroups/scripts,filetypes/php` | 1 | 40.15% | 43.41% | -3.26% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 67.25% | 67.90% | -0.65% |
| go | `filegroups/source,filetypes/go` | 0 | 4.69% | 5.21% | -0.52% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| text | `general,filetypes/text` | 1 | 5.42% | 5.82% | -0.40% |
| xml | `filegroups/config` | 1 | 7.33% | 7.72% | -0.40% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 95.41% | — | — |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source` | 0 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| png | `general,filetypes/png` | 1 | 5.50% | 5.50% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 2 | 52.99% | — | — |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 17.14% | 22.86% | -5.71% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| php | `filegroups/scripts,filetypes/php` | 1 | 40.15% | 43.41% | -3.26% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 67.25% | 67.90% | -0.65% |
| go | `filegroups/source,filetypes/go` | 0 | 4.69% | 5.21% | -0.52% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| text | `general,filetypes/text` | 1 | 5.42% | 5.82% | -0.40% |
| xml | `filegroups/config` | 1 | 7.33% | 7.72% | -0.40% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 95.41% | — | — |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source,filetypes/java` | 1 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filegroups/config` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 57.17% | — | — |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| png | `general,filetypes/png` | 1 | 5.50% | 5.50% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 2 | 52.99% | — | — |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 46.22% | 37.22% | 9.00% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| cab | `general` | 0 | 55.66% | 75.47% | -19.81% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lua | `general,filegroups/scripts,filetypes/lua` | 0 | 57.14% | 71.43% | -14.29% |
| lnk | `general,filetypes/lnk` | 0 | 61.27% | 73.77% | -12.50% |
| jar | `general,filetypes/jar` | 0 | 56.42% | 66.19% | -9.78% |
| ole_doc | `filetypes/ole_doc` | 0 | 81.63% | 88.79% | -7.17% |
| perl | `filegroups/scripts,filetypes/perl` | 0 | 60.87% | 67.39% | -6.52% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 17.14% | 22.86% | -5.71% |
| vbs | `general,filetypes/vbs` | 0 | 24.55% | 28.98% | -4.43% |
| npm | `filetypes/npm` | 0 | 44.97% | 48.74% | -3.77% |
| php | `filegroups/scripts,filetypes/php` | 1 | 40.15% | 43.41% | -3.26% |
| gem | `filetypes/gem` | 0 | 96.34% | 98.78% | -2.44% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 12.00% | 14.00% | -2.00% |
| macho | `filegroups/native,filetypes/macho` | 0 | 49.72% | 50.84% | -1.12% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 41.61% | 42.72% | -1.11% |
| shell | `filegroups/scripts,filetypes/shell` | 3 | 59.65% | 60.65% | -1.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 67.25% | 67.90% | -0.65% |
| go | `filegroups/source,filetypes/go` | 0 | 4.69% | 5.21% | -0.52% |
| apk_android | `` | 0 | 0.00% | 0.41% | -0.41% |
| text | `general,filetypes/text` | 1 | 5.42% | 5.82% | -0.40% |
| xml | `filegroups/config` | 1 | 7.33% | 7.72% | -0.40% |
| tar | `filetypes/tar` | 0 | 82.48% | 82.62% | -0.15% |
| c | `filegroups/source,filetypes/c` | 1 | 7.83% | 7.96% | -0.13% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 96.14% | -0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.28% | 73.32% | -0.04% |
| ooxml | `filetypes/ooxml` | 0 | 15.95% | 15.96% | -0.00% |
| applescript | `filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| chm | `general` | 0 | 85.00% | 85.00% | 0.00% |
| chrome_manifest | `general,filetypes/chrome_manifest` | 0 | 50.00% | 50.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 33.33% | 33.33% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `general,filegroups/native,filetypes/elf` | 2 | 95.41% | — | — |
| groovy | `general` | 0 | 11.76% | 11.76% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `filegroups/documents,filetypes/html` | 0 | 100.00% | 100.00% | 0.00% |
| java | `filegroups/source,filetypes/java` | 1 | 0.65% | 0.65% | 0.00% |
| java_class | `general` | 0 | 2.19% | 2.19% | 0.00% |
| javascript | `general,filetypes/javascript` | 2 | 44.53% | — | — |
| json | `filetypes/json` | 0 | 7.04% | 7.04% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 25.00% | 25.00% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 57.17% | — | — |
| plist | `filegroups/config` | 0 | 3.57% | 3.57% | 0.00% |
| png | `general,filetypes/png` | 1 | 5.50% | 5.50% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python | `filegroups/scripts,filetypes/python` | 2 | 52.99% | — | — |
| registry | `filetypes/registry` | 0 | 42.86% | 42.86% | 0.00% |
| rtf | `filegroups/documents,filetypes/rtf` | 0 | 97.23% | 97.23% | 0.00% |
| rust | `filegroups/source` | 0 | 1.95% | 1.95% | 0.00% |
| swift | `filegroups/source` | 0 | 25.00% | 25.00% | 0.00% |
| unknown | `general` | 1 | 0.17% | 0.17% | 0.00% |
| whl | `filetypes/whl` | 0 | 39.89% | 39.89% | 0.00% |
| zip | `filetypes/zip` | 0 | 36.26% | 36.26% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 55.47% | 55.34% | 0.13% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 8.38% | 7.92% | 0.46% |
| jpeg | `general,filegroups/media,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 15.67% | 13.95% | 1.72% |
| crx | `general,filetypes/crx` | 0 | 11.00% | 7.66% | 3.35% |
| package.json | `filegroups/config,filetypes/package.json` | 0 | 75.99% | 72.28% | 3.71% |
