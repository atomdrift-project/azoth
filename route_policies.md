# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `4407144194`
- Rows: 18454063 (2682878 malware, 15771185 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | learned_blend_at_fp_0 | 191 | 305 | 97.91% | 0 | 0.00 | 977399.40 | 0.000 | 98.94% | 99.19% | `{}` |
| filetypes/cab | joint_or_at_fp_0 | 880 | 84 | 93.64% | 0 | 0.00 | 3503503.06 | 0.000 | 96.71% | 94.19% | `{"filetypes/cab": 0.9096273183822632, "general": 0.8205718994140625}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 529 | 92.73% | 0 | 0.00 | 564700.54 | 0.000 | 96.23% | 99.32% | `{"general": 0.9400256276130676}` |
| filetypes/elf | joint_or_at_fp_0 | 196883 | 865068 | 88.34% | 0 | 0.00 | 346.30 | 0.000 | 93.81% | 97.84% | `{"filegroups/native": 0.9945506453514099, "filetypes/elf": 0.9998646378517151, "general": 0.9938169717788696}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 72 | 85.66% | 0 | 0.00 | 4075368.62 | 0.000 | 92.27% | 88.92% | `{"filetypes/chm": 0.8833631873130798, "general": 0.7627530694007874}` |
| filetypes/7z | joint_or_at_fp_0 | 9053 | 348 | 78.80% | 0 | 0.00 | 857147.97 | 0.000 | 88.14% | 79.59% | `{"filetypes/7z": 0.9702539443969727, "general": 0.9850218296051025}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 330 | 68.25% | 0 | 0.00 | 903689.62 | 0.000 | 81.13% | 94.91% | `{"filetypes/dmg": 0.8864505887031555, "general": 0.9911852478981018}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87711 | 31841 | 63.81% | 0 | 0.00 | 9407.97 | 0.000 | 77.91% | 73.45% | `{"filetypes/ole_doc": 0.9990655183792114, "general": 0.9979771971702576}` |
| filetypes/tar | joint_or_at_fp_0 | 34289 | 83358 | 62.51% | 0 | 0.00 | 3593.75 | 0.000 | 76.93% | 89.07% | `{"filetypes/tar": 0.9996609687805176, "general": 0.9956899881362915}` |
| filetypes/shell | joint_or_at_fp_0 | 18805 | 164844 | 62.08% | 0 | 0.00 | 1817.30 | 0.000 | 76.61% | 96.12% | `{"filegroups/scripts": 0.9991885423660278, "filetypes/shell": 0.9971010088920593, "general": 0.9949197173118591}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 34770 | 59.03% | 0 | 0.00 | 8615.48 | 0.000 | 74.24% | 96.89% | `{"filegroups/native": 0.9755722880363464, "filetypes/macho": 0.9910556674003601}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 972 | 56.72% | 0 | 0.00 | 307728.45 | 0.000 | 72.38% | 62.54% | `{"filegroups/documents": 0.9998050332069397, "filetypes/rtf": 0.9935161471366882, "general": 0.9992449283599854}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27784 | 56.60% | 0 | 0.00 | 10781.64 | 0.000 | 72.29% | 99.84% | `{"filetypes/lua": 0.5699777007102966}` |
| filetypes/package.json | joint_or_at_fp_0 | 22369 | 71685 | 54.50% | 0 | 0.00 | 4178.94 | 0.000 | 70.55% | 89.18% | `{"filegroups/config": 0.999984622001648, "filetypes/package.json": 0.9998195171356201, "general": 0.9995824694633484}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 83965 | 53.40% | 0 | 0.00 | 3567.77 | 0.000 | 69.62% | 87.04% | `{"filegroups/source": 0.9870133399963379, "filetypes/kotlin": 0.9359257817268372, "general": 0.9959946870803833}` |
| filetypes/npm | joint_or_at_fp_0 | 17393 | 113075 | 53.38% | 0 | 0.00 | 2649.30 | 0.000 | 69.60% | 93.78% | `{"filetypes/npm": 0.9988133907318115, "general": 0.9994874596595764}` |
| filetypes/swift | learned_blend_at_fp_0 | 69 | 44639 | 52.17% | 0 | 0.00 | 6710.79 | 0.000 | 68.57% | 99.93% | `{}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 987 | 2101 | 50.05% | 0 | 0.00 | 142484.41 | 0.000 | 66.71% | 84.03% | `{"filetypes/python_sdist": 0.9919363856315613, "general": 0.9766804575920105}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 1080842 | 45.79% | 0 | 0.00 | 277.17 | 0.000 | 62.82% | 99.82% | `{"filetypes/python_bytecode": 0.9999298453330994, "general": 0.9861279129981995}` |
| filetypes/gem | joint_or_at_fp_0 | 2107 | 58410 | 45.14% | 0 | 0.00 | 5128.67 | 0.000 | 62.20% | 98.09% | `{"filetypes/gem": 0.9976159930229187, "general": 0.9806156754493713}` |
| filetypes/powershell | joint_or_at_fp_0 | 6050 | 5770 | 44.84% | 0 | 0.00 | 51905.63 | 0.000 | 61.92% | 71.77% | `{"filegroups/scripts": 0.9986388087272644, "filetypes/powershell": 0.9955183267593384, "general": 0.9984623193740845}` |
| filetypes/python | joint_or_at_fp_0 | 23645 | 664379 | 41.43% | 0 | 0.00 | 450.91 | 0.000 | 58.59% | 97.99% | `{"filegroups/scripts": 0.9988871812820435, "filetypes/python": 0.9974990487098694, "general": 0.995307207107544}` |
| filetypes/javascript | joint_or_at_fp_0 | 145000 | 1726408 | 40.34% | 0 | 0.00 | 173.52 | 0.000 | 57.49% | 95.38% | `{"filegroups/scripts": 0.999187707901001, "filetypes/javascript": 0.9991639256477356, "general": 0.996367335319519}` |
| filetypes/pe | joint_or_at_fp_0 | 1379547 | 254413 | 39.42% | 0 | 0.00 | 1177.50 | 0.000 | 56.55% | 48.85% | `{"filegroups/native": 0.9997187256813049, "filetypes/pe": 0.9996470212936401, "general": 0.9996734261512756}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 195959 | 37.90% | 0 | 0.00 | 1528.74 | 0.000 | 54.97% | 99.90% | `{"filegroups/documents": 0.9969425797462463, "general": 0.9790993928909302}` |
| filetypes/jar | joint_or_at_fp_0 | 3944 | 35248 | 34.28% | 0 | 0.00 | 8498.65 | 0.000 | 51.06% | 93.39% | `{"filetypes/jar": 0.9973599910736084, "general": 0.972213625907898}` |
| filetypes/lnk | joint_or_at_fp_0 | 4698 | 1155 | 33.65% | 0 | 0.00 | 259034.68 | 0.000 | 50.36% | 46.75% | `{"filetypes/lnk": 0.9936846494674683, "general": 0.9986652135848999}` |
| filetypes/zip | joint_or_at_fp_0 | 109061 | 57756 | 31.91% | 0 | 0.00 | 5186.74 | 0.000 | 48.38% | 55.48% | `{"filetypes/zip": 0.9989535212516785, "general": 0.9972429275512695}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2903 | 251 | 30.55% | 0 | 0.00 | 1186424.65 | 0.000 | 46.81% | 36.08% | `{"filetypes/apk_android": 0.9066407084465027, "general": 0.49728381633758545}` |
| filetypes/rar | calibrate_inherited | 22206 | 43 | 30.53% | 0 | 0.00 | 6729675.34 | 0.000 | 46.78% | 30.66% | `{"general": 0.9994145425523139}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | learned_blend_at_fp_0 | 191 | 305 | 97.91% | 0 | 0.00 | 977399.40 | 0.000 | 98.94% | 99.19% | `{}` |
| filetypes/cab | joint_or_at_fp_0 | 880 | 84 | 93.64% | 0 | 0.00 | 3503503.06 | 0.000 | 96.71% | 94.19% | `{"filetypes/cab": 0.9096273183822632, "general": 0.8205718994140625}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 529 | 92.73% | 0 | 0.00 | 564700.54 | 0.000 | 96.23% | 99.32% | `{"general": 0.9400256276130676}` |
| filetypes/elf | joint_or_at_fp_0 | 196883 | 865068 | 88.34% | 0 | 0.00 | 346.30 | 0.000 | 93.81% | 97.84% | `{"filegroups/native": 0.9945506453514099, "filetypes/elf": 0.9998646378517151, "general": 0.9938169717788696}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 72 | 85.66% | 0 | 0.00 | 4075368.62 | 0.000 | 92.27% | 88.92% | `{"filetypes/chm": 0.8833631873130798, "general": 0.7627530694007874}` |
| filetypes/7z | joint_or_at_fp_0 | 9053 | 348 | 78.80% | 0 | 0.00 | 857147.97 | 0.000 | 88.14% | 79.59% | `{"filetypes/7z": 0.9702539443969727, "general": 0.9850218296051025}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 330 | 68.25% | 0 | 0.00 | 903689.62 | 0.000 | 81.13% | 94.91% | `{"filetypes/dmg": 0.8864505887031555, "general": 0.9911852478981018}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87711 | 31841 | 63.81% | 0 | 0.00 | 9407.97 | 0.000 | 77.91% | 73.45% | `{"filetypes/ole_doc": 0.9990655183792114, "general": 0.9979771971702576}` |
| filetypes/tar | joint_or_at_fp_0 | 34289 | 83358 | 62.51% | 0 | 0.00 | 3593.75 | 0.000 | 76.93% | 89.07% | `{"filetypes/tar": 0.9996609687805176, "general": 0.9956899881362915}` |
| filetypes/shell | joint_or_at_fp_0 | 18805 | 164844 | 62.08% | 0 | 0.00 | 1817.30 | 0.000 | 76.61% | 96.12% | `{"filegroups/scripts": 0.9991885423660278, "filetypes/shell": 0.9971010088920593, "general": 0.9949197173118591}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 34770 | 59.03% | 0 | 0.00 | 8615.48 | 0.000 | 74.24% | 96.89% | `{"filegroups/native": 0.9755722880363464, "filetypes/macho": 0.9910556674003601}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 972 | 56.72% | 0 | 0.00 | 307728.45 | 0.000 | 72.38% | 62.54% | `{"filegroups/documents": 0.9998050332069397, "filetypes/rtf": 0.9935161471366882, "general": 0.9992449283599854}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27784 | 56.60% | 0 | 0.00 | 10781.64 | 0.000 | 72.29% | 99.84% | `{"filetypes/lua": 0.5699777007102966}` |
| filetypes/package.json | joint_or_at_fp_0 | 22369 | 71685 | 54.50% | 0 | 0.00 | 4178.94 | 0.000 | 70.55% | 89.18% | `{"filegroups/config": 0.999984622001648, "filetypes/package.json": 0.9998195171356201, "general": 0.9995824694633484}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 83965 | 53.40% | 0 | 0.00 | 3567.77 | 0.000 | 69.62% | 87.04% | `{"filegroups/source": 0.9870133399963379, "filetypes/kotlin": 0.9359257817268372, "general": 0.9959946870803833}` |
| filetypes/npm | joint_or_at_fp_0 | 17393 | 113075 | 53.38% | 0 | 0.00 | 2649.30 | 0.000 | 69.60% | 93.78% | `{"filetypes/npm": 0.9988133907318115, "general": 0.9994874596595764}` |
| filetypes/swift | learned_blend_at_fp_0 | 69 | 44639 | 52.17% | 0 | 0.00 | 6710.79 | 0.000 | 68.57% | 99.93% | `{}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 987 | 2101 | 50.05% | 0 | 0.00 | 142484.41 | 0.000 | 66.71% | 84.03% | `{"filetypes/python_sdist": 0.9919363856315613, "general": 0.9766804575920105}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 1080842 | 45.79% | 0 | 0.00 | 277.17 | 0.000 | 62.82% | 99.82% | `{"filetypes/python_bytecode": 0.9999298453330994, "general": 0.9861279129981995}` |
| filetypes/gem | joint_or_at_fp_0 | 2107 | 58410 | 45.14% | 0 | 0.00 | 5128.67 | 0.000 | 62.20% | 98.09% | `{"filetypes/gem": 0.9976159930229187, "general": 0.9806156754493713}` |
| filetypes/powershell | joint_or_at_fp_0 | 6050 | 5770 | 44.84% | 0 | 0.00 | 51905.63 | 0.000 | 61.92% | 71.77% | `{"filegroups/scripts": 0.9986388087272644, "filetypes/powershell": 0.9955183267593384, "general": 0.9984623193740845}` |
| filetypes/python | joint_or_at_fp_0 | 23645 | 664379 | 41.43% | 0 | 0.00 | 450.91 | 0.000 | 58.59% | 97.99% | `{"filegroups/scripts": 0.9988871812820435, "filetypes/python": 0.9974990487098694, "general": 0.995307207107544}` |
| filetypes/javascript | joint_or_at_fp_0 | 145000 | 1726408 | 40.34% | 0 | 0.00 | 173.52 | 0.000 | 57.49% | 95.38% | `{"filegroups/scripts": 0.999187707901001, "filetypes/javascript": 0.9991639256477356, "general": 0.996367335319519}` |
| filetypes/pe | joint_or_at_fp_0 | 1379547 | 254413 | 39.42% | 0 | 0.00 | 1177.50 | 0.000 | 56.55% | 48.85% | `{"filegroups/native": 0.9997187256813049, "filetypes/pe": 0.9996470212936401, "general": 0.9996734261512756}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 195959 | 37.90% | 0 | 0.00 | 1528.74 | 0.000 | 54.97% | 99.90% | `{"filegroups/documents": 0.9969425797462463, "general": 0.9790993928909302}` |
| filetypes/rar | calibrate_inherited | 22206 | 43 | 36.42% | 0 | 0.00 | 6729675.34 | 0.000 | 53.39% | 36.54% | `{"general": 0.9991980337910535}` |
| filetypes/jar | joint_or_at_fp_0 | 3944 | 35248 | 34.28% | 0 | 0.00 | 8498.65 | 0.000 | 51.06% | 93.39% | `{"filetypes/jar": 0.9973599910736084, "general": 0.972213625907898}` |
| filetypes/lnk | joint_or_at_fp_0 | 4698 | 1155 | 33.65% | 0 | 0.00 | 259034.68 | 0.000 | 50.36% | 46.75% | `{"filetypes/lnk": 0.9936846494674683, "general": 0.9986652135848999}` |
| filetypes/zip | joint_or_at_fp_0 | 109061 | 57756 | 31.91% | 0 | 0.00 | 5186.74 | 0.000 | 48.38% | 55.48% | `{"filetypes/zip": 0.9989535212516785, "general": 0.9972429275512695}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2903 | 251 | 30.55% | 0 | 0.00 | 1186424.65 | 0.000 | 46.81% | 36.08% | `{"filetypes/apk_android": 0.9066407084465027, "general": 0.49728381633758545}` |
