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
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.12993251613655393, "general": 0.026301932556449584}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 1868 | 31331 | 93.68% | 0 | 0.00 | 95.61 | 0.000 | 96.74% | 99.64% | `{"filetypes/python-bytecode": 0.9994869232177734, "general": 0.9119303226470947}` |
| filetypes/elf | joint_or_at_fp_6 | 73273 | 136298 | 93.47% | 6 | 44.02 | 86.88 | 1.981 | 96.62% | 97.71% | `{"filegroups/native": 0.9988999366760254, "filetypes/elf": 0.9977439641952515, "general": 0.9874759316444397}` |
| filetypes/xls | calibrate_inherited | 10502 | 366 | 93.20% | 0 | 0.00 | 8151.65 | 0.000 | 96.48% | 93.43% | `{"filegroups/documents": 0.7451304793357849, "general": 0.99739009141922}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5360 | 91.96% | 0 | 0.00 | 558.75 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9650191068649292, "general": 0.9608342051506042}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.99739009141922}` |
| filetypes/macho† | filetype_only | 2068 | 10693 | 89.80% | 0 | 0.00 | 280.12 | 0.000 | 94.62% | 98.35% | `{"filetypes/macho": 0.9435528441622434}` |
| filetypes/package.json | joint_or_at_fp_0 | 17794 | 11632 | 86.00% | 0 | 0.00 | 257.51 | 0.000 | 92.47% | 91.53% | `{"filegroups/config": 0.9997491240501404, "filetypes/package.json": 0.9995682835578918, "general": 0.9865904450416565}` |
| filetypes/shell | joint_or_at_fp_0 | 6893 | 45536 | 79.66% | 0 | 0.00 | 65.79 | 0.000 | 88.68% | 97.33% | `{"filegroups/scripts": 0.9930943250656128, "filetypes/shell": 0.9591485857963562, "general": 0.9421998858451843}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/zst | calibrate_inherited | 10381 | 16157 | 75.87% | 0 | 0.00 | 185.40 | 0.000 | 86.28% | 90.56% | `{"general": 0.99739009141922}` |
| filetypes/java_class | joint_or_at_fp_9 | 1312 | 381385 | 75.08% | 9 | 23.60 | 41.18 | 2.972 | 85.43% | 99.91% | `{"filegroups/portable": 0.9987190961837769, "filetypes/java_class": 0.9990317821502686, "general": 0.9901570677757263}` |
| filetypes/perl | joint_or_at_fp_0 | 224 | 31548 | 71.88% | 0 | 0.00 | 94.95 | 0.000 | 83.64% | 99.80% | `{"filegroups/scripts": 0.9784479737281799, "filetypes/perl": 0.9990894794464111}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 70.89% | 0 | 0.00 | 37678.63 | 0.000 | 82.97% | 71.41% | `{"general": 0.99739009141922}` |
| filetypes/javascript | joint_or_at_fp_6 | 84467 | 472874 | 69.29% | 6 | 12.69 | 25.04 | 1.981 | 81.86% | 95.34% | `{"filegroups/scripts": 0.9991825222969055, "filetypes/javascript": 0.9967556595802307, "general": 0.9942488670349121}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 68.44% | 0 | 0.00 | 527129.20 | 0.000 | 81.26% | 68.46% | `{"general": 0.99739009141922}` |
| filetypes/php | joint_or_at_fp_3 | 3864 | 86590 | 67.42% | 3 | 34.65 | 89.54 | 0.991 | 80.50% | 98.60% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9827495813369751, "general": 0.9812013506889343}` |
| filetypes/python | learned_blend_at_fp_3 | 17917 | 130234 | 65.36% | 6 | 46.07 | 90.93 | 1.981 | 79.04% | 95.81% | `{}` |
| filetypes/pe | learned_blend_at_fp_4 | 901925 | 151968 | 63.02% | 4 | 26.32 | 60.23 | 1.321 | 77.32% | 68.35% | `{}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 60.59% | 0 | 0.00 | 7315.59 | 0.000 | 75.46% | 71.12% | `{"general": 0.99739009141922}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 58.90% | 0 | 0.00 | 123.09 | 0.000 | 74.14% | 99.88% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.9998502731323242, "general": 0.9020878076553345}` |
| filetypes/jar | joint_or_at_fp_0 | 1466 | 2131 | 57.57% | 0 | 0.00 | 1404.80 | 0.000 | 73.07% | 82.71% | `{"filetypes/jar": 0.8717573285102844, "general": 0.9930866956710815}` |
| filetypes/tar.gz | calibrate_inherited | 28003 | 12988 | 56.69% | 0 | 0.00 | 230.63 | 0.000 | 72.36% | 70.41% | `{"general": 0.99739009141922}` |
| filetypes/kotlin | joint_or_at_fp_0 | 23576 | 42565 | 51.99% | 0 | 0.00 | 70.38 | 0.000 | 68.41% | 82.89% | `{"filegroups/source": 0.9793435335159302, "filetypes/kotlin": 0.648093581199646, "general": 0.8884381651878357}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 49.31% | 0 | 0.00 | 2907.07 | 0.000 | 66.05% | 66.42% | `{"filetypes/lnk": 0.9913873076438904, "general": 0.9633228778839111}` |
| filetypes/html | calibrate_inherited | 49 | 7963 | 46.94% | 0 | 0.00 | 376.14 | 0.000 | 63.89% | 99.68% | `{"filegroups/documents": 0.7451304793357849, "general": 0.99739009141922}` |
| filetypes/zip | calibrate_inherited | 59697 | 7353 | 41.06% | 0 | 0.00 | 407.33 | 0.000 | 58.22% | 47.53% | `{"general": 0.99739009141922}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09909127415315319, "filetypes/rtf": 0.09909127415315319, "general": 0.09909127415315319}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.11842999317207475, "general": 0.026216834676886742}` |
| filetypes/python-bytecode | joint_or_at_fp_2 | 1868 | 31331 | 95.66% | 2 | 63.83 | 200.93 | 0.660 | 97.73% | 99.75% | `{"filetypes/python-bytecode": 0.9972035884857178, "general": 0.8912548422813416}` |
| filetypes/elf | joint_or_at_fp_6 | 73273 | 136298 | 93.47% | 6 | 44.02 | 86.88 | 1.981 | 96.62% | 97.71% | `{"filegroups/native": 0.9988999366760254, "filetypes/elf": 0.9977439641952515, "general": 0.9874759316444397}` |
| filetypes/xls | calibrate_inherited | 10502 | 366 | 93.20% | 0 | 0.00 | 8151.65 | 0.000 | 96.48% | 93.43% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9966464638710022}` |
| filetypes/ole | joint_or_at_fp_0 | 1928 | 5360 | 91.96% | 0 | 0.00 | 558.75 | 0.000 | 95.81% | 97.87% | `{"filetypes/ole": 0.9650191068649292, "general": 0.9608342051506042}` |
| filetypes/macho | joint_or_at_fp_0 | 2068 | 10693 | 90.33% | 0 | 0.00 | 280.12 | 0.000 | 94.92% | 98.43% | `{"filegroups/native": 0.9979678988456726, "filetypes/macho": 0.9445164799690247, "general": 0.9731881022453308}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9966464638710022}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 1 | 61.89 | 293.58 | 0.330 | 93.15% | 94.98% | `{"general": 0.9181550741195679}` |
| filetypes/package.json | joint_or_at_fp_0 | 17794 | 11632 | 86.00% | 0 | 0.00 | 257.51 | 0.000 | 92.47% | 91.53% | `{"filegroups/config": 0.9997491240501404, "filetypes/package.json": 0.9995682835578918, "general": 0.9865904450416565}` |
| filetypes/shell | joint_or_at_fp_3 | 6893 | 45536 | 82.24% | 3 | 65.88 | 170.27 | 0.991 | 90.23% | 97.66% | `{"filegroups/scripts": 0.9930943250656128, "filetypes/shell": 0.9222875237464905, "general": 0.9421998858451843}` |
| filetypes/perl | learned_blend_at_fp_2 | 224 | 31548 | 76.79% | 2 | 63.40 | 199.55 | 0.660 | 86.43% | 99.83% | `{}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/javascript | learned_blend_at_fp_26 | 84467 | 472874 | 76.41% | 26 | 54.98 | 76.29 | 8.586 | 86.62% | 96.42% | `{}` |
| filetypes/java_class | joint_or_at_fp_9 | 1312 | 381385 | 75.08% | 9 | 23.60 | 41.18 | 2.972 | 85.43% | 99.91% | `{"filegroups/portable": 0.9987190961837769, "filetypes/java_class": 0.9990317821502686, "general": 0.9901570677757263}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 73.77% | 0 | 0.00 | 37678.63 | 0.000 | 84.91% | 74.24% | `{"general": 0.9966464638710022}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 71.95% | 0 | 0.00 | 527129.20 | 0.000 | 83.69% | 71.97% | `{"general": 0.9966464638710022}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/php | joint_or_at_fp_7 | 3864 | 86590 | 70.68% | 7 | 80.84 | 151.84 | 2.312 | 82.73% | 98.74% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9678218960762024, "general": 0.9812013506889343}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 69.88% | 0 | 0.00 | 7315.59 | 0.000 | 82.27% | 77.93% | `{"general": 0.9966464638710022}` |
| filetypes/python | joint_or_at_fp_5 | 17917 | 130234 | 65.46% | 5 | 38.39 | 80.72 | 1.651 | 79.11% | 95.82% | `{"filegroups/scripts": 0.9985718727111816, "filetypes/python": 0.9962198138237, "general": 0.9982017874717712}` |
| filetypes/pe | learned_blend_at_fp_6 | 901925 | 151968 | 64.19% | 6 | 39.48 | 77.93 | 1.981 | 78.19% | 69.36% | `{}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 62.18% | 1 | 76.99 | 365.20 | 0.330 | 76.68% | 74.16% | `{"general": 0.9955267568355584}` |
| filetypes/kotlin | learned_blend_at_fp_6 | 23576 | 42565 | 59.27% | 3 | 70.48 | 182.15 | 0.991 | 74.42% | 85.48% | `{}` |
| filetypes/ruby | joint_or_at_fp_0 | 73 | 24337 | 58.90% | 0 | 0.00 | 123.09 | 0.000 | 74.14% | 99.88% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.9998502731323242, "general": 0.9020878076553345}` |
| filetypes/jar | joint_or_at_fp_0 | 1466 | 2131 | 57.57% | 0 | 0.00 | 1404.80 | 0.000 | 73.07% | 82.71% | `{"filetypes/jar": 0.8717573285102844, "general": 0.9930866956710815}` |
| filetypes/lnk | joint_or_at_fp_0 | 2020 | 1029 | 49.31% | 0 | 0.00 | 2907.07 | 0.000 | 66.05% | 66.42% | `{"filetypes/lnk": 0.9913873076438904, "general": 0.9633228778839111}` |
| filetypes/html | calibrate_inherited | 49 | 7963 | 46.94% | 0 | 0.00 | 376.14 | 0.000 | 63.89% | 99.68% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9966464638710022}` |
| filetypes/chrome-manifest† | or_general_primary | 41 | 354 | 31.71% | 0 | 0.00 | 8426.81 | 0.000 | 48.15% | 92.91% | `{"general": 0.7768734811466628}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 1 | 125.58 | 595.60 | 0.330 | 98.99% | 99.99% | `{"filegroups/documents": 0.06350564956665039, "general": 0.06350564956665039}` |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09749212100910538, "filetypes/rtf": 0.09749212100910538, "general": 0.09749212100910538}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.08937791822071839, "general": 0.02579088701837296}` |
| filetypes/python-bytecode | joint_or_at_fp_3 | 1868 | 31331 | 95.72% | 3 | 95.75 | 247.46 | 0.991 | 97.73% | 99.75% | `{"filetypes/python-bytecode": 0.9973898530006409, "general": 0.8371536135673523}` |
| filetypes/elf | joint_or_at_fp_17 | 73273 | 136298 | 94.27% | 17 | 124.73 | 187.08 | 5.614 | 97.04% | 97.99% | `{"filegroups/native": 0.9988999366760254, "filetypes/elf": 0.9966819882392883, "general": 0.9874759316444397}` |
| filetypes/package.json | joint_or_at_fp_3 | 17794 | 11632 | 93.50% | 3 | 257.91 | 666.44 | 0.991 | 96.63% | 96.06% | `{"filegroups/config": 0.9996020197868347, "filetypes/package.json": 0.994786262512207, "general": 0.9774463772773743}` |
| filetypes/macho | joint_or_at_fp_4 | 2068 | 10693 | 93.23% | 4 | 374.08 | 855.82 | 1.321 | 96.40% | 98.87% | `{"filegroups/native": 0.9961297512054443, "filetypes/macho": 0.9179393649101257, "general": 0.9731881022453308}` |
| filetypes/xls | calibrate_inherited | 10502 | 366 | 93.22% | 0 | 0.00 | 8151.65 | 0.000 | 96.49% | 93.45% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9893494844436646}` |
| filetypes/ole† | filetype_only | 1928 | 5360 | 92.53% | 2 | 373.13 | 1174.12 | 0.660 | 96.07% | 98.00% | `{"filetypes/ole": 0.8679388728913131}` |
| filetypes/java_class | filetype_only_at_fp_38 | 1312 | 381385 | 91.62% | 39 | 102.26 | 133.56 | 12.879 | 94.16% | 99.96% | `{"filetypes/java_class": 0.6447398662567139}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.9893494844436646}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 1 | 61.89 | 293.58 | 0.330 | 93.15% | 94.98% | `{"general": 0.9181550741195679}` |
| filetypes/ruby | joint_or_at_fp_3 | 73 | 24337 | 86.30% | 3 | 123.27 | 318.56 | 0.991 | 90.65% | 99.95% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.999492883682251, "general": 0.8310150504112244}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 85.61% | 0 | 0.00 | 7315.59 | 0.000 | 92.25% | 89.46% | `{"general": 0.9893494844436646}` |
| filetypes/shell | joint_or_at_fp_8 | 6893 | 45536 | 85.17% | 8 | 175.69 | 316.97 | 2.642 | 91.94% | 98.04% | `{"filegroups/scripts": 0.9924869537353516, "filetypes/shell": 0.8185165524482727, "general": 0.9421998858451843}` |
| filetypes/desktop-entry† | or_general_primary | 6 | 496 | 83.33% | 0 | 0.00 | 6021.58 | 0.000 | 90.91% | 99.80% | `{"general": 0.7374058055594734}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 82.68% | 0 | 0.00 | 527129.20 | 0.000 | 90.52% | 82.69% | `{"general": 0.9893494844436646}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 81.05% | 0 | 0.00 | 37678.63 | 0.000 | 89.53% | 81.38% | `{"general": 0.9893494844436646}` |
| filetypes/python | learned_blend_at_fp_32 | 17917 | 130234 | 78.22% | 31 | 238.03 | 321.24 | 10.237 | 87.69% | 97.34% | `{}` |
| filetypes/javascript | learned_blend_at_fp_47 | 84467 | 472874 | 77.91% | 47 | 99.39 | 126.75 | 15.521 | 87.56% | 96.64% | `{}` |
| filetypes/perl | learned_blend_at_fp_3 | 224 | 31548 | 77.68% | 3 | 95.09 | 245.75 | 0.991 | 86.78% | 99.83% | `{}` |
| filetypes/msi | joint_or_at_fp_0 | 1813 | 133 | 76.72% | 0 | 0.00 | 22272.52 | 0.000 | 86.83% | 78.31% | `{"filetypes/msi": 0.4743081331253052, "general": 0.9217437505722046}` |
| filetypes/php | joint_or_at_fp_11 | 3864 | 86590 | 72.80% | 11 | 127.04 | 210.26 | 3.633 | 84.12% | 98.83% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9437333345413208, "general": 0.9812013506889343}` |
| filetypes/pe | specialist_primary_with_escape | 901925 | 151968 | 71.82% | 21 | 138.19 | 198.99 | 6.935 | 83.60% | 75.88% | `{"filegroups/native": 0.9996490478515625, "filetypes/pe": 0.9996306896209717, "general": 0.997014582157135}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.9893494844436646}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 62.24% | 1 | 76.99 | 365.20 | 0.330 | 76.73% | 74.20% | `{"general": 0.9954979212345533}` |
| filetypes/kotlin | calibrate_inherited | 23576 | 42565 | 60.63% | 18 | 422.88 | 627.02 | 5.944 | 75.45% | 85.94% | `{"filegroups/source": 0.9891790151596069, "filetypes/kotlin": 0.027027010917663574, "general": 0.9893494844436646}` |
| filetypes/objc† | or_general_primary | 5 | 18405 | 60.00% | 0 | 0.00 | 162.75 | 0.000 | 75.00% | 99.99% | `{"general": 0.3085762363814833}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | max_rule | 49 | 7963 | 100.00% | 1 | 125.58 | 595.60 | 0.330 | 98.99% | 99.99% | `{"filegroups/documents": 0.06350564956665039, "general": 0.06350564956665039}` |
| filetypes/xlsb | calibrate_inherited | 1 | 0 | 100.00% | 0 | — | — | 0.000 | 100.00% | 100.00% | `{"general": 0.985923171043396}` |
| filetypes/batch | joint_or_at_fp_0 | 168952 | 3680 | 98.77% | 0 | 0.00 | 813.73 | 0.000 | 99.38% | 98.80% | `{"filegroups/scripts": 0.996911346912384, "filetypes/batch": 0.9954710006713867, "general": 0.9905926585197449}` |
| filetypes/rtf† | max_rule | 1465 | 480 | 98.09% | 0 | 0.00 | 6221.67 | 0.000 | 99.04% | 98.56% | `{"filegroups/documents": 0.09672378283708581, "filetypes/rtf": 0.09672378283708581, "general": 0.09672378283708581}` |
| filetypes/pkg-info† | specialist_primary_with_escape | 10634 | 1035 | 97.16% | 0 | 0.00 | 2890.24 | 0.000 | 98.56% | 97.41% | `{"filetypes/pkg-info": 0.08150188792287283, "general": 0.025576969392679807}` |
| filetypes/package.json | learned_blend_at_fp_8 | 17794 | 11632 | 96.12% | 9 | 773.73 | 1349.78 | 2.972 | 97.99% | 97.62% | `{}` |
| filetypes/pdf | joint_or_at_fp_9 | 173237 | 13863 | 95.82% | 9 | 649.21 | 1132.61 | 2.972 | 97.86% | 96.12% | `{"filegroups/documents": 0.9070340394973755, "filetypes/pdf": 0.0473514199256897, "general": 0.9842879772186279}` |
| filetypes/python-bytecode† | specialist_primary_with_escape | 1868 | 31331 | 95.72% | 4 | 127.67 | 292.13 | 1.321 | 97.70% | 99.75% | `{"filetypes/python-bytecode": 0.9971392154693604, "general": 0.796545684337616}` |
| filetypes/elf | joint_or_at_fp_28 | 73273 | 136298 | 95.15% | 28 | 205.43 | 281.64 | 9.246 | 97.49% | 98.29% | `{"filegroups/native": 0.9988999366760254, "filetypes/elf": 0.9948902130126953, "general": 0.9874759316444397}` |
| filetypes/macho | joint_or_at_fp_4 | 2068 | 10693 | 93.23% | 4 | 374.08 | 855.82 | 1.321 | 96.40% | 98.87% | `{"filegroups/native": 0.9961297512054443, "filetypes/macho": 0.9179393649101257, "general": 0.9731881022453308}` |
| filetypes/xls | calibrate_inherited | 10502 | 366 | 93.23% | 0 | 0.00 | 8151.65 | 0.000 | 96.50% | 93.46% | `{"filegroups/documents": 0.7451304793357849, "general": 0.985923171043396}` |
| filetypes/ole | filetype_only_at_fp_3 | 1928 | 5360 | 92.69% | 4 | 746.27 | 1706.93 | 1.321 | 96.10% | 98.01% | `{"filetypes/ole": 0.37838542461395264}` |
| filetypes/java_class | joint_or_at_fp_52 | 1312 | 381385 | 91.92% | 52 | 136.35 | 171.78 | 17.172 | 93.85% | 99.96% | `{"filetypes/java_class": 0.3393796682357788}` |
| filetypes/doc | calibrate_inherited | 11033 | 34 | 90.30% | 0 | 0.00 | 84339.64 | 0.000 | 94.90% | 90.33% | `{"filegroups/documents": 0.7451304793357849, "general": 0.985923171043396}` |
| filetypes/tar | calibrate_inherited | 1119 | 408 | 88.65% | 0 | 0.00 | 7315.59 | 0.000 | 93.98% | 91.68% | `{"general": 0.985923171043396}` |
| filetypes/zst† | or_general_primary | 10381 | 16157 | 87.19% | 2 | 123.79 | 389.61 | 0.660 | 93.15% | 94.98% | `{"general": 0.9168552756309509}` |
| filetypes/ruby | joint_or_at_fp_3 | 73 | 24337 | 86.30% | 3 | 123.27 | 318.56 | 0.991 | 90.65% | 99.95% | `{"filegroups/scripts": 0.993080198764801, "filetypes/ruby": 0.999492883682251, "general": 0.8310150504112244}` |
| filetypes/shell | learned_blend_at_fp_11 | 6893 | 45536 | 85.65% | 11 | 241.57 | 399.82 | 3.633 | 92.19% | 98.09% | `{}` |
| filetypes/rar | calibrate_inherited | 6153 | 4 | 83.42% | 0 | 0.00 | 527129.20 | 0.000 | 90.96% | 83.43% | `{"general": 0.985923171043396}` |
| filetypes/7z | calibrate_inherited | 4305 | 78 | 82.11% | 0 | 0.00 | 37678.63 | 0.000 | 90.18% | 82.43% | `{"general": 0.985923171043396}` |
| filetypes/javascript | learned_blend_at_fp_76 | 84467 | 472874 | 79.24% | 75 | 158.60 | 192.19 | 24.767 | 88.38% | 96.84% | `{}` |
| filetypes/python | learned_blend_at_fp_44 | 17917 | 130234 | 79.22% | 39 | 299.46 | 391.12 | 12.879 | 88.30% | 97.46% | `{}` |
| filetypes/perl† | specialist_primary_with_escape | 224 | 31548 | 77.68% | 8 | 253.58 | 457.50 | 2.642 | 85.71% | 99.82% | `{"filegroups/scripts": 0.95821613073349, "filetypes/perl": 0.9942952990531921, "general": 0.7089720964431763}` |
| filetypes/pe | specialist_primary_with_escape | 901925 | 151968 | 76.36% | 35 | 230.31 | 305.34 | 11.558 | 86.59% | 79.77% | `{"filegroups/native": 0.9995715022087097, "filetypes/pe": 0.9995471835136414, "general": 0.9961766600608826}` |
| filetypes/php | joint_or_at_fp_16 | 3864 | 86590 | 73.52% | 16 | 184.78 | 280.63 | 5.284 | 84.54% | 98.85% | `{"filegroups/scripts": 0.9980263113975525, "filetypes/php": 0.9354349374771118, "general": 0.9812013506889343}` |
| filetypes/docx | joint_or_at_fp_0 | 1579 | 244 | 71.50% | 0 | 0.00 | 12202.53 | 0.000 | 83.38% | 75.32% | `{"filegroups/documents": 0.9494003057479858, "filetypes/docx": 0.4488392472267151, "general": 0.9870076775550842}` |
| filetypes/tar.bz2 | calibrate_inherited | 3 | 199 | 66.67% | 0 | 0.00 | 14941.19 | 0.000 | 80.00% | 99.50% | `{"general": 0.985923171043396}` |
| filetypes/tar.gz† | or_general_primary | 28003 | 12988 | 63.12% | 2 | 153.99 | 484.66 | 0.660 | 77.39% | 74.80% | `{"general": 0.9950588941574097}` |
| filetypes/objc† | or_general_primary | 5 | 18405 | 60.00% | 2 | 108.67 | 342.03 | 0.660 | 60.00% | 99.98% | `{"general": 0.008938553743064404}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 23576 | 42565 | 59.26% | 3 | 70.48 | 182.15 | 0.991 | 74.42% | 85.47% | `{}` |
