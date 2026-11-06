# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `6309383805`
- Rows: 2652880 (382120 malware, 2270760 benign)

## L50 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 1 | 7692307.69 | 31633976.48 | 44.038 | 99.53% | 99.17% | `{}` |
| filetypes/nupkg | no_policy | 7 | 1411 | 100.00% | 0 | 0.00 | 212087.48 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908549969543036, "filegroups/source": 0.9930433099720437, "general": 0.998689530965773}` |
| filetypes/python_sdist | learned_blend_at_fp_0 | 366 | 1400 | 99.45% | 1 | 71428.57 | 338394.73 | 44.038 | 99.59% | 99.83% | `{}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 44.038 | 99.50% | 99.14% | `{"filegroups/documents": 0.954739004504151, "filegroups/historical_filegroups_documents_frozen": 0.954739004504151, "filegroups/historical_filetypes_rtf_frozen": 0.954739004504151, "filetypes/rtf": 0.954739004504151, "general": 0.954739004504151}` |
| filetypes/rar† | or_general_primary | 2814 | 7 | 98.79% | 1 | 14285714.29 | 52070297.36 | 44.038 | 99.37% | 98.76% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/pdf | joint_or_at_fp_0 | 22293 | 3713 | 98.75% | 1 | 26932.40 | 127699.26 | 44.038 | 99.37% | 98.93% | `{"filegroups/documents": 0.9802718162536621, "filetypes/pdf": 0.6133713126182556, "general": 0.9832737445831299}` |
| filetypes/elf† | max_rule | 24898 | 113018 | 98.26% | 1 | 884.81 | 4197.37 | 44.038 | 99.12% | 99.68% | `{"filegroups/historical_filetypes_elf_frozen": 0.9992675596951728, "filegroups/native": 0.9992675596951728, "filetypes/elf": 0.9992675596951728, "general": 0.9992675596951728}` |
| filetypes/batch† | max_rule | 22530 | 1136 | 98.25% | 1 | 88028.17 | 416906.22 | 44.038 | 99.11% | 98.33% | `{"filegroups/scripts": 0.9983524806710444, "filetypes/batch": 0.9983524806710444, "general": 0.9983524806710444}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3420 | 10228 | 98.04% | 1 | 9777.08 | 46372.67 | 44.038 | 99.00% | 99.50% | `{"filegroups/source": 0.9831837482422265, "filetypes/kotlin": 0.9118036081425986, "general": 0.9425888310547489}` |
| filetypes/apk_android | joint_or_at_fp_1 | 301 | 55 | 98.01% | 1 | 1818181.82 | 8337134.23 | 44.038 | 98.83% | 98.03% | `{"filegroups/apk_android_retained_hnm_recovery": 0.43480220437049866, "filegroups/archive": 0.9882510304450989, "filetypes/apk_android": 0.747052013874054, "general": 0.8061236143112183}` |
| filetypes/html | joint_or_at_fp_1 | 11560 | 53935 | 97.59% | 1 | 1854.08 | 8795.22 | 44.038 | 98.77% | 99.57% | `{"filegroups/documents": 0.9143039584159851, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9872599840164185, "general": 0.9859640598297119}` |
| filetypes/ole_doc | joint_or_at_fp_1 | 11919 | 3955 | 97.50% | 1 | 25284.45 | 119889.25 | 44.038 | 98.73% | 98.12% | `{"filegroups/documents": 0.9850714206695557, "filetypes/ole_doc": 0.9630153179168701, "general": 0.9764810800552368}` |
| filetypes/vbs† | max_rule | 1799 | 528 | 97.28% | 1 | 189393.94 | 895280.14 | 44.038 | 98.59% | 97.85% | `{"filegroups/code_pooled_recovery": 0.9908935884747717, "filegroups/scripts": 0.9908935884747717, "filegroups/vbs_hnm_recovery": 0.9908935884747717, "filetypes/vbs": 0.9908935884747717, "general": 0.9908935884747717}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 622 | 150 | 96.30% | 1 | 666666.67 | 3123381.69 | 44.038 | 98.04% | 96.89% | `{"filegroups/filetypes_lnk_oct26": 0.9967543239568158, "filegroups/lnk_general_layout_recovery": 0.9967543239568158, "filegroups/lnk_recovered": 0.9967543239568158, "filetypes/lnk": 0.9967543239568158, "general": 0.9967543239568158}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9989754868465454, "general": 0.998689530965773}` |
| filetypes/7z† | specialist_primary_with_escape | 1073 | 49 | 94.32% | 1 | 2040816.33 | 9319247.14 | 44.038 | 97.03% | 94.47% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 93.75% | 0 | 0.00 | 8203163.59 | 0.000 | 96.77% | 98.04% | `{"filegroups/media": 0.9989754868465454, "general": 0.998689530965773}` |
| filetypes/ooxml | joint_or_at_fp_1 | 8465 | 727 | 92.98% | 1 | 137551.58 | 650848.30 | 44.038 | 96.36% | 93.53% | `{"filegroups/documents": 0.9870941638946533, "filetypes/ooxml": 0.9940418004989624, "general": 0.9809531569480896}` |
| filetypes/ico | no_policy | 24 | 112 | 91.67% | 0 | 0.00 | 2639306.04 | 0.000 | 95.65% | 98.53% | `{}` |
| filetypes/dos_com† | specialist_primary_with_escape | 750 | 27 | 90.00% | 1 | 3703703.70 | 16397439.47 | 44.038 | 94.67% | 90.22% | `{"filetypes/dos_com": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/gem† | max_rule | 66 | 14863 | 87.88% | 1 | 6728.12 | 31913.25 | 44.038 | 92.80% | 99.94% | `{"filegroups/archive": 0.9966753455612106, "filetypes/gem": 0.9966753455612106, "general": 0.9966753455612106}` |
| filetypes/shell† | specialist_primary_with_escape | 2232 | 21445 | 86.92% | 1 | 4663.09 | 22119.14 | 44.038 | 92.98% | 98.76% | `{"filegroups/scripts": 0.9996479721015396, "filetypes/shell": 0.9995694949326075, "general": 0.9876934428291373}` |
| filetypes/jar | joint_or_at_fp_1 | 499 | 5120 | 86.57% | 1 | 19531.25 | 92619.74 | 44.038 | 92.70% | 98.79% | `{"filegroups/archive": 0.9253693222999573, "filetypes/jar": 0.9552077054977417, "general": 0.9010462164878845}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 44.038 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999525835570215, "general": 0.9463588880284793}` |
| filetypes/pe† | max_rule | 205693 | 33690 | 83.13% | 1 | 2968.24 | 14080.15 | 44.038 | 90.79% | 85.50% | `{"filegroups/native": 0.9999167802431892, "filegroups/native_previous": 0.9999167802431892, "filegroups/pe_previous": 0.9999167802431892, "filetypes/pe": 0.9999167802431892, "general": 0.9999167802431892}` |
| filetypes/ruby | no_policy | 39 | 25005 | 82.05% | 0 | 0.00 | 11979.82 | 0.000 | 90.14% | 99.97% | `{}` |
| filetypes/php | learned_blend_at_fp_0 | 781 | 79235 | 81.18% | 1 | 1262.07 | 5986.94 | 44.038 | 89.55% | 99.82% | `{}` |
| filetypes/macho† | max_rule | 365 | 4713 | 80.82% | 1 | 21217.91 | 100614.91 | 44.038 | 89.26% | 98.60% | `{"filegroups/historical_filetypes_macho_frozen": 0.99022960382482, "filegroups/native": 0.99022960382482, "filetypes/macho": 0.99022960382482, "general": 0.99022960382482}` |

## L100 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 1 | 7692307.69 | 31633976.48 | 44.038 | 99.53% | 99.17% | `{}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 100.00% | 0 | 0.00 | 8203163.59 | 0.000 | 100.00% | 100.00% | `{"filegroups/media": 0.9989225367273282, "general": 0.9986730306877832}` |
| filetypes/nupkg | no_policy | 7 | 1411 | 100.00% | 0 | 0.00 | 212087.48 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908133665460133, "filegroups/source": 0.9927848457221773, "general": 0.9986730306877832}` |
| filetypes/python_sdist | learned_blend_at_fp_0 | 366 | 1400 | 99.45% | 1 | 71428.57 | 338394.73 | 44.038 | 99.59% | 99.83% | `{}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 44.038 | 99.50% | 99.14% | `{"filegroups/documents": 0.9547367847141613, "filegroups/historical_filegroups_documents_frozen": 0.9547367847141613, "filegroups/historical_filetypes_rtf_frozen": 0.9547367847141613, "filetypes/rtf": 0.9547367847141613, "general": 0.9547367847141613}` |
| filetypes/rar† | or_general_primary | 2814 | 7 | 98.79% | 1 | 14285714.29 | 52070297.36 | 44.038 | 99.37% | 98.76% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/pdf | joint_or_at_fp_0 | 22293 | 3713 | 98.75% | 1 | 26932.40 | 127699.26 | 44.038 | 99.37% | 98.93% | `{"filegroups/documents": 0.9802718162536621, "filetypes/pdf": 0.6133713126182556, "general": 0.9832737445831299}` |
| filetypes/elf† | max_rule | 24898 | 113018 | 98.26% | 1 | 884.81 | 4197.37 | 44.038 | 99.12% | 99.68% | `{"filegroups/historical_filetypes_elf_frozen": 0.9991753456702376, "filegroups/native": 0.9991753456702376, "filetypes/elf": 0.9991753456702376, "general": 0.9991753456702376}` |
| filetypes/batch† | max_rule | 22530 | 1136 | 98.25% | 1 | 88028.17 | 416906.22 | 44.038 | 99.11% | 98.33% | `{"filegroups/scripts": 0.9983519463260527, "filetypes/batch": 0.9983519463260527, "general": 0.9983519463260527}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3420 | 10228 | 98.04% | 1 | 9777.08 | 46372.67 | 44.038 | 99.00% | 99.50% | `{"filegroups/source": 0.982992546843591, "filetypes/kotlin": 0.9116532448870853, "general": 0.9421648307798381}` |
| filetypes/apk_android | joint_or_at_fp_1 | 301 | 55 | 98.01% | 1 | 1818181.82 | 8337134.23 | 44.038 | 98.83% | 98.03% | `{"filegroups/apk_android_retained_hnm_recovery": 0.43480220437049866, "filegroups/archive": 0.9882510304450989, "filetypes/apk_android": 0.747052013874054, "general": 0.8061236143112183}` |
| filetypes/html | joint_or_at_fp_1 | 11560 | 53935 | 97.59% | 1 | 1854.08 | 8795.22 | 44.038 | 98.77% | 99.57% | `{"filegroups/documents": 0.9143039584159851, "filegroups/historical_filegroups_documents_frozen": 0.9956439137458801, "filegroups/historical_filetypes_html_frozen": 0.9977225661277771, "filegroups/html_benign_weight_recovery": 0.9964984059333801, "filegroups/html_general_layout_recovery": 0.9982547163963318, "filegroups/html_hnm_recovery": 0.9750067591667175, "filegroups/nightly_filetypes_html_frozen": 0.9963761568069458, "filetypes/html": 0.9872599840164185, "general": 0.9859640598297119}` |
| filetypes/ole_doc | joint_or_at_fp_1 | 11919 | 3955 | 97.50% | 1 | 25284.45 | 119889.25 | 44.038 | 98.73% | 98.12% | `{"filegroups/documents": 0.9850714206695557, "filetypes/ole_doc": 0.9630153179168701, "general": 0.9764810800552368}` |
| filetypes/vbs† | max_rule | 1799 | 528 | 97.28% | 1 | 189393.94 | 895280.14 | 44.038 | 98.59% | 97.85% | `{"filegroups/code_pooled_recovery": 0.9908913239546077, "filegroups/scripts": 0.9908913239546077, "filegroups/vbs_hnm_recovery": 0.9908913239546077, "filetypes/vbs": 0.9908913239546077, "general": 0.9908913239546077}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/lnk† | max_rule | 622 | 150 | 96.30% | 1 | 666666.67 | 3123381.69 | 44.038 | 98.04% | 96.89% | `{"filegroups/filetypes_lnk_oct26": 0.9967538125291605, "filegroups/lnk_general_layout_recovery": 0.9967538125291605, "filegroups/lnk_recovered": 0.9967538125291605, "filetypes/lnk": 0.9967538125291605, "general": 0.9967538125291605}` |
| filetypes/mp3 | calibrate_inherited | 20 | 41 | 95.00% | 0 | 0.00 | 7046111.73 | 0.000 | 97.44% | 98.36% | `{"filegroups/media": 0.9989225367273282, "general": 0.9986730306877832}` |
| filetypes/7z† | specialist_primary_with_escape | 1073 | 49 | 94.32% | 1 | 2040816.33 | 9319247.14 | 44.038 | 97.03% | 94.47% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/ooxml | joint_or_at_fp_1 | 8465 | 727 | 92.98% | 1 | 137551.58 | 650848.30 | 44.038 | 96.36% | 93.53% | `{"filegroups/documents": 0.9870941638946533, "filetypes/ooxml": 0.9940418004989624, "general": 0.9809531569480896}` |
| filetypes/ico | no_policy | 24 | 112 | 91.67% | 0 | 0.00 | 2639306.04 | 0.000 | 95.65% | 98.53% | `{}` |
| filetypes/dos_com† | specialist_primary_with_escape | 750 | 27 | 90.00% | 1 | 3703703.70 | 16397439.47 | 44.038 | 94.67% | 90.22% | `{"filetypes/dos_com": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/gem† | max_rule | 66 | 14863 | 87.88% | 1 | 6728.12 | 31913.25 | 44.038 | 92.80% | 99.94% | `{"filegroups/archive": 0.9965720687956708, "filetypes/gem": 0.9965720687956708, "general": 0.9965720687956708}` |
| filetypes/shell† | specialist_primary_with_escape | 2232 | 21445 | 86.92% | 1 | 4663.09 | 22119.14 | 44.038 | 92.98% | 98.76% | `{"filegroups/scripts": 0.9996212344153659, "filetypes/shell": 0.9995486998513118, "general": 0.9874323979279495}` |
| filetypes/jar | joint_or_at_fp_1 | 499 | 5120 | 86.57% | 1 | 19531.25 | 92619.74 | 44.038 | 92.70% | 98.79% | `{"filegroups/archive": 0.9253693222999573, "filetypes/jar": 0.9552077054977417, "general": 0.9010462164878845}` |
| filetypes/registry† | specialist_primary_with_escape | 55 | 13839 | 83.64% | 1 | 7225.96 | 34274.32 | 44.038 | 90.20% | 99.93% | `{"filetypes/registry": 0.9999514382004194, "general": 0.9445928812470086}` |
| filetypes/pe† | max_rule | 205693 | 33690 | 83.13% | 1 | 2968.24 | 14080.15 | 44.038 | 90.79% | 85.50% | `{"filegroups/native": 0.9999111468721659, "filegroups/native_previous": 0.9999111468721659, "filegroups/pe_previous": 0.9999111468721659, "filetypes/pe": 0.9999111468721659, "general": 0.9999111468721659}` |
| filetypes/ruby | no_policy | 39 | 25005 | 82.05% | 0 | 0.00 | 11979.82 | 0.000 | 90.14% | 99.97% | `{}` |
| filetypes/php | learned_blend_at_fp_0 | 781 | 79235 | 81.18% | 1 | 1262.07 | 5986.94 | 44.038 | 89.55% | 99.82% | `{}` |
| filetypes/macho† | max_rule | 365 | 4713 | 80.82% | 1 | 21217.91 | 100614.91 | 44.038 | 89.26% | 98.60% | `{"filegroups/historical_filetypes_macho_frozen": 0.9902173893904322, "filegroups/native": 0.9902173893904322, "filetypes/macho": 0.9902173893904322, "general": 0.9902173893904322}` |
