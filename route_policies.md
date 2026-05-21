# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1384435807`
- Rows: 4727598 (1703195 malware, 3024403 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1033 | 99.65% | 0 | 0.00 | 2895.83 | 0.000 | 99.83% | 99.68% | `{"filetypes/pkg-info": 0.7854055166244507, "general": 0.33910366892814636}` |
| filetypes/batch | learned_blend_at_fp_0 | 168941 | 3679 | 99.53% | 0 | 0.00 | 813.95 | 0.000 | 99.76% | 99.54% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 10500 | 51 | 99.42% | 0 | 0.00 | 57047.95 | 0.000 | 99.71% | 99.42% | `{"filegroups/documents": 0.5832405686378479}` |
| filetypes/elf | joint_or_at_fp_3 | 73175 | 135583 | 98.82% | 3 | 22.13 | 57.19 | 0.992 | 99.40% | 99.59% | `{"filegroups/native": 0.9736478924751282, "filetypes/elf": 0.9922735095024109, "general": 0.9962420463562012}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 98.77% | 0 | 0.00 | 84339.64 | 0.000 | 99.38% | 98.77% | `{"filegroups/documents": 0.9792848825454712, "general": 0.9978994131088257}` |
| filetypes/pdf | joint_or_at_fp_0 | 173215 | 13863 | 98.24% | 0 | 0.00 | 216.07 | 0.000 | 99.11% | 98.37% | `{"filegroups/documents": 0.9845300316810608, "filetypes/pdf": 0.9944063425064087, "general": 0.9771459102630615}` |
| filetypes/rtf† | filetype_only | 1465 | 480 | 97.88% | 0 | 0.00 | 6221.67 | 0.000 | 98.93% | 98.41% | `{"filetypes/rtf": 0.8121432444852511}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31544 | 97.77% | 0 | 0.00 | 94.97 | 0.000 | 98.87% | 99.98% | `{"filegroups/scripts": 0.9063920974731445, "filetypes/perl": 0.9953130483627319}` |
| filetypes/kotlin | learned_blend_at_fp_2 | 23493 | 42530 | 97.54% | 2 | 47.03 | 148.02 | 0.661 | 98.75% | 99.12% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5357 | 96.21% | 0 | 0.00 | 559.06 | 0.000 | 98.07% | 99.00% | `{"filetypes/ole": 0.9834133982658386, "general": 0.9621371626853943}` |
| filetypes/php | joint_or_at_fp_4 | 3858 | 86590 | 96.19% | 4 | 46.19 | 105.71 | 1.323 | 98.01% | 99.83% | `{"filetypes/php": 0.9661107659339905}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 95.89% | 0 | 0.00 | 123.09 | 0.000 | 97.90% | 99.99% | `{"filetypes/ruby": 0.9890751242637634}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1868 | 30924 | 95.29% | 0 | 0.00 | 96.87 | 0.000 | 97.59% | 99.73% | `{"filetypes/python-bytecode": 0.9981957077980042, "general": 0.8947155475616455}` |
| filetypes/macho | joint_or_at_fp_0 | 2067 | 10693 | 94.58% | 0 | 0.00 | 280.12 | 0.000 | 97.22% | 99.12% | `{"filegroups/native": 0.7882245779037476, "filetypes/macho": 0.9929016828536987, "general": 0.9700344800949097}` |
| filetypes/javascript | learned_blend_at_fp_23 | 84394 | 472467 | 94.34% | 23 | 48.68 | 68.97 | 7.605 | 97.08% | 99.14% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 17793 | 11626 | 93.32% | 0 | 0.00 | 257.64 | 0.000 | 96.55% | 95.96% | `{"filegroups/config": 0.9997425675392151, "filetypes/package.json": 0.9972746968269348, "general": 0.9954510927200317}` |
| filetypes/groovy | learned_blend_at_fp_0 | 123 | 5044 | 91.06% | 0 | 0.00 | 593.74 | 0.000 | 95.32% | 99.79% | `{}` |
| filetypes/pe | learned_blend_at_fp_3 | 901748 | 151968 | 90.64% | 3 | 19.74 | 51.02 | 0.992 | 95.09% | 91.99% | `{}` |
| filetypes/shell | learned_blend_at_fp_2 | 6881 | 45524 | 88.84% | 0 | 0.00 | 65.80 | 0.000 | 94.09% | 98.53% | `{}` |
| filetypes/docx | learned_blend_at_fp_0 | 1578 | 244 | 86.76% | 0 | 0.00 | 12202.53 | 0.000 | 92.91% | 88.53% | `{}` |
| filetypes/java_class | joint_or_at_fp_4 | 1312 | 381309 | 85.67% | 4 | 10.49 | 24.01 | 1.323 | 92.13% | 99.95% | `{"filetypes/java_class": 0.9993467330932617, "general": 0.9855455756187439}` |
| filetypes/python | joint_or_at_fp_3 | 17917 | 130226 | 84.18% | 3 | 23.04 | 59.54 | 0.992 | 91.40% | 98.08% | `{"filegroups/scripts": 0.9977817535400391, "filetypes/python": 0.994220495223999, "general": 0.9954965114593506}` |
| filetypes/csharp | joint_or_at_fp_3 | 1766 | 60097 | 80.46% | 3 | 49.92 | 129.01 | 0.992 | 89.09% | 99.44% | `{"filetypes/csharp": 0.9835713505744934}` |
| filetypes/jar | joint_or_at_fp_0 | 1465 | 2130 | 80.14% | 0 | 0.00 | 1405.46 | 0.000 | 88.97% | 91.91% | `{"filetypes/jar": 0.9813963174819946, "general": 0.9893839359283447}` |
| filetypes/msi | learned_blend_at_fp_2 | 1808 | 133 | 77.60% | 0 | 0.00 | 22272.52 | 0.000 | 87.39% | 79.13% | `{}` |
| filetypes/xlsx | joint_or_at_fp_0 | 17783 | 144 | 73.57% | 0 | 0.00 | 20588.79 | 0.000 | 84.77% | 73.78% | `{"filegroups/documents": 0.9967986345291138, "general": 0.9925695061683655}` |
| filetypes/tar | calibrate_inherited | 1119 | 407 | 72.39% | 0 | 0.00 | 7333.50 | 0.000 | 83.98% | 79.75% | `{"general": 0.9978994131088257}` |
| filetypes/7z | calibrate_inherited | 4304 | 78 | 70.82% | 0 | 0.00 | 37678.63 | 0.000 | 82.92% | 71.34% | `{"general": 0.9978994131088257}` |
| filetypes/vbs | joint_or_at_fp_0 | 3731 | 3282 | 70.28% | 0 | 0.00 | 912.36 | 0.000 | 82.54% | 84.19% | `{"filetypes/vbs": 0.991520881652832, "general": 0.9941376447677612}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 69.60% | 0 | 0.00 | 2907.07 | 0.000 | 82.08% | 79.86% | `{"filetypes/lnk": 0.7399867177009583, "general": 0.9830858707427979}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1033 | 99.65% | 0 | 0.00 | 2895.83 | 0.000 | 99.83% | 99.68% | `{"filetypes/pkg-info": 0.7854055166244507, "general": 0.33910366892814636}` |
| filetypes/batch | learned_blend_at_fp_0 | 168941 | 3679 | 99.53% | 0 | 0.00 | 813.95 | 0.000 | 99.76% | 99.54% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_2 | 1868 | 30924 | 99.52% | 2 | 64.67 | 203.58 | 0.661 | 99.71% | 99.97% | `{"filetypes/python-bytecode": 0.8812922835350037}` |
| filetypes/xls | joint_or_at_fp_0 | 10500 | 51 | 99.42% | 0 | 0.00 | 57047.95 | 0.000 | 99.71% | 99.42% | `{"filegroups/documents": 0.5832405686378479}` |
| filetypes/elf | joint_or_at_fp_4 | 73175 | 135583 | 99.26% | 4 | 29.50 | 67.51 | 1.323 | 99.62% | 99.74% | `{"filegroups/native": 0.9736478924751282, "filetypes/elf": 0.9848151206970215}` |
| filetypes/perl | learned_blend_at_fp_3 | 224 | 31544 | 99.11% | 2 | 63.40 | 199.57 | 0.661 | 99.11% | 99.99% | `{}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 98.77% | 0 | 0.00 | 84339.64 | 0.000 | 99.38% | 98.77% | `{"filegroups/documents": 0.9792848825454712, "general": 0.9965662956237793}` |
| filetypes/pdf† | group_only | 173215 | 13863 | 98.25% | 1 | 72.13 | 342.15 | 0.331 | 99.12% | 98.38% | `{"filegroups/documents": 0.9844970703125}` |
| filetypes/rtf† | filetype_only | 1465 | 480 | 97.88% | 0 | 0.00 | 6221.67 | 0.000 | 98.93% | 98.41% | `{"filetypes/rtf": 0.7917833771658196}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 23493 | 42530 | 97.87% | 3 | 70.54 | 182.30 | 0.992 | 98.92% | 99.24% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5357 | 96.21% | 0 | 0.00 | 559.06 | 0.000 | 98.07% | 99.00% | `{"filetypes/ole": 0.9834133982658386, "general": 0.9621371626853943}` |
| filetypes/php | joint_or_at_fp_4 | 3858 | 86590 | 96.19% | 4 | 46.19 | 105.71 | 1.323 | 98.01% | 99.83% | `{"filetypes/php": 0.9661107659339905}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 95.89% | 0 | 0.00 | 123.09 | 0.000 | 97.90% | 99.99% | `{"filetypes/ruby": 0.9890751242637634}` |
| filetypes/macho | joint_or_at_fp_0 | 2067 | 10693 | 94.58% | 0 | 0.00 | 280.12 | 0.000 | 97.22% | 99.12% | `{"filegroups/native": 0.7882245779037476, "filetypes/macho": 0.9929016828536987, "general": 0.9700344800949097}` |
| filetypes/javascript | learned_blend_at_fp_23 | 84394 | 472467 | 94.34% | 23 | 48.68 | 68.97 | 7.605 | 97.08% | 99.14% | `{}` |
| filetypes/pe | learned_blend_at_fp_6 | 901748 | 151968 | 94.32% | 6 | 39.48 | 77.93 | 1.984 | 97.08% | 95.14% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 17793 | 11626 | 93.32% | 0 | 0.00 | 257.64 | 0.000 | 96.55% | 95.96% | `{"filegroups/config": 0.9997425675392151, "filetypes/package.json": 0.9972746968269348, "general": 0.9954510927200317}` |
| filetypes/groovy | learned_blend_at_fp_0 | 123 | 5044 | 91.06% | 0 | 0.00 | 593.74 | 0.000 | 95.32% | 99.79% | `{}` |
| filetypes/shell | joint_or_at_fp_3 | 6881 | 45524 | 91.00% | 3 | 65.90 | 170.31 | 0.992 | 95.27% | 98.81% | `{"filegroups/scripts": 0.9848358035087585, "filetypes/shell": 0.9736726880073547, "general": 0.9656938314437866}` |
| filetypes/java_class | joint_or_at_fp_8 | 1312 | 381309 | 89.71% | 8 | 20.98 | 37.86 | 2.645 | 94.27% | 99.96% | `{"filetypes/java_class": 0.9985633492469788, "general": 0.9855455756187439}` |
| filetypes/zst† | or_general_primary | 10381 | 16156 | 87.19% | 1 | 61.90 | 293.59 | 0.331 | 93.15% | 94.98% | `{"general": 0.9107430577278137}` |
| filetypes/docx | learned_blend_at_fp_0 | 1578 | 244 | 86.76% | 0 | 0.00 | 12202.53 | 0.000 | 92.91% | 88.53% | `{}` |
| filetypes/python | joint_or_at_fp_5 | 17917 | 130226 | 85.85% | 5 | 38.39 | 80.73 | 1.653 | 92.37% | 98.28% | `{"filegroups/scripts": 0.9967427849769592, "filetypes/python": 0.9921128749847412, "general": 0.9954965114593506}` |
| filetypes/csharp | joint_or_at_fp_3 | 1766 | 60097 | 80.46% | 3 | 49.92 | 129.01 | 0.992 | 89.09% | 99.44% | `{"filetypes/csharp": 0.9835713505744934}` |
| filetypes/jar | joint_or_at_fp_0 | 1465 | 2130 | 80.14% | 0 | 0.00 | 1405.46 | 0.000 | 88.97% | 91.91% | `{"filetypes/jar": 0.9813963174819946, "general": 0.9893839359283447}` |
| filetypes/tar | calibrate_inherited | 1119 | 407 | 78.46% | 0 | 0.00 | 7333.50 | 0.000 | 87.93% | 84.21% | `{"general": 0.9965662956237793}` |
| filetypes/msi | learned_blend_at_fp_2 | 1808 | 133 | 77.60% | 0 | 0.00 | 22272.52 | 0.000 | 87.39% | 79.13% | `{}` |
| filetypes/7z | calibrate_inherited | 4304 | 78 | 75.53% | 0 | 0.00 | 37678.63 | 0.000 | 86.06% | 75.97% | `{"general": 0.9965662956237793}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 73.90% | 0 | 0.00 | 527129.20 | 0.000 | 84.99% | 73.92% | `{"general": 0.9965662956237793}` |
| filetypes/xlsx | joint_or_at_fp_0 | 17783 | 144 | 73.57% | 0 | 0.00 | 20588.79 | 0.000 | 84.77% | 73.78% | `{"filegroups/documents": 0.9967986345291138, "general": 0.9925695061683655}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | general_only | 49 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"general": 0.2936785888751801}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.992559552192688}` |
| filetypes/elf | joint_or_at_fp_39 | 73175 | 135583 | 99.98% | 39 | 287.65 | 375.69 | 12.895 | 99.96% | 99.97% | `{"filetypes/elf": 0.42513492703437805}` |
| filetypes/macho | joint_or_at_fp_5 | 2067 | 10693 | 99.56% | 5 | 467.60 | 982.92 | 1.653 | 99.66% | 99.89% | `{"filegroups/native": 0.840020477771759, "filetypes/macho": 0.9078754782676697}` |
| filetypes/batch | learned_blend_at_fp_0 | 168941 | 3679 | 99.53% | 0 | 0.00 | 813.95 | 0.000 | 99.76% | 99.54% | `{}` |
| filetypes/python-bytecode† | max_rule | 1868 | 30924 | 99.52% | 2 | 64.67 | 203.58 | 0.661 | 99.71% | 99.97% | `{"filetypes/python-bytecode": 0.8920788764953613, "general": 0.8920788764953613}` |
| filetypes/xls | joint_or_at_fp_0 | 10500 | 51 | 99.42% | 0 | 0.00 | 57047.95 | 0.000 | 99.71% | 99.42% | `{"filegroups/documents": 0.5832405686378479}` |
| filetypes/package.json | learned_blend_at_fp_3 | 17793 | 11626 | 99.36% | 3 | 258.04 | 666.79 | 0.992 | 99.67% | 99.61% | `{}` |
| filetypes/perl | learned_blend_at_fp_3 | 224 | 31544 | 99.11% | 2 | 63.40 | 199.57 | 0.661 | 99.11% | 99.99% | `{}` |
| filetypes/kotlin | learned_blend_at_fp_19 | 23493 | 42530 | 98.81% | 18 | 423.23 | 627.53 | 5.952 | 99.36% | 99.55% | `{}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 98.77% | 0 | 0.00 | 84339.64 | 0.000 | 99.38% | 98.77% | `{"filegroups/documents": 0.9792848825454712, "general": 0.992559552192688}` |
| filetypes/pkg-info† | filetype_only | 10634 | 1033 | 98.67% | 0 | 0.00 | 2895.83 | 0.000 | 99.33% | 98.79% | `{"filetypes/pkg-info": 0.844245043625501}` |
| filetypes/pdf | learned_blend_at_fp_2 | 173215 | 13863 | 98.54% | 2 | 144.27 | 454.07 | 0.661 | 99.27% | 98.65% | `{}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.02% | 0 | 0.00 | 6221.67 | 0.000 | 99.00% | 98.51% | `{"filegroups/documents": 0.8506083097209275, "filetypes/rtf": 0.8506083097209275, "general": 0.8506083097209275}` |
| filetypes/ruby† | specialist_primary_with_escape | 73 | 24337 | 97.26% | 4 | 164.36 | 376.08 | 1.323 | 95.95% | 99.98% | `{"filegroups/scripts": 0.902569591999054, "filetypes/ruby": 0.9534813165664673, "general": 0.9347168803215027}` |
| filetypes/pe | learned_blend_at_fp_20 | 901748 | 151968 | 97.13% | 19 | 125.03 | 183.45 | 6.282 | 98.54% | 97.54% | `{}` |
| filetypes/php | joint_or_at_fp_11 | 3858 | 86590 | 97.10% | 11 | 127.04 | 210.26 | 3.637 | 98.38% | 99.86% | `{"filetypes/php": 0.9431837797164917}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5357 | 96.21% | 0 | 0.00 | 559.06 | 0.000 | 98.07% | 99.00% | `{"filetypes/ole": 0.9834133982658386, "general": 0.9621371626853943}` |
| filetypes/javascript | learned_blend_at_fp_65 | 84394 | 472467 | 96.17% | 65 | 137.58 | 169.12 | 21.492 | 98.01% | 99.41% | `{}` |
| filetypes/shell | joint_or_at_fp_11 | 6881 | 45524 | 95.28% | 11 | 241.63 | 399.92 | 3.637 | 97.50% | 99.36% | `{"filegroups/scripts": 0.9902028441429138, "filetypes/shell": 0.9299877285957336}` |
| filetypes/java_class | specialist_primary_with_escape | 1312 | 381309 | 94.44% | 41 | 107.52 | 139.51 | 13.556 | 95.60% | 99.97% | `{"filegroups/portable": 0.9949539303779602, "filetypes/java_class": 0.9949539303779602, "general": 0.805182695388794}` |
| filetypes/groovy | learned_blend_at_fp_2 | 123 | 5044 | 93.50% | 2 | 396.51 | 1247.64 | 0.661 | 95.83% | 99.81% | `{}` |
| filetypes/csharp | learned_blend_at_fp_15 | 1766 | 60097 | 93.09% | 15 | 249.60 | 384.30 | 4.960 | 96.00% | 99.78% | `{}` |
| filetypes/python | joint_or_at_fp_15 | 17917 | 130226 | 92.21% | 15 | 115.18 | 177.36 | 4.960 | 95.90% | 99.05% | `{"filetypes/python": 0.9737240076065063}` |
| filetypes/zst† | or_general_primary | 10381 | 16156 | 87.19% | 1 | 61.90 | 293.59 | 0.331 | 93.15% | 94.98% | `{"general": 0.9107430577278137}` |
| filetypes/docx | learned_blend_at_fp_0 | 1578 | 244 | 86.76% | 0 | 0.00 | 12202.53 | 0.000 | 92.91% | 88.53% | `{}` |
| filetypes/tar | calibrate_inherited | 1119 | 407 | 86.68% | 0 | 0.00 | 7333.50 | 0.000 | 92.87% | 90.24% | `{"general": 0.992559552192688}` |
| filetypes/lua† | or_general_primary | 48 | 14268 | 81.25% | 1 | 70.09 | 332.44 | 0.331 | 88.64% | 99.93% | `{"filegroups/scripts": 0.5921839169459613, "general": 0.8843883872032166}` |
| filetypes/7z | calibrate_inherited | 4304 | 78 | 80.39% | 0 | 0.00 | 37678.63 | 0.000 | 89.13% | 80.74% | `{"general": 0.992559552192688}` |
| filetypes/jar | joint_or_at_fp_0 | 1465 | 2130 | 80.14% | 0 | 0.00 | 1405.46 | 0.000 | 88.97% | 91.91% | `{"filetypes/jar": 0.9813963174819946, "general": 0.9893839359283447}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | or_general_primary | 49 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.6525903608523271, "general": 0.11719884360397102}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9904892444610596}` |
| filetypes/elf | joint_or_at_fp_41 | 73175 | 135583 | 99.98% | 41 | 302.40 | 392.34 | 13.556 | 99.96% | 99.97% | `{"filetypes/elf": 0.38489651679992676}` |
| filetypes/python-bytecode | joint_or_at_fp_6 | 1868 | 30924 | 99.73% | 6 | 194.02 | 382.92 | 1.984 | 99.71% | 99.97% | `{"filetypes/python-bytecode": 0.4799368679523468}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1033 | 99.65% | 0 | 0.00 | 2895.83 | 0.000 | 99.83% | 99.68% | `{"filetypes/pkg-info": 0.7296848006197075, "general": 0.021295978052146336}` |
| filetypes/macho | joint_or_at_fp_5 | 2067 | 10693 | 99.56% | 5 | 467.60 | 982.92 | 1.653 | 99.66% | 99.89% | `{"filegroups/native": 0.840020477771759, "filetypes/macho": 0.9078754782676697}` |
| filetypes/batch | learned_blend_at_fp_0 | 168941 | 3679 | 99.53% | 0 | 0.00 | 813.95 | 0.000 | 99.76% | 99.54% | `{}` |
| filetypes/package.json | learned_blend_at_fp_4 | 17793 | 11626 | 99.44% | 4 | 344.06 | 787.16 | 1.323 | 99.71% | 99.65% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 10500 | 51 | 99.42% | 0 | 0.00 | 57047.95 | 0.000 | 99.71% | 99.42% | `{"filegroups/documents": 0.5832405686378479}` |
| filetypes/perl | calibrate_inherited | 224 | 31544 | 99.11% | 17 | 538.93 | 808.26 | 5.621 | 95.90% | 99.94% | `{"filegroups/scripts": 0.9443893432617188, "filetypes/perl": 0.3257211148738861, "general": 0.9904892444610596}` |
| filetypes/kotlin | joint_or_at_fp_29 | 23493 | 42530 | 99.01% | 29 | 681.87 | 929.60 | 9.589 | 99.44% | 99.60% | `{"filetypes/kotlin": 0.6651719212532043}` |
| filetypes/pdf | learned_blend_at_fp_3 | 173215 | 13863 | 98.83% | 7 | 504.94 | 948.22 | 2.315 | 99.41% | 98.91% | `{}` |
| filetypes/pe | learned_blend_at_fp_33 | 901748 | 151968 | 98.80% | 32 | 210.57 | 282.83 | 10.581 | 99.39% | 98.97% | `{}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 98.77% | 0 | 0.00 | 84339.64 | 0.000 | 99.38% | 98.77% | `{"filegroups/documents": 0.9792848825454712, "general": 0.9904892444610596}` |
| filetypes/python | joint_or_at_fp_98 | 17917 | 130226 | 98.63% | 98 | 752.54 | 890.04 | 32.403 | 99.04% | 99.77% | `{"filetypes/python": 0.7649770379066467}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.02% | 0 | 0.00 | 6221.67 | 0.000 | 99.00% | 98.51% | `{"filegroups/documents": 0.8252326469588848, "filetypes/rtf": 0.8252326469588848, "general": 0.8252326469588848}` |
| filetypes/php | joint_or_at_fp_15 | 3858 | 86590 | 97.87% | 15 | 173.23 | 266.73 | 4.960 | 98.73% | 99.89% | `{"filetypes/php": 0.9120644330978394}` |
| filetypes/ole | filetype_only_at_fp_3 | 1928 | 5357 | 97.61% | 4 | 746.69 | 1707.88 | 1.323 | 98.69% | 99.31% | `{"filetypes/ole": 0.9227592349052429}` |
| filetypes/ruby† | specialist_primary_with_escape | 73 | 24337 | 97.26% | 4 | 164.36 | 376.08 | 1.323 | 95.95% | 99.98% | `{"filegroups/scripts": 0.902569591999054, "filetypes/ruby": 0.9534813165664673, "general": 0.9347168803215027}` |
| filetypes/javascript | learned_blend_at_fp_115 | 84394 | 472467 | 96.98% | 115 | 243.40 | 284.17 | 38.024 | 98.40% | 99.52% | `{}` |
| filetypes/csharp | joint_or_at_fp_47 | 1766 | 60097 | 96.77% | 47 | 782.07 | 997.20 | 15.540 | 97.05% | 99.83% | `{"filetypes/csharp": 0.8833015561103821}` |
| filetypes/shell | joint_or_at_fp_13 | 6881 | 45524 | 96.13% | 13 | 285.56 | 453.98 | 4.298 | 97.93% | 99.47% | `{"filegroups/scripts": 0.9902028441429138, "filetypes/shell": 0.9120648503303528}` |
| filetypes/java_class | learned_blend_at_fp_53 | 1312 | 381309 | 95.96% | 73 | 191.45 | 232.60 | 24.137 | 95.23% | 99.97% | `{}` |
| filetypes/vbs | joint_or_at_fp_2 | 3731 | 3282 | 94.37% | 2 | 609.38 | 1917.02 | 0.661 | 97.08% | 96.98% | `{"filetypes/vbs": 0.9445592761039734}` |
| filetypes/groovy | learned_blend_at_fp_2 | 123 | 5044 | 93.50% | 2 | 396.51 | 1247.64 | 0.661 | 95.83% | 99.81% | `{}` |
| filetypes/lua† | group_only | 48 | 14268 | 89.58% | 2 | 140.17 | 441.19 | 0.661 | 92.47% | 99.95% | `{"filegroups/scripts": 0.4273364245891571}` |
| filetypes/tar | calibrate_inherited | 1119 | 407 | 88.20% | 0 | 0.00 | 7333.50 | 0.000 | 93.73% | 91.35% | `{"general": 0.9904892444610596}` |
| filetypes/zst† | or_general_primary | 10381 | 16156 | 87.19% | 2 | 123.79 | 389.64 | 0.661 | 93.15% | 94.98% | `{"general": 0.904411256313324}` |
| filetypes/docx | learned_blend_at_fp_0 | 1578 | 244 | 86.76% | 0 | 0.00 | 12202.53 | 0.000 | 92.91% | 88.53% | `{}` |
| filetypes/makefile | calibrate_inherited | 163 | 21581 | 82.21% | 16 | 741.39 | 1125.83 | 5.290 | 85.62% | 99.79% | `{"filegroups/source": 0.6526415944099426, "filetypes/makefile": 0.9309068918228149, "general": 0.9904892444610596}` |
