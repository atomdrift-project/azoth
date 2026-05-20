# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1349983353`
- Rows: 4727335 (1702977 malware, 3024358 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | joint_or_at_fp_0 | 168939 | 3679 | 99.45% | 0 | 0.00 | 813.95 | 0.000 | 99.72% | 99.46% | `{"filegroups/scripts": 0.9958048462867737, "filetypes/batch": 0.9944418668746948, "general": 0.9888841509819031}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1033 | 98.67% | 0 | 0.00 | 2895.83 | 0.000 | 99.33% | 98.79% | `{"filetypes/pkg-info": 0.03464825078845024}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09585988859713249, "filetypes/rtf": 0.09585988859713249, "general": 0.09585988859713249}` |
| filetypes/elf | learned_blend_at_fp_3 | 73107 | 135571 | 97.83% | 3 | 22.13 | 57.19 | 0.992 | 98.90% | 99.24% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 10498 | 51 | 96.71% | 0 | 0.00 | 57047.95 | 0.000 | 98.33% | 96.73% | `{"filegroups/documents": 0.5299120545387268, "general": 0.46501782536506653}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23477 | 42530 | 95.07% | 0 | 0.00 | 70.44 | 0.000 | 97.47% | 98.25% | `{"filegroups/source": 0.6436514854431152, "filetypes/kotlin": 0.9906653761863708, "general": 0.9797612428665161}` |
| filetypes/macho | learned_blend_at_fp_1 | 2067 | 10693 | 93.03% | 1 | 93.52 | 443.56 | 0.331 | 96.37% | 98.86% | `{}` |
| filetypes/pe | learned_blend_at_fp_4 | 901669 | 151967 | 92.29% | 4 | 26.32 | 60.23 | 1.323 | 95.99% | 93.41% | `{}` |
| filetypes/ole | filetype_only_at_fp_0 | 1928 | 5357 | 91.96% | 0 | 0.00 | 559.06 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9549445509910583}` |
| filetypes/package.json | joint_or_at_fp_0 | 17793 | 11625 | 91.59% | 0 | 0.00 | 257.66 | 0.000 | 95.61% | 94.91% | `{"filegroups/config": 0.999343991279602, "general": 0.9917721748352051}` |
| filetypes/javascript† | filetype_only | 84374 | 472458 | 88.46% | 3 | 6.35 | 16.41 | 0.992 | 93.88% | 98.25% | `{"filetypes/javascript": 0.9957202672958374}` |
| filetypes/zst† | general_only | 10381 | 16156 | 87.19% | 1 | 61.90 | 293.59 | 0.331 | 93.15% | 94.98% | `{"general": 0.9080920219421387}` |
| filetypes/7z† | general_only | 4304 | 78 | 87.01% | 1 | 12820.51 | 59378.49 | 0.331 | 93.04% | 87.22% | `{"general": 0.8931342959403992}` |
| filetypes/shell | joint_or_at_fp_0 | 6876 | 45523 | 83.26% | 0 | 0.00 | 65.80 | 0.000 | 90.87% | 97.80% | `{"filegroups/scripts": 0.9825277328491211, "filetypes/shell": 0.9574249386787415, "general": 0.9385397434234619}` |
| filetypes/perl | learned_blend_at_fp_0 | 224 | 31544 | 83.04% | 0 | 0.00 | 94.97 | 0.000 | 90.73% | 99.88% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 3856 | 86590 | 78.11% | 0 | 0.00 | 34.60 | 0.000 | 87.71% | 99.07% | `{"filegroups/scripts": 0.9972188472747803, "filetypes/php": 0.9987432360649109, "general": 0.9918663501739502}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.21% | 72.81% | `{"filegroups/documents": 0.8994224667549133, "general": 0.9983744621276855}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 71.23% | 0 | 0.00 | 123.09 | 0.000 | 83.20% | 99.91% | `{"filegroups/scripts": 0.9442169666290283, "filetypes/ruby": 0.9994116425514221}` |
| filetypes/docx | joint_or_at_fp_0 | 1578 | 244 | 69.96% | 0 | 0.00 | 12202.53 | 0.000 | 82.33% | 73.98% | `{"filegroups/documents": 0.9495398998260498, "filetypes/docx": 0.6300505995750427, "general": 0.9942312836647034}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1865 | 30915 | 68.63% | 0 | 0.00 | 96.90 | 0.000 | 81.40% | 98.22% | `{"filetypes/python-bytecode": 0.9976460337638855, "general": 0.9400534629821777}` |
| filetypes/rar | calibrate_inherited | 6152 | 4 | 65.15% | 0 | 0.00 | 527129.20 | 0.000 | 78.90% | 65.17% | `{"general": 0.9983744621276855}` |
| filetypes/msi† | filetype_only | 1806 | 133 | 65.01% | 0 | 0.00 | 22272.52 | 0.000 | 78.79% | 67.41% | `{"filetypes/msi": 0.6059523622323044}` |
| filetypes/tar.gz† | general_only | 28001 | 12975 | 63.75% | 1 | 77.07 | 365.56 | 0.331 | 77.86% | 75.23% | `{"general": 0.9945935064846165}` |
| filetypes/tar | calibrate_inherited | 1119 | 406 | 62.20% | 0 | 0.00 | 7351.50 | 0.000 | 76.69% | 72.26% | `{"general": 0.9983744621276855}` |
| filetypes/python | joint_or_at_fp_0 | 17917 | 130225 | 60.51% | 0 | 0.00 | 23.00 | 0.000 | 75.39% | 95.22% | `{"filegroups/scripts": 0.9984979033470154, "filetypes/python": 0.9996843934059143, "general": 0.9964038133621216}` |
| filetypes/jar | filetype_only_at_fp_0 | 1464 | 2130 | 57.51% | 0 | 0.00 | 1405.46 | 0.000 | 73.03% | 82.69% | `{"filetypes/jar": 0.8673824071884155}` |
| filetypes/java_class | joint_or_at_fp_0 | 1312 | 381309 | 49.85% | 0 | 0.00 | 7.86 | 0.000 | 66.53% | 99.83% | `{"filegroups/portable": 0.9999961853027344, "filetypes/java_class": 0.999689519405365, "general": 0.9735575914382935}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 49.60% | 0 | 0.00 | 2907.07 | 0.000 | 66.31% | 66.61% | `{"filetypes/lnk": 0.9819200038909912, "general": 0.9686082005500793}` |
| filetypes/zip† | general_only | 59677 | 7342 | 49.60% | 1 | 136.20 | 645.96 | 0.331 | 66.31% | 55.12% | `{"general": 0.9961912370719938}` |
| filetypes/powershell | joint_or_at_fp_0 | 2067 | 2080 | 39.91% | 0 | 0.00 | 1439.22 | 0.000 | 57.05% | 70.05% | `{"filegroups/scripts": 0.9986932277679443, "filetypes/powershell": 0.9992040991783142, "general": 0.9862196445465088}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | joint_or_at_fp_0 | 168939 | 3679 | 99.45% | 0 | 0.00 | 813.95 | 0.000 | 99.72% | 99.46% | `{"filegroups/scripts": 0.9958048462867737, "filetypes/batch": 0.9944418668746948, "general": 0.9888841509819031}` |
| filetypes/pkg-info | calibrate_inherited | 10634 | 1033 | 98.67% | 0 | 0.00 | 2895.83 | 0.000 | 99.33% | 98.79% | `{"filetypes/pkg-info": 0.03453336228308104, "general": 0.997287392616272}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09568683923172545, "filetypes/rtf": 0.09568683923172545, "general": 0.09568683923172545}` |
| filetypes/pe | learned_blend_at_fp_21 | 901669 | 151967 | 97.59% | 21 | 138.19 | 198.99 | 6.944 | 98.78% | 97.93% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 10498 | 51 | 96.71% | 0 | 0.00 | 57047.95 | 0.000 | 98.33% | 96.73% | `{"filegroups/documents": 0.5299120545387268, "general": 0.46501782536506653}` |
| filetypes/html† | max_rule | 49 | 7963 | 95.92% | 0 | 0.00 | 376.14 | 0.000 | 97.92% | 99.98% | `{"filegroups/documents": 0.6470221004938423, "general": 0.6470221004938423}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23477 | 42530 | 95.07% | 0 | 0.00 | 70.44 | 0.000 | 97.47% | 98.25% | `{"filegroups/source": 0.6436514854431152, "filetypes/kotlin": 0.9906653761863708, "general": 0.9797612428665161}` |
| filetypes/elf | learned_blend_at_fp_0 | 73107 | 135571 | 93.17% | 0 | 0.00 | 22.10 | 0.000 | 96.46% | 97.61% | `{}` |
| filetypes/ole | filetype_only_at_fp_0 | 1928 | 5357 | 91.96% | 0 | 0.00 | 559.06 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9549445509910583}` |
| filetypes/package.json | joint_or_at_fp_0 | 17793 | 11625 | 91.59% | 0 | 0.00 | 257.66 | 0.000 | 95.61% | 94.91% | `{"filegroups/config": 0.999343991279602, "general": 0.9917721748352051}` |
| filetypes/macho | joint_or_at_fp_0 | 2067 | 10693 | 91.10% | 0 | 0.00 | 280.12 | 0.000 | 95.34% | 98.56% | `{"filegroups/native": 0.8206468224525452, "filetypes/macho": 0.9754176735877991, "general": 0.9651686549186707}` |
| filetypes/javascript | joint_or_at_fp_3 | 84374 | 472458 | 89.02% | 3 | 6.35 | 16.41 | 0.992 | 94.19% | 98.34% | `{"filegroups/scripts": 0.9989272356033325, "filetypes/javascript": 0.9947577714920044, "general": 0.998352587223053}` |
| filetypes/zst† | general_only | 10381 | 16156 | 87.19% | 1 | 61.90 | 293.59 | 0.331 | 93.15% | 94.98% | `{"general": 0.9080920219421387}` |
| filetypes/perl | learned_blend_at_fp_0 | 224 | 31544 | 83.04% | 0 | 0.00 | 94.97 | 0.000 | 90.73% | 99.88% | `{}` |
| filetypes/shell† | max_rule | 6876 | 45523 | 78.84% | 0 | 0.00 | 65.80 | 0.000 | 88.17% | 97.22% | `{"filegroups/scripts": 0.993634214265587, "filetypes/shell": 0.993634214265587, "general": 0.993634214265587}` |
| filetypes/php | joint_or_at_fp_0 | 3856 | 86590 | 78.11% | 0 | 0.00 | 34.60 | 0.000 | 87.71% | 99.07% | `{"filegroups/scripts": 0.9972188472747803, "filetypes/php": 0.9987432360649109, "general": 0.9918663501739502}` |
| filetypes/tar | calibrate_inherited | 1119 | 406 | 74.35% | 0 | 0.00 | 7351.50 | 0.000 | 85.29% | 81.18% | `{"general": 0.997287392616272}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.21% | 72.81% | `{"filegroups/documents": 0.8994224667549133, "general": 0.997287392616272}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 71.23% | 0 | 0.00 | 123.09 | 0.000 | 83.20% | 99.91% | `{"filegroups/scripts": 0.9442169666290283, "filetypes/ruby": 0.9994116425514221}` |
| filetypes/rar | calibrate_inherited | 6152 | 4 | 71.18% | 0 | 0.00 | 527129.20 | 0.000 | 83.16% | 71.20% | `{"general": 0.997287392616272}` |
| filetypes/7z | calibrate_inherited | 4304 | 78 | 70.56% | 0 | 0.00 | 37678.63 | 0.000 | 82.74% | 71.09% | `{"general": 0.997287392616272}` |
| filetypes/docx | joint_or_at_fp_0 | 1578 | 244 | 69.96% | 0 | 0.00 | 12202.53 | 0.000 | 82.33% | 73.98% | `{"filegroups/documents": 0.9495398998260498, "filetypes/docx": 0.6300505995750427, "general": 0.9942312836647034}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1865 | 30915 | 68.63% | 0 | 0.00 | 96.90 | 0.000 | 81.40% | 98.22% | `{"filetypes/python-bytecode": 0.9976460337638855, "general": 0.9400534629821777}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.997287392616272}` |
| filetypes/msi† | filetype_only | 1806 | 133 | 65.28% | 0 | 0.00 | 22272.52 | 0.000 | 78.99% | 67.66% | `{"filetypes/msi": 0.5949300961448825}` |
| filetypes/tar.gz† | general_only | 28001 | 12975 | 63.75% | 1 | 77.07 | 365.56 | 0.331 | 77.86% | 75.23% | `{"general": 0.9945920451523862}` |
| filetypes/python | joint_or_at_fp_0 | 17917 | 130225 | 60.51% | 0 | 0.00 | 23.00 | 0.000 | 75.39% | 95.22% | `{"filegroups/scripts": 0.9984979033470154, "filetypes/python": 0.9996843934059143, "general": 0.9964038133621216}` |
| filetypes/jar | filetype_only_at_fp_0 | 1464 | 2130 | 57.51% | 0 | 0.00 | 1405.46 | 0.000 | 73.03% | 82.69% | `{"filetypes/jar": 0.8673824071884155}` |
| filetypes/java_class | joint_or_at_fp_0 | 1312 | 381309 | 49.85% | 0 | 0.00 | 7.86 | 0.000 | 66.53% | 99.83% | `{"filegroups/portable": 0.9999961853027344, "filetypes/java_class": 0.999689519405365, "general": 0.9735575914382935}` |
| filetypes/zip† | general_only | 59677 | 7342 | 49.67% | 1 | 136.20 | 645.96 | 0.331 | 66.38% | 55.19% | `{"general": 0.9961567722812072}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.13785160439029465, "general": 0.13785160439029465}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9920273423194885}` |
| filetypes/pe | learned_blend_at_fp_114 | 901669 | 151967 | 99.78% | 114 | 750.16 | 876.38 | 37.694 | 99.88% | 99.80% | `{}` |
| filetypes/batch | joint_or_at_fp_0 | 168939 | 3679 | 99.45% | 0 | 0.00 | 813.95 | 0.000 | 99.72% | 99.46% | `{"filegroups/scripts": 0.9958048462867737, "filetypes/batch": 0.9944418668746948, "general": 0.9888841509819031}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1033 | 98.67% | 0 | 0.00 | 2895.83 | 0.000 | 99.33% | 98.79% | `{"filetypes/pkg-info": 0.03464825078845024}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09479670708942683, "filetypes/rtf": 0.09479670708942683, "general": 0.09479670708942683}` |
| filetypes/elf | learned_blend_at_fp_3 | 73107 | 135571 | 97.83% | 3 | 22.13 | 57.19 | 0.992 | 98.90% | 99.24% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 10498 | 51 | 96.71% | 0 | 0.00 | 57047.95 | 0.000 | 98.33% | 96.73% | `{"filegroups/documents": 0.5299120545387268, "general": 0.46501782536506653}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23477 | 42530 | 95.07% | 0 | 0.00 | 70.44 | 0.000 | 97.47% | 98.25% | `{"filegroups/source": 0.6436514854431152, "filetypes/kotlin": 0.9906653761863708, "general": 0.9797612428665161}` |
| filetypes/ole | filetype_only_at_fp_0 | 1928 | 5357 | 91.96% | 0 | 0.00 | 559.06 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9549445509910583}` |
| filetypes/package.json | joint_or_at_fp_0 | 17793 | 11625 | 91.59% | 0 | 0.00 | 257.66 | 0.000 | 95.61% | 94.91% | `{"filegroups/config": 0.999343991279602, "general": 0.9917721748352051}` |
| filetypes/macho | joint_or_at_fp_0 | 2067 | 10693 | 91.10% | 0 | 0.00 | 280.12 | 0.000 | 95.34% | 98.56% | `{"filegroups/native": 0.8206468224525452, "filetypes/macho": 0.9754176735877991, "general": 0.9651686549186707}` |
| filetypes/javascript | joint_or_at_fp_3 | 84374 | 472458 | 89.02% | 3 | 6.35 | 16.41 | 0.992 | 94.19% | 98.34% | `{"filegroups/scripts": 0.9989272356033325, "filetypes/javascript": 0.9947577714920044, "general": 0.998352587223053}` |
| filetypes/7z† | general_only | 4304 | 78 | 87.01% | 1 | 12820.51 | 59378.49 | 0.331 | 93.04% | 87.22% | `{"general": 0.8931342959403992}` |
| filetypes/tar | calibrate_inherited | 1119 | 406 | 85.97% | 0 | 0.00 | 7351.50 | 0.000 | 92.46% | 89.70% | `{"general": 0.9920273423194885}` |
| filetypes/zst | calibrate_inherited | 10381 | 16156 | 85.38% | 0 | 0.00 | 185.41 | 0.000 | 92.11% | 94.28% | `{"general": 0.9920273423194885}` |
| filetypes/xlsx | learned_blend_at_fp_3 | 17783 | 144 | 85.05% | 10 | 69444.44 | 114946.03 | 3.306 | 91.89% | 85.11% | `{}` |
| filetypes/shell | joint_or_at_fp_0 | 6876 | 45523 | 83.26% | 0 | 0.00 | 65.80 | 0.000 | 90.87% | 97.80% | `{"filegroups/scripts": 0.9825277328491211, "filetypes/shell": 0.9574249386787415, "general": 0.9385397434234619}` |
| filetypes/perl | learned_blend_at_fp_0 | 224 | 31544 | 83.04% | 0 | 0.00 | 94.97 | 0.000 | 90.73% | 99.88% | `{}` |
| filetypes/rar | calibrate_inherited | 6152 | 4 | 80.61% | 0 | 0.00 | 527129.20 | 0.000 | 89.26% | 80.62% | `{"general": 0.9920273423194885}` |
| filetypes/php | joint_or_at_fp_0 | 3856 | 86590 | 78.11% | 0 | 0.00 | 34.60 | 0.000 | 87.71% | 99.07% | `{"filegroups/scripts": 0.9972188472747803, "filetypes/php": 0.9987432360649109, "general": 0.9918663501739502}` |
| filetypes/python | learned_blend_at_fp_3 | 17917 | 130225 | 75.10% | 3 | 23.04 | 59.54 | 0.992 | 85.77% | 96.99% | `{}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.21% | 72.81% | `{"filegroups/documents": 0.8994224667549133, "general": 0.9920273423194885}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 71.23% | 0 | 0.00 | 123.09 | 0.000 | 83.20% | 99.91% | `{"filegroups/scripts": 0.9442169666290283, "filetypes/ruby": 0.9994116425514221}` |
| filetypes/docx | joint_or_at_fp_0 | 1578 | 244 | 69.96% | 0 | 0.00 | 12202.53 | 0.000 | 82.33% | 73.98% | `{"filegroups/documents": 0.9495398998260498, "filetypes/docx": 0.6300505995750427, "general": 0.9942312836647034}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1865 | 30915 | 68.63% | 0 | 0.00 | 96.90 | 0.000 | 81.40% | 98.22% | `{"filetypes/python-bytecode": 0.9976460337638855, "general": 0.9400534629821777}` |
| filetypes/msi† | filetype_only | 1806 | 133 | 68.60% | 0 | 0.00 | 22272.52 | 0.000 | 81.38% | 70.76% | `{"filetypes/msi": 0.557880713319961}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.9920273423194885}` |
| filetypes/tar.gz† | general_only | 28001 | 12975 | 63.79% | 1 | 77.07 | 365.56 | 0.331 | 77.89% | 75.25% | `{"general": 0.9945569129786533}` |
| filetypes/objc† | general_only | 5 | 18405 | 60.00% | 0 | 0.00 | 162.75 | 0.000 | 75.00% | 99.99% | `{"general": 0.7365238248748498}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.08625421661427142, "general": 0.08625421661427142}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9887415170669556}` |
| filetypes/batch | learned_blend_at_fp_3 | 168939 | 3679 | 99.69% | 3 | 815.44 | 2106.18 | 0.992 | 99.84% | 99.69% | `{}` |
| filetypes/package.json | calibrate_inherited | 17793 | 11625 | 99.40% | 16 | 1376.34 | 2089.68 | 5.290 | 99.65% | 99.58% | `{"filegroups/config": 0.9670636653900146, "filetypes/package.json": 0.9819857478141785, "general": 0.9887415170669556}` |
| filetypes/elf | group_only | 73107 | 135571 | 99.08% | 11 | 81.14 | 134.30 | 3.637 | 99.53% | 99.67% | `{"filegroups/native": 0.8849342465400696}` |
| filetypes/pkg-info | filetype_only_at_fp_0 | 10634 | 1033 | 98.67% | 0 | 0.00 | 2895.83 | 0.000 | 99.33% | 98.79% | `{"filetypes/pkg-info": 0.03464825078845024}` |
| filetypes/pe | learned_blend_at_fp_31 | 901669 | 151967 | 98.60% | 31 | 203.99 | 275.30 | 10.250 | 99.29% | 98.80% | `{}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09433974274443524, "filetypes/rtf": 0.09433974274443524, "general": 0.09433974274443524}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 23477 | 42530 | 97.41% | 3 | 70.54 | 182.30 | 0.992 | 98.68% | 99.07% | `{}` |
| filetypes/msi | joint_or_at_fp_3 | 1806 | 133 | 97.40% | 3 | 22556.39 | 57263.63 | 0.992 | 98.60% | 97.42% | `{"filetypes/msi": 0.293630450963974, "general": 0.966511607170105}` |
| filetypes/xls | joint_or_at_fp_0 | 10498 | 51 | 96.71% | 0 | 0.00 | 57047.95 | 0.000 | 98.33% | 96.73% | `{"filegroups/documents": 0.5299120545387268, "general": 0.46501782536506653}` |
| filetypes/macho | learned_blend_at_fp_3 | 2067 | 10693 | 96.61% | 3 | 280.56 | 724.95 | 0.992 | 98.21% | 99.43% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_8 | 1865 | 30915 | 95.12% | 8 | 258.77 | 466.87 | 2.645 | 97.29% | 99.70% | `{"filetypes/python-bytecode": 0.9953309893608093, "general": 0.8467183113098145}` |
| filetypes/javascript | filetype_only | 84374 | 472458 | 95.10% | 38 | 80.43 | 105.42 | 12.565 | 97.47% | 99.25% | `{"filetypes/javascript": 0.954715371131897}` |
| filetypes/php | learned_blend_at_fp_3 | 3856 | 86590 | 94.79% | 3 | 34.65 | 89.54 | 0.992 | 97.29% | 99.77% | `{}` |
| filetypes/tar† | general_only | 1119 | 406 | 93.48% | 1 | 2463.05 | 11630.66 | 0.331 | 96.58% | 95.15% | `{"general": 0.8985410332679749}` |
| filetypes/ole | filetype_only_at_fp_0 | 1928 | 5357 | 91.96% | 0 | 0.00 | 559.06 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9549445509910583}` |
| filetypes/python | calibrate_inherited | 17917 | 130225 | 87.22% | 42 | 322.52 | 417.13 | 13.887 | 93.06% | 98.43% | `{"filegroups/scripts": 0.9530351161956787, "filetypes/python": 0.9926226735115051, "general": 0.9887415170669556}` |
| filetypes/zst† | general_only | 10381 | 16156 | 87.19% | 2 | 123.79 | 389.64 | 0.661 | 93.15% | 94.98% | `{"general": 0.8978598713874817}` |
| filetypes/7z† | general_only | 4304 | 78 | 87.01% | 1 | 12820.51 | 59378.49 | 0.331 | 93.04% | 87.22% | `{"general": 0.8931342959403992}` |
| filetypes/shell | calibrate_inherited | 6876 | 45523 | 86.40% | 8 | 175.74 | 317.06 | 2.645 | 92.65% | 98.20% | `{"filegroups/scripts": 0.9530351161956787, "filetypes/shell": 0.91689133605681, "general": 0.9887415170669556}` |
| filetypes/xlsx | learned_blend_at_fp_3 | 17783 | 144 | 85.05% | 10 | 69444.44 | 114946.03 | 3.306 | 91.89% | 85.11% | `{}` |
| filetypes/perl | learned_blend_at_fp_0 | 224 | 31544 | 83.04% | 0 | 0.00 | 94.97 | 0.000 | 90.73% | 99.88% | `{}` |
| filetypes/rar | calibrate_inherited | 6152 | 4 | 82.02% | 0 | 0.00 | 527129.20 | 0.000 | 90.12% | 82.03% | `{"general": 0.9887415170669556}` |
| filetypes/docx | joint_or_at_fp_3 | 1578 | 244 | 80.42% | 3 | 12295.08 | 31468.92 | 0.992 | 89.05% | 82.88% | `{"filegroups/documents": 0.8923970460891724, "filetypes/docx": 0.41208040714263916, "general": 0.9691571593284607}` |
| filetypes/powershell | learned_blend_at_fp_3 | 2067 | 2080 | 74.94% | 3 | 1442.31 | 3723.46 | 0.992 | 85.60% | 87.44% | `{}` |
| filetypes/tar.gz | calibrate_inherited | 28001 | 12975 | 73.04% | 11 | 847.78 | 1402.89 | 3.637 | 84.40% | 81.55% | `{"general": 0.9887415170669556}` |
| filetypes/doc | calibrate_inherited | 11032 | 34 | 72.72% | 0 | 0.00 | 84339.64 | 0.000 | 84.21% | 72.81% | `{"filegroups/documents": 0.8994224667549133, "general": 0.9887415170669556}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 71.23% | 0 | 0.00 | 123.09 | 0.000 | 83.20% | 99.91% | `{"filegroups/scripts": 0.9442169666290283, "filetypes/ruby": 0.9994116425514221}` |
| filetypes/lnk | learned_blend_at_fp_7 | 2020 | 1029 | 69.60% | 7 | 6802.72 | 12739.41 | 2.315 | 81.91% | 79.63% | `{}` |
