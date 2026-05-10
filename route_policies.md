# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `762136079`
- Rows: 374918 (77361 malware, 297557 benign)

## L5 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/zst | general_only | 273 | 2062 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.005351923406124115}` |
| filetypes/doc | group_only | 206 | 6 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.011448593810200691}` |
| filetypes/rar | general_only | 122 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.00030210227123461664}` |
| filetypes/msi | or_general_primary | 36 | 9 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/msi": 0.28024280071258545, "general": 0.9713645577430725}` |
| filetypes/lnk | general_only | 35 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.8371633887290955}` |
| filetypes/ole | or_general_primary | 26 | 655 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/ole": 0.9222427606582642, "general": 0.9518448114395142}` |
| filetypes/crx | general_only | 9 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8564377427101135}` |
| filetypes/rtf | or_general_primary | 9 | 59 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/rtf": 0.7234269976615906, "general": 0.9769636392593384}` |
| filetypes/ruby | group_only | 9 | 2924 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/scripts": 0.9963645935058594}` |
| filetypes/lua | general_only | 3 | 1319 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.7351991534233093}` |
| filetypes/chm | general_only | 2 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9906882047653198}` |
| filetypes/html | general_only | 2 | 177 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9354889392852783}` |
| filetypes/java | general_only | 2 | 3529 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9540349841117859}` |
| filetypes/cab | general_only | 1 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9981394410133362}` |
| filetypes/groovy | general_only | 1 | 588 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9754495620727539}` |
| filetypes/pptx | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8636189699172974}` |
| filetypes/tar.xz | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8365404009819031}` |
| filetypes/tar | or_general_primary | 146 | 46 | 99.32% | 0 | 0.00 | 0.000 | 99.66% | 99.48% | `{"filetypes/tar": 0.47724226117134094, "general": 0.7868746519088745}` |
| filetypes/pkg-info | general_only | 485 | 96 | 95.67% | 0 | 0.00 | 0.000 | 97.79% | 96.39% | `{"general": 0.02792925015091896}` |
| filetypes/xls | general_only | 21 | 4 | 95.24% | 0 | 0.00 | 0.000 | 97.56% | 96.00% | `{"general": 0.0009061877499334514}` |
| filetypes/python-bytecode | filetype_only | 109 | 1267 | 94.50% | 0 | 0.00 | 0.000 | 97.17% | 99.56% | `{"filetypes/python-bytecode": 0.9863467216491699}` |
| filetypes/data | general_only | 43 | 1064 | 90.70% | 0 | 0.00 | 0.000 | 95.12% | 99.64% | `{"general": 0.853091299533844}` |
| filetypes/docx | general_only | 67 | 27 | 89.55% | 0 | 0.00 | 0.000 | 94.49% | 92.55% | `{"general": 0.11987817287445068}` |
| filetypes/macho | specialist_primary_with_escape | 163 | 721 | 88.34% | 0 | 0.00 | 0.000 | 93.81% | 97.85% | `{"filegroups/native": 0.99602872133255, "filetypes/macho": 0.7973178625106812}` |
| filetypes/pe | specialist_primary_with_escape | 51401 | 17486 | 88.28% | 1 | 57.19 | 3.361 | 93.77% | 91.25% | `{"filegroups/native": 0.999194860458374, "filetypes/pe": 0.9990107417106628, "general": 0.9957654476165771}` |
| filetypes/applescript | general_only | 5 | 16 | 80.00% | 0 | 0.00 | 0.000 | 88.89% | 95.24% | `{"general": 0.9594946503639221}` |
| filetypes/xlsx | general_only | 17 | 8 | 76.47% | 0 | 0.00 | 0.000 | 86.67% | 84.00% | `{"general": 0.0004667504399549216}` |
| filetypes/xz | general_only | 4 | 2886 | 75.00% | 0 | 0.00 | 0.000 | 85.71% | 99.97% | `{"general": 0.9911648035049438}` |
| filetypes/perl | group_only | 21 | 3650 | 66.67% | 0 | 0.00 | 0.000 | 80.00% | 99.81% | `{"filegroups/scripts": 0.07316567003726959}` |
| filetypes/shell | group_only | 281 | 5058 | 65.84% | 0 | 0.00 | 0.000 | 79.40% | 98.20% | `{"filegroups/scripts": 0.9826321005821228}` |

## L9 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/zst | general_only | 273 | 2062 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.005351923406124115}` |
| filetypes/doc | group_only | 206 | 6 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.011448593810200691}` |
| filetypes/rar | general_only | 122 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.00030210227123461664}` |
| filetypes/msi | or_general_primary | 36 | 9 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/msi": 0.28024280071258545, "general": 0.9713645577430725}` |
| filetypes/lnk | general_only | 35 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.8371633887290955}` |
| filetypes/ole | or_general_primary | 26 | 655 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/ole": 0.9222427606582642, "general": 0.9518448114395142}` |
| filetypes/crx | general_only | 9 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8564377427101135}` |
| filetypes/rtf | or_general_primary | 9 | 59 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/rtf": 0.7234269976615906, "general": 0.9769636392593384}` |
| filetypes/ruby | group_only | 9 | 2924 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/scripts": 0.9963645935058594}` |
| filetypes/lua | general_only | 3 | 1319 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.7351991534233093}` |
| filetypes/chm | general_only | 2 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9906882047653198}` |
| filetypes/html | general_only | 2 | 177 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9354889392852783}` |
| filetypes/java | general_only | 2 | 3529 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9540349841117859}` |
| filetypes/cab | general_only | 1 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9981394410133362}` |
| filetypes/groovy | general_only | 1 | 588 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9754495620727539}` |
| filetypes/pptx | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8636189699172974}` |
| filetypes/tar.xz | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8365404009819031}` |
| filetypes/tar | or_general_primary | 146 | 46 | 99.32% | 0 | 0.00 | 0.000 | 99.66% | 99.48% | `{"filetypes/tar": 0.47724226117134094, "general": 0.7868746519088745}` |
| filetypes/pkg-info | general_only | 485 | 96 | 95.67% | 0 | 0.00 | 0.000 | 97.79% | 96.39% | `{"general": 0.02792925015091896}` |
| filetypes/xls | general_only | 21 | 4 | 95.24% | 0 | 0.00 | 0.000 | 97.56% | 96.00% | `{"general": 0.0009061877499334514}` |
| filetypes/python-bytecode | filetype_only | 109 | 1267 | 94.50% | 0 | 0.00 | 0.000 | 97.17% | 99.56% | `{"filetypes/python-bytecode": 0.9863467216491699}` |
| filetypes/data | general_only | 43 | 1064 | 90.70% | 0 | 0.00 | 0.000 | 95.12% | 99.64% | `{"general": 0.853091299533844}` |
| filetypes/docx | general_only | 67 | 27 | 89.55% | 0 | 0.00 | 0.000 | 94.49% | 92.55% | `{"general": 0.11987817287445068}` |
| filetypes/macho | specialist_primary_with_escape | 163 | 721 | 88.34% | 0 | 0.00 | 0.000 | 93.81% | 97.85% | `{"filegroups/native": 0.99602872133255, "filetypes/macho": 0.7973178625106812}` |
| filetypes/pe | specialist_primary_with_escape | 51401 | 17486 | 88.28% | 1 | 57.19 | 3.361 | 93.77% | 91.25% | `{"filegroups/native": 0.999194860458374, "filetypes/pe": 0.9990107417106628, "general": 0.9957654476165771}` |
| filetypes/javascript | group_primary_with_escape | 7213 | 47045 | 88.04% | 1 | 21.26 | 3.361 | 93.63% | 98.41% | `{"filegroups/scripts": 0.9960349798202515, "filetypes/javascript": 0.9933727979660034, "general": 0.9938915371894836}` |
| filetypes/applescript | general_only | 5 | 16 | 80.00% | 0 | 0.00 | 0.000 | 88.89% | 95.24% | `{"general": 0.9594946503639221}` |
| filetypes/xlsx | general_only | 17 | 8 | 76.47% | 0 | 0.00 | 0.000 | 86.67% | 84.00% | `{"general": 0.0004667504399549216}` |
| filetypes/xz | general_only | 4 | 2886 | 75.00% | 0 | 0.00 | 0.000 | 85.71% | 99.97% | `{"general": 0.9911648035049438}` |
| filetypes/perl | group_only | 21 | 3650 | 66.67% | 0 | 0.00 | 0.000 | 80.00% | 99.81% | `{"filegroups/scripts": 0.07316567003726959}` |

## L5 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/zst | general_only | 273 | 2062 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.005351923406124115}` |
| filetypes/doc | group_only | 206 | 6 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.011448593810200691}` |
| filetypes/rar | general_only | 122 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.00030210227123461664}` |
| filetypes/msi | or_general_primary | 36 | 9 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/msi": 0.28024280071258545, "general": 0.9713645577430725}` |
| filetypes/lnk | general_only | 35 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.8371633887290955}` |
| filetypes/ole | or_general_primary | 26 | 655 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/ole": 0.9222427606582642, "general": 0.9518448114395142}` |
| filetypes/crx | general_only | 9 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8564377427101135}` |
| filetypes/rtf | or_general_primary | 9 | 59 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/rtf": 0.7234269976615906, "general": 0.9769636392593384}` |
| filetypes/ruby | group_only | 9 | 2924 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/scripts": 0.9963645935058594}` |
| filetypes/lua | general_only | 3 | 1319 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.7351991534233093}` |
| filetypes/chm | general_only | 2 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9906882047653198}` |
| filetypes/html | general_only | 2 | 177 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9354889392852783}` |
| filetypes/java | general_only | 2 | 3529 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9540349841117859}` |
| filetypes/cab | general_only | 1 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9981394410133362}` |
| filetypes/groovy | general_only | 1 | 588 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9754495620727539}` |
| filetypes/pptx | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8636189699172974}` |
| filetypes/tar.xz | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8365404009819031}` |
| filetypes/package.json | or_general_primary | 1963 | 868 | 99.39% | 1 | 1152.07 | 3.361 | 99.67% | 99.54% | `{"filetypes/package.json": 0.8790057897567749, "general": 0.9376559257507324}` |
| filetypes/tar | or_general_primary | 146 | 46 | 99.32% | 0 | 0.00 | 0.000 | 99.66% | 99.48% | `{"filetypes/tar": 0.47724226117134094, "general": 0.7868746519088745}` |
| filetypes/7z | or_general_primary | 469 | 3 | 98.29% | 1 | 333333.33 | 3.361 | 99.03% | 98.09% | `{"filegroups/archive": 0.6381730437278748, "general": 0.6577135920524597}` |
| filetypes/elf | filetype_only | 2764 | 13799 | 97.87% | 1 | 72.47 | 3.361 | 98.90% | 99.64% | `{"filetypes/elf": 0.8628232479095459}` |
| filetypes/tar.gz | or_general_primary | 2470 | 1525 | 97.09% | 1 | 655.74 | 3.361 | 98.50% | 98.17% | `{"filegroups/archive": 0.8576307892799377, "filetypes/tar.gz": 0.6969171762466431, "general": 0.9723145961761475}` |
| filetypes/pkg-info | general_only | 485 | 96 | 95.67% | 0 | 0.00 | 0.000 | 97.79% | 96.39% | `{"general": 0.02792925015091896}` |
| filetypes/xls | general_only | 21 | 4 | 95.24% | 0 | 0.00 | 0.000 | 97.56% | 96.00% | `{"general": 0.0009061877499334514}` |
| filetypes/python-bytecode | filetype_only | 109 | 1267 | 94.50% | 0 | 0.00 | 0.000 | 97.17% | 99.56% | `{"filetypes/python-bytecode": 0.9863467216491699}` |
| filetypes/jar | group_primary_with_escape | 71 | 197 | 92.96% | 1 | 5076.14 | 3.361 | 95.65% | 97.76% | `{"filegroups/portable": 0.9876785278320312, "filetypes/jar": 0.4033418297767639, "general": 0.610687792301178}` |
| filetypes/data | general_only | 43 | 1064 | 90.70% | 0 | 0.00 | 0.000 | 95.12% | 99.64% | `{"general": 0.853091299533844}` |
| filetypes/python | specialist_primary_with_escape | 1715 | 14198 | 89.74% | 1 | 70.43 | 3.361 | 94.56% | 98.89% | `{"filegroups/scripts": 0.9956585168838501, "filetypes/python": 0.9637269377708435, "general": 0.990637481212616}` |
| filetypes/docx | general_only | 67 | 27 | 89.55% | 0 | 0.00 | 0.000 | 94.49% | 92.55% | `{"general": 0.11987817287445068}` |
| filetypes/zip | group_primary_with_escape | 4068 | 693 | 89.16% | 1 | 1443.00 | 3.361 | 94.26% | 90.72% | `{"filegroups/archive": 0.9765775799751282, "filetypes/zip": 0.9374825954437256, "general": 0.9927071928977966}` |

## L9 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info | or_general_primary | 485 | 96 | 100.00% | 1 | 10416.67 | 3.361 | 99.90% | 99.83% | `{"filetypes/pkg-info": 0.0189649760723114, "general": 0.02792925015091896}` |
| filetypes/zst | general_only | 273 | 2062 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.005351923406124115}` |
| filetypes/doc | group_only | 206 | 6 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.011448593810200691}` |
| filetypes/rar | general_only | 122 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.00030210227123461664}` |
| filetypes/msi | or_general_primary | 36 | 9 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/msi": 0.28024280071258545, "general": 0.9713645577430725}` |
| filetypes/lnk | general_only | 35 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.8371633887290955}` |
| filetypes/ole | or_general_primary | 26 | 655 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/ole": 0.9222427606582642, "general": 0.9518448114395142}` |
| filetypes/crx | general_only | 9 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8564377427101135}` |
| filetypes/rtf | or_general_primary | 9 | 59 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filetypes/rtf": 0.7234269976615906, "general": 0.9769636392593384}` |
| filetypes/ruby | group_only | 9 | 2924 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"filegroups/scripts": 0.9963645935058594}` |
| filetypes/lua | general_only | 3 | 1319 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.7351991534233093}` |
| filetypes/chm | general_only | 2 | 0 | 100.00% | 0 | — | 0.000 | 100.00% | 100.00% | `{"general": 0.9906882047653198}` |
| filetypes/html | general_only | 2 | 177 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9354889392852783}` |
| filetypes/java | general_only | 2 | 3529 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9540349841117859}` |
| filetypes/cab | general_only | 1 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9981394410133362}` |
| filetypes/groovy | general_only | 1 | 588 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9754495620727539}` |
| filetypes/pptx | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8636189699172974}` |
| filetypes/tar.xz | general_only | 1 | 26 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8365404009819031}` |
| filetypes/package.json | or_general_primary | 1963 | 868 | 99.39% | 1 | 1152.07 | 3.361 | 99.67% | 99.54% | `{"filetypes/package.json": 0.8790057897567749, "general": 0.9376559257507324}` |
| filetypes/tar | or_general_primary | 146 | 46 | 99.32% | 0 | 0.00 | 0.000 | 99.66% | 99.48% | `{"filetypes/tar": 0.47724226117134094, "general": 0.7868746519088745}` |
| filetypes/7z | or_general_primary | 469 | 3 | 98.29% | 1 | 333333.33 | 3.361 | 99.03% | 98.09% | `{"filegroups/archive": 0.6381730437278748, "general": 0.6577135920524597}` |
| filetypes/elf | filetype_only | 2764 | 13799 | 97.87% | 1 | 72.47 | 3.361 | 98.90% | 99.64% | `{"filetypes/elf": 0.8628232479095459}` |
| filetypes/tar.gz | or_general_primary | 2470 | 1525 | 97.09% | 1 | 655.74 | 3.361 | 98.50% | 98.17% | `{"filegroups/archive": 0.8576307892799377, "filetypes/tar.gz": 0.6969171762466431, "general": 0.9723145961761475}` |
| filetypes/xls | general_only | 21 | 4 | 95.24% | 0 | 0.00 | 0.000 | 97.56% | 96.00% | `{"general": 0.0009061877499334514}` |
| filetypes/python-bytecode | filetype_only | 109 | 1267 | 94.50% | 0 | 0.00 | 0.000 | 97.17% | 99.56% | `{"filetypes/python-bytecode": 0.9863467216491699}` |
| filetypes/jar | group_primary_with_escape | 71 | 197 | 92.96% | 1 | 5076.14 | 3.361 | 95.65% | 97.76% | `{"filegroups/portable": 0.9876785278320312, "filetypes/jar": 0.4033418297767639, "general": 0.610687792301178}` |
| filetypes/data | general_only | 43 | 1064 | 90.70% | 0 | 0.00 | 0.000 | 95.12% | 99.64% | `{"general": 0.853091299533844}` |
| filetypes/javascript | group_primary_with_escape | 7213 | 47045 | 90.31% | 3 | 63.77 | 10.082 | 94.89% | 98.71% | `{"filegroups/scripts": 0.9906684756278992, "general": 0.9938915371894836}` |
| filetypes/python | specialist_primary_with_escape | 1715 | 14198 | 89.74% | 1 | 70.43 | 3.361 | 94.56% | 98.89% | `{"filegroups/scripts": 0.9956585168838501, "filetypes/python": 0.9637269377708435, "general": 0.990637481212616}` |
| filetypes/docx | general_only | 67 | 27 | 89.55% | 0 | 0.00 | 0.000 | 94.49% | 92.55% | `{"general": 0.11987817287445068}` |
