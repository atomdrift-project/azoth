# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `6309383805`
- Rows: 2658700 (383937 malware, 2274763 benign)

## L50 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 1 | 7692307.69 | 31633976.48 | 43.961 | 99.53% | 99.17% | `{}` |
| filetypes/nupkg | no_policy | 10 | 1534 | 100.00% | 0 | 0.00 | 195098.37 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.990863007116086, "filegroups/source": 0.9932046812949984, "general": 0.9991883600725521}` |
| filetypes/python_sdist† | max_rule | 367 | 1398 | 99.18% | 1 | 71530.76 | 338878.20 | 43.961 | 99.45% | 99.77% | `{"filegroups/archive": 0.7709468335652443, "filetypes/python_sdist": 0.7709468335652443, "general": 0.7709468335652443}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 43.961 | 99.50% | 99.14% | `{"filegroups/documents": 0.9482319645030224, "filegroups/historical_filegroups_documents_frozen": 0.9482319645030224, "filegroups/historical_filetypes_rtf_frozen": 0.9482319645030224, "filetypes/rtf": 0.9482319645030224, "general": 0.9482319645030224}` |
| filetypes/pdf | joint_or_at_fp_1 | 22292 | 3713 | 98.71% | 1 | 26932.40 | 127699.26 | 43.961 | 99.35% | 98.89% | `{"filegroups/documents": 0.9630042314529419, "filetypes/pdf": 0.554283082485199, "general": 0.9740650057792664}` |
| filetypes/batch | joint_or_at_fp_1 | 22536 | 1140 | 98.44% | 1 | 87719.30 | 415445.79 | 43.961 | 99.21% | 98.51% | `{"filegroups/scripts": 0.998256266117096, "filetypes/batch": 0.9772656559944153, "general": 0.9874888062477112}` |
| filetypes/elf† | max_rule | 25081 | 113027 | 98.32% | 1 | 884.74 | 4197.04 | 43.961 | 99.15% | 99.69% | `{"filegroups/historical_filetypes_elf_frozen": 0.9996072459018176, "filegroups/native": 0.9996072459018176, "filetypes/elf": 0.9996072459018176, "general": 0.9996072459018176}` |
| filetypes/rar† | or_general_primary | 2822 | 7 | 98.19% | 1 | 14285714.29 | 52070297.36 | 43.961 | 99.07% | 98.16% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/vbs† | max_rule | 1793 | 538 | 97.88% | 1 | 185873.61 | 878697.12 | 43.961 | 98.90% | 98.33% | `{"filegroups/code_pooled_recovery": 0.9908939908423027, "filegroups/scripts": 0.9908939908423027, "filegroups/vbs_hnm_recovery": 0.9908939908423027, "filetypes/vbs": 0.9908939908423027, "general": 0.9908939908423027}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3425 | 10118 | 97.69% | 1 | 9883.38 | 46876.72 | 43.961 | 98.82% | 99.41% | `{"filegroups/source": 0.9925793288424383, "filetypes/kotlin": 0.9107777723165124, "general": 0.9338049500357124}` |
| filetypes/html | joint_or_at_fp_1 | 11562 | 53999 | 97.69% | 1 | 1851.89 | 8784.79 | 43.961 | 98.83% | 99.59% | `{"filegroups/documents": 0.9038472771644592, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9928556084632874, "general": 0.9863055944442749}` |
| filetypes/ole_doc† | max_rule | 11935 | 3955 | 97.53% | 1 | 25284.45 | 119889.25 | 43.961 | 98.74% | 98.14% | `{"filegroups/documents": 0.9857118738073043, "filetypes/ole_doc": 0.9857118738073043, "general": 0.9857118738073043}` |
| filetypes/apk_android | learned_blend_at_fp_0 | 307 | 56 | 97.39% | 1 | 1785714.29 | 8193215.95 | 43.961 | 98.52% | 97.52% | `{}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 623 | 150 | 96.31% | 1 | 666666.67 | 3123381.69 | 43.961 | 98.04% | 96.90% | `{"filegroups/filetypes_lnk_oct26": 0.9978947688914513, "filegroups/lnk_general_layout_recovery": 0.9978947688914513, "filegroups/lnk_recovered": 0.9978947688914513, "filetypes/lnk": 0.9978947688914513, "general": 0.9978947688914513}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9987946294377223, "general": 0.9991883600725521}` |
| filetypes/static-lib† | max_rule | 259 | 1763 | 94.59% | 1 | 56721.50 | 268793.56 | 43.961 | 97.03% | 99.26% | `{"filetypes/static-lib": 0.9802574051448264, "general": 0.9802574051448264}` |
| filetypes/ooxml† | max_rule | 8467 | 726 | 93.80% | 1 | 137741.05 | 651742.48 | 43.961 | 96.79% | 94.28% | `{"filegroups/documents": 0.993057113644306, "filetypes/ooxml": 0.993057113644306, "general": 0.993057113644306}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 93.75% | 0 | 0.00 | 8203163.59 | 0.000 | 96.77% | 98.04% | `{"filegroups/media": 0.9987946294377223, "general": 0.9991883600725521}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 48 | 93.58% | 1 | 2083333.33 | 9505862.46 | 43.961 | 96.64% | 93.77% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/ico | no_policy | 24 | 113 | 91.67% | 0 | 0.00 | 2616257.60 | 0.000 | 95.65% | 98.54% | `{}` |
| filetypes/groovy | no_policy | 8 | 1332 | 87.50% | 0 | 0.00 | 224652.10 | 0.000 | 93.33% | 99.93% | `{}` |
| filetypes/shell† | max_rule | 2252 | 21544 | 87.03% | 1 | 4641.66 | 22017.51 | 43.961 | 93.05% | 98.77% | `{"filegroups/scripts": 0.9997536016134467, "filetypes/shell": 0.9997536016134467, "general": 0.9997536016134467}` |
| filetypes/gem | no_policy | 37 | 14781 | 86.49% | 0 | 0.00 | 20265.40 | 0.000 | 92.75% | 99.97% | `{}` |
| filetypes/ruby | no_policy | 34 | 25025 | 85.29% | 0 | 0.00 | 11970.24 | 0.000 | 92.06% | 99.98% | `{}` |
| filetypes/jar | joint_or_at_fp_1 | 520 | 5118 | 84.42% | 1 | 19538.88 | 92655.92 | 43.961 | 91.46% | 98.55% | `{"filegroups/archive": 0.9296517968177795, "filetypes/jar": 0.9572367072105408, "general": 0.9013851881027222}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 43.961 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999580399887877, "general": 0.9464871152152342}` |
| filetypes/gif† | max_rule | 61 | 220 | 83.61% | 1 | 454545.45 | 2138041.18 | 43.961 | 90.27% | 96.09% | `{"filegroups/media": 0.9719532827608367, "filetypes/gif": 0.9719532827608367, "general": 0.9719532827608367}` |
| filetypes/zip† | specialist_primary_with_escape | 13624 | 18069 | 83.32% | 1 | 5534.34 | 26251.44 | 43.961 | 90.90% | 92.82% | `{"filegroups/archive": 0.9992664281041109, "filetypes/zip": 0.999048320207996, "general": 0.9842358180840227}` |

## L100 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 1 | 7692307.69 | 31633976.48 | 43.961 | 99.53% | 99.17% | `{}` |
| filetypes/nupkg | no_policy | 10 | 1534 | 100.00% | 0 | 0.00 | 195098.37 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908295771164081, "filegroups/source": 0.9930671164707298, "general": 0.9981635639211858}` |
| filetypes/python_sdist† | max_rule | 367 | 1398 | 99.18% | 1 | 71530.76 | 338878.20 | 43.961 | 99.45% | 99.77% | `{"filegroups/archive": 0.7708212497006635, "filetypes/python_sdist": 0.7708212497006635, "general": 0.7708212497006635}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 43.961 | 99.50% | 99.14% | `{"filegroups/documents": 0.9482287706093055, "filegroups/historical_filegroups_documents_frozen": 0.9482287706093055, "filegroups/historical_filetypes_rtf_frozen": 0.9482287706093055, "filetypes/rtf": 0.9482287706093055, "general": 0.9482287706093055}` |
| filetypes/pdf | joint_or_at_fp_1 | 22292 | 3713 | 98.71% | 1 | 26932.40 | 127699.26 | 43.961 | 99.35% | 98.89% | `{"filegroups/documents": 0.9630042314529419, "filetypes/pdf": 0.554283082485199, "general": 0.9740650057792664}` |
| filetypes/batch | joint_or_at_fp_1 | 22536 | 1140 | 98.44% | 1 | 87719.30 | 415445.79 | 43.961 | 99.21% | 98.51% | `{"filegroups/scripts": 0.998256266117096, "filetypes/batch": 0.9772656559944153, "general": 0.9874888062477112}` |
| filetypes/elf† | max_rule | 25081 | 113027 | 98.32% | 1 | 884.74 | 4197.04 | 43.961 | 99.15% | 99.69% | `{"filegroups/historical_filetypes_elf_frozen": 0.999520037116952, "filegroups/native": 0.999520037116952, "filetypes/elf": 0.999520037116952, "general": 0.999520037116952}` |
| filetypes/rar† | or_general_primary | 2822 | 7 | 98.19% | 1 | 14285714.29 | 52070297.36 | 43.961 | 99.07% | 98.16% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/vbs† | max_rule | 1793 | 538 | 97.88% | 1 | 185873.61 | 878697.12 | 43.961 | 98.90% | 98.33% | `{"filegroups/code_pooled_recovery": 0.9908921369852757, "filegroups/scripts": 0.9908921369852757, "filegroups/vbs_hnm_recovery": 0.9908921369852757, "filetypes/vbs": 0.9908921369852757, "general": 0.9908921369852757}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3425 | 10118 | 97.69% | 1 | 9883.38 | 46876.72 | 43.961 | 98.82% | 99.41% | `{"filegroups/source": 0.9924882369757821, "filetypes/kotlin": 0.9107146969839861, "general": 0.9334020890928428}` |
| filetypes/html | joint_or_at_fp_1 | 11562 | 53999 | 97.69% | 1 | 1851.89 | 8784.79 | 43.961 | 98.83% | 99.59% | `{"filegroups/documents": 0.9038472771644592, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9928556084632874, "general": 0.9863055944442749}` |
| filetypes/ole_doc† | max_rule | 11935 | 3955 | 97.53% | 1 | 25284.45 | 119889.25 | 43.961 | 98.74% | 98.14% | `{"filegroups/documents": 0.9857095072854686, "filetypes/ole_doc": 0.9857095072854686, "general": 0.9857095072854686}` |
| filetypes/apk_android | learned_blend_at_fp_0 | 307 | 56 | 97.39% | 1 | 1785714.29 | 8193215.95 | 43.961 | 98.52% | 97.52% | `{}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 623 | 150 | 96.31% | 1 | 666666.67 | 3123381.69 | 43.961 | 98.04% | 96.90% | `{"filegroups/filetypes_lnk_oct26": 0.9978942872956885, "filegroups/lnk_general_layout_recovery": 0.9978942872956885, "filegroups/lnk_recovered": 0.9978942872956885, "filetypes/lnk": 0.9978942872956885, "general": 0.9978942872956885}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9987229312501931, "general": 0.9981635639211858}` |
| filetypes/static-lib† | max_rule | 259 | 1763 | 94.59% | 1 | 56721.50 | 268793.56 | 43.961 | 97.03% | 99.26% | `{"filetypes/static-lib": 0.9802111909143278, "general": 0.9802111909143278}` |
| filetypes/ooxml† | max_rule | 8467 | 726 | 93.80% | 1 | 137741.05 | 651742.48 | 43.961 | 96.79% | 94.28% | `{"filegroups/documents": 0.9930551490366089, "filetypes/ooxml": 0.9930551490366089, "general": 0.9930551490366089}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 93.75% | 0 | 0.00 | 8203163.59 | 0.000 | 96.77% | 98.04% | `{"filegroups/media": 0.9987229312501931, "general": 0.9981635639211858}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 48 | 93.58% | 1 | 2083333.33 | 9505862.46 | 43.961 | 96.64% | 93.77% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/ico | no_policy | 24 | 113 | 91.67% | 0 | 0.00 | 2616257.60 | 0.000 | 95.65% | 98.54% | `{}` |
| filetypes/groovy | no_policy | 8 | 1332 | 87.50% | 0 | 0.00 | 224652.10 | 0.000 | 93.33% | 99.93% | `{}` |
| filetypes/shell† | max_rule | 2252 | 21544 | 87.03% | 1 | 4641.66 | 22017.51 | 43.961 | 93.05% | 98.77% | `{"filegroups/scripts": 0.999741951735045, "filetypes/shell": 0.999741951735045, "general": 0.999741951735045}` |
| filetypes/gem | no_policy | 37 | 14781 | 86.49% | 0 | 0.00 | 20265.40 | 0.000 | 92.75% | 99.97% | `{}` |
| filetypes/ruby | no_policy | 34 | 25025 | 85.29% | 0 | 0.00 | 11970.24 | 0.000 | 92.06% | 99.98% | `{}` |
| filetypes/jar | joint_or_at_fp_1 | 520 | 5118 | 84.42% | 1 | 19538.88 | 92655.92 | 43.961 | 91.46% | 98.55% | `{"filegroups/archive": 0.9296517968177795, "filetypes/jar": 0.9572367072105408, "general": 0.9013851881027222}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 43.961 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999564105302579, "general": 0.944974520848534}` |
| filetypes/gif† | max_rule | 61 | 220 | 83.61% | 1 | 454545.45 | 2138041.18 | 43.961 | 90.27% | 96.09% | `{"filegroups/media": 0.9719515900012825, "filetypes/gif": 0.9719515900012825, "general": 0.9719515900012825}` |
| filetypes/zip† | specialist_primary_with_escape | 13624 | 18069 | 83.32% | 1 | 5534.34 | 26251.44 | 43.961 | 90.90% | 92.82% | `{"filegroups/archive": 0.9992485030562741, "filetypes/zip": 0.9990234228963106, "general": 0.9842316522650206}` |
