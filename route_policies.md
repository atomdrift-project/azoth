# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `6309383805`
- Rows: 2658700 (383937 malware, 2274763 benign)

## L50 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 100.00% | 0 | 0.00 | 8203163.59 | 0.000 | 100.00% | 100.00% | `{"filegroups/media": 0.9987403878784917, "general": 0.9988697318756322}` |
| filetypes/nupkg | no_policy | 10 | 1534 | 100.00% | 0 | 0.00 | 195098.37 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.990863007116086, "filegroups/source": 0.9932046812949984, "general": 0.9988697318756322}` |
| filetypes/python_sdist† | max_rule | 367 | 1398 | 99.18% | 1 | 71530.76 | 338878.20 | 43.961 | 99.45% | 99.77% | `{"filegroups/archive": 0.8465854283673353, "filetypes/python_sdist": 0.8465854283673353, "general": 0.8465854283673353}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 43.961 | 99.50% | 99.14% | `{"filegroups/documents": 0.9411611100935762, "filegroups/historical_filegroups_documents_frozen": 0.9411611100935762, "filegroups/historical_filetypes_rtf_frozen": 0.9411611100935762, "filetypes/rtf": 0.9411611100935762, "general": 0.9411611100935762}` |
| filetypes/cab | max_rule | 107 | 13 | 99.07% | 0 | 0.00 | 20581666.52 | 0.000 | 99.53% | 99.17% | `{}` |
| filetypes/pdf | joint_or_at_fp_1 | 22292 | 3713 | 98.71% | 1 | 26932.40 | 127699.26 | 43.961 | 99.35% | 98.89% | `{"filegroups/documents": 0.9630042314529419, "filetypes/pdf": 0.554283082485199, "general": 0.98346346616745}` |
| filetypes/batch | joint_or_at_fp_1 | 22536 | 1140 | 98.38% | 1 | 87719.30 | 415445.79 | 43.961 | 99.18% | 98.45% | `{"filegroups/scripts": 0.9979577660560608, "filetypes/batch": 0.9772656559944153, "general": 0.9898199439048767}` |
| filetypes/elf† | max_rule | 25081 | 113027 | 98.27% | 1 | 884.74 | 4197.04 | 43.961 | 99.13% | 99.69% | `{"filegroups/historical_filetypes_elf_frozen": 0.9996072459018176, "filegroups/native": 0.9996072459018176, "filetypes/elf": 0.9996072459018176, "general": 0.9996072459018176}` |
| filetypes/rar† | or_general_primary | 2822 | 7 | 98.16% | 1 | 14285714.29 | 52070297.36 | 43.961 | 99.05% | 98.13% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/vbs† | max_rule | 1793 | 538 | 98.05% | 1 | 185873.61 | 878697.12 | 43.961 | 98.99% | 98.46% | `{"filegroups/code_pooled_recovery": 0.990894365133512, "filegroups/scripts": 0.990894365133512, "filegroups/vbs_hnm_recovery": 0.990894365133512, "filetypes/vbs": 0.990894365133512, "general": 0.990894365133512}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3425 | 10118 | 97.69% | 1 | 9883.38 | 46876.72 | 43.961 | 98.82% | 99.41% | `{"filegroups/source": 0.9925793288424383, "filetypes/kotlin": 0.9107777723165124, "general": 0.947537876913557}` |
| filetypes/html | joint_or_at_fp_1 | 11562 | 53999 | 97.69% | 1 | 1851.89 | 8784.79 | 43.961 | 98.83% | 99.59% | `{"filegroups/documents": 0.9038472771644592, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9928556084632874, "general": 0.9818704128265381}` |
| filetypes/ole_doc† | max_rule | 11935 | 3955 | 97.51% | 1 | 25284.45 | 119889.25 | 43.961 | 98.74% | 98.12% | `{"filegroups/documents": 0.9857139429005451, "filetypes/ole_doc": 0.9857139429005451, "general": 0.9857139429005451}` |
| filetypes/apk_android | learned_blend_at_fp_1 | 307 | 56 | 97.39% | 1 | 1785714.29 | 8193215.95 | 43.961 | 98.52% | 97.52% | `{}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 623 | 150 | 96.31% | 1 | 666666.67 | 3123381.69 | 43.961 | 98.04% | 96.90% | `{"filegroups/filetypes_lnk_oct26": 0.9948535778845926, "filegroups/lnk_general_layout_recovery": 0.9948535778845926, "filegroups/lnk_recovered": 0.9948535778845926, "filetypes/lnk": 0.9948535778845926, "general": 0.9948535778845926}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9987403878784917, "general": 0.9988697318756322}` |
| filetypes/ooxml† | max_rule | 8467 | 726 | 93.86% | 1 | 137741.05 | 651742.48 | 43.961 | 96.83% | 94.33% | `{"filegroups/documents": 0.993057113644306, "filetypes/ooxml": 0.993057113644306, "general": 0.993057113644306}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 48 | 93.40% | 1 | 2083333.33 | 9505862.46 | 43.961 | 96.54% | 93.59% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/static-lib† | max_rule | 259 | 1763 | 91.89% | 1 | 56721.50 | 268793.56 | 43.961 | 95.58% | 98.91% | `{"filetypes/static-lib": 0.9512767060349488, "general": 0.9512767060349488}` |
| filetypes/ico | no_policy | 24 | 113 | 91.67% | 0 | 0.00 | 2616257.60 | 0.000 | 95.65% | 98.54% | `{}` |
| filetypes/groovy | no_policy | 8 | 1332 | 87.50% | 0 | 0.00 | 224652.10 | 0.000 | 93.33% | 99.93% | `{}` |
| filetypes/shell† | max_rule | 2252 | 21544 | 87.03% | 1 | 4641.66 | 22017.51 | 43.961 | 93.05% | 98.77% | `{"filegroups/scripts": 0.9997536016134467, "filetypes/shell": 0.9997536016134467, "general": 0.9997536016134467}` |
| filetypes/gem | no_policy | 37 | 14781 | 86.49% | 0 | 0.00 | 20265.40 | 0.000 | 92.75% | 99.97% | `{}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 43.961 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999580399887877, "general": 0.9637311765838902}` |
| filetypes/pe† | max_rule | 207371 | 33704 | 82.77% | 1 | 2967.01 | 14074.30 | 43.961 | 90.57% | 85.18% | `{"filegroups/native": 0.9999170231104826, "filegroups/native_previous": 0.9999170231104826, "filegroups/pe_previous": 0.9999170231104826, "filetypes/pe": 0.9999170231104826, "general": 0.9999170231104826}` |
| filetypes/zip† | max_rule | 13624 | 18069 | 82.71% | 1 | 5534.34 | 26251.44 | 43.961 | 90.53% | 92.56% | `{"filegroups/archive": 0.999376397577413, "filetypes/zip": 0.999376397577413, "general": 0.999376397577413}` |
| filetypes/php | learned_blend_at_fp_0 | 783 | 79243 | 82.25% | 1 | 1261.94 | 5986.34 | 43.961 | 90.20% | 99.83% | `{}` |
| filetypes/jar | joint_or_at_fp_1 | 520 | 5118 | 82.12% | 1 | 19538.88 | 92655.92 | 43.961 | 90.08% | 98.33% | `{"filegroups/archive": 0.9318544864654541, "filetypes/jar": 0.9572367072105408, "general": 0.9140117764472961}` |

## L100 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 100.00% | 0 | 0.00 | 8203163.59 | 0.000 | 100.00% | 100.00% | `{"filegroups/media": 0.9985459057067835, "general": 0.998513638859241}` |
| filetypes/nupkg | no_policy | 10 | 1534 | 100.00% | 0 | 0.00 | 195098.37 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908295771164081, "filegroups/source": 0.9930671164707298, "general": 0.998513638859241}` |
| filetypes/python_sdist† | max_rule | 367 | 1398 | 99.18% | 1 | 71530.76 | 338878.20 | 43.961 | 99.45% | 99.77% | `{"filegroups/archive": 0.8464426476691064, "filetypes/python_sdist": 0.8464426476691064, "general": 0.8464426476691064}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 43.961 | 99.50% | 99.14% | `{"filegroups/documents": 0.9411606378362878, "filegroups/historical_filegroups_documents_frozen": 0.9411606378362878, "filegroups/historical_filetypes_rtf_frozen": 0.9411606378362878, "filetypes/rtf": 0.9411606378362878, "general": 0.9411606378362878}` |
| filetypes/cab | max_rule | 107 | 13 | 99.07% | 0 | 0.00 | 20581666.52 | 0.000 | 99.53% | 99.17% | `{}` |
| filetypes/pdf | joint_or_at_fp_1 | 22292 | 3713 | 98.71% | 1 | 26932.40 | 127699.26 | 43.961 | 99.35% | 98.89% | `{"filegroups/documents": 0.9630042314529419, "filetypes/pdf": 0.554283082485199, "general": 0.98346346616745}` |
| filetypes/batch | joint_or_at_fp_1 | 22536 | 1140 | 98.38% | 1 | 87719.30 | 415445.79 | 43.961 | 99.18% | 98.45% | `{"filegroups/scripts": 0.9979577660560608, "filetypes/batch": 0.9772656559944153, "general": 0.9898199439048767}` |
| filetypes/elf† | max_rule | 25081 | 113027 | 98.27% | 1 | 884.74 | 4197.04 | 43.961 | 99.13% | 99.69% | `{"filegroups/historical_filetypes_elf_frozen": 0.999520037116952, "filegroups/native": 0.999520037116952, "filetypes/elf": 0.999520037116952, "general": 0.999520037116952}` |
| filetypes/rar† | or_general_primary | 2822 | 7 | 98.16% | 1 | 14285714.29 | 52070297.36 | 43.961 | 99.05% | 98.13% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/vbs† | max_rule | 1793 | 538 | 98.05% | 1 | 185873.61 | 878697.12 | 43.961 | 98.99% | 98.46% | `{"filegroups/code_pooled_recovery": 0.9908928932414298, "filegroups/scripts": 0.9908928932414298, "filegroups/vbs_hnm_recovery": 0.9908928932414298, "filetypes/vbs": 0.9908928932414298, "general": 0.9908928932414298}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3425 | 10118 | 97.69% | 1 | 9883.38 | 46876.72 | 43.961 | 98.82% | 99.41% | `{"filegroups/source": 0.9924882369757821, "filetypes/kotlin": 0.9107146969839861, "general": 0.9470629618767565}` |
| filetypes/html | joint_or_at_fp_1 | 11562 | 53999 | 97.69% | 1 | 1851.89 | 8784.79 | 43.961 | 98.83% | 99.59% | `{"filegroups/documents": 0.9038472771644592, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9928556084632874, "general": 0.9818704128265381}` |
| filetypes/ole_doc† | max_rule | 11935 | 3955 | 97.51% | 1 | 25284.45 | 119889.25 | 43.961 | 98.74% | 98.12% | `{"filegroups/documents": 0.9857136839551899, "filetypes/ole_doc": 0.9857136839551899, "general": 0.9857136839551899}` |
| filetypes/apk_android | learned_blend_at_fp_1 | 307 | 56 | 97.39% | 1 | 1785714.29 | 8193215.95 | 43.961 | 98.52% | 97.52% | `{}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 623 | 150 | 96.31% | 1 | 666666.67 | 3123381.69 | 43.961 | 98.04% | 96.90% | `{"filegroups/filetypes_lnk_oct26": 0.994852991823587, "filegroups/lnk_general_layout_recovery": 0.994852991823587, "filegroups/lnk_recovered": 0.994852991823587, "filetypes/lnk": 0.994852991823587, "general": 0.994852991823587}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9985459057067835, "general": 0.998513638859241}` |
| filetypes/ooxml† | max_rule | 8467 | 726 | 93.86% | 1 | 137741.05 | 651742.48 | 43.961 | 96.83% | 94.33% | `{"filegroups/documents": 0.9930551490366089, "filetypes/ooxml": 0.9930551490366089, "general": 0.9930551490366089}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 48 | 93.40% | 1 | 2083333.33 | 9505862.46 | 43.961 | 96.54% | 93.59% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/static-lib† | max_rule | 259 | 1763 | 91.89% | 1 | 56721.50 | 268793.56 | 43.961 | 95.58% | 98.91% | `{"filetypes/static-lib": 0.9512162183041093, "general": 0.9512162183041093}` |
| filetypes/ico | no_policy | 24 | 113 | 91.67% | 0 | 0.00 | 2616257.60 | 0.000 | 95.65% | 98.54% | `{}` |
| filetypes/groovy | no_policy | 8 | 1332 | 87.50% | 0 | 0.00 | 224652.10 | 0.000 | 93.33% | 99.93% | `{}` |
| filetypes/shell† | max_rule | 2252 | 21544 | 87.03% | 1 | 4641.66 | 22017.51 | 43.961 | 93.05% | 98.77% | `{"filegroups/scripts": 0.999741951735045, "filetypes/shell": 0.999741951735045, "general": 0.999741951735045}` |
| filetypes/gem | no_policy | 37 | 14781 | 86.49% | 0 | 0.00 | 20265.40 | 0.000 | 92.75% | 99.97% | `{}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 43.961 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999564105302579, "general": 0.9623424042387706}` |
| filetypes/pe† | max_rule | 207371 | 33704 | 82.77% | 1 | 2967.01 | 14074.30 | 43.961 | 90.57% | 85.18% | `{"filegroups/native": 0.9999116657473432, "filegroups/native_previous": 0.9999116657473432, "filegroups/pe_previous": 0.9999116657473432, "filetypes/pe": 0.9999116657473432, "general": 0.9999116657473432}` |
| filetypes/zip† | max_rule | 13624 | 18069 | 82.71% | 1 | 5534.34 | 26251.44 | 43.961 | 90.53% | 92.56% | `{"filegroups/archive": 0.9993612521890195, "filetypes/zip": 0.9993612521890195, "general": 0.9993612521890195}` |
| filetypes/php | learned_blend_at_fp_0 | 783 | 79243 | 82.25% | 1 | 1261.94 | 5986.34 | 43.961 | 90.20% | 99.83% | `{}` |
| filetypes/jar | joint_or_at_fp_1 | 520 | 5118 | 82.12% | 1 | 19538.88 | 92655.92 | 43.961 | 90.08% | 98.33% | `{"filegroups/archive": 0.9318544864654541, "filetypes/jar": 0.9572367072105408, "general": 0.9140117764472961}` |
