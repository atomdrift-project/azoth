# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1618843881`
- Rows: 5591524 (1834873 malware, 3756651 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info† | filetype_only | 10635 | 1194 | 99.78% | 0 | 0.00 | 2505.84 | 0.000 | 99.89% | 99.81% | `{"filetypes/pkg-info": 0.29691197685494564}` |
| filetypes/batch | joint_or_at_fp_0 | 173427 | 4145 | 98.51% | 0 | 0.00 | 722.47 | 0.000 | 99.25% | 98.55% | `{"filegroups/scripts": 0.9973234534263611, "filetypes/batch": 0.9958939552307129, "general": 0.9816225171089172}` |
| filetypes/rtf | learned_blend_at_fp_0 | 1887 | 480 | 98.25% | 0 | 0.00 | 6221.67 | 0.000 | 99.12% | 98.61% | `{}` |
| filetypes/tar | joint_or_at_fp_0 | 1165 | 478 | 96.82% | 0 | 0.00 | 6247.62 | 0.000 | 98.39% | 97.75% | `{"filetypes/tar": 0.38358986377716064}` |
| filetypes/xls | learned_blend_at_fp_2 | 13169 | 20721 | 96.20% | 1 | 48.26 | 228.92 | 0.266 | 98.06% | 98.52% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_3 | 2114 | 62340 | 95.93% | 3 | 48.12 | 124.37 | 0.799 | 97.85% | 99.86% | `{"filetypes/python-bytecode": 0.9941364526748657}` |
| filetypes/doc | calibrate_inherited | 13170 | 54 | 94.02% | 0 | 0.00 | 53965.77 | 0.000 | 96.92% | 94.04% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9979211688041687}` |
| filetypes/elf | joint_or_at_fp_3 | 90231 | 152973 | 92.92% | 3 | 19.61 | 50.69 | 0.799 | 96.33% | 97.37% | `{"filegroups/native": 0.9956063628196716, "filetypes/elf": 0.9987130165100098, "general": 0.9808173775672913}` |
| filetypes/package.json | joint_or_at_fp_0 | 18222 | 12966 | 90.92% | 0 | 0.00 | 231.02 | 0.000 | 95.24% | 94.69% | `{"filegroups/config": 0.9997115731239319, "filetypes/package.json": 0.996483325958252, "general": 0.9953767657279968}` |
| filetypes/ole | joint_or_at_fp_0 | 2419 | 5714 | 89.05% | 0 | 0.00 | 524.14 | 0.000 | 94.21% | 96.74% | `{"filegroups/documents": 0.8479767441749573, "filetypes/ole": 0.9413946866989136, "general": 0.9813792705535889}` |
| filetypes/crx | joint_or_at_fp_0 | 363 | 79 | 85.12% | 0 | 0.00 | 37210.68 | 0.000 | 91.96% | 87.78% | `{"filetypes/crx": 0.8975868821144104, "general": 0.9390619397163391}` |
| filetypes/shell | joint_or_at_fp_2 | 8477 | 49248 | 84.31% | 2 | 40.61 | 127.83 | 0.532 | 91.48% | 97.69% | `{"filegroups/scripts": 0.9926738142967224, "filetypes/shell": 0.9558824896812439, "general": 0.9548232555389404}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 57 | 397 | 80.70% | 0 | 0.00 | 7517.53 | 0.000 | 89.32% | 97.58% | `{"filetypes/chrome-manifest": 0.8839526176452637, "general": 0.8681843280792236}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 29727 | 14285 | 75.99% | 0 | 0.00 | 209.69 | 0.000 | 86.36% | 83.79% | `{"filetypes/tar.gz": 0.9945971965789795, "general": 0.9962186217308044}` |
| filetypes/html | joint_or_at_fp_0 | 156 | 25611 | 73.72% | 0 | 0.00 | 116.96 | 0.000 | 84.87% | 99.84% | `{"filegroups/documents": 0.39611321687698364, "filetypes/html": 0.9142829179763794}` |
| filetypes/java_class | learned_blend_at_fp_8 | 1402 | 463572 | 73.40% | 8 | 17.26 | 31.14 | 2.130 | 84.38% | 99.92% | `{}` |
| filetypes/lnk† | filetype_only | 2350 | 1055 | 72.85% | 0 | 0.00 | 2835.53 | 0.000 | 84.29% | 81.26% | `{"filetypes/lnk": 0.7509527551950674}` |
| filetypes/macho | joint_or_at_fp_0 | 2160 | 10937 | 72.82% | 0 | 0.00 | 273.87 | 0.000 | 84.28% | 95.52% | `{"filegroups/native": 0.9948294758796692, "filetypes/macho": 0.9828328490257263, "general": 0.9152836799621582}` |
| filetypes/clojure | joint_or_at_fp_0 | 89 | 904 | 70.79% | 0 | 0.00 | 3308.38 | 0.000 | 82.89% | 97.38% | `{"filetypes/clojure": 0.99104905128479, "general": 0.45181596279144287}` |
| filetypes/pe | learned_blend_at_fp_3 | 954300 | 154485 | 69.90% | 3 | 19.42 | 50.19 | 0.799 | 82.29% | 74.10% | `{}` |
| filetypes/javascript | learned_blend_at_fp_17 | 91701 | 537021 | 68.72% | 17 | 31.66 | 47.48 | 4.525 | 81.45% | 95.43% | `{}` |
| filetypes/python | joint_or_at_fp_3 | 18251 | 144877 | 65.97% | 3 | 20.71 | 53.52 | 0.799 | 79.49% | 96.19% | `{"filegroups/scripts": 0.9974439144134521, "filetypes/python": 0.9980592131614685, "general": 0.9907415509223938}` |
| filetypes/zst | calibrate_inherited | 10381 | 16291 | 65.43% | 0 | 0.00 | 183.87 | 0.000 | 79.10% | 86.54% | `{"general": 0.9979211688041687}` |
| filetypes/docx | calibrate_inherited | 1885 | 309 | 63.77% | 0 | 0.00 | 9648.08 | 0.000 | 77.87% | 68.87% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9979211688041687}` |
| filetypes/rar | calibrate_inherited | 7553 | 4 | 62.76% | 0 | 0.00 | 527129.20 | 0.000 | 77.12% | 62.78% | `{"general": 0.9979211688041687}` |
| filetypes/jar | joint_or_at_fp_0 | 1682 | 2888 | 62.13% | 0 | 0.00 | 1036.77 | 0.000 | 76.64% | 86.06% | `{"filetypes/jar": 0.9026422500610352, "general": 0.9715058207511902}` |
| filetypes/perl | joint_or_at_fp_0 | 243 | 32125 | 59.26% | 0 | 0.00 | 93.25 | 0.000 | 74.42% | 99.69% | `{"filegroups/scripts": 0.9925407767295837, "filetypes/perl": 0.9953613877296448}` |
| filetypes/php | joint_or_at_fp_3 | 4094 | 108338 | 57.94% | 3 | 27.69 | 71.57 | 0.799 | 73.33% | 98.47% | `{"filegroups/scripts": 0.9964056015014648, "filetypes/php": 0.9967387318611145, "general": 0.9925193190574646}` |
| filetypes/msi | joint_or_at_fp_0 | 2456 | 154 | 57.08% | 0 | 0.00 | 19264.82 | 0.000 | 72.68% | 59.62% | `{"filetypes/msi": 0.8698219656944275, "general": 0.9631515145301819}` |
| filetypes/powershell | joint_or_at_fp_0 | 3026 | 2183 | 55.55% | 0 | 0.00 | 1371.36 | 0.000 | 71.43% | 74.18% | `{"filegroups/scripts": 0.9980354905128479, "filetypes/powershell": 0.9727897047996521, "general": 0.9757954478263855}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info† | max_rule | 10635 | 1194 | 99.87% | 0 | 0.00 | 2505.84 | 0.000 | 99.93% | 99.88% | `{"filetypes/pkg-info": 0.2777818191778481, "general": 0.2777818191778481}` |
| filetypes/batch | joint_or_at_fp_0 | 173427 | 4145 | 98.51% | 0 | 0.00 | 722.47 | 0.000 | 99.25% | 98.55% | `{"filegroups/scripts": 0.9973234534263611, "filetypes/batch": 0.9958939552307129, "general": 0.9816225171089172}` |
| filetypes/rtf | learned_blend_at_fp_0 | 1887 | 480 | 98.25% | 0 | 0.00 | 6221.67 | 0.000 | 99.12% | 98.61% | `{}` |
| filetypes/tar | joint_or_at_fp_0 | 1165 | 478 | 96.82% | 0 | 0.00 | 6247.62 | 0.000 | 98.39% | 97.75% | `{"filetypes/tar": 0.38358986377716064}` |
| filetypes/python-bytecode | learned_blend_at_fp_6 | 2114 | 62340 | 96.59% | 4 | 64.16 | 146.83 | 1.065 | 98.17% | 99.88% | `{}` |
| filetypes/xls | learned_blend_at_fp_2 | 13169 | 20721 | 96.20% | 1 | 48.26 | 228.92 | 0.266 | 98.06% | 98.52% | `{}` |
| filetypes/doc | calibrate_inherited | 13170 | 54 | 94.02% | 0 | 0.00 | 53965.77 | 0.000 | 96.92% | 94.04% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9967629313468933}` |
| filetypes/elf | joint_or_at_fp_9 | 90231 | 152973 | 93.96% | 9 | 58.83 | 102.66 | 2.396 | 96.88% | 97.76% | `{"filegroups/native": 0.9956186413764954, "filetypes/elf": 0.9968541264533997, "general": 0.9808173775672913}` |
| filetypes/package.json | joint_or_at_fp_0 | 18222 | 12966 | 90.92% | 0 | 0.00 | 231.02 | 0.000 | 95.24% | 94.69% | `{"filegroups/config": 0.9997115731239319, "filetypes/package.json": 0.996483325958252, "general": 0.9953767657279968}` |
| filetypes/ole | joint_or_at_fp_0 | 2419 | 5714 | 89.05% | 0 | 0.00 | 524.14 | 0.000 | 94.21% | 96.74% | `{"filegroups/documents": 0.8479767441749573, "filetypes/ole": 0.9413946866989136, "general": 0.9813792705535889}` |
| filetypes/crx | joint_or_at_fp_0 | 363 | 79 | 85.12% | 0 | 0.00 | 37210.68 | 0.000 | 91.96% | 87.78% | `{"filetypes/crx": 0.8975868821144104, "general": 0.9390619397163391}` |
| filetypes/shell | joint_or_at_fp_3 | 8477 | 49248 | 84.36% | 3 | 60.92 | 157.43 | 0.799 | 91.50% | 97.70% | `{"filegroups/scripts": 0.9926738142967224, "filetypes/shell": 0.954556941986084, "general": 0.9548232555389404}` |
| filetypes/java_class | learned_blend_at_fp_14 | 1402 | 463572 | 82.74% | 14 | 30.20 | 47.21 | 3.727 | 90.06% | 99.94% | `{}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 57 | 397 | 80.70% | 0 | 0.00 | 7517.53 | 0.000 | 89.32% | 97.58% | `{"filetypes/chrome-manifest": 0.8839526176452637, "general": 0.8681843280792236}` |
| filetypes/html | joint_or_at_fp_2 | 156 | 25611 | 76.28% | 2 | 78.09 | 245.80 | 0.532 | 85.92% | 99.85% | `{"filegroups/documents": 0.39611321687698364, "filetypes/html": 0.8343577980995178}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 29727 | 14285 | 75.99% | 0 | 0.00 | 209.69 | 0.000 | 86.36% | 83.79% | `{"filetypes/tar.gz": 0.9945971965789795, "general": 0.9962186217308044}` |
| filetypes/lnk† | filetype_only | 2350 | 1055 | 72.85% | 0 | 0.00 | 2835.53 | 0.000 | 84.29% | 81.26% | `{"filetypes/lnk": 0.7505718497850927}` |
| filetypes/macho | joint_or_at_fp_0 | 2160 | 10937 | 72.82% | 0 | 0.00 | 273.87 | 0.000 | 84.28% | 95.52% | `{"filegroups/native": 0.9948294758796692, "filetypes/macho": 0.9828328490257263, "general": 0.9152836799621582}` |
| filetypes/clojure | joint_or_at_fp_0 | 89 | 904 | 70.79% | 0 | 0.00 | 3308.38 | 0.000 | 82.89% | 97.38% | `{"filetypes/clojure": 0.99104905128479, "general": 0.45181596279144287}` |
| filetypes/zst | calibrate_inherited | 10381 | 16291 | 70.46% | 0 | 0.00 | 183.87 | 0.000 | 82.67% | 88.50% | `{"general": 0.9967629313468933}` |
| filetypes/pe | learned_blend_at_fp_5 | 954300 | 154485 | 70.24% | 5 | 32.37 | 68.05 | 1.331 | 82.52% | 74.39% | `{}` |
| filetypes/javascript | learned_blend_at_fp_19 | 91701 | 537021 | 69.72% | 19 | 35.38 | 51.91 | 5.058 | 82.15% | 95.58% | `{}` |
| filetypes/python | calibrate_inherited | 18251 | 144877 | 67.32% | 11 | 75.93 | 125.67 | 2.928 | 80.44% | 96.34% | `{"filegroups/scripts": 0.9976997971534729, "filetypes/python": 0.997091350543215, "general": 0.9967629313468933}` |
| filetypes/rar | calibrate_inherited | 7553 | 4 | 67.26% | 0 | 0.00 | 527129.20 | 0.000 | 80.42% | 67.28% | `{"general": 0.9967629313468933}` |
| filetypes/docx | calibrate_inherited | 1885 | 309 | 63.77% | 0 | 0.00 | 9648.08 | 0.000 | 77.87% | 68.87% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9967629313468933}` |
| filetypes/php | learned_blend_at_fp_6 | 4094 | 108338 | 63.02% | 6 | 55.38 | 109.31 | 1.597 | 77.25% | 98.65% | `{}` |
| filetypes/perl | joint_or_at_fp_2 | 243 | 32125 | 62.14% | 2 | 62.26 | 195.96 | 0.532 | 76.26% | 99.71% | `{"filegroups/scripts": 0.9925407767295837, "filetypes/perl": 0.986786425113678}` |
| filetypes/jar | joint_or_at_fp_0 | 1682 | 2888 | 62.13% | 0 | 0.00 | 1036.77 | 0.000 | 76.64% | 86.06% | `{"filetypes/jar": 0.9026422500610352, "general": 0.9715058207511902}` |
| filetypes/7z | calibrate_inherited | 4539 | 101 | 60.89% | 0 | 0.00 | 29225.15 | 0.000 | 75.69% | 61.75% | `{"general": 0.9967629313468933}` |
| filetypes/msi | joint_or_at_fp_0 | 2456 | 154 | 57.08% | 0 | 0.00 | 19264.82 | 0.000 | 72.68% | 59.62% | `{"filetypes/msi": 0.8698219656944275, "general": 0.9631515145301819}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9919607639312744}` |
| filetypes/pkg-info† | max_rule | 10635 | 1194 | 99.87% | 0 | 0.00 | 2505.84 | 0.000 | 99.93% | 99.88% | `{"filetypes/pkg-info": 0.22489915146802192, "general": 0.22489915146802192}` |
| filetypes/python-bytecode | calibrate_inherited | 2114 | 62340 | 98.58% | 13 | 208.53 | 331.53 | 3.461 | 98.98% | 99.93% | `{"filetypes/python-bytecode": 0.5463529004577621, "general": 0.9919607639312744}` |
| filetypes/batch | joint_or_at_fp_0 | 173427 | 4145 | 98.51% | 0 | 0.00 | 722.47 | 0.000 | 99.25% | 98.55% | `{"filegroups/scripts": 0.9973234534263611, "filetypes/batch": 0.9958939552307129, "general": 0.9816225171089172}` |
| filetypes/rtf | learned_blend_at_fp_0 | 1887 | 480 | 98.25% | 0 | 0.00 | 6221.67 | 0.000 | 99.12% | 98.61% | `{}` |
| filetypes/tar | joint_or_at_fp_0 | 1165 | 478 | 96.82% | 0 | 0.00 | 6247.62 | 0.000 | 98.39% | 97.75% | `{"filetypes/tar": 0.38358986377716064}` |
| filetypes/package.json | learned_blend_at_fp_3 | 18222 | 12966 | 96.45% | 3 | 231.37 | 597.89 | 0.799 | 98.18% | 97.92% | `{}` |
| filetypes/xls | joint_or_at_fp_5 | 13169 | 20721 | 96.25% | 5 | 241.30 | 507.29 | 1.331 | 98.07% | 98.53% | `{"filetypes/xls": 0.4969820976257324}` |
| filetypes/elf | joint_or_at_fp_21 | 90231 | 152973 | 94.51% | 21 | 137.28 | 197.68 | 5.590 | 97.17% | 97.95% | `{"filegroups/native": 0.9956186413764954, "filetypes/elf": 0.995214581489563, "general": 0.9816262125968933}` |
| filetypes/doc | calibrate_inherited | 13170 | 54 | 94.02% | 0 | 0.00 | 53965.77 | 0.000 | 96.92% | 94.04% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9919607639312744}` |
| filetypes/java_class | learned_blend_at_fp_56 | 1402 | 463572 | 91.37% | 56 | 120.80 | 150.91 | 14.907 | 93.54% | 99.96% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 2419 | 5714 | 89.05% | 0 | 0.00 | 524.14 | 0.000 | 94.21% | 96.74% | `{"filegroups/documents": 0.8479767441749573, "filetypes/ole": 0.9413946866989136, "general": 0.9813792705535889}` |
| filetypes/zst† | or_general_primary | 10381 | 16291 | 87.19% | 2 | 122.77 | 386.41 | 0.532 | 93.15% | 95.01% | `{"general": 0.9350612163543701}` |
| filetypes/shell | joint_or_at_fp_16 | 8477 | 49248 | 86.76% | 16 | 324.89 | 493.40 | 4.259 | 92.82% | 98.03% | `{"filegroups/scripts": 0.9923356175422668, "filetypes/shell": 0.8914312720298767, "general": 0.957266628742218}` |
| filetypes/crx | joint_or_at_fp_0 | 363 | 79 | 85.12% | 0 | 0.00 | 37210.68 | 0.000 | 91.96% | 87.78% | `{"filetypes/crx": 0.8975868821144104, "general": 0.9390619397163391}` |
| filetypes/macho | joint_or_at_fp_3 | 2160 | 10937 | 84.21% | 3 | 274.30 | 708.78 | 0.799 | 91.36% | 97.37% | `{"filegroups/native": 0.9974283576011658, "filetypes/macho": 0.8975948095321655, "general": 0.923566460609436}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 57 | 397 | 80.70% | 0 | 0.00 | 7517.53 | 0.000 | 89.32% | 97.58% | `{"filetypes/chrome-manifest": 0.8839526176452637, "general": 0.8681843280792236}` |
| filetypes/tar.gz | joint_or_at_fp_3 | 29727 | 14285 | 80.22% | 3 | 210.01 | 542.69 | 0.799 | 89.02% | 86.64% | `{"filetypes/tar.gz": 0.9922123551368713, "general": 0.9945246577262878}` |
| filetypes/pe | learned_blend_at_fp_23 | 954300 | 154485 | 79.27% | 23 | 148.88 | 210.92 | 6.122 | 88.43% | 82.16% | `{}` |
| filetypes/javascript | learned_blend_at_fp_64 | 91701 | 537021 | 77.21% | 64 | 119.18 | 146.74 | 17.036 | 87.11% | 96.67% | `{}` |
| filetypes/html | joint_or_at_fp_1 | 156 | 25611 | 76.28% | 1 | 39.05 | 185.21 | 0.266 | 86.23% | 99.85% | `{"filegroups/documents": 0.39611321687698364, "filetypes/html": 0.8553459048271179}` |
| filetypes/rar | calibrate_inherited | 7553 | 4 | 73.03% | 0 | 0.00 | 527129.20 | 0.000 | 84.41% | 73.04% | `{"general": 0.9919607639312744}` |
| filetypes/lnk† | filetype_only | 2350 | 1055 | 72.94% | 0 | 0.00 | 2835.53 | 0.000 | 84.35% | 81.32% | `{"filetypes/lnk": 0.7479178009959538}` |
| filetypes/7z | calibrate_inherited | 4539 | 101 | 72.75% | 0 | 0.00 | 29225.15 | 0.000 | 84.22% | 73.34% | `{"general": 0.9919607639312744}` |
| filetypes/clojure | joint_or_at_fp_0 | 89 | 904 | 70.79% | 0 | 0.00 | 3308.38 | 0.000 | 82.89% | 97.38% | `{"filetypes/clojure": 0.99104905128479, "general": 0.45181596279144287}` |
| filetypes/python | joint_or_at_fp_26 | 18251 | 144877 | 70.39% | 26 | 179.46 | 249.01 | 6.921 | 82.55% | 96.67% | `{"filegroups/scripts": 0.9972172975540161, "filetypes/python": 0.9945857524871826, "general": 0.989145815372467}` |
| filetypes/php | specialist_primary_with_escape | 4094 | 108338 | 68.91% | 14 | 129.23 | 202.01 | 3.727 | 81.43% | 98.86% | `{"filegroups/scripts": 0.9913653135299683, "filetypes/php": 0.995466947555542, "general": 0.9220582842826843}` |
| filetypes/ruby† | specialist_primary_with_escape | 94 | 24611 | 67.02% | 3 | 121.90 | 315.02 | 0.799 | 78.75% | 99.86% | `{"filegroups/scripts": 0.9918362498283386, "filetypes/ruby": 0.9999791383743286, "general": 0.8919362425804138}` |
| filetypes/perl | joint_or_at_fp_3 | 243 | 32125 | 65.43% | 3 | 93.39 | 241.34 | 0.799 | 78.52% | 99.73% | `{"filegroups/scripts": 0.9925407767295837, "filetypes/perl": 0.9790210723876953}` |
| filetypes/docx | calibrate_inherited | 1885 | 309 | 63.82% | 0 | 0.00 | 9648.08 | 0.000 | 77.91% | 68.92% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9919607639312744}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9903141260147095}` |
| filetypes/pkg-info† | max_rule | 10635 | 1194 | 99.94% | 0 | 0.00 | 2505.84 | 0.000 | 99.97% | 99.95% | `{"filetypes/pkg-info": 0.2092215348118425, "general": 0.2092215348118425}` |
| filetypes/python-bytecode | calibrate_inherited | 2114 | 62340 | 98.63% | 16 | 256.66 | 389.79 | 4.259 | 98.93% | 99.93% | `{"filetypes/python-bytecode": 0.3576384268485472, "general": 0.9903141260147095}` |
| filetypes/batch | learned_blend_at_fp_3 | 173427 | 4145 | 98.54% | 3 | 723.76 | 1869.53 | 0.799 | 99.26% | 98.57% | `{}` |
| filetypes/rtf | learned_blend_at_fp_0 | 1887 | 480 | 98.25% | 0 | 0.00 | 6221.67 | 0.000 | 99.12% | 98.61% | `{}` |
| filetypes/package.json | learned_blend_at_fp_3 | 18222 | 12966 | 96.45% | 3 | 231.37 | 597.89 | 0.799 | 98.18% | 97.92% | `{}` |
| filetypes/xls | learned_blend_at_fp_3 | 13169 | 20721 | 96.22% | 2 | 96.52 | 303.80 | 0.532 | 98.07% | 98.52% | `{}` |
| filetypes/elf | joint_or_at_fp_33 | 90231 | 152973 | 95.11% | 33 | 215.72 | 288.44 | 8.784 | 97.47% | 98.17% | `{"filegroups/native": 0.9956386685371399, "filetypes/elf": 0.9914050102233887, "general": 0.9816262125968933}` |
| filetypes/doc | calibrate_inherited | 13170 | 54 | 94.02% | 0 | 0.00 | 53965.77 | 0.000 | 96.92% | 94.04% | `{"filegroups/documents": 0.8868567943572998, "general": 0.9903141260147095}` |
| filetypes/java_class | calibrate_inherited | 1402 | 463572 | 91.94% | 72 | 155.32 | 188.96 | 19.166 | 93.30% | 99.96% | `{"filegroups/portable": 0.7666139006614685, "filetypes/java_class": 0.7384461760520935, "general": 0.9903141260147095}` |
| filetypes/ole | joint_or_at_fp_3 | 2419 | 5714 | 91.32% | 3 | 525.03 | 1356.39 | 0.799 | 95.40% | 97.38% | `{"filegroups/documents": 0.06991982460021973, "filetypes/ole": 0.7206702828407288}` |
| filetypes/tar† | filetype_only | 1165 | 478 | 90.13% | 0 | 0.00 | 6247.62 | 0.000 | 94.81% | 93.00% | `{"filetypes/tar": 0.9162974059815815}` |
| filetypes/perl | calibrate_inherited | 243 | 32125 | 87.65% | 19 | 591.44 | 867.72 | 5.058 | 89.68% | 99.85% | `{"filegroups/scripts": 0.9911733269691467, "filetypes/perl": 0.7574929628755294, "general": 0.9903141260147095}` |
| filetypes/zst† | or_general_primary | 10381 | 16291 | 87.19% | 2 | 122.77 | 386.41 | 0.532 | 93.15% | 95.01% | `{"general": 0.9350612163543701}` |
| filetypes/shell | joint_or_at_fp_17 | 8477 | 49248 | 86.93% | 17 | 345.19 | 517.73 | 4.525 | 92.91% | 98.05% | `{"filegroups/scripts": 0.9923356175422668, "filetypes/shell": 0.881182849407196, "general": 0.957266628742218}` |
| filetypes/crx | joint_or_at_fp_0 | 363 | 79 | 85.12% | 0 | 0.00 | 37210.68 | 0.000 | 91.96% | 87.78% | `{"filetypes/crx": 0.8975868821144104, "general": 0.9390619397163391}` |
| filetypes/macho | joint_or_at_fp_3 | 2160 | 10937 | 84.21% | 3 | 274.30 | 708.78 | 0.799 | 91.36% | 97.37% | `{"filegroups/native": 0.9974283576011658, "filetypes/macho": 0.8975948095321655, "general": 0.923566460609436}` |
| filetypes/pe | learned_blend_at_fp_35 | 954300 | 154485 | 81.66% | 35 | 226.56 | 300.37 | 9.317 | 89.90% | 84.22% | `{}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 57 | 397 | 80.70% | 0 | 0.00 | 7517.53 | 0.000 | 89.32% | 97.58% | `{"filetypes/chrome-manifest": 0.8839526176452637, "general": 0.8681843280792236}` |
| filetypes/tar.gz | joint_or_at_fp_3 | 29727 | 14285 | 80.22% | 3 | 210.01 | 542.69 | 0.799 | 89.02% | 86.64% | `{"filetypes/tar.gz": 0.9922123551368713, "general": 0.9945246577262878}` |
| filetypes/html | joint_or_at_fp_12 | 156 | 25611 | 80.13% | 12 | 468.55 | 759.04 | 3.194 | 85.32% | 99.83% | `{"filegroups/documents": 0.39611321687698364, "filetypes/html": 0.6958538293838501}` |
| filetypes/javascript | learned_blend_at_fp_91 | 91701 | 537021 | 79.03% | 91 | 169.45 | 201.71 | 24.224 | 88.24% | 96.93% | `{}` |
| filetypes/7z | calibrate_inherited | 4539 | 101 | 74.25% | 0 | 0.00 | 29225.15 | 0.000 | 85.22% | 74.81% | `{"general": 0.9903141260147095}` |
| filetypes/rar | calibrate_inherited | 7553 | 4 | 73.89% | 0 | 0.00 | 527129.20 | 0.000 | 84.99% | 73.90% | `{"general": 0.9903141260147095}` |
| filetypes/lnk† | filetype_only | 2350 | 1055 | 72.94% | 0 | 0.00 | 2835.53 | 0.000 | 84.35% | 81.32% | `{"filetypes/lnk": 0.7461979514678406}` |
| filetypes/php | specialist_primary_with_escape | 4094 | 108338 | 70.81% | 20 | 184.61 | 268.24 | 5.324 | 82.68% | 98.92% | `{"filegroups/scripts": 0.9903101325035095, "filetypes/php": 0.9943021535873413, "general": 0.8866659998893738}` |
| filetypes/clojure | joint_or_at_fp_0 | 89 | 904 | 70.79% | 0 | 0.00 | 3308.38 | 0.000 | 82.89% | 97.38% | `{"filetypes/clojure": 0.99104905128479, "general": 0.45181596279144287}` |
| filetypes/python | learned_blend_at_fp_31 | 18251 | 144877 | 70.75% | 30 | 207.07 | 280.85 | 7.986 | 82.79% | 96.71% | `{}` |
| filetypes/ruby† | specialist_primary_with_escape | 94 | 24611 | 67.02% | 3 | 121.90 | 315.02 | 0.799 | 78.75% | 99.86% | `{"filegroups/scripts": 0.9918362498283386, "filetypes/ruby": 0.9999791383743286, "general": 0.8919362425804138}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 227 | 66.67% | 0 | 0.00 | 13110.36 | 0.000 | 80.00% | 99.57% | `{"general": 0.9903141260147095}` |
