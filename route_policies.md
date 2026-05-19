# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1310931333`
- Rows: 4682982 (1692465 malware, 2990517 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | learned_blend_at_fp_3 | 168290 | 3602 | 98.77% | 3 | 832.87 | 2151.18 | 1.003 | 99.38% | 98.79% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 1455 | 480 | 98.08% | 0 | 0.00 | 6221.67 | 0.000 | 99.03% | 98.55% | `{"filetypes/rtf": 0.13613398373126984, "general": 0.9704356789588928}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1022 | 97.16% | 0 | 0.00 | 2926.95 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.038695644587278366}` |
| filetypes/xls | joint_or_at_fp_0 | 10475 | 51 | 96.26% | 0 | 0.00 | 57047.95 | 0.000 | 98.09% | 96.28% | `{"filegroups/documents": 0.5229080319404602, "general": 0.5542850494384766}` |
| filetypes/elf | learned_blend_at_fp_0 | 70572 | 134241 | 93.15% | 0 | 0.00 | 22.32 | 0.000 | 96.45% | 97.64% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 17780 | 11022 | 92.41% | 0 | 0.00 | 271.76 | 0.000 | 96.05% | 95.31% | `{"filegroups/config": 0.9993044137954712, "filetypes/package.json": 0.998593807220459, "general": 0.9932883381843567}` |
| filetypes/ole | joint_or_at_fp_0 | 1924 | 5357 | 91.79% | 0 | 0.00 | 559.06 | 0.000 | 95.72% | 97.83% | `{"filetypes/ole": 0.971983015537262, "general": 0.8828756809234619}` |
| filetypes/zst† | general_only | 10381 | 16152 | 84.38% | 1 | 61.91 | 293.67 | 0.334 | 91.53% | 93.89% | `{"general": 0.9945176839828491}` |
| filetypes/macho | learned_blend_at_fp_0 | 2045 | 10672 | 82.69% | 0 | 0.00 | 280.67 | 0.000 | 90.52% | 97.22% | `{}` |
| filetypes/pe | learned_blend_at_fp_3 | 897596 | 151723 | 78.94% | 3 | 19.77 | 51.10 | 1.003 | 88.23% | 81.99% | `{}` |
| filetypes/data | filetype_only_at_fp_0 | 405 | 9024 | 76.05% | 0 | 0.00 | 331.92 | 0.000 | 86.40% | 98.97% | `{"filetypes/data": 0.33864685893058777}` |
| filetypes/tar | calibrate_inherited | 1117 | 400 | 73.41% | 0 | 0.00 | 7461.36 | 0.000 | 84.67% | 80.42% | `{"general": 0.9986128807067871}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31515 | 73.21% | 0 | 0.00 | 95.05 | 0.000 | 84.54% | 99.81% | `{"filegroups/scripts": 0.9746114611625671, "filetypes/perl": 0.9969062209129333}` |
| filetypes/msi | joint_or_at_fp_0 | 1652 | 129 | 73.00% | 0 | 0.00 | 22955.16 | 0.000 | 84.39% | 74.96% | `{"filetypes/msi": 0.4237603545188904, "general": 0.9914309978485107}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.20% | 72.80% | `{"filegroups/documents": 0.9203116297721863, "general": 0.9986128807067871}` |
| filetypes/docx | joint_or_at_fp_0 | 1553 | 244 | 69.93% | 0 | 0.00 | 12202.53 | 0.000 | 82.30% | 74.01% | `{"filegroups/documents": 0.9344643354415894, "filetypes/docx": 0.6182230710983276, "general": 0.9969958066940308}` |
| filetypes/javascript† | filetype_only | 83592 | 468481 | 67.35% | 3 | 6.40 | 16.55 | 1.003 | 80.49% | 95.06% | `{"filetypes/javascript": 0.9872211813926697}` |
| filetypes/7z | calibrate_inherited | 4275 | 78 | 63.25% | 0 | 0.00 | 37678.63 | 0.000 | 77.49% | 63.91% | `{"general": 0.9986128807067871}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 23485 | 61.64% | 0 | 0.00 | 127.55 | 0.000 | 76.27% | 99.88% | `{"filegroups/scripts": 0.9916245341300964, "filetypes/ruby": 0.999415397644043, "general": 0.9674877524375916}` |
| filetypes/shell† | filetype_only | 6515 | 45253 | 59.69% | 0 | 0.00 | 66.20 | 0.000 | 74.76% | 94.93% | `{"filetypes/shell": 0.9911778943880287}` |
| filetypes/jar | joint_or_at_fp_0 | 1459 | 2085 | 59.22% | 0 | 0.00 | 1435.77 | 0.000 | 74.39% | 83.21% | `{"filetypes/jar": 0.892769992351532, "general": 0.9893239140510559}` |
| filetypes/rar | calibrate_inherited | 6090 | 4 | 55.01% | 0 | 0.00 | 527129.20 | 0.000 | 70.97% | 55.04% | `{"general": 0.9986128807067871}` |
| filetypes/python | joint_or_at_fp_0 | 17903 | 129483 | 54.68% | 0 | 0.00 | 23.14 | 0.000 | 70.70% | 94.49% | `{"filegroups/scripts": 0.9971925616264343, "filetypes/python": 0.9979390501976013, "general": 0.99903804063797}` |
| filetypes/php | joint_or_at_fp_0 | 3838 | 84624 | 53.75% | 0 | 0.00 | 35.40 | 0.000 | 69.92% | 97.99% | `{"filegroups/scripts": 0.9949019551277161, "filetypes/php": 0.9974962472915649, "general": 0.996723473072052}` |
| filetypes/tar.gz | calibrate_inherited | 27924 | 12887 | 51.59% | 0 | 0.00 | 232.43 | 0.000 | 68.07% | 66.88% | `{"general": 0.9986128807067871}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23336 | 42240 | 49.88% | 0 | 0.00 | 70.92 | 0.000 | 66.56% | 82.16% | `{"filegroups/source": 0.9805557727813721, "filetypes/kotlin": 0.9480752944946289, "general": 0.9353598952293396}` |
| filetypes/lnk | joint_or_at_fp_0 | 1992 | 1024 | 47.59% | 0 | 0.00 | 2921.24 | 0.000 | 64.49% | 65.38% | `{"filetypes/lnk": 0.9884122610092163, "general": 0.9862244129180908}` |
| filetypes/zip | calibrate_inherited | 59322 | 7245 | 39.75% | 1 | 138.03 | 654.61 | 0.334 | 56.89% | 46.31% | `{"general": 0.9986128807067871}` |
| filetypes/pptx | learned_blend_at_fp_0 | 128 | 191 | 38.28% | 0 | 0.00 | 15562.10 | 0.000 | 55.37% | 75.24% | `{}` |
| filetypes/unknown | filetype_only_at_fp_3 | 11064 | 15945 | 36.80% | 3 | 188.15 | 486.20 | 1.003 | 53.79% | 74.10% | `{"filetypes/unknown": 0.014323970302939415}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | learned_blend_at_fp_3 | 168290 | 3602 | 98.77% | 3 | 832.87 | 2151.18 | 1.003 | 99.38% | 98.79% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 1455 | 480 | 98.08% | 0 | 0.00 | 6221.67 | 0.000 | 99.03% | 98.55% | `{"filetypes/rtf": 0.13613398373126984, "general": 0.9704356789588928}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1022 | 97.16% | 0 | 0.00 | 2926.95 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.038695644587278366}` |
| filetypes/xls | joint_or_at_fp_0 | 10475 | 51 | 96.26% | 0 | 0.00 | 57047.95 | 0.000 | 98.09% | 96.28% | `{"filegroups/documents": 0.5229080319404602, "general": 0.5542850494384766}` |
| filetypes/html† | max_rule | 46 | 7963 | 95.65% | 0 | 0.00 | 376.14 | 0.000 | 97.78% | 99.98% | `{"filegroups/documents": 0.6968451112340149, "general": 0.6968451112340149}` |
| filetypes/elf | joint_or_at_fp_3 | 70572 | 134241 | 95.13% | 3 | 22.35 | 57.76 | 1.003 | 97.50% | 98.32% | `{"filegroups/native": 0.9991791844367981, "filetypes/elf": 0.998521089553833, "general": 0.9919582009315491}` |
| filetypes/package.json | joint_or_at_fp_0 | 17780 | 11022 | 92.41% | 0 | 0.00 | 271.76 | 0.000 | 96.05% | 95.31% | `{"filegroups/config": 0.9993044137954712, "filetypes/package.json": 0.998593807220459, "general": 0.9932883381843567}` |
| filetypes/ole | joint_or_at_fp_0 | 1924 | 5357 | 91.79% | 0 | 0.00 | 559.06 | 0.000 | 95.72% | 97.83% | `{"filetypes/ole": 0.971983015537262, "general": 0.8828756809234619}` |
| filetypes/zst† | general_only | 10381 | 16152 | 84.38% | 1 | 61.91 | 293.67 | 0.334 | 91.53% | 93.89% | `{"general": 0.9945176839828491}` |
| filetypes/macho | learned_blend_at_fp_0 | 2045 | 10672 | 82.69% | 0 | 0.00 | 280.67 | 0.000 | 90.52% | 97.22% | `{}` |
| filetypes/7z† | general_only | 4275 | 78 | 82.48% | 1 | 12820.51 | 59378.49 | 0.334 | 90.39% | 82.77% | `{"general": 0.989359438419342}` |
| filetypes/pe | learned_blend_at_fp_3 | 897596 | 151723 | 78.94% | 3 | 19.77 | 51.10 | 1.003 | 88.23% | 81.99% | `{}` |
| filetypes/shell | joint_or_at_fp_1 | 6515 | 45253 | 78.60% | 1 | 22.10 | 104.83 | 0.334 | 88.01% | 97.31% | `{"filegroups/scripts": 0.9917110204696655, "filetypes/shell": 0.9677558541297913, "general": 0.9742692708969116}` |
| filetypes/data | filetype_only_at_fp_0 | 405 | 9024 | 76.05% | 0 | 0.00 | 331.92 | 0.000 | 86.40% | 98.97% | `{"filetypes/data": 0.33864685893058777}` |
| filetypes/tar | calibrate_inherited | 1117 | 400 | 75.11% | 0 | 0.00 | 7461.36 | 0.000 | 85.79% | 81.67% | `{"general": 0.9982483386993408}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31515 | 73.21% | 0 | 0.00 | 95.05 | 0.000 | 84.54% | 99.81% | `{"filegroups/scripts": 0.9746114611625671, "filetypes/perl": 0.9969062209129333}` |
| filetypes/msi | joint_or_at_fp_0 | 1652 | 129 | 73.00% | 0 | 0.00 | 22955.16 | 0.000 | 84.39% | 74.96% | `{"filetypes/msi": 0.4237603545188904, "general": 0.9914309978485107}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.20% | 72.80% | `{"filegroups/documents": 0.9203116297721863, "general": 0.9982483386993408}` |
| filetypes/docx | joint_or_at_fp_0 | 1553 | 244 | 69.93% | 0 | 0.00 | 12202.53 | 0.000 | 82.30% | 74.01% | `{"filegroups/documents": 0.9344643354415894, "filetypes/docx": 0.6182230710983276, "general": 0.9969958066940308}` |
| filetypes/javascript | joint_or_at_fp_3 | 83592 | 468481 | 67.78% | 3 | 6.40 | 16.55 | 1.003 | 80.79% | 95.12% | `{"filegroups/scripts": 0.9972375631332397, "filetypes/javascript": 0.9867234230041504, "general": 0.9984337091445923}` |
| filetypes/python | joint_or_at_fp_3 | 17903 | 129483 | 63.48% | 3 | 23.17 | 59.88 | 1.003 | 77.65% | 95.56% | `{"filegroups/scripts": 0.9972020387649536, "filetypes/python": 0.9915239810943604}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 23485 | 61.64% | 0 | 0.00 | 127.55 | 0.000 | 76.27% | 99.88% | `{"filegroups/scripts": 0.9916245341300964, "filetypes/ruby": 0.999415397644043, "general": 0.9674877524375916}` |
| filetypes/rar | calibrate_inherited | 6090 | 4 | 60.85% | 0 | 0.00 | 527129.20 | 0.000 | 75.66% | 60.88% | `{"general": 0.9982483386993408}` |
| filetypes/kotlin | joint_or_at_fp_3 | 23336 | 42240 | 60.22% | 3 | 71.02 | 183.55 | 1.003 | 75.17% | 85.84% | `{"filegroups/source": 0.9334213137626648, "filetypes/kotlin": 0.06153268739581108, "general": 0.9473177194595337}` |
| filetypes/jar | joint_or_at_fp_0 | 1459 | 2085 | 59.22% | 0 | 0.00 | 1435.77 | 0.000 | 74.39% | 83.21% | `{"filetypes/jar": 0.892769992351532, "general": 0.9893239140510559}` |
| filetypes/tar.gz | calibrate_inherited | 27924 | 12887 | 54.31% | 1 | 77.60 | 368.06 | 0.334 | 70.39% | 68.74% | `{"general": 0.9982483386993408}` |
| filetypes/php | joint_or_at_fp_0 | 3838 | 84624 | 53.75% | 0 | 0.00 | 35.40 | 0.000 | 69.92% | 97.99% | `{"filegroups/scripts": 0.9949019551277161, "filetypes/php": 0.9974962472915649, "general": 0.996723473072052}` |
| filetypes/lnk | joint_or_at_fp_0 | 1992 | 1024 | 47.59% | 0 | 0.00 | 2921.24 | 0.000 | 64.49% | 65.38% | `{"filetypes/lnk": 0.9884122610092163, "general": 0.9862244129180908}` |
| filetypes/zip | calibrate_inherited | 59322 | 7245 | 42.62% | 1 | 138.03 | 654.61 | 0.334 | 59.76% | 48.86% | `{"general": 0.9982483386993408}` |
| filetypes/pptx | learned_blend_at_fp_0 | 128 | 191 | 38.28% | 0 | 0.00 | 15562.10 | 0.000 | 55.37% | 75.24% | `{}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 46 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.14087531102693135, "general": 0.14087531102693135}` |
| filetypes/batch | learned_blend_at_fp_3 | 168290 | 3602 | 98.77% | 3 | 832.87 | 2151.18 | 1.003 | 99.38% | 98.79% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 1455 | 480 | 98.08% | 0 | 0.00 | 6221.67 | 0.000 | 99.03% | 98.55% | `{"filetypes/rtf": 0.13613398373126984, "general": 0.9704356789588928}` |
| filetypes/package.json | joint_or_at_fp_4 | 17780 | 11022 | 97.68% | 4 | 362.91 | 830.28 | 1.338 | 98.81% | 98.55% | `{"filegroups/config": 0.9987237453460693, "filetypes/package.json": 0.9745490550994873, "general": 0.9932883381843567}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1022 | 97.16% | 0 | 0.00 | 2926.95 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.038695644587278366}` |
| filetypes/xls | joint_or_at_fp_0 | 10475 | 51 | 96.26% | 0 | 0.00 | 57047.95 | 0.000 | 98.09% | 96.28% | `{"filegroups/documents": 0.5229080319404602, "general": 0.5542850494384766}` |
| filetypes/msi | joint_or_at_fp_2 | 1652 | 129 | 96.07% | 2 | 15503.88 | 47998.30 | 0.669 | 97.93% | 96.24% | `{"filetypes/msi": 0.29757893085479736, "general": 0.9915217161178589}` |
| filetypes/elf | joint_or_at_fp_3 | 70572 | 134241 | 95.13% | 3 | 22.35 | 57.76 | 1.003 | 97.50% | 98.32% | `{"filegroups/native": 0.9991791844367981, "filetypes/elf": 0.998521089553833, "general": 0.9919582009315491}` |
| filetypes/tar† | general_only | 1117 | 400 | 93.46% | 1 | 2500.00 | 11804.30 | 0.334 | 96.58% | 95.12% | `{"general": 0.9228709936141968}` |
| filetypes/ole | joint_or_at_fp_0 | 1924 | 5357 | 91.79% | 0 | 0.00 | 559.06 | 0.000 | 95.72% | 97.83% | `{"filetypes/ole": 0.971983015537262, "general": 0.8828756809234619}` |
| filetypes/pe | or_general_primary | 897596 | 151723 | 87.95% | 23 | 151.59 | 214.76 | 7.691 | 93.59% | 89.69% | `{"filegroups/native": 0.9985171556472778, "filetypes/pe": 0.9996024966239929, "general": 0.9989888668060303}` |
| filetypes/zst† | general_only | 10381 | 16152 | 84.38% | 1 | 61.91 | 293.67 | 0.334 | 91.53% | 93.89% | `{"general": 0.9945176839828491}` |
| filetypes/macho | learned_blend_at_fp_0 | 2045 | 10672 | 82.69% | 0 | 0.00 | 280.67 | 0.000 | 90.52% | 97.22% | `{}` |
| filetypes/docx | joint_or_at_fp_3 | 1553 | 244 | 82.61% | 3 | 12295.08 | 31468.92 | 1.003 | 90.38% | 84.81% | `{"filegroups/documents": 0.6899821162223816, "filetypes/docx": 0.40807923674583435}` |
| filetypes/7z† | general_only | 4275 | 78 | 82.48% | 1 | 12820.51 | 59378.49 | 0.334 | 90.39% | 82.77% | `{"general": 0.989359438419342}` |
| filetypes/python-bytecode | learned_blend_at_fp_2 | 1856 | 29501 | 81.84% | 1 | 33.90 | 160.79 | 0.334 | 89.99% | 98.92% | `{}` |
| filetypes/javascript | joint_or_at_fp_43 | 83592 | 468481 | 76.84% | 43 | 91.79 | 118.36 | 14.379 | 86.88% | 96.49% | `{"filetypes/javascript": 0.9563503265380859, "general": 0.9921667575836182}` |
| filetypes/shell | joint_or_at_fp_0 | 6515 | 45253 | 76.13% | 0 | 0.00 | 66.20 | 0.000 | 86.45% | 97.00% | `{"filegroups/scripts": 0.9917110204696655, "filetypes/shell": 0.9825712442398071, "general": 0.9742692708969116}` |
| filetypes/data | filetype_only_at_fp_0 | 405 | 9024 | 76.05% | 0 | 0.00 | 331.92 | 0.000 | 86.40% | 98.97% | `{"filetypes/data": 0.33864685893058777}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31515 | 73.21% | 0 | 0.00 | 95.05 | 0.000 | 84.54% | 99.81% | `{"filegroups/scripts": 0.9746114611625671, "filetypes/perl": 0.9969062209129333}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.20% | 72.80% | `{"filegroups/documents": 0.9203116297721863, "general": 0.9966467022895813}` |
| filetypes/rar | calibrate_inherited | 6090 | 4 | 70.90% | 0 | 0.00 | 527129.20 | 0.000 | 82.97% | 70.92% | `{"general": 0.9966467022895813}` |
| filetypes/python | filetype_only | 17903 | 129483 | 65.42% | 7 | 54.06 | 101.54 | 2.341 | 79.08% | 95.79% | `{"filetypes/python": 0.9881898164749146}` |
| filetypes/php | joint_or_at_fp_3 | 3838 | 84624 | 64.20% | 3 | 35.45 | 91.62 | 1.003 | 78.16% | 98.44% | `{"filegroups/scripts": 0.9949507713317871, "filetypes/php": 0.9918634295463562, "general": 0.996723473072052}` |
| filetypes/tar.gz | calibrate_inherited | 27924 | 12887 | 62.21% | 7 | 543.18 | 1020.02 | 2.341 | 76.69% | 74.12% | `{"general": 0.9966467022895813}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 23485 | 61.64% | 0 | 0.00 | 127.55 | 0.000 | 76.27% | 99.88% | `{"filegroups/scripts": 0.9916245341300964, "filetypes/ruby": 0.999415397644043, "general": 0.9674877524375916}` |
| filetypes/kotlin | joint_or_at_fp_6 | 23336 | 42240 | 61.46% | 6 | 142.05 | 280.34 | 2.006 | 76.12% | 86.28% | `{"filegroups/source": 0.9334213137626648, "filetypes/kotlin": 0.035727716982364655, "general": 0.9473177194595337}` |
| filetypes/objc† | general_only | 5 | 18400 | 60.00% | 0 | 0.00 | 162.80 | 0.000 | 75.00% | 99.99% | `{"general": 0.19480751055401205}` |
| filetypes/jar | joint_or_at_fp_0 | 1459 | 2085 | 59.22% | 0 | 0.00 | 1435.77 | 0.000 | 74.39% | 83.21% | `{"filetypes/jar": 0.892769992351532, "general": 0.9893239140510559}` |
| filetypes/cab† | general_only | 230 | 55 | 59.13% | 1 | 18181.82 | 83371.34 | 0.334 | 74.11% | 66.67% | `{"general": 0.986416757106781}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 46 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.08675141988202646, "general": 0.08675141988202646}` |
| filetypes/batch | learned_blend_at_fp_3 | 168290 | 3602 | 98.77% | 3 | 832.87 | 2151.18 | 1.003 | 99.38% | 98.79% | `{}` |
| filetypes/package.json | joint_or_at_fp_6 | 17780 | 11022 | 98.45% | 6 | 544.37 | 1074.15 | 2.006 | 99.20% | 99.02% | `{"filegroups/config": 0.9989033341407776, "filetypes/package.json": 0.9524045586585999, "general": 0.9932883381843567}` |
| filetypes/rtf | joint_or_at_fp_0 | 1455 | 480 | 98.08% | 0 | 0.00 | 6221.67 | 0.000 | 99.03% | 98.55% | `{"filetypes/rtf": 0.13613398373126984, "general": 0.9704356789588928}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1022 | 97.16% | 0 | 0.00 | 2926.95 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.038695644587278366}` |
| filetypes/elf | or_general_primary | 70572 | 134241 | 96.72% | 27 | 201.13 | 277.36 | 9.029 | 98.31% | 98.86% | `{"filegroups/native": 0.9969664812088013, "filetypes/elf": 0.9979577660560608, "general": 0.9760764837265015}` |
| filetypes/xls | joint_or_at_fp_0 | 10475 | 51 | 96.26% | 0 | 0.00 | 57047.95 | 0.000 | 98.09% | 96.28% | `{"filegroups/documents": 0.5229080319404602, "general": 0.5542850494384766}` |
| filetypes/msi | joint_or_at_fp_2 | 1652 | 129 | 96.07% | 2 | 15503.88 | 47998.30 | 0.669 | 97.93% | 96.24% | `{"filetypes/msi": 0.29757893085479736, "general": 0.9915217161178589}` |
| filetypes/tar† | general_only | 1117 | 400 | 93.46% | 1 | 2500.00 | 11804.30 | 0.334 | 96.58% | 95.12% | `{"general": 0.9228709936141968}` |
| filetypes/ole | joint_or_at_fp_0 | 1924 | 5357 | 91.79% | 0 | 0.00 | 559.06 | 0.000 | 95.72% | 97.83% | `{"filetypes/ole": 0.971983015537262, "general": 0.8828756809234619}` |
| filetypes/pe | or_general_primary | 897596 | 151723 | 91.17% | 36 | 237.27 | 313.33 | 12.038 | 95.38% | 92.44% | `{"filegroups/native": 0.9979126453399658, "filetypes/pe": 0.9995587468147278, "general": 0.9988341331481934}` |
| filetypes/python-bytecode | learned_blend_at_fp_8 | 1856 | 29501 | 90.19% | 3 | 101.69 | 262.81 | 1.003 | 94.76% | 99.41% | `{}` |
| filetypes/zst† | general_only | 10381 | 16152 | 84.59% | 2 | 123.82 | 389.73 | 0.669 | 91.64% | 93.96% | `{"general": 0.9941810965538025}` |
| filetypes/macho | learned_blend_at_fp_0 | 2045 | 10672 | 82.69% | 0 | 0.00 | 280.67 | 0.000 | 90.52% | 97.22% | `{}` |
| filetypes/docx | joint_or_at_fp_3 | 1553 | 244 | 82.61% | 3 | 12295.08 | 31468.92 | 1.003 | 90.38% | 84.81% | `{"filegroups/documents": 0.6899821162223816, "filetypes/docx": 0.40807923674583435}` |
| filetypes/7z† | general_only | 4275 | 78 | 82.48% | 1 | 12820.51 | 59378.49 | 0.334 | 90.39% | 82.77% | `{"general": 0.989359438419342}` |
| filetypes/shell | joint_or_at_fp_3 | 6515 | 45253 | 80.45% | 3 | 66.29 | 171.33 | 1.003 | 89.14% | 97.53% | `{"filegroups/scripts": 0.9917110204696655, "filetypes/shell": 0.9524685144424438, "general": 0.9612765908241272}` |
| filetypes/powershell | joint_or_at_fp_12 | 1895 | 2038 | 79.74% | 12 | 5888.13 | 9522.60 | 4.013 | 88.41% | 89.93% | `{"filegroups/scripts": 0.9960102438926697, "filetypes/powershell": 0.8439257740974426, "general": 0.9780750274658203}` |
| filetypes/javascript | filetype_only | 83592 | 468481 | 76.54% | 38 | 81.11 | 106.32 | 12.707 | 86.69% | 96.44% | `{"filetypes/javascript": 0.9587202072143555}` |
| filetypes/data | filetype_only_at_fp_0 | 405 | 9024 | 76.05% | 0 | 0.00 | 331.92 | 0.000 | 86.40% | 98.97% | `{"filetypes/data": 0.33864685893058777}` |
| filetypes/rar | calibrate_inherited | 6090 | 4 | 74.63% | 0 | 0.00 | 527129.20 | 0.000 | 85.47% | 74.65% | `{"general": 0.9949313402175903}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31515 | 73.21% | 0 | 0.00 | 95.05 | 0.000 | 84.54% | 99.81% | `{"filegroups/scripts": 0.9746114611625671, "filetypes/perl": 0.9969062209129333}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.20% | 72.80% | `{"filegroups/documents": 0.9203116297721863, "general": 0.9949313402175903}` |
| filetypes/python | learned_blend_at_fp_25 | 17903 | 129483 | 72.35% | 25 | 193.08 | 269.65 | 8.360 | 83.89% | 96.62% | `{}` |
| filetypes/php | joint_or_at_fp_9 | 3838 | 84624 | 70.22% | 9 | 106.35 | 185.58 | 3.010 | 82.39% | 98.70% | `{"filegroups/scripts": 0.9949507713317871, "filetypes/php": 0.9765686988830566, "general": 0.9975818395614624}` |
| filetypes/tar.gz | calibrate_inherited | 27924 | 12887 | 67.50% | 14 | 1086.37 | 1697.82 | 4.681 | 80.57% | 77.73% | `{"general": 0.9949313402175903}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.9949313402175903}` |
| filetypes/jar | joint_or_at_fp_2 | 1459 | 2085 | 62.65% | 2 | 959.23 | 3016.46 | 0.669 | 76.97% | 84.57% | `{"filetypes/jar": 0.8229566216468811, "general": 0.9893239140510559}` |
| filetypes/lnk | joint_or_at_fp_4 | 1992 | 1024 | 62.25% | 4 | 3906.25 | 8916.51 | 1.338 | 76.64% | 74.93% | `{"filetypes/lnk": 0.937574565410614, "general": 0.9907349944114685}` |
| filetypes/kotlin | joint_or_at_fp_8 | 23336 | 42240 | 61.89% | 8 | 189.39 | 341.70 | 2.675 | 76.44% | 86.43% | `{"filegroups/source": 0.9334213137626648, "filetypes/kotlin": 0.021102188155055046, "general": 0.9473177194595337}` |
