# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1464203399`
- Rows: 4731967 (1703780 malware, 3028187 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09942859733381969, "filetypes/rtf": 0.09942859733381969, "general": 0.09942859733381969}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"general": 0.12204946577548981}` |
| filetypes/xls | joint_or_at_fp_0 | 10502 | 366 | 95.87% | 0 | 0.00 | 8151.65 | 0.000 | 97.89% | 96.01% | `{"filegroups/documents": 0.4442390203475952, "filetypes/xls": 0.9128599166870117, "general": 0.9861240386962891}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1868 | 31331 | 93.68% | 0 | 0.00 | 95.61 | 0.000 | 96.74% | 99.64% | `{"filetypes/python-bytecode": 0.9994869232177734, "general": 0.9119303226470947}` |
| filetypes/elf | joint_or_at_fp_3 | 73273 | 136298 | 93.35% | 3 | 22.01 | 56.89 | 0.991 | 96.56% | 97.67% | `{"filegroups/native": 0.9869728088378906, "filetypes/elf": 0.999223530292511, "general": 0.9877766966819763}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5360 | 91.96% | 0 | 0.00 | 558.75 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9650191068649292, "general": 0.9608342051506042}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.99739009141922}` |
| filetypes/macho† | filetype_only | 2068 | 10693 | 89.80% | 0 | 0.00 | 280.12 | 0.000 | 94.62% | 98.35% | `{"filetypes/macho": 0.9435528441622434}` |
| filetypes/package.json | joint_or_at_fp_0 | 17794 | 11632 | 89.52% | 0 | 0.00 | 257.51 | 0.000 | 94.47% | 93.67% | `{"filegroups/config": 0.9988580346107483, "filetypes/package.json": 0.9981180429458618, "general": 0.9865904450416565}` |
| filetypes/shell | joint_or_at_fp_0 | 6893 | 45536 | 79.66% | 0 | 0.00 | 65.79 | 0.000 | 88.68% | 97.33% | `{"filegroups/scripts": 0.9930943250656128, "filetypes/shell": 0.9591485857963562, "general": 0.9421998858451843}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/zst | calibrate_inherited | 10381 | 16157 | 75.87% | 0 | 0.00 | 185.40 | 0.000 | 86.28% | 90.56% | `{"general": 0.99739009141922}` |
| filetypes/java_class | joint_or_at_fp_5 | 1312 | 381385 | 75.46% | 5 | 13.11 | 27.57 | 1.651 | 85.83% | 99.91% | `{"filegroups/portable": 0.9648229479789734, "filetypes/java_class": 0.9483261108398438, "general": 0.964408814907074}` |
| filetypes/javascript | learned_blend_at_fp_7 | 84463 | 472874 | 75.24% | 7 | 14.80 | 27.80 | 2.312 | 85.87% | 96.25% | `{}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31548 | 72.32% | 0 | 0.00 | 94.95 | 0.000 | 83.94% | 99.80% | `{"filetypes/perl": 0.8564482927322388}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 70.89% | 0 | 0.00 | 37678.63 | 0.000 | 82.97% | 71.41% | `{"general": 0.99739009141922}` |
| filetypes/python | joint_or_at_fp_6 | 17916 | 130234 | 69.04% | 6 | 46.07 | 90.93 | 1.981 | 81.67% | 96.25% | `{"filegroups/scripts": 0.9985737800598145, "filetypes/python": 0.9855971932411194}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 68.44% | 0 | 0.00 | 527129.20 | 0.000 | 81.26% | 68.46% | `{"general": 0.99739009141922}` |
| filetypes/php | joint_or_at_fp_3 | 3864 | 86590 | 67.42% | 3 | 34.65 | 89.54 | 0.991 | 80.50% | 98.60% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9827495813369751, "general": 0.9812013506889343}` |
| filetypes/pe | learned_blend_at_fp_3 | 901925 | 151968 | 63.36% | 3 | 19.74 | 51.02 | 0.991 | 77.57% | 68.64% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 60.89% | 0 | 0.00 | 2907.07 | 0.000 | 75.69% | 74.09% | `{"filetypes/lnk": 0.690523087978363, "general": 0.9603573083877563}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 60.59% | 0 | 0.00 | 7315.59 | 0.000 | 75.46% | 71.12% | `{"general": 0.99739009141922}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 58.90% | 0 | 0.00 | 123.09 | 0.000 | 74.14% | 99.88% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.9998502731323242, "general": 0.9020878076553345}` |
| filetypes/jar | joint_or_at_fp_0 | 1466 | 2131 | 57.57% | 0 | 0.00 | 1404.80 | 0.000 | 73.07% | 82.71% | `{"filetypes/jar": 0.8717573285102844, "general": 0.9930866956710815}` |
| filetypes/tar.gz | calibrate_inherited | 28003 | 12988 | 56.69% | 0 | 0.00 | 230.63 | 0.000 | 72.36% | 70.41% | `{"general": 0.99739009141922}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23576 | 42565 | 51.99% | 0 | 0.00 | 70.38 | 0.000 | 68.41% | 82.89% | `{"filegroups/source": 0.9793435335159302, "filetypes/kotlin": 0.648093581199646, "general": 0.8884381651878357}` |
| filetypes/html | calibrate_inherited | 49 | 7963 | 46.94% | 0 | 0.00 | 376.14 | 0.000 | 63.89% | 99.68% | `{"filegroups/documents": 0.7451304793357849, "general": 0.99739009141922}` |
| filetypes/zip | calibrate_inherited | 59697 | 7353 | 41.06% | 0 | 0.00 | 407.33 | 0.000 | 58.22% | 47.53% | `{"general": 0.99739009141922}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09909127415315319, "filetypes/rtf": 0.09909127415315319, "general": 0.09909127415315319}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"general": 0.12204946577548981}` |
| filetypes/xls | joint_or_at_fp_0 | 10502 | 366 | 95.87% | 0 | 0.00 | 8151.65 | 0.000 | 97.89% | 96.01% | `{"filegroups/documents": 0.4442390203475952, "filetypes/xls": 0.9128599166870117, "general": 0.9861240386962891}` |
| filetypes/python-bytecode | joint_or_at_fp_2 | 1868 | 31331 | 95.66% | 2 | 63.83 | 200.93 | 0.660 | 97.73% | 99.75% | `{"filetypes/python-bytecode": 0.9972035884857178, "general": 0.8912548422813416}` |
| filetypes/elf | joint_or_at_fp_3 | 73273 | 136298 | 93.35% | 3 | 22.01 | 56.89 | 0.991 | 96.56% | 97.67% | `{"filegroups/native": 0.9869728088378906, "filetypes/elf": 0.999223530292511, "general": 0.9877766966819763}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5360 | 91.96% | 0 | 0.00 | 558.75 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9650191068649292, "general": 0.9608342051506042}` |
| filetypes/macho | joint_or_at_fp_0 | 2068 | 10693 | 91.44% | 0 | 0.00 | 280.12 | 0.000 | 95.53% | 98.61% | `{"filegroups/native": 0.9182161092758179, "filetypes/macho": 0.9445164799690247, "general": 0.9760084748268127}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9966464638710022}` |
| filetypes/package.json | joint_or_at_fp_0 | 17794 | 11632 | 89.52% | 0 | 0.00 | 257.51 | 0.000 | 94.47% | 93.67% | `{"filegroups/config": 0.9988580346107483, "filetypes/package.json": 0.9981180429458618, "general": 0.9865904450416565}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 1 | 61.89 | 293.58 | 0.330 | 93.15% | 94.98% | `{"general": 0.9181550741195679}` |
| filetypes/shell | joint_or_at_fp_3 | 6893 | 45536 | 82.24% | 3 | 65.88 | 170.27 | 0.991 | 90.23% | 97.66% | `{"filegroups/scripts": 0.9930943250656128, "filetypes/shell": 0.9222875237464905, "general": 0.9421998858451843}` |
| filetypes/java_class | filetype_only_at_fp_9 | 1312 | 381385 | 81.25% | 10 | 26.22 | 44.47 | 3.302 | 89.28% | 99.93% | `{"filetypes/java_class": 0.8830877542495728}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/javascript | joint_or_at_fp_12 | 84463 | 472874 | 76.52% | 12 | 25.38 | 41.12 | 3.963 | 86.69% | 96.44% | `{"filegroups/scripts": 0.9991405010223389, "filetypes/javascript": 0.9700271487236023, "general": 0.9943726658821106}` |
| filetypes/perl | joint_or_at_fp_2 | 224 | 31548 | 74.11% | 2 | 63.40 | 199.55 | 0.660 | 84.69% | 99.81% | `{"filetypes/perl": 0.8395268321037292, "general": 0.7128100991249084}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 73.77% | 0 | 0.00 | 37678.63 | 0.000 | 84.91% | 74.24% | `{"general": 0.9966464638710022}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 71.95% | 0 | 0.00 | 527129.20 | 0.000 | 83.69% | 71.97% | `{"general": 0.9966464638710022}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/php | joint_or_at_fp_7 | 3864 | 86590 | 70.68% | 7 | 80.84 | 151.84 | 2.312 | 82.73% | 98.74% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9678218960762024, "general": 0.9812013506889343}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 69.88% | 0 | 0.00 | 7315.59 | 0.000 | 82.27% | 77.93% | `{"general": 0.9966464638710022}` |
| filetypes/python | joint_or_at_fp_6 | 17916 | 130234 | 69.04% | 6 | 46.07 | 90.93 | 1.981 | 81.67% | 96.25% | `{"filegroups/scripts": 0.9985737800598145, "filetypes/python": 0.9855971932411194}` |
| filetypes/pe | learned_blend_at_fp_3 | 901925 | 151968 | 63.36% | 3 | 19.74 | 51.02 | 0.991 | 77.57% | 68.64% | `{}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 62.18% | 1 | 76.99 | 365.20 | 0.330 | 76.68% | 74.16% | `{"general": 0.9955267568355584}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 60.89% | 0 | 0.00 | 2907.07 | 0.000 | 75.69% | 74.09% | `{"filetypes/lnk": 0.690523087978363, "general": 0.9603573083877563}` |
| filetypes/kotlin | learned_blend_at_fp_6 | 23576 | 42565 | 59.27% | 3 | 70.48 | 182.15 | 0.991 | 74.42% | 85.48% | `{}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 58.90% | 0 | 0.00 | 123.09 | 0.000 | 74.14% | 99.88% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.9998502731323242, "general": 0.9020878076553345}` |
| filetypes/jar | joint_or_at_fp_0 | 1466 | 2131 | 57.57% | 0 | 0.00 | 1404.80 | 0.000 | 73.07% | 82.71% | `{"filetypes/jar": 0.8717573285102844, "general": 0.9930866956710815}` |
| filetypes/html | calibrate_inherited | 49 | 7963 | 46.94% | 0 | 0.00 | 376.14 | 0.000 | 63.89% | 99.68% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9966464638710022}` |
| filetypes/chrome-manifest† | or_general_primary | 41 | 354 | 31.71% | 0 | 0.00 | 8426.81 | 0.000 | 48.15% | 92.91% | `{"general": 0.7768734811466628}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 1 | 125.58 | 595.60 | 0.330 | 98.99% | 99.99% | `{"filegroups/documents": 0.06350564956665039, "general": 0.06350564956665039}` |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09749212100910538, "filetypes/rtf": 0.09749212100910538, "general": 0.09749212100910538}` |
| filetypes/package.json | joint_or_at_fp_4 | 17794 | 11632 | 98.06% | 4 | 343.88 | 786.75 | 1.321 | 99.01% | 98.81% | `{"filegroups/config": 0.9839301109313965, "filetypes/package.json": 0.9619410634040833, "general": 0.9871711134910583}` |
| filetypes/elf | learned_blend_at_fp_18 | 73273 | 136298 | 97.45% | 18 | 132.06 | 195.83 | 5.944 | 98.70% | 99.10% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"general": 0.12204946577548981}` |
| filetypes/xls | joint_or_at_fp_0 | 10502 | 366 | 95.87% | 0 | 0.00 | 8151.65 | 0.000 | 97.89% | 96.01% | `{"filegroups/documents": 0.4442390203475952, "filetypes/xls": 0.9128599166870117, "general": 0.9861240386962891}` |
| filetypes/python-bytecode | joint_or_at_fp_3 | 1868 | 31331 | 95.72% | 3 | 95.75 | 247.46 | 0.991 | 97.73% | 99.75% | `{"filetypes/python-bytecode": 0.9973898530006409, "general": 0.8371536135673523}` |
| filetypes/macho | joint_or_at_fp_4 | 2068 | 10693 | 93.62% | 4 | 374.08 | 855.82 | 1.321 | 96.61% | 98.93% | `{"filegroups/native": 0.9182161092758179, "filetypes/macho": 0.9191778302192688, "general": 0.9760084748268127}` |
| filetypes/ole† | filetype_only | 1928 | 5360 | 92.53% | 2 | 373.13 | 1174.12 | 0.660 | 96.07% | 98.00% | `{"filetypes/ole": 0.8679388728913131}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9893494844436646}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 1 | 61.89 | 293.58 | 0.330 | 93.15% | 94.98% | `{"general": 0.9181550741195679}` |
| filetypes/java_class | filetype_only_at_fp_38 | 1312 | 381385 | 86.66% | 38 | 99.64 | 130.60 | 12.549 | 91.44% | 99.94% | `{"filetypes/java_class": 0.48867344856262207}` |
| filetypes/ruby | joint_or_at_fp_3 | 73 | 24337 | 86.30% | 3 | 123.27 | 318.56 | 0.991 | 90.65% | 99.95% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.999492883682251, "general": 0.8310150504112244}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 85.61% | 0 | 0.00 | 7315.59 | 0.000 | 92.25% | 89.46% | `{"general": 0.9893494844436646}` |
| filetypes/shell | joint_or_at_fp_8 | 6893 | 45536 | 85.17% | 8 | 175.69 | 316.97 | 2.642 | 91.94% | 98.04% | `{"filegroups/scripts": 0.9924869537353516, "filetypes/shell": 0.8185165524482727, "general": 0.9421998858451843}` |
| filetypes/desktop-entry† | or_general_primary | 6 | 496 | 83.33% | 0 | 0.00 | 6021.58 | 0.000 | 90.91% | 99.80% | `{"general": 0.7374058055594734}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 82.68% | 0 | 0.00 | 527129.20 | 0.000 | 90.52% | 82.69% | `{"general": 0.9893494844436646}` |
| filetypes/javascript | joint_or_at_fp_53 | 84463 | 472874 | 81.07% | 53 | 112.08 | 140.90 | 17.502 | 89.52% | 97.12% | `{"filegroups/scripts": 0.9994582533836365, "filetypes/javascript": 0.9085571765899658, "general": 0.9985303282737732}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 81.05% | 0 | 0.00 | 37678.63 | 0.000 | 89.53% | 81.38% | `{"general": 0.9893494844436646}` |
| filetypes/perl | calibrate_inherited | 224 | 31548 | 79.02% | 10 | 316.98 | 537.60 | 3.302 | 86.13% | 99.82% | `{"filegroups/scripts": 0.9950908422470093, "filetypes/perl": 0.7245799145927766, "general": 0.9893494844436646}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/php | joint_or_at_fp_11 | 3864 | 86590 | 72.80% | 11 | 127.04 | 210.26 | 3.633 | 84.12% | 98.83% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9437333345413208, "general": 0.9812013506889343}` |
| filetypes/python | joint_or_at_fp_27 | 17916 | 130234 | 72.36% | 27 | 207.32 | 285.89 | 8.916 | 83.89% | 96.64% | `{"filegroups/scripts": 0.9985737800598145, "filetypes/python": 0.9695929288864136}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/pe | specialist_primary_with_escape | 901925 | 151968 | 69.97% | 19 | 125.03 | 183.45 | 6.274 | 82.33% | 74.29% | `{"filegroups/native": 0.9995619654655457, "filetypes/pe": 0.9997455477714539, "general": 0.997014582157135}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.9893494844436646}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 62.24% | 1 | 76.99 | 365.20 | 0.330 | 76.73% | 74.20% | `{"general": 0.9954979212345533}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 60.89% | 0 | 0.00 | 2907.07 | 0.000 | 75.69% | 74.09% | `{"filetypes/lnk": 0.690523087978363, "general": 0.9603573083877563}` |
| filetypes/kotlin | calibrate_inherited | 23576 | 42565 | 60.63% | 18 | 422.88 | 627.02 | 5.944 | 75.45% | 85.94% | `{"filegroups/source": 0.9891790151596069, "filetypes/kotlin": 0.027027010917663574, "general": 0.9893494844436646}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 1 | 125.58 | 595.60 | 0.330 | 98.99% | 99.99% | `{"filegroups/documents": 0.06350564956665039, "general": 0.06350564956665039}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.985923171043396}` |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/package.json | joint_or_at_fp_5 | 17794 | 11632 | 98.45% | 5 | 429.85 | 903.59 | 1.651 | 99.20% | 99.05% | `{"filegroups/config": 0.9844081997871399, "filetypes/package.json": 0.9428770542144775, "general": 0.9871711134910583}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09672378283708581, "filetypes/rtf": 0.09672378283708581, "general": 0.09672378283708581}` |
| filetypes/elf | learned_blend_at_fp_29 | 73273 | 136298 | 97.92% | 28 | 205.43 | 281.64 | 9.246 | 98.93% | 99.26% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"general": 0.12204946577548981}` |
| filetypes/xls | joint_or_at_fp_0 | 10502 | 366 | 95.87% | 0 | 0.00 | 8151.65 | 0.000 | 97.89% | 96.01% | `{"filegroups/documents": 0.4442390203475952, "filetypes/xls": 0.9128599166870117, "general": 0.9861240386962891}` |
| filetypes/python-bytecode† | specialist_primary_with_escape | 1868 | 31331 | 95.72% | 4 | 127.67 | 292.13 | 1.321 | 97.70% | 99.75% | `{"filetypes/python-bytecode": 0.9971392154693604, "general": 0.796545684337616}` |
| filetypes/macho | joint_or_at_fp_4 | 2068 | 10693 | 93.62% | 4 | 374.08 | 855.82 | 1.321 | 96.61% | 98.93% | `{"filegroups/native": 0.9182161092758179, "filetypes/macho": 0.9191778302192688, "general": 0.9760084748268127}` |
| filetypes/ole | filetype_only_at_fp_3 | 1928 | 5360 | 92.69% | 4 | 746.27 | 1706.93 | 1.321 | 96.10% | 98.01% | `{"filetypes/ole": 0.37838542461395264}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.985923171043396}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 88.65% | 0 | 0.00 | 7315.59 | 0.000 | 93.98% | 91.68% | `{"general": 0.985923171043396}` |
| filetypes/java_class | filetype_only_at_fp_53 | 1312 | 381385 | 88.26% | 53 | 138.97 | 174.70 | 17.502 | 91.80% | 99.95% | `{"filetypes/java_class": 0.326313316822052}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 2 | 123.79 | 389.61 | 0.660 | 93.15% | 94.98% | `{"general": 0.9168552756309509}` |
| filetypes/ruby | joint_or_at_fp_3 | 73 | 24337 | 86.30% | 3 | 123.27 | 318.56 | 0.991 | 90.65% | 99.95% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.999492883682251, "general": 0.8310150504112244}` |
| filetypes/shell | learned_blend_at_fp_11 | 6893 | 45536 | 85.65% | 11 | 241.57 | 399.82 | 3.633 | 92.19% | 98.09% | `{}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 83.42% | 0 | 0.00 | 527129.20 | 0.000 | 90.96% | 83.43% | `{"general": 0.985923171043396}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 82.11% | 0 | 0.00 | 37678.63 | 0.000 | 90.18% | 82.43% | `{"general": 0.985923171043396}` |
| filetypes/javascript | joint_or_at_fp_75 | 84463 | 472874 | 81.92% | 75 | 158.60 | 192.19 | 24.767 | 90.02% | 97.25% | `{"filegroups/scripts": 0.9994582533836365, "filetypes/javascript": 0.8800194263458252}` |
| filetypes/perl | calibrate_inherited | 224 | 31548 | 79.46% | 14 | 443.77 | 693.67 | 4.623 | 85.58% | 99.81% | `{"filegroups/scripts": 0.9915443658828735, "filetypes/perl": 0.685601445324008, "general": 0.985923171043396}` |
| filetypes/python | joint_or_at_fp_41 | 17916 | 130234 | 74.02% | 41 | 314.82 | 408.46 | 13.539 | 84.96% | 96.83% | `{"filegroups/scripts": 0.9979294538497925, "filetypes/python": 0.9558942317962646}` |
| filetypes/pe | specialist_primary_with_escape | 901925 | 151968 | 73.86% | 34 | 223.73 | 297.85 | 11.228 | 84.96% | 77.62% | `{"filegroups/native": 0.9995200037956238, "filetypes/pe": 0.9997068643569946, "general": 0.9961766600608826}` |
| filetypes/php | joint_or_at_fp_16 | 3864 | 86590 | 73.52% | 16 | 184.78 | 280.63 | 5.284 | 84.54% | 98.85% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9354349374771118, "general": 0.9812013506889343}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.985923171043396}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 63.12% | 2 | 153.99 | 484.66 | 0.660 | 77.39% | 74.80% | `{"general": 0.9950588941574097}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 60.89% | 0 | 0.00 | 2907.07 | 0.000 | 75.69% | 74.09% | `{"filetypes/lnk": 0.690523087978363, "general": 0.9603573083877563}` |
| filetypes/objc† | or_general_primary | 5 | 18405 | 60.00% | 2 | 108.67 | 342.03 | 0.660 | 60.00% | 99.98% | `{"general": 0.008938553743064404}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 23576 | 42565 | 59.26% | 3 | 70.48 | 182.15 | 0.991 | 74.42% | 85.47% | `{}` |
