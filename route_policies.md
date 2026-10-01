# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `5613821836`
- Rows: 19975007 (2965083 malware, 17009924 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 130 | 268 | 99.23% | 0 | 0.00 | 1111586.26 | 0.000 | 99.61% | 99.75% | `{"filegroups/media": 0.8131539821624756, "filetypes/bmp": 0.9034414887428284}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 563 | 92.86% | 0 | 0.00 | 530688.49 | 0.000 | 96.30% | 99.35% | `{"filetypes/applescript": 0.6951413750648499, "general": 0.9860565066337585}` |
| filetypes/mp3 | learned_blend_at_fp_3 | 196 | 344 | 91.84% | 0 | 0.00 | 867071.47 | 0.000 | 95.74% | 97.04% | `{}` |
| filetypes/asar | learned_blend_at_fp_0 | 199 | 364 | 82.41% | 0 | 0.00 | 819625.97 | 0.000 | 90.36% | 93.78% | `{}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 96 | 82.35% | 0 | 0.00 | 3072367.68 | 0.000 | 90.32% | 84.11% | `{"filetypes/cab": 0.9307347536087036, "general": 0.7709099054336548}` |
| filetypes/elf | joint_or_at_fp_0 | 197676 | 896866 | 81.33% | 0 | 0.00 | 334.02 | 0.000 | 89.70% | 96.63% | `{"filegroups/native": 0.9985135793685913, "filetypes/elf": 0.99980229139328, "general": 0.9979054927825928}` |
| filetypes/dos_com | learned_blend_at_fp_0 | 6038 | 161 | 76.35% | 0 | 0.00 | 1843499.06 | 0.000 | 86.59% | 76.96% | `{}` |
| filetypes/html | joint_or_at_fp_0 | 355 | 276474 | 75.77% | 0 | 0.00 | 1083.54 | 0.000 | 86.22% | 99.97% | `{"filegroups/documents": 0.8878531455993652, "general": 0.9789305925369263}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3338 | 8509 | 72.65% | 0 | 0.00 | 35200.43 | 0.000 | 84.16% | 92.29% | `{"filetypes/python_sdist": 0.9991171360015869, "general": 0.9431789517402649}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 194613 | 70.82% | 0 | 0.00 | 1539.32 | 0.000 | 82.92% | 99.96% | `{"filegroups/scripts": 0.9586095809936523, "filetypes/ruby": 0.9896800518035889, "general": 0.8961415886878967}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 398 | 69.80% | 0 | 0.00 | 749870.88 | 0.000 | 82.21% | 71.11% | `{"filetypes/7z": 0.9957196712493896, "general": 0.9939015507698059}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 629 | 64.02% | 0 | 0.00 | 475136.68 | 0.000 | 78.06% | 89.36% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 60.27% | 0 | 0.00 | 292981.55 | 0.000 | 75.21% | 65.96% | `{"filegroups/documents": 0.999670684337616, "filetypes/rtf": 0.9928717613220215, "general": 0.9986768960952759}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 267 | 58.62% | 0 | 0.00 | 1115726.19 | 0.000 | 73.91% | 89.83% | `{"filetypes/dex": 0.8515744209289551, "general": 0.9369150996208191}` |
| filetypes/shell | joint_or_at_fp_0 | 18944 | 164170 | 56.92% | 0 | 0.00 | 1824.76 | 0.000 | 72.54% | 95.54% | `{"filegroups/scripts": 0.995939314365387, "filetypes/shell": 0.9970433712005615, "general": 0.9917930364608765}` |
| filetypes/tar | joint_or_at_fp_0 | 24273 | 91026 | 55.96% | 0 | 0.00 | 3291.02 | 0.000 | 71.76% | 90.73% | `{"filetypes/tar": 0.9986486434936523, "general": 0.9964206218719482}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44775 | 55.93% | 0 | 0.00 | 6690.41 | 0.000 | 71.74% | 99.94% | `{"general": 0.08708036690950394}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 54.15% | 0 | 0.00 | 2980667.38 | 0.000 | 70.25% | 67.99% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9924805760383606}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3446 | 1200154 | 50.20% | 0 | 0.00 | 249.61 | 0.000 | 66.85% | 99.86% | `{"filetypes/python_bytecode": 0.9999611973762512, "general": 0.982094943523407}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 49.58% | 0 | 0.00 | 255936.45 | 0.000 | 66.29% | 59.57% | `{"filetypes/lnk": 0.9949637651443481, "general": 0.996843695640564}` |
| filetypes/perl | joint_or_at_fp_0 | 436 | 80338 | 48.39% | 0 | 0.00 | 3728.84 | 0.000 | 65.22% | 99.72% | `{"filegroups/scripts": 0.9822450280189514, "filetypes/perl": 0.994028627872467}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28630 | 48.28% | 0 | 0.00 | 10463.07 | 0.000 | 65.12% | 99.84% | `{"filegroups/scripts": 0.9903539419174194, "filetypes/lua": 0.9960379600524902, "general": 0.9883124828338623}` |
| filetypes/xpi | joint_or_at_fp_0 | 63 | 3913 | 47.62% | 0 | 0.00 | 76529.15 | 0.000 | 64.52% | 99.17% | `{"filetypes/xpi": 0.9696596264839172, "general": 0.9048258066177368}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27344 | 84230 | 47.52% | 0 | 0.00 | 3556.55 | 0.000 | 64.43% | 87.14% | `{"filegroups/source": 0.9874275326728821, "filetypes/kotlin": 0.9528374075889587, "general": 0.9966769218444824}` |
| filetypes/python | joint_or_at_fp_0 | 23542 | 676557 | 46.01% | 0 | 0.00 | 442.79 | 0.000 | 63.02% | 98.18% | `{"filegroups/scripts": 0.9966300129890442, "filetypes/python": 0.9974817037582397, "general": 0.9930309653282166}` |
| filetypes/npm | joint_or_at_fp_0 | 24446 | 200862 | 37.75% | 0 | 0.00 | 1491.43 | 0.000 | 54.81% | 93.25% | `{"filetypes/npm": 0.999963641166687, "general": 0.9995905756950378}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 36.88% | 0 | 0.00 | 5495548.85 | 0.000 | 53.88% | 37.03% | `{"general": 0.9993423300584818}` |
| filetypes/zip | joint_or_at_fp_0 | 107317 | 96776 | 33.79% | 0 | 0.00 | 3095.48 | 0.000 | 50.52% | 65.19% | `{"filetypes/zip": 0.9995381236076355, "general": 0.9984875917434692}` |
| filetypes/powershell | joint_or_at_fp_0 | 5951 | 6154 | 33.00% | 0 | 0.00 | 48667.59 | 0.000 | 49.63% | 67.06% | `{"filegroups/scripts": 0.9979239106178284, "filetypes/powershell": 0.9979373812675476, "general": 0.9984102249145508}` |
| filetypes/pdf | joint_or_at_fp_0 | 178761 | 29855 | 31.92% | 0 | 0.00 | 10033.77 | 0.000 | 48.40% | 41.66% | `{"filegroups/documents": 0.9976078867912292, "filetypes/pdf": 0.9793338179588318, "general": 0.9932764768600464}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 130 | 268 | 99.23% | 0 | 0.00 | 1111586.26 | 0.000 | 99.61% | 99.75% | `{"filegroups/media": 0.8131539821624756, "filetypes/bmp": 0.9034414887428284}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 563 | 92.86% | 0 | 0.00 | 530688.49 | 0.000 | 96.30% | 99.35% | `{"filetypes/applescript": 0.6951413750648499, "general": 0.9860565066337585}` |
| filetypes/mp3 | learned_blend_at_fp_3 | 196 | 344 | 91.84% | 0 | 0.00 | 867071.47 | 0.000 | 95.74% | 97.04% | `{}` |
| filetypes/asar | learned_blend_at_fp_0 | 199 | 364 | 82.41% | 0 | 0.00 | 819625.97 | 0.000 | 90.36% | 93.78% | `{}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 96 | 82.35% | 0 | 0.00 | 3072367.68 | 0.000 | 90.32% | 84.11% | `{"filetypes/cab": 0.9307347536087036, "general": 0.7709099054336548}` |
| filetypes/elf | joint_or_at_fp_0 | 197676 | 896866 | 81.33% | 0 | 0.00 | 334.02 | 0.000 | 89.70% | 96.63% | `{"filegroups/native": 0.9985135793685913, "filetypes/elf": 0.99980229139328, "general": 0.9979054927825928}` |
| filetypes/dos_com | learned_blend_at_fp_0 | 6038 | 161 | 76.35% | 0 | 0.00 | 1843499.06 | 0.000 | 86.59% | 76.96% | `{}` |
| filetypes/html | joint_or_at_fp_0 | 355 | 276474 | 75.77% | 0 | 0.00 | 1083.54 | 0.000 | 86.22% | 99.97% | `{"filegroups/documents": 0.8878531455993652, "general": 0.9789305925369263}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3338 | 8509 | 72.65% | 0 | 0.00 | 35200.43 | 0.000 | 84.16% | 92.29% | `{"filetypes/python_sdist": 0.9991171360015869, "general": 0.9431789517402649}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 194613 | 70.82% | 0 | 0.00 | 1539.32 | 0.000 | 82.92% | 99.96% | `{"filegroups/scripts": 0.9586095809936523, "filetypes/ruby": 0.9896800518035889, "general": 0.8961415886878967}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 398 | 69.80% | 0 | 0.00 | 749870.88 | 0.000 | 82.21% | 71.11% | `{"filetypes/7z": 0.9957196712493896, "general": 0.9939015507698059}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 629 | 64.02% | 0 | 0.00 | 475136.68 | 0.000 | 78.06% | 89.36% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 60.27% | 0 | 0.00 | 292981.55 | 0.000 | 75.21% | 65.96% | `{"filegroups/documents": 0.999670684337616, "filetypes/rtf": 0.9928717613220215, "general": 0.9986768960952759}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 267 | 58.62% | 0 | 0.00 | 1115726.19 | 0.000 | 73.91% | 89.83% | `{"filetypes/dex": 0.8515744209289551, "general": 0.9369150996208191}` |
| filetypes/shell | joint_or_at_fp_0 | 18944 | 164170 | 56.92% | 0 | 0.00 | 1824.76 | 0.000 | 72.54% | 95.54% | `{"filegroups/scripts": 0.995939314365387, "filetypes/shell": 0.9970433712005615, "general": 0.9917930364608765}` |
| filetypes/tar | joint_or_at_fp_0 | 24273 | 91026 | 55.96% | 0 | 0.00 | 3291.02 | 0.000 | 71.76% | 90.73% | `{"filetypes/tar": 0.9986486434936523, "general": 0.9964206218719482}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44775 | 55.93% | 0 | 0.00 | 6690.41 | 0.000 | 71.74% | 99.94% | `{"general": 0.08708036690950394}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 54.15% | 0 | 0.00 | 2980667.38 | 0.000 | 70.25% | 67.99% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9924805760383606}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3446 | 1200154 | 50.20% | 0 | 0.00 | 249.61 | 0.000 | 66.85% | 99.86% | `{"filetypes/python_bytecode": 0.9999611973762512, "general": 0.982094943523407}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 49.58% | 0 | 0.00 | 255936.45 | 0.000 | 66.29% | 59.57% | `{"filetypes/lnk": 0.9949637651443481, "general": 0.996843695640564}` |
| filetypes/perl | joint_or_at_fp_0 | 436 | 80338 | 48.39% | 0 | 0.00 | 3728.84 | 0.000 | 65.22% | 99.72% | `{"filegroups/scripts": 0.9822450280189514, "filetypes/perl": 0.994028627872467}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28630 | 48.28% | 0 | 0.00 | 10463.07 | 0.000 | 65.12% | 99.84% | `{"filegroups/scripts": 0.9903539419174194, "filetypes/lua": 0.9960379600524902, "general": 0.9883124828338623}` |
| filetypes/xpi | joint_or_at_fp_0 | 63 | 3913 | 47.62% | 0 | 0.00 | 76529.15 | 0.000 | 64.52% | 99.17% | `{"filetypes/xpi": 0.9696596264839172, "general": 0.9048258066177368}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27344 | 84230 | 47.52% | 0 | 0.00 | 3556.55 | 0.000 | 64.43% | 87.14% | `{"filegroups/source": 0.9874275326728821, "filetypes/kotlin": 0.9528374075889587, "general": 0.9966769218444824}` |
| filetypes/python | joint_or_at_fp_0 | 23542 | 676557 | 46.01% | 0 | 0.00 | 442.79 | 0.000 | 63.02% | 98.18% | `{"filegroups/scripts": 0.9966300129890442, "filetypes/python": 0.9974817037582397, "general": 0.9930309653282166}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 41.30% | 0 | 0.00 | 5495548.85 | 0.000 | 58.45% | 41.44% | `{"general": 0.999160497496093}` |
| filetypes/npm | joint_or_at_fp_0 | 24446 | 200862 | 37.75% | 0 | 0.00 | 1491.43 | 0.000 | 54.81% | 93.25% | `{"filetypes/npm": 0.999963641166687, "general": 0.9995905756950378}` |
| filetypes/zip | joint_or_at_fp_0 | 107317 | 96776 | 33.79% | 0 | 0.00 | 3095.48 | 0.000 | 50.52% | 65.19% | `{"filetypes/zip": 0.9995381236076355, "general": 0.9984875917434692}` |
| filetypes/powershell | joint_or_at_fp_0 | 5951 | 6154 | 33.00% | 0 | 0.00 | 48667.59 | 0.000 | 49.63% | 67.06% | `{"filegroups/scripts": 0.9979239106178284, "filetypes/powershell": 0.9979373812675476, "general": 0.9984102249145508}` |
| filetypes/pdf | joint_or_at_fp_0 | 178761 | 29855 | 31.92% | 0 | 0.00 | 10033.77 | 0.000 | 48.40% | 41.66% | `{"filegroups/documents": 0.9976078867912292, "filetypes/pdf": 0.9793338179588318, "general": 0.9932764768600464}` |
