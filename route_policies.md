# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1123787257`
- Rows: 3285920 (699360 malware, 2586560 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | or_general_primary | 9 | 7719 | 100.00% | 0 | 0.00 | 388.02 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 1.0, "general": 0.002978071091096475}` |
| filetypes/tar† | group_only | 1043 | 363 | 95.11% | 1 | 2754.82 | 13001.30 | 0.387 | 97.45% | 96.30% | `{"filegroups/archive": 0.8576492667198181}` |
| filetypes/pkg-info† | general_only | 3683 | 877 | 94.73% | 1 | 1140.25 | 5397.66 | 0.387 | 97.28% | 95.72% | `{"general": 0.010649630799889565}` |
| filetypes/tar.gz† | group_only | 19546 | 12062 | 92.66% | 0 | 0.00 | 248.33 | 0.000 | 96.19% | 95.46% | `{"filegroups/archive": 0.9976688324894445}` |
| filetypes/package.json† | general_only | 15739 | 8999 | 86.00% | 1 | 111.12 | 527.04 | 0.387 | 92.47% | 91.09% | `{"general": 0.9922307042913745}` |
| filetypes/javascript† | filetype_only | 58630 | 396958 | 84.64% | 2 | 5.04 | 15.86 | 0.773 | 91.68% | 98.02% | `{"filetypes/javascript": 0.9953958988189697}` |
| filetypes/zip† | group_only | 33696 | 5814 | 80.98% | 1 | 172.00 | 815.68 | 0.387 | 89.49% | 83.78% | `{"filegroups/archive": 0.9984125573844418}` |
| filetypes/data† | or_general_primary | 403 | 8928 | 78.41% | 0 | 0.00 | 335.49 | 0.000 | 87.90% | 99.07% | `{"filetypes/data": 0.20151853692671656, "general": 1.0}` |
| filetypes/elf† | or_general_primary | 22261 | 117951 | 76.38% | 1 | 8.48 | 40.22 | 0.387 | 86.61% | 96.25% | `{"filegroups/native": 0.9989244932141729, "filetypes/elf": 1.0, "general": 1.0}` |
| filetypes/pe† | or_general_primary | 470591 | 144206 | 74.73% | 3 | 20.80 | 53.77 | 1.160 | 85.54% | 80.66% | `{"filegroups/native": 0.9992181939077774, "filetypes/pe": 0.9995771544268709, "general": 0.9991543184131343}` |
| filetypes/objc† | general_only | 5 | 18189 | 60.00% | 0 | 0.00 | 164.69 | 0.000 | 75.00% | 99.99% | `{"general": 0.4529446889761865}` |
| filetypes/macho† | filetype_only | 1354 | 6179 | 54.65% | 0 | 0.00 | 484.71 | 0.000 | 70.68% | 91.85% | `{"filetypes/macho": 0.9359214508153115}` |
| filetypes/shell† | group_only | 2437 | 42326 | 48.42% | 1 | 23.63 | 112.07 | 0.387 | 65.23% | 97.19% | `{"filegroups/scripts": 0.9921182385209892}` |
| filetypes/php† | general_only | 3374 | 49169 | 47.84% | 0 | 0.00 | 60.93 | 0.000 | 64.72% | 96.65% | `{"general": 0.9924473054987893}` |
| filetypes/python† | or_general_primary | 14625 | 117204 | 45.03% | 1 | 8.53 | 40.47 | 0.387 | 62.10% | 93.90% | `{"filegroups/scripts": 1.0, "filetypes/python": 0.9984022844156876, "general": 1.0}` |
| filetypes/groovy† | general_only | 4 | 4821 | 25.00% | 0 | 0.00 | 621.20 | 0.000 | 40.00% | 99.94% | `{"general": 0.04252844272098258}` |
| filetypes/jpeg† | group_only | 772 | 7875 | 1.81% | 0 | 0.00 | 380.34 | 0.000 | 3.56% | 91.23% | `{"filegroups/media": 0.08468795089407685}` |
| filetypes/c | no_policy | 14225 | 495122 | 0.00% | 0 | 0.00 | 6.05 | 0.000 | 0.00% | 97.21% | `{}` |
| filetypes/go† | or_general_primary | 8879 | 92099 | 0.00% | 0 | 0.00 | 32.53 | 0.000 | 0.00% | 91.21% | `{"filegroups/source": 1.0, "filetypes/go": 1.0, "general": 1.0}` |
| filetypes/png† | filetype_only | 5002 | 97184 | 0.00% | 0 | 0.00 | 30.82 | 0.000 | 0.00% | 95.11% | `{"filetypes/png": 1.0}` |
| filetypes/7z† | or_general_primary | 3780 | 37 | 0.00% | 0 | 0.00 | 77774.71 | 0.000 | 0.00% | 0.97% | `{"filegroups/archive": 1.0, "general": 1.0}` |
| filetypes/zst† | or_general_primary | 2283 | 16150 | 0.00% | 0 | 0.00 | 185.48 | 0.000 | 0.00% | 87.61% | `{"filegroups/archive": 1.0, "filetypes/zst": 1.0, "general": 1.0}` |
| filetypes/doc† | or_general_primary | 1899 | 26 | 0.00% | 0 | 0.00 | 108830.36 | 0.000 | 0.00% | 1.35% | `{"filegroups/documents": 1.0, "general": 1.0}` |
| filetypes/csharp† | or_general_primary | 1728 | 59153 | 0.00% | 0 | 0.00 | 50.64 | 0.000 | 0.00% | 97.16% | `{"filegroups/source": 1.0, "filetypes/csharp": 1.0, "general": 1.0}` |
| filetypes/xml | no_policy | 1388 | 126044 | 0.00% | 0 | 0.00 | 23.77 | 0.000 | 0.00% | 98.91% | `{}` |
| filetypes/rust† | general_only | 1279 | 76370 | 0.00% | 0 | 0.00 | 39.23 | 0.000 | 0.00% | 98.35% | `{"general": 1.0}` |
| filetypes/text† | or_general_primary | 1016 | 60157 | 0.00% | 0 | 0.00 | 49.80 | 0.000 | 0.00% | 98.34% | `{"filetypes/text": 1.0, "general": 1.0}` |
| filetypes/kotlin† | filetype_only | 1009 | 38814 | 0.00% | 0 | 0.00 | 77.18 | 0.000 | 0.00% | 97.47% | `{"filetypes/kotlin": 1.0}` |
| filetypes/python-bytecode† | or_general_primary | 959 | 12386 | 0.00% | 0 | 0.00 | 241.84 | 0.000 | 0.00% | 92.81% | `{"filetypes/python-bytecode": 1.0, "general": 1.0}` |
| filetypes/rar† | or_general_primary | 957 | 4 | 0.00% | 0 | 0.00 | 527129.20 | 0.000 | 0.00% | 0.42% | `{"filegroups/archive": 1.0, "general": 1.0}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | or_general_primary | 9 | 7719 | 100.00% | 0 | 0.00 | 388.02 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 1.0, "general": 0.0027821661048183606}` |
| filetypes/tar† | group_only | 1043 | 363 | 95.11% | 1 | 2754.82 | 13001.30 | 0.387 | 97.45% | 96.30% | `{"filegroups/archive": 0.8576492667198181}` |
| filetypes/pkg-info† | general_only | 3683 | 877 | 94.73% | 1 | 1140.25 | 5397.66 | 0.387 | 97.28% | 95.72% | `{"general": 0.010649630799889565}` |
| filetypes/tar.gz† | group_only | 19546 | 12062 | 92.98% | 0 | 0.00 | 248.33 | 0.000 | 96.36% | 95.66% | `{"filegroups/archive": 0.9973773848099445}` |
| filetypes/elf† | filetype_only | 22261 | 117951 | 90.21% | 2 | 16.96 | 53.38 | 0.773 | 94.85% | 98.44% | `{"filetypes/elf": 0.993247389793396}` |
| filetypes/docx† | filetype_only | 375 | 232 | 88.53% | 1 | 4310.34 | 20283.45 | 0.387 | 93.79% | 92.75% | `{"filetypes/docx": 0.3691062331199646}` |
| filetypes/package.json† | or_general_primary | 15739 | 8999 | 87.93% | 2 | 222.25 | 699.44 | 0.773 | 93.57% | 92.31% | `{"filegroups/config": 1.0, "filetypes/package.json": 0.9984623299570813, "general": 0.9921933021577007}` |
| filetypes/javascript | filetype_only | 58630 | 396958 | 85.78% | 4 | 10.08 | 23.06 | 1.546 | 92.34% | 98.17% | `{"filetypes/javascript": 0.9942663908004761}` |
| filetypes/pe† | or_general_primary | 470591 | 144206 | 81.50% | 6 | 41.61 | 82.12 | 2.320 | 89.80% | 85.84% | `{"filegroups/native": 0.9988124966621399, "filetypes/pe": 0.999357283115387, "general": 0.9989871382713318}` |
| filetypes/zip† | group_only | 33696 | 5814 | 81.00% | 1 | 172.00 | 815.68 | 0.387 | 89.50% | 83.80% | `{"filegroups/archive": 0.9984059007149543}` |
| filetypes/data† | or_general_primary | 403 | 8928 | 78.41% | 0 | 0.00 | 335.49 | 0.000 | 87.90% | 99.07% | `{"filetypes/data": 0.19911032799592884, "general": 1.0}` |
| filetypes/jar† | filetype_only | 616 | 1712 | 75.97% | 1 | 584.11 | 2767.92 | 0.387 | 86.27% | 93.60% | `{"filetypes/jar": 0.8501611351966858}` |
| filetypes/macho† | filetype_only | 1354 | 6179 | 74.96% | 0 | 0.00 | 484.71 | 0.000 | 85.69% | 95.50% | `{"filetypes/macho": 0.8909680579845873}` |
| filetypes/python† | group_only | 14625 | 117204 | 72.51% | 2 | 17.06 | 53.72 | 0.773 | 84.06% | 96.95% | `{"filegroups/scripts": 0.9976996183395386}` |
| filetypes/objc† | general_only | 5 | 18189 | 60.00% | 0 | 0.00 | 164.69 | 0.000 | 75.00% | 99.99% | `{"general": 0.21346462406925695}` |
| filetypes/vbs† | or_general_primary | 759 | 3230 | 51.91% | 1 | 309.60 | 1467.84 | 0.387 | 68.28% | 90.82% | `{"filetypes/vbs": 0.9953848060449432, "general": 0.9841346762127909}` |
| filetypes/php† | general_only | 3374 | 49169 | 49.59% | 0 | 0.00 | 60.93 | 0.000 | 66.30% | 96.76% | `{"general": 0.9898073694682117}` |
| filetypes/shell† | group_only | 2437 | 42326 | 48.50% | 1 | 23.63 | 112.07 | 0.387 | 65.30% | 97.19% | `{"filegroups/scripts": 0.9920952936100418}` |
| filetypes/groovy† | general_only | 4 | 4821 | 25.00% | 0 | 0.00 | 621.20 | 0.000 | 40.00% | 99.94% | `{"general": 0.024752541600838684}` |
| filetypes/jpeg† | group_only | 772 | 7875 | 1.81% | 0 | 0.00 | 380.34 | 0.000 | 3.56% | 91.23% | `{"filegroups/media": 0.08434004917600534}` |
| filetypes/c | no_policy | 14225 | 495122 | 0.00% | 0 | 0.00 | 6.05 | 0.000 | 0.00% | 97.21% | `{}` |
| filetypes/go† | or_general_primary | 8879 | 92099 | 0.00% | 0 | 0.00 | 32.53 | 0.000 | 0.00% | 91.21% | `{"filegroups/source": 1.0, "filetypes/go": 1.0, "general": 1.0}` |
| filetypes/png† | filetype_only | 5002 | 97184 | 0.00% | 0 | 0.00 | 30.82 | 0.000 | 0.00% | 95.11% | `{"filetypes/png": 1.0}` |
| filetypes/7z† | or_general_primary | 3780 | 37 | 0.00% | 0 | 0.00 | 77774.71 | 0.000 | 0.00% | 0.97% | `{"filegroups/archive": 1.0, "general": 1.0}` |
| filetypes/zst† | or_general_primary | 2283 | 16150 | 0.00% | 0 | 0.00 | 185.48 | 0.000 | 0.00% | 87.61% | `{"filegroups/archive": 1.0, "filetypes/zst": 1.0, "general": 1.0}` |
| filetypes/doc† | or_general_primary | 1899 | 26 | 0.00% | 0 | 0.00 | 108830.36 | 0.000 | 0.00% | 1.35% | `{"filegroups/documents": 1.0, "general": 1.0}` |
| filetypes/csharp† | or_general_primary | 1728 | 59153 | 0.00% | 0 | 0.00 | 50.64 | 0.000 | 0.00% | 97.16% | `{"filegroups/source": 1.0, "filetypes/csharp": 1.0, "general": 1.0}` |
| filetypes/xml | no_policy | 1388 | 126044 | 0.00% | 0 | 0.00 | 23.77 | 0.000 | 0.00% | 98.91% | `{}` |
| filetypes/rust† | filetype_only | 1279 | 76370 | 0.00% | 0 | 0.00 | 39.23 | 0.000 | 0.00% | 98.35% | `{"filetypes/rust": 1.0}` |
| filetypes/text† | or_general_primary | 1016 | 60157 | 0.00% | 0 | 0.00 | 49.80 | 0.000 | 0.00% | 98.34% | `{"filetypes/text": 1.0, "general": 1.0}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | or_general_primary | 9 | 7719 | 100.00% | 0 | 0.00 | 388.02 | 0.000 | 100.00% | 100.00% | `{"filegroups/documents": 1.0, "general": 0.0022247655875445183}` |
| filetypes/rtf† | filetype_only | 89 | 472 | 98.88% | 1 | 2118.64 | 10010.79 | 0.387 | 98.88% | 99.64% | `{"filetypes/rtf": 0.18790295720100403}` |
| filetypes/tar† | group_only | 1043 | 363 | 95.11% | 1 | 2754.82 | 13001.30 | 0.387 | 97.45% | 96.30% | `{"filegroups/archive": 0.8576492667198181}` |
| filetypes/pkg-info† | general_only | 3683 | 877 | 94.73% | 1 | 1140.25 | 5397.66 | 0.387 | 97.28% | 95.72% | `{"general": 0.010649630799889565}` |
| filetypes/tar.gz† | or_general_primary | 19546 | 12062 | 94.22% | 2 | 165.81 | 521.86 | 0.773 | 97.02% | 96.42% | `{"filegroups/archive": 0.9951800349469136, "filetypes/tar.gz": 0.97941678409237, "general": 0.9962962987224528}` |
| filetypes/elf | group_only | 22261 | 117951 | 93.96% | 6 | 50.87 | 100.40 | 2.320 | 96.87% | 99.04% | `{"filegroups/native": 0.9945414066314697}` |
| filetypes/package.json† | or_general_primary | 15739 | 8999 | 90.96% | 2 | 222.25 | 699.44 | 0.773 | 95.26% | 94.24% | `{"filegroups/config": 1.0, "filetypes/package.json": 0.9971594664721332, "general": 0.9915923786194532}` |
| filetypes/macho† | filetype_only | 1354 | 6179 | 89.44% | 0 | 0.00 | 484.71 | 0.000 | 94.42% | 98.10% | `{"filetypes/macho": 0.7553354428646395}` |
| filetypes/ruby† | filetype_only | 72 | 23181 | 88.89% | 2 | 86.28 | 271.57 | 0.773 | 92.75% | 99.96% | `{"filetypes/ruby": 0.9971839189529419}` |
| filetypes/docx† | filetype_only | 375 | 232 | 88.53% | 1 | 4310.34 | 20283.45 | 0.387 | 93.79% | 92.75% | `{"filetypes/docx": 0.3691062331199646}` |
| filetypes/javascript | filetype_only | 58630 | 396958 | 87.95% | 20 | 50.38 | 73.21 | 7.732 | 93.57% | 98.45% | `{"filetypes/javascript": 0.986707329750061}` |
| filetypes/pe | or_general_primary | 470591 | 144206 | 85.32% | 25 | 173.36 | 242.12 | 9.665 | 92.08% | 88.76% | `{"filegroups/native": 0.9983007907867432, "filetypes/pe": 0.9992949366569519, "general": 0.998110830783844}` |
| filetypes/zip† | or_general_primary | 33696 | 5814 | 82.84% | 3 | 516.00 | 1333.07 | 1.160 | 90.61% | 85.36% | `{"filegroups/archive": 0.9983360018104933, "filetypes/zip": 0.994047725674308, "general": 0.99631903796437}` |
| filetypes/ole† | general_only | 259 | 5320 | 80.69% | 1 | 187.97 | 891.39 | 0.387 | 89.13% | 99.09% | `{"general": 0.1988119782961558}` |
| filetypes/data† | or_general_primary | 403 | 8928 | 78.41% | 2 | 224.01 | 705.00 | 0.773 | 87.66% | 99.05% | `{"filetypes/data": 0.18820296993206637, "general": 1.0}` |
| filetypes/python | filetype_only | 14625 | 117204 | 78.18% | 6 | 51.19 | 101.04 | 2.320 | 87.73% | 97.57% | `{"filetypes/python": 0.9928712844848633}` |
| filetypes/jar† | filetype_only | 616 | 1712 | 75.97% | 1 | 584.11 | 2767.92 | 0.387 | 86.27% | 93.60% | `{"filetypes/jar": 0.8501611351966858}` |
| filetypes/perl† | filetype_only | 194 | 29926 | 75.26% | 2 | 66.83 | 210.36 | 0.773 | 85.38% | 99.83% | `{"filetypes/perl": 0.982920229434967}` |
| filetypes/php† | filetype_only | 3374 | 49169 | 63.66% | 3 | 61.01 | 157.69 | 1.160 | 77.76% | 97.66% | `{"filetypes/php": 0.9724526405334473}` |
| filetypes/batch† | filetype_only | 439 | 2169 | 61.28% | 1 | 461.04 | 2185.23 | 0.387 | 75.88% | 93.44% | `{"filetypes/batch": 0.9818213582038879}` |
| filetypes/objc† | general_only | 5 | 18189 | 60.00% | 0 | 0.00 | 164.69 | 0.000 | 75.00% | 99.99% | `{"general": 0.0253654532817897}` |
| filetypes/powershell† | filetype_only | 506 | 1968 | 57.91% | 1 | 508.13 | 2408.21 | 0.387 | 73.25% | 91.35% | `{"filetypes/powershell": 0.9687137007713318}` |
| filetypes/shell† | filetype_only | 2437 | 42326 | 57.73% | 3 | 70.88 | 183.18 | 1.160 | 73.15% | 97.69% | `{"filetypes/shell": 0.6831484436988831}` |
| filetypes/kotlin† | filetype_only | 1009 | 38814 | 57.28% | 2 | 51.53 | 162.20 | 0.773 | 72.75% | 98.91% | `{"filetypes/kotlin": 0.070709228515625}` |
| filetypes/msi† | group_only | 308 | 103 | 56.82% | 1 | 9708.74 | 45228.30 | 0.387 | 72.31% | 67.40% | `{"filegroups/archive": 0.9808922410011292}` |
| filetypes/vbs† | or_general_primary | 759 | 3230 | 52.04% | 1 | 309.60 | 1467.84 | 0.387 | 68.40% | 90.85% | `{"filetypes/vbs": 0.9952775892526398, "general": 0.9841317020738094}` |
| filetypes/xlsx† | or_general_primary | 121 | 105 | 42.98% | 1 | 9523.81 | 44382.14 | 0.387 | 59.77% | 69.03% | `{"filegroups/documents": 0.9951799511909485, "filetypes/xlsx": 0.584685206413269, "general": 0.9924589395523071}` |
| filetypes/groovy† | general_only | 4 | 4821 | 25.00% | 0 | 0.00 | 621.20 | 0.000 | 40.00% | 99.94% | `{"general": 0.005560552936283234}` |
| filetypes/csharp† | group_only | 1728 | 59153 | 20.95% | 3 | 50.72 | 131.07 | 1.160 | 34.59% | 97.75% | `{"filegroups/source": 0.9888947010040283}` |
| filetypes/c | group_only | 14225 | 495122 | 13.62% | 24 | 48.47 | 68.17 | 9.279 | 23.95% | 97.58% | `{"filegroups/source": 0.9865555763244629}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/zst† | or_general_primary | 2283 | 16150 | 100.00% | 2 | 123.84 | 389.78 | 0.773 | 99.96% | 99.99% | `{"filegroups/archive": 0.9629115462303162, "filetypes/zst": 0.2697281837463379, "general": 0.8537424206733704}` |
| filetypes/rtf† | filetype_only | 89 | 472 | 98.88% | 1 | 2118.64 | 10010.79 | 0.387 | 98.88% | 99.64% | `{"filetypes/rtf": 0.18790295720100403}` |
| filetypes/tar† | group_only | 1043 | 363 | 95.11% | 1 | 2754.82 | 13001.30 | 0.387 | 97.45% | 96.30% | `{"filegroups/archive": 0.8576492667198181}` |
| filetypes/pkg-info† | general_only | 3683 | 877 | 94.73% | 1 | 1140.25 | 5397.66 | 0.387 | 97.28% | 95.72% | `{"general": 0.010649630799889565}` |
| filetypes/tar.gz† | group_only | 19546 | 12062 | 94.44% | 1 | 82.90 | 393.23 | 0.387 | 97.14% | 96.56% | `{"filegroups/archive": 0.9936721268536048}` |
| filetypes/elf | group_only | 22261 | 117951 | 94.35% | 10 | 84.78 | 143.80 | 3.866 | 97.07% | 99.10% | `{"filegroups/native": 0.9937821626663208}` |
| filetypes/package.json† | or_general_primary | 15739 | 8999 | 92.15% | 3 | 333.37 | 861.39 | 1.160 | 95.91% | 95.00% | `{"filegroups/config": 1.0, "filetypes/package.json": 0.995870958371395, "general": 0.9909160635106804}` |
| filetypes/macho† | filetype_only | 1354 | 6179 | 91.88% | 0 | 0.00 | 484.71 | 0.000 | 95.77% | 98.54% | `{"filetypes/macho": 0.7115956445631395}` |
| filetypes/javascript | filetype_only | 58630 | 396958 | 89.37% | 32 | 80.61 | 108.28 | 12.372 | 94.36% | 98.62% | `{"filetypes/javascript": 0.9755575656890869}` |
| filetypes/docx† | filetype_only | 375 | 232 | 88.53% | 1 | 4310.34 | 20283.45 | 0.387 | 93.79% | 92.75% | `{"filetypes/docx": 0.3691062331199646}` |
| filetypes/java_class | group_only | 619 | 254875 | 87.88% | 22 | 86.32 | 123.25 | 8.506 | 91.81% | 99.96% | `{"filegroups/portable": 0.9267590641975403}` |
| filetypes/pe | or_general_primary | 470591 | 144206 | 86.97% | 32 | 221.90 | 298.05 | 12.372 | 93.03% | 90.02% | `{"filegroups/native": 0.9980571866035461, "filetypes/pe": 0.9992949366569519, "general": 0.997146487236023}` |
| filetypes/zip† | or_general_primary | 33696 | 5814 | 82.91% | 3 | 516.00 | 1333.07 | 1.160 | 90.65% | 85.42% | `{"filegroups/archive": 0.9982757461225161, "filetypes/zip": 0.9939255230539884, "general": 0.9962238159387328}` |
| filetypes/ole† | or_general_primary | 259 | 5320 | 81.85% | 2 | 375.94 | 1182.94 | 0.773 | 89.64% | 99.12% | `{"filegroups/documents": 0.37927838839688977, "filetypes/ole": 1.0, "general": 0.05612311129974548}` |
| filetypes/python | filetype_only | 14625 | 117204 | 79.65% | 10 | 85.32 | 144.72 | 3.866 | 88.64% | 97.73% | `{"filetypes/python": 0.9918257594108582}` |
| filetypes/data† | or_general_primary | 403 | 8928 | 78.41% | 2 | 224.01 | 705.00 | 0.773 | 87.66% | 99.05% | `{"filetypes/data": 0.18315653380257085, "general": 1.0}` |
| filetypes/perl† | filetype_only | 194 | 29926 | 76.29% | 3 | 100.25 | 259.07 | 1.160 | 85.80% | 99.84% | `{"filetypes/perl": 0.9780732989311218}` |
| filetypes/jar† | filetype_only | 616 | 1712 | 75.97% | 1 | 584.11 | 2767.92 | 0.387 | 86.27% | 93.60% | `{"filetypes/jar": 0.8501611351966858}` |
| filetypes/php | filetype_only | 3374 | 49169 | 71.64% | 4 | 81.35 | 186.15 | 1.546 | 83.42% | 98.17% | `{"filetypes/php": 0.9225525856018066}` |
| filetypes/deb† | general_only | 31 | 4498 | 61.29% | 1 | 222.32 | 1054.22 | 0.387 | 74.51% | 99.71% | `{"general": 0.9048204659021054}` |
| filetypes/batch† | filetype_only | 439 | 2169 | 61.28% | 1 | 461.04 | 2185.23 | 0.387 | 75.88% | 93.44% | `{"filetypes/batch": 0.9818213582038879}` |
| filetypes/kotlin | filetype_only | 1009 | 38814 | 58.97% | 4 | 103.06 | 235.81 | 1.546 | 74.00% | 98.95% | `{"filetypes/kotlin": 0.05867532640695572}` |
| filetypes/shell | filetype_only | 2437 | 42326 | 58.76% | 4 | 94.50 | 216.25 | 1.546 | 73.95% | 97.75% | `{"filetypes/shell": 0.6562391519546509}` |
| filetypes/powershell† | filetype_only | 506 | 1968 | 57.91% | 1 | 508.13 | 2408.21 | 0.387 | 73.25% | 91.35% | `{"filetypes/powershell": 0.9687137007713318}` |
| filetypes/msi† | group_only | 308 | 103 | 56.82% | 1 | 9708.74 | 45228.30 | 0.387 | 72.31% | 67.40% | `{"filegroups/archive": 0.9808922410011292}` |
| filetypes/vbs† | or_general_primary | 759 | 3230 | 52.31% | 1 | 309.60 | 1467.84 | 0.387 | 68.63% | 90.90% | `{"filetypes/vbs": 0.995169213803772, "general": 0.9841272627310651}` |
| filetypes/xlsx† | or_general_primary | 121 | 105 | 42.98% | 1 | 9523.81 | 44382.14 | 0.387 | 59.77% | 69.03% | `{"filegroups/documents": 0.9951799511909485, "filetypes/xlsx": 0.584685206413269, "general": 0.9924589395523071}` |
| filetypes/groovy† | general_only | 4 | 4821 | 25.00% | 0 | 0.00 | 621.20 | 0.000 | 40.00% | 99.94% | `{"general": 0.0036344909287529233}` |
| filetypes/csharp | group_only | 1728 | 59153 | 21.82% | 5 | 84.53 | 177.72 | 1.933 | 35.73% | 97.77% | `{"filegroups/source": 0.9881306290626526}` |
| filetypes/c | group_only | 14225 | 495122 | 14.16% | 40 | 80.79 | 105.16 | 15.465 | 24.74% | 97.59% | `{"filegroups/source": 0.9795798659324646}` |
