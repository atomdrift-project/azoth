# Azoth Route Policy Eval

- Partition: `test`
- Score table: `out/models/azoth/score_table.npz`
- Route policies: `out/models/azoth/route_policies.json`
- Rows in partition: 1608866 (326316 malware, 1282550 benign)

## Per-filetype: single-route Pareto vs deployed OR-rule

Columns: best single route's recall at FP budget, vs deployed OR-rule's recall at its **own** observed FP count. A negative delta means the ensemble loses to the best single route AT THE OR's actual operating point — the headline regression.

| Filetype | Mal | Ben | Routes | Best route@0FP | OR FP | OR recall | Δ vs best@OR-FP | Best route@1FP | Spec PR-AUC | Max-rule PR-AUC |
| --- | ---: | ---: | --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| pe | 169146 | 23659 | `general,filegroups/native,filetypes/pe` | filegroups/native: 39.42% | 0 | 42.77% | 3.35% | filegroups/native: 54.12% | 1.000 | 0.974 |
| elf | 23668 | 49142 | `general,filegroups/native,filetypes/elf` | filegroups/native: 88.28% | 0 | 90.51% | 2.24% | filetypes/elf: 91.03% | 0.999 | 0.976 |
| pdf | 22517 | 3421 | `general,filegroups/documents,filetypes/pdf` | filetypes/pdf: 73.26% | 0 | 73.54% | 0.28% | filetypes/pdf: 74.66% | 0.994 | 0.982 |
| batch | 22134 | 939 | `general,filegroups/scripts,filetypes/batch` | filegroups/scripts: 15.96% | 0 | 16.04% | 0.08% | filegroups/scripts: 16.07% | 0.990 | 0.973 |
| javascript | 16728 | 150115 | `general,filegroups/scripts,filetypes/javascript` | filetypes/javascript: 42.11% | 0 | 33.09% | -9.02% | filetypes/javascript: 48.42% | 0.913 | 0.688 |
| zip | 13110 | 2708 | `general,filetypes/zip` | filetypes/zip: 32.18% | 0 | 22.71% | -9.47% | filetypes/zip: 41.37% | 0.951 | 0.845 |
| ole_doc | 10603 | 3886 | `general,filetypes/ole_doc` | filetypes/ole_doc: 88.92% | 0 | 85.35% | -3.57% | filetypes/ole_doc: 91.76% | 0.995 | 0.990 |
| ooxml | 8558 | 351 | `general,filetypes/ooxml` | filetypes/ooxml: 23.25% | 0 | 23.24% | -0.01% | filetypes/ooxml: 34.35% | 0.990 | 0.964 |
| kotlin | 3891 | 9206 | `general,filegroups/source,filetypes/kotlin` | filetypes/kotlin: 57.52% | 0 | 57.57% | 0.05% | filetypes/kotlin: 57.93% | 0.959 | 0.871 |
| tar | 2951 | 7087 | `general,filetypes/tar` | filetypes/tar: 78.66% | 0 | 78.45% | -0.21% | filetypes/tar: 79.44% | 0.983 | 0.588 |
| python | 2851 | 61657 | `general,filegroups/scripts,filetypes/python` | filetypes/python: 52.05% | 0 | 46.51% | -5.54% | filetypes/python: 54.26% | 0.798 | 0.585 |
| rar | 2719 | 2 | `general` | general: 80.18% | 0 | 55.94% | -24.24% | general: 80.18% | — | 1.000 |
| package.json | 2490 | 5361 | `general,filegroups/config,filetypes/package.json` | filegroups/config: 83.61% | 0 | 83.61% | 0.00% | filegroups/config: 90.64% | 0.991 | 0.977 |
| shell | 2305 | 16083 | `general,filegroups/scripts,filetypes/shell` | filetypes/shell: 45.51% | 0 | 53.36% | 7.85% | filegroups/scripts: 54.62% | 0.938 | 0.640 |
| c | 2297 | 168691 | `general,filegroups/source,filetypes/c` | filegroups/source: 10.19% | 0 | 9.53% | -0.65% | filegroups/source: 13.37% | 0.026 | 0.080 |
| go | 2113 | 26285 | `general,filegroups/source,filetypes/go` | filegroups/source: 8.94% | 0 | 5.02% | -3.93% | filetypes/go: 10.55% | 0.241 | 0.166 |
| unknown | 1902 | 5512 | `general` | general: 0.00% | — | — | — | general: 0.16% | — | 0.731 |
| vbs | 1560 | 458 | `general,filetypes/vbs` | filetypes/vbs: 52.50% | 0 | 43.40% | -9.10% | filetypes/vbs: 71.73% | 0.994 | 0.949 |
| zst | 1288 | 19141 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.876 |
| pkg_info | 1270 | 1392 | `general,filetypes/pkg_info` | filetypes/pkg_info: 95.75% | 0 | 96.06% | 0.31% | filetypes/pkg_info: 96.22% | 0.989 | 0.990 |
| 7z | 1163 | 19 | `general` | general: 16.42% | — | — | — | general: 20.89% | — | 0.994 |
| png | 1091 | 45357 | `general,filegroups/media,filetypes/png` | general: 0.37% | 0 | 0.37% | 0.00% | general: 0.37% | 0.089 | 0.094 |
| rtf | 830 | 94 | `general,filegroups/documents,filetypes/rtf` | filegroups/documents: 97.35% | 0 | 97.23% | -0.12% | filegroups/documents: 97.35% | 0.999 | 0.999 |
| php | 798 | 67356 | `general,filegroups/scripts,filetypes/php` | filetypes/php: 49.75% | 0 | 39.10% | -10.65% | filetypes/php: 51.25% | 0.703 | 0.369 |
| powershell | 723 | 568 | `general,filegroups/scripts,filetypes/powershell` | filegroups/scripts: 43.57% | 0 | 37.21% | -6.36% | filegroups/scripts: 46.47% | 0.966 | 0.924 |
| lnk | 569 | 132 | `general,filetypes/lnk` | filetypes/lnk: 72.06% | 0 | 61.86% | -10.19% | filetypes/lnk: 72.23% | 0.992 | 0.987 |
| gz | 560 | 17142 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.348 |
| xml | 506 | 50413 | `general,filegroups/config,filetypes/xml` | filegroups/config: 8.10% | 0 | 7.31% | -0.79% | filegroups/config: 8.50% | 0.055 | 0.070 |
| text | 500 | 30369 | `general,filetypes/text` | filetypes/text: 2.80% | 0 | 2.80% | 0.00% | filetypes/text: 4.20% | 0.098 | 0.069 |
| jar | 494 | 1635 | `general,filetypes/jar` | filetypes/jar: 47.37% | 0 | 38.87% | -8.50% | filetypes/jar: 57.49% | 0.923 | 0.646 |
| csharp | 466 | 11125 | `general,filegroups/source,filetypes/csharp` | filegroups/source: 18.67% | 0 | 19.96% | 1.29% | filegroups/source: 19.53% | 0.352 | 0.227 |
| python_bytecode | 461 | 81658 | `general,filetypes/python_bytecode` | filetypes/python_bytecode: 55.31% | 0 | 55.31% | 0.00% | filetypes/python_bytecode: 66.81% | 0.699 | 0.660 |
| java | 459 | 19271 | `general,filegroups/source,filetypes/java` | filegroups/source: 1.09% | 0 | 1.09% | 0.00% | filegroups/source: 1.09% | 0.028 | 0.031 |
| npm | 410 | 522 | `general,filetypes/npm` | filetypes/npm: 55.61% | 0 | 49.02% | -6.59% | filetypes/npm: 62.93% | 0.927 | 0.716 |
| whl | 373 | 699 | `general,filetypes/whl` | filetypes/whl: 54.42% | 0 | 54.42% | 0.00% | filetypes/whl: 57.91% | 0.930 | 0.649 |
| macho | 361 | 2670 | `general,filegroups/native,filetypes/macho` | filegroups/native: 54.57% | 0 | 57.34% | 2.77% | filetypes/macho: 67.04% | 0.964 | 0.327 |
| java_class | 280 | 188136 | `general,filegroups/portable,filetypes/java_class` | general: 1.43% | 0 | 1.43% | 0.00% | general: 1.79% | 0.106 | 0.346 |
| apk_android | 263 | 21 | `general` | general: 0.38% | 0 | 0.00% | -0.38% | general: 0.38% | — | 0.865 |
| rust | 258 | 39635 | `general,filegroups/source,filetypes/rust` | filegroups/source: 1.16% | 0 | 1.16% | 0.00% | filegroups/source: 3.88% | 0.015 | 0.017 |
| crx | 230 | 174 | `general,filetypes/crx` | filetypes/crx: 65.65% | 0 | 66.09% | 0.43% | filetypes/crx: 68.26% | 0.981 | 0.879 |
| json | 202 | 18698 | `general,filegroups/config,filetypes/json` | filegroups/config: 6.93% | 0 | 6.93% | 0.00% | filegroups/config: 6.93% | 0.038 | 0.032 |
| jpeg | 180 | 5391 | `general,filegroups/media,filetypes/jpeg` | general: 2.78% | 0 | 3.89% | 1.11% | filetypes/jpeg: 14.44% | 0.205 | 0.180 |
| cab | 105 | 11 | `general` | general: 32.38% | — | — | — | general: 90.48% | — | 0.988 |
| makefile | 102 | 7392 | `general,filegroups/source,filetypes/makefile` | filegroups/source: 0.98% | 0 | 0.98% | 0.00% | filegroups/source: 0.98% | 0.016 | 0.028 |
| gem | 87 | 237 | `general,filetypes/gem` | filetypes/gem: 90.80% | 0 | 90.80% | 0.00% | filetypes/gem: 91.95% | 0.967 | 0.630 |
| plist | 84 | 11955 | `general,filegroups/config,filetypes/plist` | filegroups/config: 2.38% | 0 | 2.38% | 0.00% | filegroups/config: 3.57% | 0.053 | 0.030 |
| data | 78 | 7473 | `general` | general: 3.85% | — | — | — | general: 3.85% | — | 0.239 |
| deb | 57 | 2336 | `general,filetypes/deb` | filetypes/deb: 10.53% | 0 | 8.77% | -1.75% | filetypes/deb: 10.53% | 0.137 | 0.019 |
| registry | 56 | 8954 | `general,filetypes/registry` | general: 50.00% | 0 | 50.00% | 0.00% | general: 57.14% | 0.440 | 0.858 |
| cargo.toml | 50 | 823 | `general,filetypes/cargo.toml` | general: 28.00% | 0 | 28.00% | 0.00% | general: 28.00% | 0.478 | 0.389 |
| perl | 46 | 8104 | `general,filegroups/scripts,filetypes/perl` | filetypes/perl: 71.74% | 0 | 71.74% | 0.00% | filetypes/perl: 76.09% | 0.810 | 0.350 |
| chm | 40 | 5 | `general` | general: 82.50% | 0 | 60.00% | -22.50% | general: 82.50% | — | 0.985 |
| ruby | 35 | 20972 | `general,filegroups/scripts,filetypes/ruby` | filegroups/scripts: 17.14% | 0 | 22.86% | 5.71% | filetypes/ruby: 20.00% | 0.369 | 0.111 |
| html | 31 | 2010 | `general,filegroups/documents,filetypes/html` | filegroups/documents: 96.77% | 0 | 96.77% | 0.00% | filegroups/documents: 96.77% | 0.996 | 0.983 |
| dockerfile | 25 | 541 | `general,filetypes/dockerfile` | general: 0.00% | — | — | — | general: 8.00% | 0.145 | 0.144 |
| asar | 22 | 5 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.655 |
| groovy | 17 | 1331 | `general,filetypes/groovy` | filetypes/groovy: 23.53% | 0 | 23.53% | 0.00% | filetypes/groovy: 23.53% | 0.248 | 0.181 |
| go.mod | 16 | 58 | `general` | general: 18.75% | 0 | 6.25% | -12.50% | general: 18.75% | — | 0.430 |
| xz | 15 | 5501 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.075 |
| package-lock.json | 14 | 161 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.096 |
| chrome_manifest | 12 | 119 | `general,filetypes/chrome_manifest` | filetypes/chrome_manifest: 83.33% | 0 | 41.67% | -41.67% | filetypes/chrome_manifest: 91.67% | 0.942 | 0.631 |
| lua | 12 | 3202 | `general,filegroups/scripts,filetypes/lua` | filetypes/lua: 83.33% | 0 | 83.33% | 0.00% | filetypes/lua: 91.67% | 0.911 | 0.276 |
| markdown | 12 | 13128 | `general,filetypes/markdown` | general: 16.67% | 0 | 16.67% | 0.00% | general: 25.00% | 0.375 | 0.408 |
| applescript | 9 | 48 | `general,filetypes/applescript` | general: 88.89% | 0 | 88.89% | 0.00% | general: 88.89% | 0.908 | 0.908 |
| cargo.lock | 9 | 96 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.101 |
| vsix | 9 | 169 | `general,filetypes/vsix` | general: 0.00% | — | — | — | general: 0.00% | 0.057 | 0.045 |
| github_actions | 8 | 2007 | `general,filetypes/github_actions` | general: 0.00% | — | — | — | general: 0.00% | 0.626 | 0.118 |
| swift | 8 | 4601 | `general,filegroups/source,filetypes/swift` | filegroups/source: 75.00% | 0 | 75.00% | 0.00% | filegroups/source: 75.00% | 0.201 | 0.200 |
| clojure | 7 | 980 | `general,filetypes/clojure` | filetypes/clojure: 57.14% | 0 | 57.14% | 0.00% | filetypes/clojure: 57.14% | 0.653 | 0.592 |
| pyproject.toml | 7 | 38 | `general` | general: 14.29% | 0 | 0.00% | -14.29% | general: 14.29% | — | 0.289 |
| rpm | 7 | 410 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.048 |
| nupkg | 6 | 272 | `general,filetypes/nupkg` | general: 0.00% | — | — | — | general: 0.00% | 0.298 | 0.209 |
| xpi | 6 | 48 | `general` | general: 0.00% | — | — | — | general: 16.67% | — | 0.308 |
| zig | 6 | 160 | `general` | general: 0.00% | — | — | — | general: 16.67% | — | 0.159 |
| go.sum | 5 | 51 | `general` | general: 40.00% | 0 | 0.00% | -40.00% | general: 40.00% | — | 0.766 |
| objective_c | 5 | 3194 | `general` | general: 20.00% | — | — | — | general: 20.00% | — | 0.253 |
| bz2 | 4 | 1652 | `general` | general: 50.00% | — | — | — | general: 100.00% | — | 0.887 |
| composer.json | 4 | 297 | `general` | general: 25.00% | 0 | 25.00% | 0.00% | general: 25.00% | — | 0.263 |
| crate | 4 | 627 | `general,filetypes/crate` | filetypes/crate: 50.00% | 0 | 50.00% | 0.00% | filetypes/crate: 50.00% | 0.507 | 0.058 |
| desktop_entry | 3 | 629 | `general` | general: 33.33% | 0 | 33.33% | 0.00% | general: 33.33% | — | 0.356 |
| apk_alpine | 2 | 1830 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.003 |
| dmg | 2 | 20 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.341 |
| python_sdist | 2 | 4 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.267 |
| svg | 2 | 24299 | `general,filegroups/media` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.001 |
| systemd_service | 2 | 384 | `general` | general: 50.00% | 0 | 50.00% | 0.00% | general: 50.00% | — | 0.503 |
| composer.lock | 1 | 23 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.048 |
| conda | 1 | 177 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.034 |
| gyp | 1 | 62 | `general` | general: 0.00% | 0 | 0.00% | 0.00% | general: 0.00% | — | 0.056 |
| odf | 1 | 0 | `general` | general: 100.00% | 0 | 0.00% | -100.00% | general: 100.00% | — | — |
| pkg_macos | 1 | 11 | `general` | general: 0.00% | — | — | — | general: 0.00% | — | 0.100 |

## Deployed OR-rule at L0 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 50.00% | 82.50% | -32.50% |
| rar | `general` | 0 | 53.11% | 80.18% | -27.07% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L1 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 55.00% | 82.50% | -27.50% |
| rar | `general` | 0 | 53.11% | 80.18% | -27.07% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L2 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 55.00% | 82.50% | -27.50% |
| rar | `general` | 0 | 53.14% | 80.18% | -27.03% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L3 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 55.00% | 82.50% | -27.50% |
| rar | `general` | 0 | 53.18% | 80.18% | -27.00% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L4 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 55.00% | 82.50% | -27.50% |
| rar | `general` | 0 | 53.22% | 80.18% | -26.96% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L5 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 53.29% | 80.18% | -26.88% |
| chm | `general` | 0 | 57.50% | 82.50% | -25.00% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L10 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 53.51% | 80.18% | -26.66% |
| chm | `general` | 0 | 57.50% | 82.50% | -25.00% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `general,filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L20 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 54.65% | 80.18% | -25.52% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L30 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 55.24% | 80.18% | -24.94% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L40 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 55.79% | 80.18% | -24.38% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L50 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 55.94% | 80.18% | -24.24% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L60 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 59.80% | 80.18% | -20.38% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L70 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.21% | 80.18% | -19.97% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L80 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.76% | 80.18% | -19.42% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L90 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.76% | 80.18% | -19.42% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L100 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.76% | 80.18% | -19.42% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L200 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.90% | 80.18% | -19.27% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L300 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 60.98% | 80.18% | -19.20% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| chm | `general` | 0 | 60.00% | 82.50% | -22.50% |
| rar | `general` | 0 | 61.05% | 80.18% | -19.12% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L1000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 63.11% | 80.18% | -17.07% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| go.mod | `general` | 0 | 6.25% | 18.75% | -12.50% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 0 | 1.43% | 1.43% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| systemd_service | `general` | 0 | 50.00% | 50.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L2000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.02% | 80.18% | -15.15% |
| pyproject.toml | `general` | 0 | 0.00% | 14.29% | -14.29% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| javascript | `filegroups/scripts,filetypes/javascript` | 0 | 33.09% | 42.11% | -9.02% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| c | `filegroups/source` | 0 | 9.53% | 10.19% | -0.65% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 0 | 55.31% | 55.31% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L5000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.06% | 80.18% | -15.12% |
| php | `filegroups/scripts,filetypes/php` | 0 | 39.10% | 49.75% | -10.65% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| python | `filegroups/scripts,filetypes/python` | 0 | 46.51% | 52.05% | -5.54% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| xml | `filegroups/config` | 0 | 7.31% | 8.10% | -0.79% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L7500 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.06% | 80.18% | -15.12% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| php | `filegroups/scripts,filetypes/php` | 0 | 48.75% | 49.75% | -1.00% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| xml | `general,filegroups/config` | 0 | 7.91% | 8.10% | -0.20% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| png | `general` | 0 | 0.37% | 0.37% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 0 | 1.16% | 1.16% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| python | `filegroups/scripts,filetypes/python` | 1 | 54.33% | 54.26% | 0.07% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| elf | `general,filegroups/native,filetypes/elf` | 0 | 90.51% | 88.28% | 2.24% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L10000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.10% | 80.18% | -15.08% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| go | `general,filegroups/source,filetypes/go` | 0 | 5.02% | 8.94% | -3.93% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| php | `filegroups/scripts,filetypes/php` | 0 | 48.75% | 49.75% | -1.00% |
| png | `general,filegroups/media,filetypes/png` | 3 | 5.13% | 5.59% | -0.46% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| xml | `general,filegroups/config` | 0 | 7.91% | 8.10% | -0.20% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 95.77% | — | — |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 1 | 3.88% | 3.88% | 0.00% |
| svg | `general` | 0 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| text | `general,filetypes/text` | 0 | 2.80% | 2.80% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| python | `filegroups/scripts,filetypes/python` | 1 | 54.33% | 54.26% | 0.07% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L15000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| go | `general,filegroups/source,filetypes/go` | 1 | 8.05% | 10.55% | -2.51% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| php | `filegroups/scripts,filetypes/php` | 0 | 48.75% | 49.75% | -1.00% |
| png | `general,filegroups/media,filetypes/png` | 3 | 5.13% | 5.59% | -0.46% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| xml | `general,filegroups/config` | 0 | 7.91% | 8.10% | -0.20% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 95.77% | — | — |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source` | 0 | 1.09% | 1.09% | 0.00% |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 0 | 16.67% | 16.67% | 0.00% |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| rust | `filegroups/source` | 1 | 3.88% | 3.88% | 0.00% |
| svg | `general,filegroups/media` | 1 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| python | `filegroups/scripts,filetypes/python` | 1 | 54.33% | 54.26% | 0.07% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| text | `general,filetypes/text` | 1 | 4.40% | 4.20% | 0.20% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| pe | `general,filegroups/native,filetypes/pe` | 0 | 42.77% | 39.42% | 3.35% |
| ruby | `filegroups/scripts,filetypes/ruby` | 0 | 22.86% | 17.14% | 5.71% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L20000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| go | `general,filegroups/source,filetypes/go` | 1 | 8.05% | 10.55% | -2.51% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| php | `filegroups/scripts,filetypes/php` | 0 | 48.75% | 49.75% | -1.00% |
| png | `general,filegroups/media,filetypes/png` | 3 | 5.13% | 5.59% | -0.46% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| xml | `general,filegroups/config` | 0 | 7.91% | 8.10% | -0.20% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 95.77% | — | — |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source,filetypes/java` | 2 | 1.53% | — | — |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 2 | 33.33% | — | — |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 64.75% | — | — |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| ruby | `filetypes/ruby` | 2 | 31.43% | — | — |
| rust | `filegroups/source` | 1 | 3.88% | 3.88% | 0.00% |
| svg | `general,filegroups/media` | 1 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| python | `filegroups/scripts,filetypes/python` | 1 | 54.33% | 54.26% | 0.07% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| text | `general,filetypes/text` | 1 | 4.40% | 4.20% | 0.20% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
| shell | `filegroups/scripts,filetypes/shell` | 0 | 53.36% | 45.51% | 7.85% |

## Deployed OR-rule at L25000 hostile

Per filetype, the OR-rule operating point and the gap to the best single route's recall at the SAME FP count.

| Filetype | OR routes | OR FP | OR recall | Best single@OR-FP | Δ |
| --- | --- | ---: | ---: | --- | ---: |
| odf | `` | 0 | 0.00% | 100.00% | -100.00% |
| chrome_manifest | `filetypes/chrome_manifest` | 0 | 41.67% | 83.33% | -41.67% |
| go.sum | `general` | 0 | 0.00% | 40.00% | -40.00% |
| rar | `general` | 0 | 65.28% | 80.18% | -14.90% |
| lnk | `general,filetypes/lnk` | 0 | 61.86% | 72.06% | -10.19% |
| zip | `filetypes/zip` | 0 | 22.71% | 32.18% | -9.47% |
| vbs | `filetypes/vbs` | 0 | 43.40% | 52.50% | -9.10% |
| jar | `filetypes/jar` | 0 | 38.87% | 47.37% | -8.50% |
| npm | `filetypes/npm` | 0 | 49.02% | 55.61% | -6.59% |
| powershell | `general,filegroups/scripts,filetypes/powershell` | 0 | 37.21% | 43.57% | -6.36% |
| go.mod | `general` | 0 | 12.50% | 18.75% | -6.25% |
| ole_doc | `filetypes/ole_doc` | 0 | 85.35% | 88.92% | -3.57% |
| go | `general,filegroups/source,filetypes/go` | 1 | 8.05% | 10.55% | -2.51% |
| deb | `filetypes/deb` | 0 | 8.77% | 10.53% | -1.75% |
| php | `filegroups/scripts,filetypes/php` | 0 | 48.75% | 49.75% | -1.00% |
| png | `general,filegroups/media,filetypes/png` | 3 | 5.13% | 5.59% | -0.46% |
| apk_android | `` | 0 | 0.00% | 0.38% | -0.38% |
| tar | `filetypes/tar` | 0 | 78.45% | 78.66% | -0.21% |
| xml | `general,filegroups/config` | 0 | 7.91% | 8.10% | -0.20% |
| rtf | `filetypes/rtf` | 0 | 97.23% | 97.35% | -0.12% |
| c | `filegroups/source` | 1 | 13.28% | 13.37% | -0.09% |
| ooxml | `filetypes/ooxml` | 0 | 23.24% | 23.25% | -0.01% |
| applescript | `general,filetypes/applescript` | 0 | 88.89% | 88.89% | 0.00% |
| cargo.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| cargo.toml | `general,filetypes/cargo.toml` | 0 | 28.00% | 28.00% | 0.00% |
| chm | `general` | 0 | 82.50% | 82.50% | 0.00% |
| clojure | `general,filetypes/clojure` | 0 | 57.14% | 57.14% | 0.00% |
| composer.json | `general` | 0 | 25.00% | 25.00% | 0.00% |
| composer.lock | `general` | 0 | 0.00% | 0.00% | 0.00% |
| crate | `filetypes/crate` | 0 | 50.00% | 50.00% | 0.00% |
| desktop_entry | `general` | 0 | 33.33% | 33.33% | 0.00% |
| elf | `filegroups/native,filetypes/elf` | 2 | 95.77% | — | — |
| gem | `filetypes/gem` | 0 | 90.80% | 90.80% | 0.00% |
| groovy | `filetypes/groovy` | 0 | 23.53% | 23.53% | 0.00% |
| gyp | `general` | 0 | 0.00% | 0.00% | 0.00% |
| html | `general,filetypes/html` | 0 | 96.77% | 96.77% | 0.00% |
| java | `filegroups/source,filetypes/java` | 2 | 1.53% | — | — |
| java_class | `general` | 3 | 2.14% | 2.14% | 0.00% |
| json | `filegroups/config` | 0 | 6.93% | 6.93% | 0.00% |
| lua | `filetypes/lua` | 0 | 83.33% | 83.33% | 0.00% |
| makefile | `filegroups/source` | 0 | 0.98% | 0.98% | 0.00% |
| markdown | `general,filetypes/markdown` | 2 | 33.33% | — | — |
| package.json | `filegroups/config` | 0 | 83.61% | 83.61% | 0.00% |
| pe | `general,filegroups/native,filetypes/pe` | 2 | 64.75% | — | — |
| perl | `filetypes/perl` | 0 | 71.74% | 71.74% | 0.00% |
| plist | `filegroups/config` | 0 | 2.38% | 2.38% | 0.00% |
| pyproject.toml | `general` | 0 | 14.29% | 14.29% | 0.00% |
| python_bytecode | `filetypes/python_bytecode` | 1 | 66.81% | 66.81% | 0.00% |
| python_sdist | `` | 0 | 0.00% | 0.00% | 0.00% |
| registry | `general` | 0 | 50.00% | 50.00% | 0.00% |
| ruby | `filetypes/ruby` | 2 | 31.43% | — | — |
| rust | `filegroups/source` | 1 | 3.88% | 3.88% | 0.00% |
| shell | `filegroups/scripts,filetypes/shell` | 2 | 58.31% | — | — |
| svg | `general,filegroups/media` | 1 | 0.00% | 0.00% | 0.00% |
| swift | `filegroups/source,filetypes/swift` | 0 | 75.00% | 75.00% | 0.00% |
| unknown | `general` | 1 | 0.16% | 0.16% | 0.00% |
| whl | `filetypes/whl` | 0 | 54.42% | 54.42% | 0.00% |
| kotlin | `filegroups/source,filetypes/kotlin` | 0 | 57.57% | 57.52% | 0.05% |
| python | `filegroups/scripts,filetypes/python` | 1 | 54.33% | 54.26% | 0.07% |
| batch | `general,filegroups/scripts,filetypes/batch` | 0 | 16.04% | 15.96% | 0.08% |
| text | `general,filetypes/text` | 1 | 4.40% | 4.20% | 0.20% |
| pdf | `filegroups/documents,filetypes/pdf` | 0 | 73.54% | 73.26% | 0.28% |
| pkg_info | `general,filetypes/pkg_info` | 0 | 96.06% | 95.75% | 0.31% |
| crx | `general,filetypes/crx` | 0 | 66.09% | 65.65% | 0.43% |
| javascript | `general,filetypes/javascript` | 0 | 43.01% | 42.11% | 0.90% |
| jpeg | `general,filetypes/jpeg` | 0 | 3.89% | 2.78% | 1.11% |
| csharp | `filegroups/source,filetypes/csharp` | 0 | 19.96% | 18.67% | 1.29% |
| macho | `filegroups/native,filetypes/macho` | 0 | 57.34% | 54.57% | 2.77% |
