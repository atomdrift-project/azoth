# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1525145935`
- Rows: 5053489 (1766770 malware, 3286719 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 56 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf† | max_rule | 1488 | 480 | 98.19% | 0 | 0.00 | 6221.67 | 0.000 | 99.08% | 98.63% | `{"filegroups/documents": 0.08551054844825635, "filetypes/rtf": 0.08551054844825635, "general": 0.08551054844825635}` |
| filetypes/tar | joint_or_at_fp_0 | 1145 | 436 | 97.47% | 0 | 0.00 | 6847.39 | 0.000 | 98.72% | 98.17% | `{"filetypes/tar": 0.19932818412780762, "general": 0.900611937046051}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1137 | 97.11% | 0 | 0.00 | 2631.30 | 0.000 | 98.54% | 97.39% | `{"filetypes/pkg-info": 0.5929597800227345, "general": 0.10212018525080178}` |
| filetypes/xls | learned_blend_at_fp_0 | 10570 | 20711 | 95.92% | 0 | 0.00 | 144.63 | 0.000 | 97.92% | 98.62% | `{}` |
| filetypes/batch† | filetype_only | 173234 | 3988 | 94.11% | 0 | 0.00 | 750.90 | 0.000 | 96.97% | 94.24% | `{"filetypes/batch": 0.994774935343046}` |
| filetypes/elf | joint_or_at_fp_3 | 82465 | 149754 | 93.62% | 3 | 20.03 | 51.78 | 0.913 | 96.70% | 97.73% | `{"filegroups/native": 0.9992499947547913, "filetypes/elf": 0.9984168410301208, "general": 0.9962329864501953}` |
| filetypes/ole | joint_or_at_fp_0 | 1915 | 5594 | 92.48% | 0 | 0.00 | 535.38 | 0.000 | 96.09% | 98.08% | `{"filetypes/ole": 0.9836302399635315, "general": 0.966600775718689}` |
| filetypes/package.json | joint_or_at_fp_0 | 18113 | 12595 | 89.06% | 0 | 0.00 | 237.82 | 0.000 | 94.21% | 93.55% | `{"filegroups/config": 0.9997130036354065, "general": 0.9963971972465515}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2060 | 53975 | 88.16% | 0 | 0.00 | 55.50 | 0.000 | 93.70% | 99.56% | `{"filetypes/python-bytecode": 0.9988518953323364, "general": 0.9484255313873291}` |
| filetypes/7z | joint_or_at_fp_0 | 4396 | 88 | 87.74% | 0 | 0.00 | 33469.49 | 0.000 | 93.47% | 87.98% | `{"general": 0.8118060231208801}` |
| filetypes/shell | joint_or_at_fp_2 | 8040 | 47837 | 83.28% | 2 | 41.81 | 131.60 | 0.609 | 90.87% | 97.59% | `{"filegroups/scripts": 0.9936608076095581, "filetypes/shell": 0.9300264716148376, "general": 0.9458252787590027}` |
| filetypes/perl | joint_or_at_fp_0 | 227 | 31851 | 82.82% | 0 | 0.00 | 94.05 | 0.000 | 90.60% | 99.88% | `{"filegroups/scripts": 0.9734857082366943, "filetypes/perl": 0.9864103198051453}` |
| filetypes/zst | calibrate_inherited | 10381 | 16229 | 80.78% | 0 | 0.00 | 184.57 | 0.000 | 89.37% | 92.50% | `{"general": 0.997033953666687}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 62 | 379 | 80.65% | 0 | 0.00 | 7873.15 | 0.000 | 89.29% | 97.28% | `{"filetypes/chrome-manifest": 0.8864092230796814, "general": 0.8742436170578003}` |
| filetypes/macho† | filetype_only | 2147 | 10878 | 76.43% | 0 | 0.00 | 275.36 | 0.000 | 86.64% | 96.12% | `{"filetypes/macho": 0.9637553829645649}` |
| filetypes/javascript | joint_or_at_fp_7 | 91391 | 516880 | 76.26% | 7 | 13.54 | 25.44 | 2.130 | 86.52% | 96.43% | `{"filegroups/scripts": 0.9983312487602234, "filetypes/javascript": 0.9243029952049255, "general": 0.9975904226303101}` |
| filetypes/java_class | joint_or_at_fp_8 | 1335 | 446327 | 75.06% | 8 | 17.92 | 32.34 | 2.434 | 85.46% | 99.92% | `{"filegroups/portable": 0.9995619654655457, "filetypes/java_class": 0.9983499050140381, "general": 0.9755237698554993}` |
| filetypes/rar | calibrate_inherited | 6357 | 4 | 73.79% | 0 | 0.00 | 527129.20 | 0.000 | 84.92% | 73.81% | `{"general": 0.997033953666687}` |
| filetypes/doc | calibrate_inherited | 11040 | 45 | 72.73% | 0 | 0.00 | 64404.29 | 0.000 | 84.21% | 72.84% | `{"filegroups/documents": 0.9462325572967529, "general": 0.997033953666687}` |
| filetypes/docx | joint_or_at_fp_0 | 1623 | 244 | 72.40% | 0 | 0.00 | 12202.53 | 0.000 | 83.99% | 76.00% | `{"filegroups/documents": 0.995581328868866, "filetypes/docx": 0.2577665448188782, "general": 0.9918083548545837}` |
| filetypes/lnk | joint_or_at_fp_0 | 2199 | 1055 | 71.94% | 0 | 0.00 | 2835.53 | 0.000 | 83.68% | 81.04% | `{"filetypes/lnk": 0.6444272994995117, "general": 0.9828563928604126}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 28860 | 13664 | 69.47% | 0 | 0.00 | 219.22 | 0.000 | 81.98% | 79.28% | `{"filetypes/tar.gz": 0.9969723224639893, "general": 0.9970033764839172}` |
| filetypes/pe | learned_blend_at_fp_3 | 919590 | 153831 | 69.31% | 3 | 19.50 | 50.40 | 0.913 | 81.87% | 73.71% | `{}` |
| filetypes/php | joint_or_at_fp_3 | 4021 | 106168 | 68.76% | 3 | 28.26 | 73.03 | 0.913 | 81.46% | 98.86% | `{"filegroups/scripts": 0.9954961538314819, "filetypes/php": 0.9864422082901001, "general": 0.9912244081497192}` |
| filetypes/python | joint_or_at_fp_3 | 18170 | 135406 | 58.74% | 3 | 22.16 | 57.26 | 0.913 | 74.00% | 95.12% | `{"filegroups/scripts": 0.9982014894485474, "filetypes/python": 0.9995548129081726, "general": 0.9948862791061401}` |
| filetypes/jar | joint_or_at_fp_0 | 1523 | 2558 | 56.20% | 0 | 0.00 | 1170.44 | 0.000 | 71.96% | 83.66% | `{"filetypes/jar": 0.9479639530181885, "general": 0.9600642919540405}` |
| filetypes/zip† | filetype_only | 61370 | 8211 | 51.94% | 0 | 0.00 | 364.78 | 0.000 | 68.37% | 57.61% | `{"filetypes/zip": 0.9948407219596067}` |
| filetypes/ruby | joint_or_at_fp_0 | 76 | 24532 | 51.32% | 0 | 0.00 | 122.11 | 0.000 | 67.83% | 99.85% | `{"filegroups/scripts": 0.9915425777435303, "filetypes/ruby": 0.9999542236328125, "general": 0.9834613800048828}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32415 | 44649 | 50.54% | 0 | 0.00 | 67.09 | 0.000 | 67.15% | 79.20% | `{"filegroups/source": 0.8008937239646912, "filetypes/kotlin": 0.6424857974052429, "general": 0.9067947864532471}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 56 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf† | max_rule | 1488 | 480 | 98.19% | 0 | 0.00 | 6221.67 | 0.000 | 99.08% | 98.63% | `{"filegroups/documents": 0.08493378763380678, "filetypes/rtf": 0.08493378763380678, "general": 0.08493378763380678}` |
| filetypes/tar | joint_or_at_fp_0 | 1145 | 436 | 97.47% | 0 | 0.00 | 6847.39 | 0.000 | 98.72% | 98.17% | `{"filetypes/tar": 0.19932818412780762, "general": 0.900611937046051}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1137 | 97.15% | 0 | 0.00 | 2631.30 | 0.000 | 98.55% | 97.43% | `{"filetypes/pkg-info": 0.4571703251162017, "general": 0.08088518457529643}` |
| filetypes/xls | learned_blend_at_fp_0 | 10570 | 20711 | 95.92% | 0 | 0.00 | 144.63 | 0.000 | 97.92% | 98.62% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_3 | 2060 | 53975 | 94.56% | 3 | 55.58 | 143.65 | 0.913 | 97.13% | 99.79% | `{"filetypes/python-bytecode": 0.9976792931556702, "general": 0.9515623450279236}` |
| filetypes/elf | joint_or_at_fp_6 | 82465 | 149754 | 94.36% | 6 | 40.07 | 79.08 | 1.826 | 97.09% | 97.99% | `{"filegroups/native": 0.9992499947547913, "filetypes/elf": 0.9979050159454346, "general": 0.9969760179519653}` |
| filetypes/batch† | filetype_only | 173234 | 3988 | 94.12% | 0 | 0.00 | 750.90 | 0.000 | 96.97% | 94.25% | `{"filetypes/batch": 0.9946941512728201}` |
| filetypes/ole | joint_or_at_fp_0 | 1915 | 5594 | 92.48% | 0 | 0.00 | 535.38 | 0.000 | 96.09% | 98.08% | `{"filetypes/ole": 0.9836302399635315, "general": 0.966600775718689}` |
| filetypes/package.json† | group_only | 18113 | 12595 | 89.89% | 1 | 79.40 | 376.59 | 0.304 | 94.67% | 94.03% | `{"filegroups/config": 0.9996566933136564}` |
| filetypes/7z | joint_or_at_fp_0 | 4396 | 88 | 87.74% | 0 | 0.00 | 33469.49 | 0.000 | 93.47% | 87.98% | `{"general": 0.8118060231208801}` |
| filetypes/zst† | or_general_primary | 10381 | 16229 | 87.14% | 1 | 61.62 | 292.27 | 0.304 | 93.12% | 94.98% | `{"general": 0.9422164559364319}` |
| filetypes/java_class | learned_blend_at_fp_11 | 1335 | 446327 | 85.92% | 13 | 29.13 | 46.31 | 3.955 | 91.94% | 99.96% | `{}` |
| filetypes/shell | joint_or_at_fp_3 | 8040 | 47837 | 84.30% | 3 | 62.71 | 162.08 | 0.913 | 91.46% | 97.74% | `{"filegroups/scripts": 0.9938329458236694, "filetypes/shell": 0.9021183848381042, "general": 0.9460817575454712}` |
| filetypes/perl | joint_or_at_fp_0 | 227 | 31851 | 82.82% | 0 | 0.00 | 94.05 | 0.000 | 90.60% | 99.88% | `{"filegroups/scripts": 0.9734857082366943, "filetypes/perl": 0.9864103198051453}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 62 | 379 | 80.65% | 0 | 0.00 | 7873.15 | 0.000 | 89.29% | 97.28% | `{"filetypes/chrome-manifest": 0.8864092230796814, "general": 0.8742436170578003}` |
| filetypes/javascript | joint_or_at_fp_12 | 91391 | 516880 | 78.07% | 12 | 23.22 | 37.61 | 3.651 | 87.68% | 96.70% | `{"filegroups/scripts": 0.9983312487602234, "filetypes/javascript": 0.9080305099487305, "general": 0.9975904226303101}` |
| filetypes/macho† | filetype_only | 2147 | 10878 | 77.88% | 0 | 0.00 | 275.36 | 0.000 | 87.56% | 96.35% | `{"filetypes/macho": 0.9559758060500917}` |
| filetypes/rar | calibrate_inherited | 6357 | 4 | 74.61% | 0 | 0.00 | 527129.20 | 0.000 | 85.46% | 74.63% | `{"general": 0.9968461990356445}` |
| filetypes/doc | calibrate_inherited | 11040 | 45 | 72.73% | 0 | 0.00 | 64404.29 | 0.000 | 84.21% | 72.84% | `{"filegroups/documents": 0.9462325572967529, "general": 0.9968461990356445}` |
| filetypes/docx | joint_or_at_fp_0 | 1623 | 244 | 72.40% | 0 | 0.00 | 12202.53 | 0.000 | 83.99% | 76.00% | `{"filegroups/documents": 0.995581328868866, "filetypes/docx": 0.2577665448188782, "general": 0.9918083548545837}` |
| filetypes/php | joint_or_at_fp_7 | 4021 | 106168 | 71.97% | 7 | 65.93 | 123.84 | 2.130 | 83.62% | 98.97% | `{"filetypes/php": 0.9786117672920227, "general": 0.9912244081497192}` |
| filetypes/lnk | joint_or_at_fp_0 | 2199 | 1055 | 71.94% | 0 | 0.00 | 2835.53 | 0.000 | 83.68% | 81.04% | `{"filetypes/lnk": 0.6444272994995117, "general": 0.9828563928604126}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 28860 | 13664 | 69.47% | 0 | 0.00 | 219.22 | 0.000 | 81.98% | 79.28% | `{"filetypes/tar.gz": 0.9969723224639893, "general": 0.9970033764839172}` |
| filetypes/pe | learned_blend_at_fp_3 | 919590 | 153831 | 69.31% | 3 | 19.50 | 50.40 | 0.913 | 81.87% | 73.71% | `{}` |
| filetypes/python | joint_or_at_fp_9 | 18170 | 135406 | 67.02% | 9 | 66.47 | 115.98 | 2.738 | 80.23% | 96.09% | `{"filegroups/scripts": 0.9983513355255127, "filetypes/python": 0.9980587363243103, "general": 0.9948862791061401}` |
| filetypes/jar | joint_or_at_fp_0 | 1523 | 2558 | 56.20% | 0 | 0.00 | 1170.44 | 0.000 | 71.96% | 83.66% | `{"filetypes/jar": 0.9479639530181885, "general": 0.9600642919540405}` |
| filetypes/kotlin | joint_or_at_fp_4 | 32415 | 44649 | 54.22% | 4 | 89.59 | 205.00 | 1.217 | 70.31% | 80.74% | `{"filegroups/source": 0.7787376046180725, "filetypes/kotlin": 0.2600405812263489, "general": 0.9086011052131653}` |
| filetypes/zip† | filetype_only | 61370 | 8211 | 52.18% | 0 | 0.00 | 364.78 | 0.000 | 68.58% | 57.82% | `{"filetypes/zip": 0.9946607494628015}` |
| filetypes/ruby | joint_or_at_fp_0 | 76 | 24532 | 51.32% | 0 | 0.00 | 122.11 | 0.000 | 67.83% | 99.85% | `{"filegroups/scripts": 0.9915425777435303, "filetypes/ruby": 0.9999542236328125, "general": 0.9834613800048828}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 56 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9922753572463989}` |
| filetypes/package.json | learned_blend_at_fp_3 | 18113 | 12595 | 98.93% | 3 | 238.19 | 615.50 | 0.913 | 99.46% | 99.36% | `{}` |
| filetypes/batch | joint_or_at_fp_0 | 173234 | 3988 | 98.80% | 0 | 0.00 | 750.90 | 0.000 | 99.40% | 98.83% | `{"filegroups/scripts": 0.9966073036193848, "filetypes/batch": 0.99470055103302, "general": 0.9811878204345703}` |
| filetypes/rtf† | max_rule | 1488 | 480 | 98.19% | 0 | 0.00 | 6221.67 | 0.000 | 99.08% | 98.63% | `{"filegroups/documents": 0.08253136367295094, "filetypes/rtf": 0.08253136367295094, "general": 0.08253136367295094}` |
| filetypes/tar | joint_or_at_fp_0 | 1145 | 436 | 97.47% | 0 | 0.00 | 6847.39 | 0.000 | 98.72% | 98.17% | `{"filetypes/tar": 0.19932818412780762, "general": 0.900611937046051}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1137 | 97.16% | 0 | 0.00 | 2631.30 | 0.000 | 98.56% | 97.43% | `{"filetypes/pkg-info": 0.21777706189928275, "general": 0.04232543761346173}` |
| filetypes/elf | learned_blend_at_fp_22 | 82465 | 149754 | 97.02% | 22 | 146.91 | 209.77 | 6.694 | 98.47% | 98.93% | `{}` |
| filetypes/xls | learned_blend_at_fp_6 | 10570 | 20711 | 96.93% | 5 | 241.42 | 507.54 | 1.521 | 98.41% | 98.95% | `{}` |
| filetypes/python-bytecode† | specialist_primary_with_escape | 2060 | 53975 | 95.00% | 6 | 111.16 | 219.39 | 1.826 | 97.29% | 99.81% | `{"filetypes/python-bytecode": 0.9976792931556702, "general": 0.9372822046279907}` |
| filetypes/java_class | learned_blend_at_fp_48 | 1335 | 446327 | 94.16% | 47 | 105.30 | 134.28 | 14.300 | 95.26% | 99.97% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 1915 | 5594 | 92.48% | 0 | 0.00 | 535.38 | 0.000 | 96.09% | 98.08% | `{"filetypes/ole": 0.9836302399635315, "general": 0.966600775718689}` |
| filetypes/7z | joint_or_at_fp_0 | 4396 | 88 | 87.74% | 0 | 0.00 | 33469.49 | 0.000 | 93.47% | 87.98% | `{"general": 0.8118060231208801}` |
| filetypes/zst† | or_general_primary | 10381 | 16229 | 87.14% | 1 | 61.62 | 292.27 | 0.304 | 93.12% | 94.98% | `{"general": 0.9422164559364319}` |
| filetypes/shell | joint_or_at_fp_9 | 8040 | 47837 | 85.88% | 9 | 188.14 | 328.28 | 2.738 | 92.35% | 97.95% | `{"filegroups/scripts": 0.9938526153564453, "filetypes/shell": 0.8250308036804199, "general": 0.9460817575454712}` |
| filetypes/perl | joint_or_at_fp_5 | 227 | 31851 | 85.46% | 5 | 156.98 | 330.04 | 1.521 | 91.08% | 99.88% | `{"filegroups/scripts": 0.9734857082366943, "filetypes/perl": 0.9815962910652161}` |
| filetypes/macho | joint_or_at_fp_3 | 2147 | 10878 | 84.77% | 3 | 275.79 | 712.63 | 0.913 | 91.69% | 97.47% | `{"filetypes/macho": 0.8447932004928589, "general": 0.9192343950271606}` |
| filetypes/javascript | joint_or_at_fp_58 | 91391 | 516880 | 83.21% | 58 | 112.21 | 139.64 | 17.647 | 90.81% | 97.47% | `{"filegroups/scripts": 0.9974867105484009, "filetypes/javascript": 0.7621225118637085, "general": 0.9917900562286377}` |
| filetypes/tar.gz | joint_or_at_fp_3 | 28860 | 13664 | 82.54% | 3 | 219.56 | 567.35 | 0.913 | 90.43% | 88.15% | `{"filetypes/tar.gz": 0.9920740127563477, "general": 0.9970124959945679}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 62 | 379 | 80.65% | 0 | 0.00 | 7873.15 | 0.000 | 89.29% | 97.28% | `{"filetypes/chrome-manifest": 0.8864092230796814, "general": 0.8742436170578003}` |
| filetypes/rar | calibrate_inherited | 6357 | 4 | 79.06% | 0 | 0.00 | 527129.20 | 0.000 | 88.31% | 79.08% | `{"general": 0.9922753572463989}` |
| filetypes/ruby† | specialist_primary_with_escape | 76 | 24532 | 77.63% | 5 | 203.82 | 428.50 | 1.521 | 84.29% | 99.91% | `{"filegroups/scripts": 0.991405725479126, "filetypes/ruby": 0.9998947381973267, "general": 0.8616284728050232}` |
| filetypes/php | joint_or_at_fp_13 | 4021 | 106168 | 74.66% | 13 | 122.45 | 194.67 | 3.955 | 85.33% | 99.06% | `{"filetypes/php": 0.9651328921318054, "general": 0.9912244081497192}` |
| filetypes/pe | specialist_primary_with_escape | 919590 | 153831 | 73.77% | 21 | 136.51 | 196.58 | 6.389 | 84.90% | 77.53% | `{"filegroups/native": 0.9995330572128296, "filetypes/pe": 0.9994704127311707, "general": 0.9977425932884216}` |
| filetypes/doc | calibrate_inherited | 11040 | 45 | 72.73% | 0 | 0.00 | 64404.29 | 0.000 | 84.21% | 72.84% | `{"filegroups/documents": 0.9462325572967529, "general": 0.9922753572463989}` |
| filetypes/docx | joint_or_at_fp_0 | 1623 | 244 | 72.40% | 0 | 0.00 | 12202.53 | 0.000 | 83.99% | 76.00% | `{"filegroups/documents": 0.995581328868866, "filetypes/docx": 0.2577665448188782, "general": 0.9918083548545837}` |
| filetypes/lnk | joint_or_at_fp_0 | 2199 | 1055 | 71.94% | 0 | 0.00 | 2835.53 | 0.000 | 83.68% | 81.04% | `{"filetypes/lnk": 0.6444272994995117, "general": 0.9828563928604126}` |
| filetypes/pdf | learned_blend_at_fp_3 | 177135 | 13939 | 71.42% | 4 | 286.96 | 656.56 | 1.217 | 83.33% | 73.50% | `{}` |
| filetypes/python | joint_or_at_fp_17 | 18170 | 135406 | 70.22% | 17 | 125.55 | 188.31 | 5.172 | 82.46% | 96.47% | `{"filegroups/scripts": 0.9972741007804871, "filetypes/python": 0.996508777141571, "general": 0.9924877882003784}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 217 | 66.67% | 0 | 0.00 | 13710.36 | 0.000 | 80.00% | 99.55% | `{"general": 0.9922753572463989}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 56 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9895492196083069}` |
| filetypes/package.json | learned_blend_at_fp_3 | 18113 | 12595 | 98.93% | 3 | 238.19 | 615.50 | 0.913 | 99.46% | 99.36% | `{}` |
| filetypes/batch | joint_or_at_fp_3 | 173234 | 3988 | 98.87% | 3 | 752.26 | 1943.09 | 0.913 | 99.43% | 98.90% | `{"filegroups/scripts": 0.9966073036193848, "filetypes/batch": 0.9863048791885376, "general": 0.9811878204345703}` |
| filetypes/rtf† | max_rule | 1488 | 480 | 98.19% | 0 | 0.00 | 6221.67 | 0.000 | 99.08% | 98.63% | `{"filegroups/documents": 0.08149569722701493, "filetypes/rtf": 0.08149569722701493, "general": 0.08149569722701493}` |
| filetypes/python-bytecode | joint_or_at_fp_12 | 2060 | 53975 | 98.11% | 12 | 222.33 | 360.19 | 3.651 | 98.75% | 99.91% | `{"filetypes/python-bytecode": 0.8024982213973999}` |
| filetypes/elf | learned_blend_at_fp_33 | 82465 | 149754 | 97.40% | 33 | 220.36 | 294.64 | 10.040 | 98.66% | 99.06% | `{}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1137 | 97.16% | 0 | 0.00 | 2631.30 | 0.000 | 98.56% | 97.43% | `{"filetypes/pkg-info": 0.17360176359468804, "general": 0.03496789116981309}` |
| filetypes/xls | learned_blend_at_fp_3 | 10570 | 20711 | 96.67% | 2 | 96.57 | 303.95 | 0.609 | 98.30% | 98.87% | `{}` |
| filetypes/java_class | joint_or_at_fp_66 | 1335 | 446327 | 95.21% | 66 | 147.87 | 181.50 | 20.081 | 95.13% | 99.97% | `{"filegroups/portable": 0.939242959022522, "filetypes/java_class": 0.384799063205719}` |
| filetypes/ole | filetype_only_at_fp_3 | 1915 | 5594 | 93.68% | 4 | 715.05 | 1635.56 | 1.217 | 96.63% | 98.34% | `{"filetypes/ole": 0.5541327595710754}` |
| filetypes/tar† | filetype_only | 1145 | 436 | 88.30% | 0 | 0.00 | 6847.39 | 0.000 | 93.78% | 91.52% | `{"filetypes/tar": 0.9365685462398945}` |
| filetypes/ruby | joint_or_at_fp_9 | 76 | 24532 | 88.16% | 9 | 366.87 | 640.11 | 2.738 | 88.16% | 99.93% | `{"filetypes/ruby": 0.9997696280479431, "general": 0.8493431806564331}` |
| filetypes/7z | joint_or_at_fp_0 | 4396 | 88 | 87.74% | 0 | 0.00 | 33469.49 | 0.000 | 93.47% | 87.98% | `{"general": 0.8118060231208801}` |
| filetypes/zst† | or_general_primary | 10381 | 16229 | 87.14% | 2 | 123.24 | 387.88 | 0.609 | 93.12% | 94.98% | `{"general": 0.9386515617370605}` |
| filetypes/shell | joint_or_at_fp_12 | 8040 | 47837 | 86.65% | 12 | 250.85 | 406.40 | 3.651 | 92.78% | 98.06% | `{"filegroups/scripts": 0.9938526153564453, "filetypes/shell": 0.7835757732391357, "general": 0.9460817575454712}` |
| filetypes/perl | joint_or_at_fp_7 | 227 | 31851 | 85.90% | 7 | 219.77 | 412.76 | 2.130 | 90.91% | 99.88% | `{"filegroups/scripts": 0.9734857082366943, "filetypes/perl": 0.9797120690345764}` |
| filetypes/javascript | joint_or_at_fp_94 | 91391 | 516880 | 85.13% | 94 | 181.86 | 215.87 | 28.600 | 91.91% | 97.75% | `{"filegroups/scripts": 0.9947445392608643, "filetypes/javascript": 0.6837907433509827, "general": 0.9917906522750854}` |
| filetypes/macho | joint_or_at_fp_3 | 2147 | 10878 | 84.77% | 3 | 275.79 | 712.63 | 0.913 | 91.69% | 97.47% | `{"filetypes/macho": 0.8447932004928589, "general": 0.9192343950271606}` |
| filetypes/tar.gz | joint_or_at_fp_4 | 28860 | 13664 | 83.65% | 4 | 292.74 | 669.77 | 1.217 | 91.09% | 88.90% | `{"filetypes/tar.gz": 0.9908198714256287, "general": 0.9970124959945679}` |
| filetypes/pe | learned_blend_at_fp_44 | 919590 | 153831 | 83.16% | 44 | 286.03 | 367.74 | 13.387 | 90.81% | 85.57% | `{}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 62 | 379 | 80.65% | 0 | 0.00 | 7873.15 | 0.000 | 89.29% | 97.28% | `{"filetypes/chrome-manifest": 0.8864092230796814, "general": 0.8742436170578003}` |
| filetypes/rar | calibrate_inherited | 6357 | 4 | 80.45% | 0 | 0.00 | 527129.20 | 0.000 | 89.16% | 80.46% | `{"general": 0.9895492196083069}` |
| filetypes/python | learned_blend_at_fp_29 | 18170 | 135406 | 77.47% | 28 | 206.79 | 283.50 | 8.519 | 87.23% | 97.32% | `{}` |
| filetypes/php | joint_or_at_fp_29 | 4021 | 106168 | 76.70% | 29 | 273.15 | 372.42 | 8.823 | 86.46% | 99.12% | `{"filetypes/php": 0.9469060897827148, "general": 0.9231586456298828}` |
| filetypes/doc | calibrate_inherited | 11040 | 45 | 72.73% | 0 | 0.00 | 64404.29 | 0.000 | 84.21% | 72.84% | `{"filegroups/documents": 0.9462325572967529, "general": 0.9895492196083069}` |
| filetypes/docx | joint_or_at_fp_0 | 1623 | 244 | 72.40% | 0 | 0.00 | 12202.53 | 0.000 | 83.99% | 76.00% | `{"filegroups/documents": 0.995581328868866, "filetypes/docx": 0.2577665448188782, "general": 0.9918083548545837}` |
| filetypes/lnk | joint_or_at_fp_0 | 2199 | 1055 | 71.94% | 0 | 0.00 | 2835.53 | 0.000 | 83.68% | 81.04% | `{"filetypes/lnk": 0.6444272994995117, "general": 0.9828563928604126}` |
| filetypes/pdf | learned_blend_at_fp_5 | 177135 | 13939 | 71.85% | 5 | 358.71 | 754.07 | 1.521 | 83.62% | 73.90% | `{}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 217 | 66.67% | 0 | 0.00 | 13710.36 | 0.000 | 80.00% | 99.55% | `{"general": 0.9895492196083069}` |
