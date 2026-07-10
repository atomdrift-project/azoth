# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2203636289`
- Rows: 13597415 (2653623 malware, 10943792 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 828 | 97.89% | 0 | 0.00 | 361149.69 | 0.000 | 98.93% | 98.14% | `{"filetypes/rtf": 0.4016873240470886, "general": 0.8443288207054138}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.47% | 0 | 0.00 | 18783.79 | 0.000 | 98.20% | 99.94% | `{"general": 0.08868321031332016}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 459 | 93.10% | 0 | 0.00 | 650539.75 | 0.000 | 96.43% | 99.23% | `{"filetypes/applescript": 0.7369557619094849}` |
| filetypes/gem | joint_or_at_fp_0 | 881 | 2405 | 92.05% | 0 | 0.00 | 124485.13 | 0.000 | 95.86% | 97.87% | `{"filetypes/gem": 0.9809819459915161, "general": 0.8593581318855286}` |
| filetypes/asar | joint_or_at_fp_0 | 181 | 80 | 90.61% | 0 | 0.00 | 3675419.78 | 0.000 | 95.07% | 93.49% | `{"filetypes/asar": 0.7991325855255127, "general": 0.7868700623512268}` |
| filetypes/elf | joint_or_at_fp_0 | 191368 | 447361 | 88.53% | 0 | 0.00 | 669.64 | 0.000 | 93.92% | 96.56% | `{"filegroups/native": 0.9904534816741943, "filetypes/elf": 0.9998020529747009, "general": 0.9841664433479309}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10622 | 12579 | 74.04% | 0 | 0.00 | 23812.51 | 0.000 | 85.08% | 88.11% | `{"filetypes/pkg_info": 0.9957355260848999, "general": 0.9966630935668945}` |
| filetypes/macho | joint_or_at_fp_0 | 2810 | 21749 | 62.24% | 0 | 0.00 | 13773.17 | 0.000 | 76.73% | 95.68% | `{"filegroups/native": 0.9591631889343262, "filetypes/macho": 0.9872281551361084, "general": 0.9444067478179932}` |
| filetypes/tar | joint_or_at_fp_0 | 33973 | 62637 | 61.68% | 0 | 0.00 | 4782.57 | 0.000 | 76.30% | 86.52% | `{"filetypes/tar": 0.9996676445007324, "general": 0.9948330521583557}` |
| filetypes/package.json | joint_or_at_fp_0 | 20310 | 47568 | 61.62% | 0 | 0.00 | 6297.59 | 0.000 | 76.26% | 88.52% | `{"filegroups/config": 0.9999880790710449, "filetypes/package.json": 0.9997749924659729, "general": 0.998114824295044}` |
| filetypes/swift | joint_or_at_fp_0 | 65 | 38621 | 58.46% | 0 | 0.00 | 7756.44 | 0.000 | 73.79% | 99.93% | `{"filegroups/source": 0.02822774648666382}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87519 | 30735 | 57.36% | 0 | 0.00 | 9746.50 | 0.000 | 72.90% | 68.44% | `{"filetypes/ole_doc": 0.9984715580940247, "general": 0.9995750188827515}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25866 | 54.72% | 0 | 0.00 | 11581.07 | 0.000 | 70.73% | 99.82% | `{"filegroups/scripts": 0.9874284863471985, "filetypes/lua": 0.9004098176956177}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32383 | 73231 | 53.45% | 0 | 0.00 | 4090.71 | 0.000 | 69.67% | 85.73% | `{"filegroups/source": 0.9796195030212402, "filetypes/kotlin": 0.9959867596626282, "general": 0.9734386801719666}` |
| filetypes/perl | learned_blend_at_fp_0 | 400 | 67791 | 49.75% | 0 | 0.00 | 4418.97 | 0.000 | 66.44% | 99.71% | `{}` |
| filetypes/shell | joint_or_at_fp_0 | 17932 | 131867 | 49.16% | 0 | 0.00 | 2271.76 | 0.000 | 65.91% | 93.91% | `{"filegroups/scripts": 0.9967226386070251, "filetypes/shell": 0.99748694896698, "general": 0.9918321371078491}` |
| filetypes/python | learned_blend_at_fp_0 | 23096 | 540541 | 48.32% | 0 | 0.00 | 554.21 | 0.000 | 65.16% | 97.88% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4626 | 1070 | 47.02% | 0 | 0.00 | 279583.41 | 0.000 | 63.96% | 56.97% | `{"filetypes/lnk": 0.991326630115509, "general": 0.998199999332428}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8419 | 45.45% | 0 | 0.00 | 35576.66 | 0.000 | 62.50% | 99.30% | `{"filetypes/clojure": 0.9952961802482605, "general": 0.020179837942123413}` |
| filetypes/jar | joint_or_at_fp_0 | 3843 | 18077 | 42.67% | 0 | 0.00 | 16570.69 | 0.000 | 59.82% | 89.95% | `{"filetypes/jar": 0.9905960559844971, "general": 0.9949970245361328}` |
| filetypes/powershell | joint_or_at_fp_0 | 5976 | 4553 | 40.80% | 0 | 0.00 | 65775.25 | 0.000 | 57.95% | 66.40% | `{"filegroups/scripts": 0.9978869557380676, "filetypes/powershell": 0.9949578642845154, "general": 0.9890596270561218}` |
| filetypes/npm | joint_or_at_fp_0 | 4130 | 4964 | 40.77% | 0 | 0.00 | 60330.95 | 0.000 | 57.93% | 73.10% | `{"filetypes/npm": 0.9957634210586548, "general": 0.9975879788398743}` |
| filetypes/whl | joint_or_at_fp_0 | 3476 | 5963 | 40.22% | 0 | 0.00 | 50226.06 | 0.000 | 57.37% | 77.98% | `{"filetypes/whl": 0.9926167130470276, "general": 0.9642204642295837}` |
| filetypes/javascript | joint_or_at_fp_0 | 139646 | 1266021 | 38.21% | 0 | 0.00 | 236.63 | 0.000 | 55.29% | 93.86% | `{"filegroups/scripts": 0.9983587861061096, "filetypes/javascript": 0.9986760020256042, "general": 0.9988428354263306}` |
| filetypes/crate | joint_or_at_fp_0 | 90 | 5126 | 37.78% | 0 | 0.00 | 58424.84 | 0.000 | 54.84% | 98.93% | `{"filetypes/crate": 0.995481014251709, "general": 0.5001893043518066}` |
| filetypes/pe | joint_or_at_fp_0 | 1372192 | 194588 | 36.78% | 0 | 0.00 | 1539.51 | 0.000 | 53.78% | 44.63% | `{"filegroups/native": 0.9995879530906677, "filetypes/pe": 0.9996156692504883, "general": 0.9998260736465454}` |
| filetypes/php | joint_or_at_fp_0 | 6053 | 551094 | 36.41% | 0 | 0.00 | 543.60 | 0.000 | 53.39% | 99.31% | `{"filegroups/scripts": 0.9980560541152954, "filetypes/php": 0.9982245564460754, "general": 0.9984949231147766}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3498 | 753228 | 35.16% | 0 | 0.00 | 397.72 | 0.000 | 52.03% | 99.70% | `{"filetypes/python_bytecode": 0.9999874830245972, "general": 0.9745393991470337}` |
| filetypes/ruby | joint_or_at_fp_0 | 350 | 173111 | 34.86% | 0 | 0.00 | 1730.51 | 0.000 | 51.69% | 99.87% | `{"filegroups/scripts": 0.9758837819099426, "general": 0.9481370449066162}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67953 | 3077 | 29.21% | 0 | 0.00 | 97311.49 | 0.000 | 45.22% | 32.28% | `{"filetypes/ooxml": 0.9976078271865845, "general": 0.9961952567100525}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 828 | 97.89% | 0 | 0.00 | 361149.69 | 0.000 | 98.93% | 98.14% | `{"filetypes/rtf": 0.4016873240470886, "general": 0.8443288207054138}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.47% | 0 | 0.00 | 18783.79 | 0.000 | 98.20% | 99.94% | `{"general": 0.08868321031332016}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 459 | 93.10% | 0 | 0.00 | 650539.75 | 0.000 | 96.43% | 99.23% | `{"filetypes/applescript": 0.7369557619094849}` |
| filetypes/gem | joint_or_at_fp_0 | 881 | 2405 | 92.05% | 0 | 0.00 | 124485.13 | 0.000 | 95.86% | 97.87% | `{"filetypes/gem": 0.9809819459915161, "general": 0.8593581318855286}` |
| filetypes/asar | joint_or_at_fp_0 | 181 | 80 | 90.61% | 0 | 0.00 | 3675419.78 | 0.000 | 95.07% | 93.49% | `{"filetypes/asar": 0.7991325855255127, "general": 0.7868700623512268}` |
| filetypes/elf | joint_or_at_fp_0 | 191368 | 447361 | 88.53% | 0 | 0.00 | 669.64 | 0.000 | 93.92% | 96.56% | `{"filegroups/native": 0.9904534816741943, "filetypes/elf": 0.9998020529747009, "general": 0.9841664433479309}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10622 | 12579 | 74.04% | 0 | 0.00 | 23812.51 | 0.000 | 85.08% | 88.11% | `{"filetypes/pkg_info": 0.9957355260848999, "general": 0.9966630935668945}` |
| filetypes/macho | joint_or_at_fp_0 | 2810 | 21749 | 62.24% | 0 | 0.00 | 13773.17 | 0.000 | 76.73% | 95.68% | `{"filegroups/native": 0.9591631889343262, "filetypes/macho": 0.9872281551361084, "general": 0.9444067478179932}` |
| filetypes/tar | joint_or_at_fp_0 | 33973 | 62637 | 61.68% | 0 | 0.00 | 4782.57 | 0.000 | 76.30% | 86.52% | `{"filetypes/tar": 0.9996676445007324, "general": 0.9948330521583557}` |
| filetypes/package.json | joint_or_at_fp_0 | 20310 | 47568 | 61.62% | 0 | 0.00 | 6297.59 | 0.000 | 76.26% | 88.52% | `{"filegroups/config": 0.9999880790710449, "filetypes/package.json": 0.9997749924659729, "general": 0.998114824295044}` |
| filetypes/swift | joint_or_at_fp_0 | 65 | 38621 | 58.46% | 0 | 0.00 | 7756.44 | 0.000 | 73.79% | 99.93% | `{"filegroups/source": 0.02822774648666382}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87519 | 30735 | 57.36% | 0 | 0.00 | 9746.50 | 0.000 | 72.90% | 68.44% | `{"filetypes/ole_doc": 0.9984715580940247, "general": 0.9995750188827515}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25866 | 54.72% | 0 | 0.00 | 11581.07 | 0.000 | 70.73% | 99.82% | `{"filegroups/scripts": 0.9874284863471985, "filetypes/lua": 0.9004098176956177}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32383 | 73231 | 53.45% | 0 | 0.00 | 4090.71 | 0.000 | 69.67% | 85.73% | `{"filegroups/source": 0.9796195030212402, "filetypes/kotlin": 0.9959867596626282, "general": 0.9734386801719666}` |
| filetypes/perl | learned_blend_at_fp_0 | 400 | 67791 | 49.75% | 0 | 0.00 | 4418.97 | 0.000 | 66.44% | 99.71% | `{}` |
| filetypes/shell | joint_or_at_fp_0 | 17932 | 131867 | 49.16% | 0 | 0.00 | 2271.76 | 0.000 | 65.91% | 93.91% | `{"filegroups/scripts": 0.9967226386070251, "filetypes/shell": 0.99748694896698, "general": 0.9918321371078491}` |
| filetypes/python | learned_blend_at_fp_0 | 23096 | 540541 | 48.32% | 0 | 0.00 | 554.21 | 0.000 | 65.16% | 97.88% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4626 | 1070 | 47.02% | 0 | 0.00 | 279583.41 | 0.000 | 63.96% | 56.97% | `{"filetypes/lnk": 0.991326630115509, "general": 0.998199999332428}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8419 | 45.45% | 0 | 0.00 | 35576.66 | 0.000 | 62.50% | 99.30% | `{"filetypes/clojure": 0.9952961802482605, "general": 0.020179837942123413}` |
| filetypes/jar | joint_or_at_fp_0 | 3843 | 18077 | 42.67% | 0 | 0.00 | 16570.69 | 0.000 | 59.82% | 89.95% | `{"filetypes/jar": 0.9905960559844971, "general": 0.9949970245361328}` |
| filetypes/zst | calibrate_inherited | 10472 | 176909 | 42.46% | 0 | 0.00 | 1693.36 | 0.000 | 59.61% | 96.78% | `{"general": 0.9992215663726269}` |
| filetypes/powershell | joint_or_at_fp_0 | 5976 | 4553 | 40.80% | 0 | 0.00 | 65775.25 | 0.000 | 57.95% | 66.40% | `{"filegroups/scripts": 0.9978869557380676, "filetypes/powershell": 0.9949578642845154, "general": 0.9890596270561218}` |
| filetypes/npm | joint_or_at_fp_0 | 4130 | 4964 | 40.77% | 0 | 0.00 | 60330.95 | 0.000 | 57.93% | 73.10% | `{"filetypes/npm": 0.9957634210586548, "general": 0.9975879788398743}` |
| filetypes/whl | joint_or_at_fp_0 | 3476 | 5963 | 40.22% | 0 | 0.00 | 50226.06 | 0.000 | 57.37% | 77.98% | `{"filetypes/whl": 0.9926167130470276, "general": 0.9642204642295837}` |
| filetypes/javascript | joint_or_at_fp_0 | 139646 | 1266021 | 38.21% | 0 | 0.00 | 236.63 | 0.000 | 55.29% | 93.86% | `{"filegroups/scripts": 0.9983587861061096, "filetypes/javascript": 0.9986760020256042, "general": 0.9988428354263306}` |
| filetypes/crate | joint_or_at_fp_0 | 90 | 5126 | 37.78% | 0 | 0.00 | 58424.84 | 0.000 | 54.84% | 98.93% | `{"filetypes/crate": 0.995481014251709, "general": 0.5001893043518066}` |
| filetypes/pe | joint_or_at_fp_0 | 1372192 | 194588 | 36.78% | 0 | 0.00 | 1539.51 | 0.000 | 53.78% | 44.63% | `{"filegroups/native": 0.9995879530906677, "filetypes/pe": 0.9996156692504883, "general": 0.9998260736465454}` |
| filetypes/php | joint_or_at_fp_0 | 6053 | 551094 | 36.41% | 0 | 0.00 | 543.60 | 0.000 | 53.39% | 99.31% | `{"filegroups/scripts": 0.9980560541152954, "filetypes/php": 0.9982245564460754, "general": 0.9984949231147766}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3498 | 753228 | 35.16% | 0 | 0.00 | 397.72 | 0.000 | 52.03% | 99.70% | `{"filetypes/python_bytecode": 0.9999874830245972, "general": 0.9745393991470337}` |
| filetypes/ruby | joint_or_at_fp_0 | 350 | 173111 | 34.86% | 0 | 0.00 | 1730.51 | 0.000 | 51.69% | 99.87% | `{"filegroups/scripts": 0.9758837819099426, "general": 0.9481370449066162}` |
