# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1234486188`
- Rows: 4231044 (1486369 malware, 2744675 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info† | filetype_only | 10633 | 926 | 97.19% | 1 | 1079.91 | 5112.62 | 0.364 | 98.57% | 97.40% | `{"filetypes/pkg-info": 0.04703900218009949}` |
| filetypes/batch† | filetype_only | 138295 | 2350 | 93.90% | 1 | 425.53 | 2017.06 | 0.364 | 96.85% | 94.00% | `{"filetypes/batch": 0.969633162021637}` |
| filetypes/package.json† | or_general_primary | 17700 | 9607 | 92.56% | 1 | 104.09 | 493.70 | 0.364 | 96.14% | 95.18% | `{"filegroups/config": 0.9993524238035854, "filetypes/package.json": 1.0, "general": 0.9959707656715375}` |
| filetypes/elf† | group_only | 36386 | 122822 | 84.30% | 1 | 8.14 | 38.62 | 0.364 | 91.48% | 96.41% | `{"filegroups/native": 0.9949713296511951}` |
| filetypes/tar.gz† | filetype_only | 27692 | 12445 | 77.29% | 1 | 80.35 | 381.13 | 0.364 | 87.19% | 84.33% | `{"filetypes/tar.gz": 0.996148285985647}` |
| filetypes/macho† | filetype_only | 1680 | 8497 | 72.26% | 0 | 0.00 | 352.50 | 0.000 | 83.90% | 95.42% | `{"filetypes/macho": 0.9428038355470432}` |
| filetypes/javascript† | filetype_only | 76882 | 435823 | 68.46% | 3 | 6.88 | 17.79 | 1.093 | 81.27% | 95.27% | `{"filetypes/javascript": 0.9915398955345154}` |
| filetypes/pe† | or_general_primary | 812716 | 148764 | 66.95% | 4 | 26.89 | 61.53 | 1.457 | 80.20% | 72.06% | `{"filegroups/native": 0.9992764984931257, "filetypes/pe": 0.9995644088833987, "general": 0.9983970317084286}` |
| filetypes/kotlin† | or_general_primary | 19277 | 40371 | 57.94% | 1 | 24.77 | 117.50 | 0.364 | 73.37% | 86.41% | `{"filegroups/source": 1.0, "filetypes/kotlin": 0.34509502017828664, "general": 1.0}` |
| filetypes/shell† | filetype_only | 3301 | 43132 | 57.04% | 0 | 0.00 | 69.45 | 0.000 | 72.65% | 96.95% | `{"filetypes/shell": 0.9523731247460309}` |
| filetypes/zip† | group_only | 54773 | 6416 | 56.57% | 0 | 0.00 | 466.81 | 0.000 | 72.26% | 61.12% | `{"filegroups/archive": 0.998715106124108}` |
| filetypes/xz† | or_general_primary | 54 | 23573 | 51.85% | 0 | 0.00 | 127.08 | 0.000 | 68.29% | 99.89% | `{"filegroups/archive": 1.0, "filetypes/xz": 0.9996869012591414, "general": 1.0}` |
| filetypes/pdf† | or_general_primary | 144691 | 13852 | 6.36% | 0 | 0.00 | 216.24 | 0.000 | 11.96% | 14.54% | `{"filegroups/documents": 1.0, "filetypes/pdf": 1.0, "general": 0.9731354873351924}` |
| filetypes/jpeg† | group_only | 875 | 10642 | 0.57% | 0 | 0.00 | 281.46 | 0.000 | 1.14% | 92.45% | `{"filegroups/media": 0.9593055027476315}` |
| filetypes/data† | or_general_primary | 405 | 8979 | 0.49% | 0 | 0.00 | 333.58 | 0.000 | 0.98% | 95.71% | `{"filetypes/data": 0.8482785636308231, "general": 1.0}` |
| filetypes/python† | general_only | 17651 | 123369 | 0.00% | 0 | 0.00 | 24.28 | 0.000 | 0.00% | 87.48% | `{"general": 1.0}` |
| filetypes/xlsx | no_policy | 17359 | 109 | 0.00% | 0 | 0.00 | 27109.54 | 0.000 | 0.00% | 0.62% | `{}` |
| filetypes/c | no_policy | 14230 | 511522 | 0.00% | 0 | 0.00 | 5.86 | 0.000 | 0.00% | 97.29% | `{}` |
| filetypes/doc† | or_general_primary | 10986 | 32 | 0.00% | 0 | 0.00 | 89368.20 | 0.000 | 0.00% | 0.29% | `{"filegroups/documents": 1.0, "general": 1.0}` |
| filetypes/zst† | or_general_primary | 10380 | 16150 | 0.00% | 0 | 0.00 | 185.48 | 0.000 | 0.00% | 60.87% | `{"filegroups/archive": 1.0, "filetypes/zst": 1.0, "general": 1.0}` |
| filetypes/xls† | or_general_primary | 10183 | 49 | 0.00% | 0 | 0.00 | 59306.01 | 0.000 | 0.00% | 0.48% | `{"filegroups/documents": 1.0, "filetypes/xls": 1.0, "general": 1.0}` |
| filetypes/unknown† | filetype_only | 9190 | 15729 | 0.00% | 0 | 0.00 | 190.44 | 0.000 | 0.00% | 63.12% | `{"filetypes/unknown": 0.024507722583496136}` |
| filetypes/go† | or_general_primary | 8880 | 93174 | 0.00% | 0 | 0.00 | 32.15 | 0.000 | 0.00% | 91.30% | `{"filegroups/source": 1.0, "filetypes/go": 1.0, "general": 1.0}` |
| filetypes/rar† | or_general_primary | 5384 | 4 | 0.00% | 0 | 0.00 | 527129.20 | 0.000 | 0.00% | 0.07% | `{"filegroups/archive": 1.0, "general": 1.0}` |
| filetypes/png† | group_only | 5205 | 103275 | 0.00% | 0 | 0.00 | 29.01 | 0.000 | 0.00% | 95.20% | `{"filegroups/media": 1.0}` |
| filetypes/7z | no_policy | 4026 | 71 | 0.00% | 0 | 0.00 | 41315.66 | 0.000 | 0.00% | 1.73% | `{}` |
| filetypes/php† | general_only | 3743 | 61791 | 0.00% | 0 | 0.00 | 48.48 | 0.000 | 0.00% | 94.29% | `{"general": 1.0}` |
| filetypes/xml† | general_only | 2029 | 133537 | 0.00% | 0 | 0.00 | 22.43 | 0.000 | 0.00% | 98.50% | `{"general": 1.0}` |
| filetypes/vbs | no_policy | 1881 | 3239 | 0.00% | 0 | 0.00 | 924.47 | 0.000 | 0.00% | 63.26% | `{}` |
| filetypes/ole† | or_general_primary | 1844 | 5325 | 0.00% | 0 | 0.00 | 562.42 | 0.000 | 0.00% | 74.28% | `{"filegroups/documents": 1.0, "filetypes/ole": 1.0, "general": 1.0}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/pkg-info† | filetype_only | 10633 | 926 | 97.19% | 1 | 1079.91 | 5112.62 | 0.364 | 98.57% | 97.40% | `{"filetypes/pkg-info": 0.04703900218009949}` |
| filetypes/elf† | filetype_only | 36386 | 122822 | 94.06% | 2 | 16.28 | 51.26 | 0.729 | 96.94% | 98.64% | `{"filetypes/elf": 0.9975075125694275}` |
| filetypes/batch† | filetype_only | 138295 | 2350 | 93.90% | 1 | 425.53 | 2017.06 | 0.364 | 96.85% | 94.00% | `{"filetypes/batch": 0.969633162021637}` |
| filetypes/package.json† | or_general_primary | 17700 | 9607 | 92.71% | 1 | 104.09 | 493.70 | 0.364 | 96.21% | 95.27% | `{"filegroups/config": 0.9993277875510026, "filetypes/package.json": 1.0, "general": 0.9958369761951773}` |
| filetypes/7z† | group_only | 4026 | 71 | 87.11% | 1 | 14084.51 | 65078.98 | 0.364 | 93.10% | 87.31% | `{"filegroups/archive": 0.9716348052024841}` |
| filetypes/tar.gz† | filetype_only | 27692 | 12445 | 77.29% | 1 | 80.35 | 381.13 | 0.364 | 87.19% | 84.33% | `{"filetypes/tar.gz": 0.9961476878199462}` |
| filetypes/javascript | filetype_only | 76882 | 435823 | 68.62% | 4 | 9.18 | 21.00 | 1.457 | 81.39% | 95.29% | `{"filetypes/javascript": 0.9913226962089539}` |
| filetypes/pe† | or_general_primary | 812716 | 148764 | 67.87% | 6 | 40.33 | 79.60 | 2.186 | 80.86% | 72.84% | `{"filegroups/native": 0.9991918802261353, "filetypes/pe": 0.9995474219322205, "general": 0.998418390750885}` |
| filetypes/python† | filetype_only | 17651 | 123369 | 62.09% | 2 | 16.21 | 51.03 | 0.729 | 76.61% | 95.25% | `{"filetypes/python": 0.9935399889945984}` |
| filetypes/data† | or_general_primary | 405 | 8979 | 61.73% | 0 | 0.00 | 333.58 | 0.000 | 76.34% | 98.35% | `{"filetypes/data": 0.7000386478446775, "general": 1.0}` |
| filetypes/kotlin† | or_general_primary | 19277 | 40371 | 58.62% | 1 | 24.77 | 117.50 | 0.364 | 73.91% | 86.63% | `{"filegroups/source": 1.0, "filetypes/kotlin": 0.19480704585095207, "general": 1.0}` |
| filetypes/shell† | filetype_only | 3301 | 43132 | 57.62% | 1 | 23.18 | 109.98 | 0.364 | 73.10% | 96.98% | `{"filetypes/shell": 0.9478809187065081}` |
| filetypes/zip† | group_only | 54773 | 6416 | 56.67% | 1 | 155.86 | 739.16 | 0.364 | 72.34% | 61.21% | `{"filegroups/archive": 0.9986951613701044}` |
| filetypes/xz† | or_general_primary | 54 | 23573 | 51.85% | 0 | 0.00 | 127.08 | 0.000 | 68.29% | 99.89% | `{"filegroups/archive": 1.0, "filetypes/xz": 0.9996832022031537, "general": 1.0}` |
| filetypes/macho† | general_only | 1680 | 8497 | 47.68% | 0 | 0.00 | 352.50 | 0.000 | 64.57% | 91.36% | `{"general": 0.9596894185729058}` |
| filetypes/php† | or_general_primary | 3743 | 61791 | 35.24% | 1 | 16.18 | 76.77 | 0.364 | 52.10% | 96.30% | `{"filegroups/scripts": 0.9931522811563559, "filetypes/php": 1.0, "general": 1.0}` |
| filetypes/xlsx† | group_only | 17359 | 109 | 29.37% | 1 | 9174.31 | 42781.36 | 0.364 | 45.40% | 29.80% | `{"filegroups/documents": 0.8666261434555054}` |
| filetypes/jpeg† | group_only | 875 | 10642 | 8.57% | 0 | 0.00 | 281.46 | 0.000 | 15.79% | 93.05% | `{"filegroups/media": 0.8480581263337451}` |
| filetypes/pdf† | or_general_primary | 144691 | 13852 | 6.36% | 0 | 0.00 | 216.24 | 0.000 | 11.96% | 14.54% | `{"filegroups/documents": 1.0, "filetypes/pdf": 1.0, "general": 0.972687271237783}` |
| filetypes/c | no_policy | 14230 | 511522 | 0.00% | 0 | 0.00 | 5.86 | 0.000 | 0.00% | 97.29% | `{}` |
| filetypes/doc† | or_general_primary | 10986 | 32 | 0.00% | 0 | 0.00 | 89368.20 | 0.000 | 0.00% | 0.29% | `{"filegroups/documents": 1.0, "general": 1.0}` |
| filetypes/zst† | or_general_primary | 10380 | 16150 | 0.00% | 0 | 0.00 | 185.48 | 0.000 | 0.00% | 60.87% | `{"filegroups/archive": 1.0, "filetypes/zst": 1.0, "general": 1.0}` |
| filetypes/xls† | or_general_primary | 10183 | 49 | 0.00% | 0 | 0.00 | 59306.01 | 0.000 | 0.00% | 0.48% | `{"filegroups/documents": 1.0, "filetypes/xls": 1.0, "general": 1.0}` |
| filetypes/unknown† | filetype_only | 9190 | 15729 | 0.00% | 0 | 0.00 | 190.44 | 0.000 | 0.00% | 63.12% | `{"filetypes/unknown": 0.02316776032594075}` |
| filetypes/go† | general_only | 8880 | 93174 | 0.00% | 0 | 0.00 | 32.15 | 0.000 | 0.00% | 91.30% | `{"general": 1.0}` |
| filetypes/rar† | or_general_primary | 5384 | 4 | 0.00% | 0 | 0.00 | 527129.20 | 0.000 | 0.00% | 0.07% | `{"filegroups/archive": 1.0, "general": 1.0}` |
| filetypes/png† | group_only | 5205 | 103275 | 0.00% | 0 | 0.00 | 29.01 | 0.000 | 0.00% | 95.20% | `{"filegroups/media": 1.0}` |
| filetypes/xml | no_policy | 2029 | 133537 | 0.00% | 0 | 0.00 | 22.43 | 0.000 | 0.00% | 98.50% | `{}` |
| filetypes/vbs | no_policy | 1881 | 3239 | 0.00% | 0 | 0.00 | 924.47 | 0.000 | 0.00% | 63.26% | `{}` |
| filetypes/ole† | or_general_primary | 1844 | 5325 | 0.00% | 0 | 0.00 | 562.42 | 0.000 | 0.00% | 74.28% | `{"filegroups/documents": 1.0, "filetypes/ole": 1.0, "general": 1.0}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | or_general_primary | 22 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.6023048389504125, "general": 0.5230051684512254}` |
| filetypes/rtf† | filetype_only | 1340 | 475 | 98.06% | 1 | 2105.26 | 9947.81 | 0.364 | 98.98% | 98.51% | `{"filetypes/rtf": 0.09638823568820953}` |
| filetypes/pkg-info† | filetype_only | 10633 | 926 | 97.19% | 1 | 1079.91 | 5112.62 | 0.364 | 98.57% | 97.40% | `{"filetypes/pkg-info": 0.04703900218009949}` |
| filetypes/package.json† | or_general_primary | 17700 | 9607 | 95.38% | 4 | 416.36 | 952.54 | 1.457 | 97.62% | 96.99% | `{"filegroups/config": 0.9988960860718094, "filetypes/package.json": 1.0, "general": 0.9942013115839675}` |
| filetypes/tar† | filetype_only | 1110 | 377 | 95.32% | 1 | 2652.52 | 12520.89 | 0.364 | 97.56% | 96.44% | `{"filetypes/tar": 0.27894526720046997}` |
| filetypes/elf | filetype_only | 36386 | 122822 | 94.60% | 6 | 48.85 | 96.42 | 2.186 | 97.22% | 98.76% | `{"filetypes/elf": 0.9968318939208984}` |
| filetypes/batch† | or_general_primary | 138295 | 2350 | 94.08% | 3 | 1276.60 | 3296.09 | 1.093 | 96.95% | 94.18% | `{"filegroups/scripts": 0.9959076046943665, "filetypes/batch": 0.969633162021637, "general": 0.9751875996589661}` |
| filetypes/ole† | or_general_primary | 1844 | 5325 | 92.73% | 2 | 375.59 | 1181.83 | 0.729 | 96.18% | 98.10% | `{"filegroups/documents": 0.5059333996291607, "filetypes/ole": 0.9224145684864336, "general": 1.0}` |
| filetypes/python-bytecode† | filetype_only | 1576 | 21326 | 89.47% | 2 | 93.78 | 295.19 | 0.729 | 94.38% | 99.27% | `{"filetypes/python-bytecode": 0.9962243437767029}` |
| filetypes/zst† | or_general_primary | 10380 | 16150 | 87.19% | 2 | 123.84 | 389.78 | 0.729 | 93.15% | 94.98% | `{"filegroups/archive": 1.0, "filetypes/zst": 1.0, "general": 0.6405683044864404}` |
| filetypes/7z† | group_only | 4026 | 71 | 87.11% | 1 | 14084.51 | 65078.98 | 0.364 | 93.10% | 87.31% | `{"filegroups/archive": 0.9716348052024841}` |
| filetypes/cab† | or_general_primary | 208 | 55 | 85.10% | 1 | 18181.82 | 83371.34 | 0.364 | 91.71% | 87.83% | `{"filegroups/archive": 0.9855297803878784, "filetypes/cab": 0.7788318395614624, "general": 0.9697627425193787}` |
| filetypes/tar.gz† | or_general_primary | 27692 | 12445 | 81.76% | 4 | 321.41 | 735.37 | 1.457 | 89.96% | 87.41% | `{"filegroups/archive": 0.9988252439125402, "filetypes/tar.gz": 0.9961282162302092, "general": 0.9945940760940684}` |
| filetypes/pe | or_general_primary | 812716 | 148764 | 81.60% | 22 | 147.89 | 211.17 | 8.016 | 89.86% | 84.44% | `{"filegroups/native": 0.9984410405158997, "filetypes/pe": 0.9992114305496216, "general": 0.996691107749939}` |
| filetypes/javascript | filetype_only | 76882 | 435823 | 76.51% | 21 | 48.18 | 69.39 | 7.651 | 86.68% | 96.47% | `{"filetypes/javascript": 0.9733543395996094}` |
| filetypes/data† | or_general_primary | 405 | 8979 | 73.09% | 0 | 0.00 | 333.58 | 0.000 | 84.45% | 98.84% | `{"filetypes/data": 0.3967029488060513, "general": 1.0}` |
| filetypes/macho† | filetype_only | 1680 | 8497 | 72.56% | 1 | 117.69 | 558.18 | 0.364 | 84.07% | 95.46% | `{"filetypes/macho": 0.9386150690185787}` |
| filetypes/python | filetype_only | 17651 | 123369 | 66.81% | 6 | 48.63 | 95.99 | 2.186 | 80.08% | 95.84% | `{"filetypes/python": 0.9871286749839783}` |
| filetypes/docx† | or_general_primary | 1379 | 242 | 66.35% | 1 | 4132.23 | 19451.76 | 0.364 | 79.74% | 71.31% | `{"filegroups/documents": 0.9442232251167297, "filetypes/docx": 0.6277602314949036, "general": 0.9937783479690552}` |
| filetypes/php† | filetype_only | 3743 | 61791 | 65.91% | 3 | 48.55 | 125.48 | 1.093 | 79.41% | 98.05% | `{"filetypes/php": 0.9447157382965088}` |
| filetypes/gz† | filetype_only | 1240 | 44908 | 65.00% | 3 | 66.80 | 172.65 | 1.093 | 78.67% | 99.05% | `{"filetypes/gz": 0.823357880115509}` |
| filetypes/msi† | filetype_only | 904 | 119 | 64.82% | 1 | 8403.36 | 39242.78 | 0.364 | 78.60% | 68.82% | `{"filetypes/msi": 0.7786945104598999}` |
| filetypes/shell† | filetype_only | 3301 | 43132 | 63.41% | 3 | 69.55 | 179.76 | 1.093 | 77.56% | 97.39% | `{"filetypes/shell": 0.9303211569786072}` |
| filetypes/kotlin† | or_general_primary | 19277 | 40371 | 60.91% | 5 | 123.85 | 260.39 | 1.822 | 75.69% | 87.36% | `{"filegroups/source": 0.9225418567657471, "filetypes/kotlin": 0.17140279710292816, "general": 0.82243812084198}` |
| filetypes/zip† | or_general_primary | 54773 | 6416 | 59.79% | 2 | 311.72 | 980.94 | 0.729 | 74.83% | 64.00% | `{"filegroups/archive": 0.9985120979539459, "filetypes/zip": 1.0, "general": 0.9953032773125141}` |
| filetypes/jar† | group_only | 1246 | 1779 | 49.68% | 1 | 562.11 | 2663.79 | 0.364 | 66.35% | 79.24% | `{"filegroups/portable": 0.9981715679168701}` |
| filetypes/lnk† | filetype_only | 1349 | 796 | 37.36% | 1 | 1256.28 | 5945.63 | 0.364 | 54.37% | 60.56% | `{"filetypes/lnk": 0.9848120212554932}` |
| filetypes/powershell† | general_only | 906 | 2001 | 30.46% | 1 | 499.75 | 2368.53 | 0.364 | 46.66% | 78.29% | `{"general": 0.9801609516143799}` |
| filetypes/xlsx† | group_only | 17359 | 109 | 29.37% | 1 | 9174.31 | 42781.36 | 0.364 | 45.40% | 29.80% | `{"filegroups/documents": 0.8666261434555054}` |
| filetypes/vbs† | filetype_only | 1881 | 3239 | 24.61% | 1 | 308.74 | 1463.76 | 0.364 | 39.49% | 72.29% | `{"filetypes/vbs": 0.9966105190257007}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/zst† | or_general_primary | 10380 | 16150 | 100.00% | 2 | 123.84 | 389.78 | 0.729 | 99.99% | 99.99% | `{"filegroups/archive": 0.9092978835105896, "filetypes/zst": 0.22847750782966614, "general": 0.785312294960022}` |
| filetypes/html† | or_general_primary | 22 | 7963 | 100.00% | 0 | 0.00 | 376.14 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 0.2603931201784217, "general": 0.21075834114648162}` |
| filetypes/rtf† | filetype_only | 1340 | 475 | 98.06% | 1 | 2105.26 | 9947.81 | 0.364 | 98.98% | 98.51% | `{"filetypes/rtf": 0.09638823568820953}` |
| filetypes/pkg-info† | filetype_only | 10633 | 926 | 97.19% | 1 | 1079.91 | 5112.62 | 0.364 | 98.57% | 97.40% | `{"filetypes/pkg-info": 0.04703900218009949}` |
| filetypes/package.json† | or_general_primary | 17700 | 9607 | 97.02% | 4 | 416.36 | 952.54 | 1.457 | 98.48% | 98.06% | `{"filegroups/config": 0.9983846571955909, "filetypes/package.json": 1.0, "general": 0.9926454024355029}` |
| filetypes/elf | filetype_only | 36386 | 122822 | 95.86% | 10 | 81.42 | 138.10 | 3.643 | 97.87% | 99.05% | `{"filetypes/elf": 0.9945598840713501}` |
| filetypes/tar† | filetype_only | 1110 | 377 | 95.32% | 1 | 2652.52 | 12520.89 | 0.364 | 97.56% | 96.44% | `{"filetypes/tar": 0.27894526720046997}` |
| filetypes/batch† | or_general_primary | 138295 | 2350 | 94.08% | 3 | 1276.60 | 3296.09 | 1.093 | 96.95% | 94.18% | `{"filegroups/scripts": 0.9959076046943665, "filetypes/batch": 0.969633162021637, "general": 0.9751875996589661}` |
| filetypes/ole† | or_general_primary | 1844 | 5325 | 93.38% | 2 | 375.59 | 1181.83 | 0.729 | 96.52% | 98.27% | `{"filegroups/documents": 0.343390091225461, "filetypes/ole": 0.7453228232087031, "general": 1.0}` |
| filetypes/python-bytecode† | filetype_only | 1576 | 21326 | 89.47% | 2 | 93.78 | 295.19 | 0.729 | 94.38% | 99.27% | `{"filetypes/python-bytecode": 0.9962243437767029}` |
| filetypes/7z† | group_only | 4026 | 71 | 87.11% | 1 | 14084.51 | 65078.98 | 0.364 | 93.10% | 87.31% | `{"filegroups/archive": 0.9716348052024841}` |
| filetypes/cab† | or_general_primary | 208 | 55 | 85.10% | 1 | 18181.82 | 83371.34 | 0.364 | 91.71% | 87.83% | `{"filegroups/archive": 0.9855297803878784, "filetypes/cab": 0.7788318395614624, "general": 0.9697627425193787}` |
| filetypes/perl† | filetype_only | 217 | 30053 | 83.87% | 3 | 99.82 | 257.98 | 1.093 | 90.55% | 99.87% | `{"filetypes/perl": 0.989916980266571}` |
| filetypes/pe | or_general_primary | 812716 | 148764 | 82.74% | 40 | 268.88 | 350.00 | 14.574 | 90.55% | 85.40% | `{"filegroups/native": 0.9982402324676514, "filetypes/pe": 0.9992101192474365, "general": 0.996110737323761}` |
| filetypes/tar.gz† | or_general_primary | 27692 | 12445 | 82.16% | 5 | 401.77 | 844.57 | 1.822 | 90.20% | 87.68% | `{"filegroups/archive": 0.9988218813118432, "filetypes/tar.gz": 0.9960957866069502, "general": 0.9936880932621421}` |
| filetypes/javascript | filetype_only | 76882 | 435823 | 79.13% | 35 | 80.31 | 106.47 | 12.752 | 88.32% | 96.86% | `{"filetypes/javascript": 0.9561986327171326}` |
| filetypes/data† | or_general_primary | 405 | 8979 | 75.31% | 0 | 0.00 | 333.58 | 0.000 | 85.92% | 98.93% | `{"filetypes/data": 0.33067154962133655, "general": 1.0}` |
| filetypes/macho† | filetype_only | 1680 | 8497 | 72.92% | 1 | 117.69 | 558.18 | 0.364 | 84.31% | 95.52% | `{"filetypes/macho": 0.93579559256023}` |
| filetypes/python | filetype_only | 17651 | 123369 | 67.76% | 10 | 81.06 | 137.49 | 3.643 | 80.76% | 95.96% | `{"filetypes/python": 0.9851399660110474}` |
| filetypes/php | filetype_only | 3743 | 61791 | 67.35% | 6 | 97.10 | 191.64 | 2.186 | 80.41% | 98.13% | `{"filetypes/php": 0.930044949054718}` |
| filetypes/docx† | or_general_primary | 1379 | 242 | 66.35% | 1 | 4132.23 | 19451.76 | 0.364 | 79.74% | 71.31% | `{"filegroups/documents": 0.9442232251167297, "filetypes/docx": 0.6277602314949036, "general": 0.9937783479690552}` |
| filetypes/gz | filetype_only | 1240 | 44908 | 65.00% | 4 | 89.07 | 203.82 | 1.457 | 78.63% | 99.05% | `{"filetypes/gz": 0.8190240859985352}` |
| filetypes/shell | filetype_only | 3301 | 43132 | 64.95% | 4 | 92.74 | 212.21 | 1.457 | 78.69% | 97.50% | `{"filetypes/shell": 0.9193582534790039}` |
| filetypes/msi† | filetype_only | 904 | 119 | 64.82% | 1 | 8403.36 | 39242.78 | 0.364 | 78.60% | 68.82% | `{"filetypes/msi": 0.7786945104598999}` |
| filetypes/kotlin | or_general_primary | 19277 | 40371 | 63.08% | 10 | 247.70 | 420.12 | 3.643 | 77.33% | 88.05% | `{"filegroups/source": 0.9135615825653076, "filetypes/kotlin": 0.039571721106767654, "general": 0.7423425316810608}` |
| filetypes/zip† | or_general_primary | 54773 | 6416 | 60.86% | 3 | 467.58 | 1208.04 | 1.093 | 75.66% | 64.96% | `{"filegroups/archive": 0.9983679122323195, "filetypes/zip": 0.9959930322117148, "general": 0.994897862544111}` |
| filetypes/jar† | group_only | 1246 | 1779 | 49.68% | 1 | 562.11 | 2663.79 | 0.364 | 66.35% | 79.24% | `{"filegroups/portable": 0.9981715679168701}` |
| filetypes/lnk† | filetype_only | 1349 | 796 | 37.36% | 1 | 1256.28 | 5945.63 | 0.364 | 54.37% | 60.56% | `{"filetypes/lnk": 0.9848120212554932}` |
| filetypes/powershell† | general_only | 906 | 2001 | 30.46% | 1 | 499.75 | 2368.53 | 0.364 | 46.66% | 78.29% | `{"general": 0.9801609516143799}` |
| filetypes/xlsx† | group_only | 17359 | 109 | 29.37% | 1 | 9174.31 | 42781.36 | 0.364 | 45.40% | 29.80% | `{"filegroups/documents": 0.8666261434555054}` |
