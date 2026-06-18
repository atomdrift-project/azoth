# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1750548459`
- Rows: 8128149 (2620313 malware, 5507836 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6241 | 524 | 97.90% | 0 | 0.00 | 570073.51 | 0.000 | 98.94% | 98.06% | `{"filetypes/rtf": 0.7381324172019958, "general": 0.02348741702735424}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2693 | 96.87% | 0 | 0.00 | 111179.60 | 0.000 | 98.41% | 97.51% | `{"filetypes/pkg-info": 0.30312973260879517, "general": 0.9942280054092407}` |
| filetypes/doc | calibrate_inherited | 34612 | 85 | 96.18% | 0 | 0.00 | 3463007.50 | 0.000 | 98.05% | 96.19% | `{"filegroups/documents": 0.1351274847984314, "general": 0.9992721973259767}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.36% | 0 | 0.00 | 14427.88 | 0.000 | 97.10% | 96.30% | `{"filegroups/documents": 0.874903678894043, "filetypes/xls": 0.9140002131462097}` |
| filetypes/elf | joint_or_at_fp_0 | 189137 | 196346 | 94.30% | 0 | 0.00 | 1525.73 | 0.000 | 97.07% | 97.20% | `{"filegroups/native": 0.9818642139434814, "filetypes/elf": 0.9931139349937439, "general": 0.9899529218673706}` |
| filetypes/gem | joint_or_at_fp_0 | 228 | 710 | 92.98% | 0 | 0.00 | 421045.23 | 0.000 | 96.36% | 98.29% | `{"filetypes/gem": 0.8543568849563599}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 96 | 278 | 91.67% | 0 | 0.00 | 1071816.21 | 0.000 | 95.65% | 97.86% | `{"filetypes/chrome-manifest": 0.8557124137878418}` |
| filetypes/package.json | joint_or_at_fp_0 | 19088 | 25105 | 90.79% | 0 | 0.00 | 11932.10 | 0.000 | 95.17% | 96.02% | `{"filegroups/config": 0.9989756345748901, "filetypes/package.json": 0.9978435039520264, "general": 0.9981568455696106}` |
| filetypes/tar | filetype_only_at_fp_0 | 31248 | 44312 | 88.93% | 0 | 0.00 | 6760.32 | 0.000 | 94.14% | 95.42% | `{"filetypes/tar": 0.9756215810775757}` |
| filetypes/macho | joint_or_at_fp_0 | 2657 | 13026 | 81.41% | 0 | 0.00 | 22995.45 | 0.000 | 89.75% | 96.85% | `{"filegroups/native": 0.8544701933860779, "filetypes/macho": 0.9803261756896973, "general": 0.9821993112564087}` |
| filetypes/docx | learned_blend_at_fp_0 | 5055 | 287 | 81.29% | 0 | 0.00 | 1038380.37 | 0.000 | 89.68% | 82.29% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3391 | 315459 | 79.00% | 0 | 0.00 | 949.64 | 0.000 | 88.27% | 99.78% | `{"filetypes/python-bytecode": 0.9992499947547913}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6600 | 78.92% | 0 | 0.00 | 45379.58 | 0.000 | 88.22% | 88.86% | `{"filegroups/documents": 0.4592741131782532, "filetypes/ole": 0.9985519051551819}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 207 | 78.74% | 0 | 0.00 | 1436791.86 | 0.000 | 88.10% | 79.49% | `{"filetypes/msi": 0.6349083185195923, "general": 0.9905281662940979}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5925 | 75.57% | 0 | 0.00 | 50548.10 | 0.000 | 86.09% | 99.47% | `{"filetypes/clojure": 0.3021196722984314}` |
| filetypes/npm | joint_or_at_fp_0 | 1286 | 240 | 75.12% | 0 | 0.00 | 1240463.81 | 0.000 | 85.79% | 79.03% | `{"filetypes/npm": 0.6450783610343933}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24578 | 73.81% | 0 | 0.00 | 12187.93 | 0.000 | 84.93% | 76.98% | `{"filegroups/documents": 0.9940502047538757, "filetypes/pdf": 0.9411760568618774, "general": 0.9859932065010071}` |
| filetypes/lnk | joint_or_at_fp_0 | 4601 | 1065 | 73.74% | 0 | 0.00 | 280894.17 | 0.000 | 84.89% | 78.68% | `{"filetypes/lnk": 0.9755615592002869, "general": 0.9985138773918152}` |
| filetypes/shell | joint_or_at_fp_0 | 15674 | 70445 | 66.63% | 0 | 0.00 | 4252.49 | 0.000 | 79.98% | 93.93% | `{"filegroups/scripts": 0.9875247478485107, "filetypes/shell": 0.9744633436203003, "general": 0.9610124826431274}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19079 | 59.80% | 0 | 0.00 | 15700.49 | 0.000 | 74.85% | 99.79% | `{"filegroups/scripts": 0.9553812742233276, "filetypes/lua": 0.5479393005371094}` |
| filetypes/perl | joint_or_at_fp_0 | 374 | 44704 | 59.63% | 0 | 0.00 | 6701.04 | 0.000 | 74.71% | 99.67% | `{"filegroups/scripts": 0.914364218711853, "filetypes/perl": 0.9869017004966736}` |
| filetypes/pe | joint_or_at_fp_0 | 1368600 | 167458 | 57.49% | 0 | 0.00 | 1788.93 | 0.000 | 73.01% | 62.12% | `{"filegroups/native": 0.9995348453521729, "filetypes/pe": 0.9965785145759583, "general": 0.9997629523277283}` |
| filetypes/powershell | joint_or_at_fp_0 | 5854 | 2573 | 53.64% | 0 | 0.00 | 116361.80 | 0.000 | 69.82% | 67.79% | `{"filegroups/scripts": 0.9921417236328125, "filetypes/powershell": 0.9980397820472717, "general": 0.9950742125511169}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32525 | 58945 | 51.77% | 0 | 0.00 | 5082.12 | 0.000 | 68.22% | 82.85% | `{"filegroups/source": 0.9843071699142456, "filetypes/kotlin": 0.8525990843772888, "general": 0.8872737288475037}` |
| filetypes/whl | joint_or_at_fp_0 | 836 | 4520 | 51.56% | 0 | 0.00 | 66255.30 | 0.000 | 68.03% | 92.44% | `{"filetypes/whl": 0.9819996356964111}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1950 | 822476 | 50.21% | 0 | 0.00 | 364.23 | 0.000 | 66.85% | 99.88% | `{}` |
| filetypes/jar | joint_or_at_fp_0 | 3681 | 6577 | 48.68% | 0 | 0.00 | 45538.24 | 0.000 | 65.49% | 81.59% | `{"filetypes/jar": 0.9506745934486389, "general": 0.9777916669845581}` |
| filetypes/python | joint_or_at_fp_0 | 23359 | 241601 | 44.21% | 0 | 0.00 | 1239.94 | 0.000 | 61.31% | 95.08% | `{"filegroups/scripts": 0.9960886240005493, "filetypes/python": 0.9996517896652222, "general": 0.9964639544487}` |
| filetypes/javascript | joint_or_at_fp_0 | 126993 | 693034 | 39.87% | 0 | 0.00 | 432.26 | 0.000 | 57.01% | 90.69% | `{"filegroups/scripts": 0.996956467628479, "filetypes/javascript": 0.999489426612854, "general": 0.9989144206047058}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6241 | 524 | 97.90% | 0 | 0.00 | 570073.51 | 0.000 | 98.94% | 98.06% | `{"filetypes/rtf": 0.7381324172019958, "general": 0.02348741702735424}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2693 | 96.87% | 0 | 0.00 | 111179.60 | 0.000 | 98.41% | 97.51% | `{"filetypes/pkg-info": 0.30312973260879517, "general": 0.9942280054092407}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.36% | 0 | 0.00 | 14427.88 | 0.000 | 97.10% | 96.30% | `{"filegroups/documents": 0.874903678894043, "filetypes/xls": 0.9140002131462097}` |
| filetypes/elf | joint_or_at_fp_0 | 189137 | 196346 | 94.30% | 0 | 0.00 | 1525.73 | 0.000 | 97.07% | 97.20% | `{"filegroups/native": 0.9818642139434814, "filetypes/elf": 0.9931139349937439, "general": 0.9899529218673706}` |
| filetypes/gem | joint_or_at_fp_0 | 228 | 710 | 92.98% | 0 | 0.00 | 421045.23 | 0.000 | 96.36% | 98.29% | `{"filetypes/gem": 0.8543568849563599}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 96 | 278 | 91.67% | 0 | 0.00 | 1071816.21 | 0.000 | 95.65% | 97.86% | `{"filetypes/chrome-manifest": 0.8557124137878418}` |
| filetypes/package.json | joint_or_at_fp_0 | 19088 | 25105 | 90.79% | 0 | 0.00 | 11932.10 | 0.000 | 95.17% | 96.02% | `{"filegroups/config": 0.9989756345748901, "filetypes/package.json": 0.9978435039520264, "general": 0.9981568455696106}` |
| filetypes/tar | filetype_only_at_fp_0 | 31248 | 44312 | 88.93% | 0 | 0.00 | 6760.32 | 0.000 | 94.14% | 95.42% | `{"filetypes/tar": 0.9756215810775757}` |
| filetypes/macho | joint_or_at_fp_0 | 2657 | 13026 | 81.41% | 0 | 0.00 | 22995.45 | 0.000 | 89.75% | 96.85% | `{"filegroups/native": 0.8544701933860779, "filetypes/macho": 0.9803261756896973, "general": 0.9821993112564087}` |
| filetypes/docx | learned_blend_at_fp_0 | 5055 | 287 | 81.29% | 0 | 0.00 | 1038380.37 | 0.000 | 89.68% | 82.29% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3391 | 315459 | 79.00% | 0 | 0.00 | 949.64 | 0.000 | 88.27% | 99.78% | `{"filetypes/python-bytecode": 0.9992499947547913}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6600 | 78.92% | 0 | 0.00 | 45379.58 | 0.000 | 88.22% | 88.86% | `{"filegroups/documents": 0.4592741131782532, "filetypes/ole": 0.9985519051551819}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 207 | 78.74% | 0 | 0.00 | 1436791.86 | 0.000 | 88.10% | 79.49% | `{"filetypes/msi": 0.6349083185195923, "general": 0.9905281662940979}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5925 | 75.57% | 0 | 0.00 | 50548.10 | 0.000 | 86.09% | 99.47% | `{"filetypes/clojure": 0.3021196722984314}` |
| filetypes/npm | joint_or_at_fp_0 | 1286 | 240 | 75.12% | 0 | 0.00 | 1240463.81 | 0.000 | 85.79% | 79.03% | `{"filetypes/npm": 0.6450783610343933}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24578 | 73.81% | 0 | 0.00 | 12187.93 | 0.000 | 84.93% | 76.98% | `{"filegroups/documents": 0.9940502047538757, "filetypes/pdf": 0.9411760568618774, "general": 0.9859932065010071}` |
| filetypes/lnk | joint_or_at_fp_0 | 4601 | 1065 | 73.74% | 0 | 0.00 | 280894.17 | 0.000 | 84.89% | 78.68% | `{"filetypes/lnk": 0.9755615592002869, "general": 0.9985138773918152}` |
| filetypes/shell | joint_or_at_fp_0 | 15674 | 70445 | 66.63% | 0 | 0.00 | 4252.49 | 0.000 | 79.98% | 93.93% | `{"filegroups/scripts": 0.9875247478485107, "filetypes/shell": 0.9744633436203003, "general": 0.9610124826431274}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19079 | 59.80% | 0 | 0.00 | 15700.49 | 0.000 | 74.85% | 99.79% | `{"filegroups/scripts": 0.9553812742233276, "filetypes/lua": 0.5479393005371094}` |
| filetypes/perl | joint_or_at_fp_0 | 374 | 44704 | 59.63% | 0 | 0.00 | 6701.04 | 0.000 | 74.71% | 99.67% | `{"filegroups/scripts": 0.914364218711853, "filetypes/perl": 0.9869017004966736}` |
| filetypes/pe | joint_or_at_fp_0 | 1368600 | 167458 | 57.49% | 0 | 0.00 | 1788.93 | 0.000 | 73.01% | 62.12% | `{"filegroups/native": 0.9995348453521729, "filetypes/pe": 0.9965785145759583, "general": 0.9997629523277283}` |
| filetypes/powershell | joint_or_at_fp_0 | 5854 | 2573 | 53.64% | 0 | 0.00 | 116361.80 | 0.000 | 69.82% | 67.79% | `{"filegroups/scripts": 0.9921417236328125, "filetypes/powershell": 0.9980397820472717, "general": 0.9950742125511169}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32525 | 58945 | 51.77% | 0 | 0.00 | 5082.12 | 0.000 | 68.22% | 82.85% | `{"filegroups/source": 0.9843071699142456, "filetypes/kotlin": 0.8525990843772888, "general": 0.8872737288475037}` |
| filetypes/whl | joint_or_at_fp_0 | 836 | 4520 | 51.56% | 0 | 0.00 | 66255.30 | 0.000 | 68.03% | 92.44% | `{"filetypes/whl": 0.9819996356964111}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1950 | 822476 | 50.21% | 0 | 0.00 | 364.23 | 0.000 | 66.85% | 99.88% | `{}` |
| filetypes/jar | joint_or_at_fp_0 | 3681 | 6577 | 48.68% | 0 | 0.00 | 45538.24 | 0.000 | 65.49% | 81.59% | `{"filetypes/jar": 0.9506745934486389, "general": 0.9777916669845581}` |
| filetypes/python | joint_or_at_fp_0 | 23359 | 241601 | 44.21% | 0 | 0.00 | 1239.94 | 0.000 | 61.31% | 95.08% | `{"filegroups/scripts": 0.9960886240005493, "filetypes/python": 0.9996517896652222, "general": 0.9964639544487}` |
| filetypes/zst | calibrate_inherited | 10382 | 22342 | 42.43% | 0 | 0.00 | 13407.62 | 0.000 | 59.58% | 81.74% | `{"general": 0.999056934992377}` |
| filetypes/7z | calibrate_inherited | 8865 | 82 | 41.69% | 0 | 0.00 | 3587403.17 | 0.000 | 58.85% | 42.23% | `{"general": 0.999056934992377}` |
