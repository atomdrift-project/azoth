# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `6309383805`
- Rows: 2652931 (382587 malware, 2270344 benign)

## L50 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 0 | 0.00 | 20581666.52 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 100.00% | 0 | 0.00 | 8203163.59 | 0.000 | 100.00% | 100.00% | `{"filegroups/media": 0.9988318690912369, "general": 0.9990562313772477}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908549801468282, "filegroups/source": 0.9947689075113982, "general": 0.9990562313772477}` |
| filetypes/python_sdist† | max_rule | 366 | 1402 | 99.18% | 1 | 71326.68 | 337912.64 | 44.046 | 99.45% | 99.77% | `{"filegroups/archive": 0.9470124969109345, "filetypes/python_sdist": 0.9470124969109345, "general": 0.9470124969109345}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 44.046 | 99.50% | 99.14% | `{"filegroups/documents": 0.9606474437030769, "filegroups/historical_filegroups_documents_frozen": 0.9606474437030769, "filegroups/historical_filetypes_rtf_frozen": 0.9606474437030769, "filetypes/rtf": 0.9606474437030769, "general": 0.9606474437030769}` |
| filetypes/pdf | joint_or_at_fp_1 | 22298 | 3708 | 98.69% | 1 | 26968.72 | 127871.37 | 44.046 | 99.34% | 98.87% | `{"filegroups/documents": 0.9853893518447876, "filetypes/pdf": 0.6671142578125, "general": 0.9835995435714722}` |
| filetypes/batch | joint_or_at_fp_1 | 22534 | 1132 | 98.47% | 1 | 88339.22 | 418376.95 | 44.046 | 99.23% | 98.54% | `{"filegroups/scripts": 0.9976352453231812, "filetypes/batch": 0.9839461445808411, "general": 0.9781961441040039}` |
| filetypes/elf† | max_rule | 24901 | 113015 | 98.42% | 1 | 884.84 | 4197.48 | 44.046 | 99.20% | 99.71% | `{"filegroups/historical_filetypes_elf_frozen": 0.9991920511080045, "filegroups/native": 0.9991920511080045, "filetypes/elf": 0.9991920511080045, "general": 0.9991920511080045}` |
| filetypes/rar† | or_general_primary | 2816 | 7 | 98.08% | 1 | 14285714.29 | 52070297.36 | 44.046 | 99.01% | 98.05% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/apk_android | joint_or_at_fp_1 | 301 | 55 | 98.01% | 1 | 1818181.82 | 8337134.23 | 44.046 | 98.83% | 98.03% | `{"filegroups/apk_android_retained_hnm_recovery": 0.43480220437049866, "filegroups/archive": 0.9911814332008362, "filetypes/apk_android": 0.39192554354667664, "general": 0.8427503705024719}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3437 | 10231 | 97.41% | 1 | 9774.22 | 46359.07 | 44.046 | 98.67% | 99.34% | `{"filegroups/source": 0.990062424508119, "filetypes/kotlin": 0.9527585263754375, "general": 0.9355679843210519}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/vbs† | max_rule | 1800 | 528 | 96.94% | 1 | 189393.94 | 895280.14 | 44.046 | 98.42% | 97.59% | `{"filegroups/code_pooled_recovery": 0.9908950173958693, "filegroups/scripts": 0.9908950173958693, "filegroups/vbs_hnm_recovery": 0.9908950173958693, "filetypes/vbs": 0.9908950173958693, "general": 0.9908950173958693}` |
| filetypes/html† | max_rule | 11559 | 53931 | 96.22% | 1 | 1854.22 | 8795.87 | 44.046 | 98.07% | 99.33% | `{"filegroups/documents": 0.9999391681933224, "filegroups/historical_filegroups_documents_frozen": 0.9999391681933224, "filegroups/historical_filetypes_html_frozen": 0.9999391681933224, "filegroups/html_benign_weight_recovery": 0.9999391681933224, "filegroups/html_general_layout_recovery": 0.9999391681933224, "filegroups/html_hnm_recovery": 0.9999391681933224, "filegroups/nightly_filetypes_html_frozen": 0.9999391681933224, "filetypes/html": 0.9999391681933224, "general": 0.9999391681933224}` |
| filetypes/ole_doc† | specialist_primary_with_escape | 11920 | 3954 | 96.10% | 1 | 25290.84 | 119919.56 | 44.046 | 98.01% | 97.06% | `{"filegroups/documents": 0.9962617186309309, "filetypes/ole_doc": 0.9918482018194927, "general": 0.9847046922235729}` |
| filetypes/lnk† | max_rule | 628 | 149 | 95.38% | 1 | 671140.94 | 3144081.01 | 44.046 | 97.56% | 96.14% | `{"filegroups/filetypes_lnk_oct26": 0.9963261781147345, "filegroups/lnk_general_layout_recovery": 0.9963261781147345, "filegroups/lnk_recovered": 0.9963261781147345, "filetypes/lnk": 0.9963261781147345, "general": 0.9963261781147345}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 47 | 94.23% | 1 | 2127659.57 | 9700098.59 | 44.046 | 96.98% | 94.39% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/ooxml | joint_or_at_fp_1 | 8471 | 721 | 92.72% | 1 | 138696.26 | 656250.46 | 44.046 | 96.21% | 93.28% | `{"filegroups/documents": 0.9786916971206665, "filetypes/ooxml": 0.9964943528175354, "general": 0.9797331094741821}` |
| filetypes/jar† | max_rule | 497 | 5120 | 92.15% | 1 | 19531.25 | 92619.74 | 44.046 | 95.82% | 99.29% | `{"filegroups/archive": 0.9465099216895059, "filetypes/jar": 0.9465099216895059, "general": 0.9465099216895059}` |
| filetypes/mp3 | calibrate_inherited | 21 | 40 | 90.48% | 0 | 0.00 | 7215752.45 | 0.000 | 95.00% | 96.72% | `{"filegroups/media": 0.9988318690912369, "general": 0.9990562313772477}` |
| filetypes/dos_com† | specialist_primary_with_escape | 751 | 26 | 90.01% | 1 | 3846153.85 | 16983122.30 | 44.046 | 94.68% | 90.22% | `{"filetypes/dos_com": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/gem | joint_or_at_fp_1 | 76 | 14846 | 88.16% | 0 | 0.00 | 20176.68 | 0.000 | 93.71% | 99.94% | `{"filegroups/archive": 0.8988714218139648, "filetypes/gem": 0.8286291360855103, "general": 0.8357003331184387}` |
| filetypes/shell† | specialist_primary_with_escape | 2246 | 21427 | 86.02% | 1 | 4667.01 | 22137.72 | 44.046 | 92.46% | 98.67% | `{"filegroups/scripts": 0.9996237141546661, "filetypes/shell": 0.9998233581711575, "general": 0.9833777813644715}` |
| filetypes/nupkg | no_policy | 7 | 1411 | 85.71% | 0 | 0.00 | 212087.48 | 0.000 | 92.31% | 99.93% | `{}` |
| filetypes/lua | no_policy | 6 | 3623 | 83.33% | 0 | 0.00 | 82652.33 | 0.000 | 90.91% | 99.97% | `{}` |
| filetypes/pe† | max_rule | 205699 | 33689 | 82.69% | 1 | 2968.33 | 14080.56 | 44.046 | 90.52% | 85.12% | `{"filegroups/native": 0.9999167804030593, "filegroups/native_previous": 0.9999167804030593, "filegroups/pe_previous": 0.9999167804030593, "filetypes/pe": 0.9999167804030593, "general": 0.9999167804030593}` |
| filetypes/registry† | specialist_primary_with_escape | 56 | 13839 | 82.14% | 1 | 7225.96 | 34274.32 | 44.046 | 89.32% | 99.92% | `{"filetypes/registry": 0.9999676605791498, "general": 0.9451954059950236}` |
| filetypes/groovy | no_policy | 10 | 1332 | 80.00% | 0 | 0.00 | 224652.10 | 0.000 | 88.89% | 99.85% | `{}` |
| filetypes/macho | joint_or_at_fp_1 | 372 | 4708 | 79.84% | 1 | 21240.44 | 100721.72 | 44.046 | 88.66% | 98.50% | `{"filegroups/historical_filetypes_macho_frozen": 0.9902840852737427, "filegroups/native": 0.48048922419548035, "filetypes/macho": 0.9597336053848267, "general": 0.9647952318191528}` |
| filetypes/php | learned_blend_at_fp_1 | 802 | 79215 | 79.55% | 1 | 1262.39 | 5988.45 | 44.046 | 88.55% | 99.79% | `{}` |

## L100 Hostile

Levels use the [shared pool-adjusted allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. Rows marked † have limited calibration resolution; the marker does not mean zero observed FPs. FP/100M is the observed rate on the reported partition. The 95% upper bound is separate from the count allowance and assumes representative sampling.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/cab | max_rule | 107 | 13 | 100.00% | 0 | 0.00 | 20581666.52 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/bmp | calibrate_inherited | 16 | 35 | 100.00% | 0 | 0.00 | 8203163.59 | 0.000 | 100.00% | 100.00% | `{"filegroups/media": 0.9988068866802998, "general": 0.9986335874655291}` |
| filetypes/swift | calibrate_inherited | 2 | 5564 | 100.00% | 0 | 0.00 | 53826.85 | 0.000 | 100.00% | 100.00% | `{"filegroups/code_pooled_recovery": 0.9908133325989518, "filegroups/source": 0.9946805843033826, "general": 0.9986335874655291}` |
| filetypes/python_sdist† | max_rule | 366 | 1402 | 99.18% | 1 | 71326.68 | 337912.64 | 44.046 | 99.45% | 99.77% | `{"filegroups/archive": 0.9468920338379037, "filetypes/python_sdist": 0.9468920338379037, "general": 0.9468920338379037}` |
| filetypes/rtf† | max_rule | 796 | 135 | 99.12% | 1 | 740740.74 | 3465622.47 | 44.046 | 99.50% | 99.14% | `{"filegroups/documents": 0.9606454161386361, "filegroups/historical_filegroups_documents_frozen": 0.9606454161386361, "filegroups/historical_filetypes_rtf_frozen": 0.9606454161386361, "filetypes/rtf": 0.9606454161386361, "general": 0.9606454161386361}` |
| filetypes/pdf | joint_or_at_fp_1 | 22298 | 3708 | 98.69% | 1 | 26968.72 | 127871.37 | 44.046 | 99.34% | 98.87% | `{"filegroups/documents": 0.9853893518447876, "filetypes/pdf": 0.6671142578125, "general": 0.9835995435714722}` |
| filetypes/batch | joint_or_at_fp_1 | 22534 | 1132 | 98.47% | 1 | 88339.22 | 418376.95 | 44.046 | 99.23% | 98.54% | `{"filegroups/scripts": 0.9976352453231812, "filetypes/batch": 0.9839461445808411, "general": 0.9781961441040039}` |
| filetypes/elf† | max_rule | 24901 | 113015 | 98.42% | 1 | 884.84 | 4197.48 | 44.046 | 99.20% | 99.71% | `{"filegroups/historical_filetypes_elf_frozen": 0.999092037450793, "filegroups/native": 0.999092037450793, "filetypes/elf": 0.999092037450793, "general": 0.999092037450793}` |
| filetypes/rar† | or_general_primary | 2816 | 7 | 98.08% | 1 | 14285714.29 | 52070297.36 | 44.046 | 99.01% | 98.05% | `{"filegroups/archive": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/apk_android | joint_or_at_fp_1 | 301 | 55 | 98.01% | 1 | 1818181.82 | 8337134.23 | 44.046 | 98.83% | 98.03% | `{"filegroups/apk_android_retained_hnm_recovery": 0.43480220437049866, "filegroups/archive": 0.9911814332008362, "filetypes/apk_android": 0.39192554354667664, "general": 0.8427503705024719}` |
| filetypes/kotlin† | specialist_primary_with_escape | 3437 | 10231 | 97.41% | 1 | 9774.22 | 46359.07 | 44.046 | 98.67% | 99.34% | `{"filegroups/source": 0.9899654135503001, "filetypes/kotlin": 0.9524749030255466, "general": 0.935072446293933}` |
| filetypes/asar | no_policy | 35 | 51 | 97.14% | 0 | 0.00 | 5704795.24 | 0.000 | 98.55% | 98.84% | `{}` |
| filetypes/vbs† | max_rule | 1800 | 528 | 96.94% | 1 | 189393.94 | 895280.14 | 44.046 | 98.42% | 97.59% | `{"filegroups/code_pooled_recovery": 0.9908942110597813, "filegroups/scripts": 0.9908942110597813, "filegroups/vbs_hnm_recovery": 0.9908942110597813, "filetypes/vbs": 0.9908942110597813, "general": 0.9908942110597813}` |
| filetypes/html† | max_rule | 11559 | 53931 | 96.22% | 1 | 1854.22 | 8795.87 | 44.046 | 98.07% | 99.33% | `{"filegroups/documents": 0.999930684912026, "filegroups/historical_filegroups_documents_frozen": 0.999930684912026, "filegroups/historical_filetypes_html_frozen": 0.999930684912026, "filegroups/html_benign_weight_recovery": 0.999930684912026, "filegroups/html_general_layout_recovery": 0.999930684912026, "filegroups/html_hnm_recovery": 0.999930684912026, "filegroups/nightly_filetypes_html_frozen": 0.999930684912026, "filetypes/html": 0.999930684912026, "general": 0.999930684912026}` |
| filetypes/ole_doc† | specialist_primary_with_escape | 11920 | 3954 | 96.10% | 1 | 25290.84 | 119919.56 | 44.046 | 98.01% | 97.06% | `{"filegroups/documents": 0.9962513128002363, "filetypes/ole_doc": 0.9918268722110005, "general": 0.9846894604263835}` |
| filetypes/lnk† | max_rule | 628 | 149 | 95.38% | 1 | 671140.94 | 3144081.01 | 44.046 | 97.56% | 96.14% | `{"filegroups/filetypes_lnk_oct26": 0.9963254783910402, "filegroups/lnk_general_layout_recovery": 0.9963254783910402, "filegroups/lnk_recovered": 0.9963254783910402, "filetypes/lnk": 0.9963254783910402, "general": 0.9963254783910402}` |
| filetypes/7z† | specialist_primary_with_escape | 1075 | 47 | 94.23% | 1 | 2127659.57 | 9700098.59 | 44.046 | 96.98% | 94.39% | `{"filegroups/archive": 1.0000001192092896, "filetypes/7z": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/ooxml | joint_or_at_fp_1 | 8471 | 721 | 92.72% | 1 | 138696.26 | 656250.46 | 44.046 | 96.21% | 93.28% | `{"filegroups/documents": 0.9786916971206665, "filetypes/ooxml": 0.9964943528175354, "general": 0.9797331094741821}` |
| filetypes/jar† | max_rule | 497 | 5120 | 92.15% | 1 | 19531.25 | 92619.74 | 44.046 | 95.82% | 99.29% | `{"filegroups/archive": 0.946401875553578, "filetypes/jar": 0.946401875553578, "general": 0.946401875553578}` |
| filetypes/mp3 | calibrate_inherited | 21 | 40 | 90.48% | 0 | 0.00 | 7215752.45 | 0.000 | 95.00% | 96.72% | `{"filegroups/media": 0.9988068866802998, "general": 0.9986335874655291}` |
| filetypes/dos_com† | specialist_primary_with_escape | 751 | 26 | 90.01% | 1 | 3846153.85 | 16983122.30 | 44.046 | 94.68% | 90.22% | `{"filetypes/dos_com": 1.0000001192092896, "general": 1.0000001192092896}` |
| filetypes/gem | joint_or_at_fp_1 | 76 | 14846 | 88.16% | 0 | 0.00 | 20176.68 | 0.000 | 93.71% | 99.94% | `{"filegroups/archive": 0.8988714218139648, "filetypes/gem": 0.8286291360855103, "general": 0.8357003331184387}` |
| filetypes/shell† | specialist_primary_with_escape | 2246 | 21427 | 86.02% | 1 | 4667.01 | 22137.72 | 44.046 | 92.46% | 98.67% | `{"filegroups/scripts": 0.9995983444769582, "filetypes/shell": 0.9998144752808346, "general": 0.9829638127825604}` |
| filetypes/nupkg | no_policy | 7 | 1411 | 85.71% | 0 | 0.00 | 212087.48 | 0.000 | 92.31% | 99.93% | `{}` |
| filetypes/lua | no_policy | 6 | 3623 | 83.33% | 0 | 0.00 | 82652.33 | 0.000 | 90.91% | 99.97% | `{}` |
| filetypes/pe† | max_rule | 205699 | 33689 | 82.69% | 1 | 2968.33 | 14080.56 | 44.046 | 90.52% | 85.12% | `{"filegroups/native": 0.99991114721141, "filegroups/native_previous": 0.99991114721141, "filegroups/pe_previous": 0.99991114721141, "filetypes/pe": 0.99991114721141, "general": 0.99991114721141}` |
| filetypes/registry† | specialist_primary_with_escape | 56 | 13839 | 82.14% | 1 | 7225.96 | 34274.32 | 44.046 | 89.32% | 99.92% | `{"filetypes/registry": 0.999966434136836, "general": 0.9432827653596524}` |
| filetypes/groovy | no_policy | 10 | 1332 | 80.00% | 0 | 0.00 | 224652.10 | 0.000 | 88.89% | 99.85% | `{}` |
| filetypes/macho | joint_or_at_fp_1 | 372 | 4708 | 79.84% | 1 | 21240.44 | 100721.72 | 44.046 | 88.66% | 98.50% | `{"filegroups/historical_filetypes_macho_frozen": 0.9902840852737427, "filegroups/native": 0.48048922419548035, "filetypes/macho": 0.9597336053848267, "general": 0.9647952318191528}` |
| filetypes/php | learned_blend_at_fp_1 | 802 | 79215 | 79.55% | 1 | 1262.39 | 5988.45 | 44.046 | 88.55% | 99.79% | `{}` |
