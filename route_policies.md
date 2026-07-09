# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2173356472`
- Rows: 13546141 (2651358 malware, 10894783 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 828 | 97.90% | 0 | 0.00 | 361149.69 | 0.000 | 98.94% | 98.15% | `{"filetypes/rtf": 0.0524369478225708}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.86% | 0 | 0.00 | 18783.79 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9956018924713135}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10622 | 12444 | 95.52% | 0 | 0.00 | 24070.81 | 0.000 | 97.71% | 97.94% | `{"filetypes/pkg_info": 0.9434366226196289, "general": 0.9962251782417297}` |
| filetypes/gem | joint_or_at_fp_0 | 880 | 2393 | 93.52% | 0 | 0.00 | 125108.98 | 0.000 | 96.65% | 98.26% | `{"filetypes/gem": 0.8199471831321716}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 458 | 93.10% | 0 | 0.00 | 651955.50 | 0.000 | 96.43% | 99.22% | `{"filetypes/applescript": 0.7366812229156494}` |
| filetypes/elf | joint_or_at_fp_0 | 191237 | 444331 | 90.09% | 0 | 0.00 | 674.21 | 0.000 | 94.79% | 97.02% | `{"filegroups/native": 0.9917224049568176, "filetypes/elf": 0.9997132420539856, "general": 0.9837158918380737}` |
| filetypes/asar | joint_or_at_fp_0 | 181 | 77 | 89.50% | 0 | 0.00 | 3815851.07 | 0.000 | 94.46% | 92.64% | `{"filetypes/asar": 0.8219209909439087, "general": 0.8244945406913757}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87515 | 30698 | 88.04% | 0 | 0.00 | 9758.25 | 0.000 | 93.64% | 91.14% | `{"filetypes/ole_doc": 0.9859822988510132}` |
| filetypes/package.json | joint_or_at_fp_0 | 20270 | 47358 | 86.68% | 0 | 0.00 | 6325.52 | 0.000 | 92.86% | 96.01% | `{"filegroups/config": 0.9996541738510132, "filetypes/package.json": 0.9977337121963501, "general": 0.9972124695777893}` |
| filetypes/tar | filetype_only_at_fp_0 | 33886 | 62411 | 77.97% | 0 | 0.00 | 4799.89 | 0.000 | 87.62% | 92.25% | `{"filetypes/tar": 0.9939283132553101}` |
| filetypes/macho | joint_or_at_fp_0 | 2806 | 21649 | 73.56% | 0 | 0.00 | 13836.78 | 0.000 | 84.76% | 96.97% | `{"filegroups/native": 0.9603014588356018, "filetypes/macho": 0.9615113735198975, "general": 0.9726599454879761}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25815 | 72.64% | 0 | 0.00 | 11603.95 | 0.000 | 84.15% | 99.89% | `{"filegroups/scripts": 0.9432601928710938, "filetypes/lua": 0.6346017122268677}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 27559 | 71.31% | 0 | 0.00 | 10869.66 | 0.000 | 83.25% | 75.14% | `{"filegroups/documents": 0.8146635890007019, "filetypes/pdf": 0.975774884223938}` |
| filetypes/lnk | joint_or_at_fp_0 | 4624 | 1070 | 66.35% | 0 | 0.00 | 279583.41 | 0.000 | 79.77% | 72.67% | `{"filetypes/lnk": 0.9951815009117126, "general": 0.9965935945510864}` |
| filetypes/shell | joint_or_at_fp_0 | 17897 | 131541 | 63.82% | 0 | 0.00 | 2277.39 | 0.000 | 77.92% | 95.67% | `{"filegroups/scripts": 0.9875808954238892, "filetypes/shell": 0.979455828666687, "general": 0.9930244088172913}` |
| filetypes/swift | joint_or_at_fp_0 | 65 | 38577 | 63.08% | 0 | 0.00 | 7765.29 | 0.000 | 77.36% | 99.94% | `{"filegroups/source": 0.010843515396118164}` |
| filetypes/powershell | joint_or_at_fp_0 | 5972 | 4541 | 56.61% | 0 | 0.00 | 65949.01 | 0.000 | 72.30% | 75.35% | `{"filegroups/scripts": 0.9920329451560974, "filetypes/powershell": 0.9225752949714661, "general": 0.988877534866333}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 67210 | 56.00% | 0 | 0.00 | 4457.17 | 0.000 | 71.79% | 99.74% | `{"filegroups/scripts": 0.9831438660621643, "filetypes/perl": 0.9813404679298401}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32383 | 73209 | 55.57% | 0 | 0.00 | 4091.94 | 0.000 | 71.44% | 86.37% | `{"filegroups/source": 0.9821229577064514, "filetypes/kotlin": 0.9196711778640747, "general": 0.9678019881248474}` |
| filetypes/python_bytecode | learned_blend_at_fp_0 | 3497 | 744155 | 54.76% | 0 | 0.00 | 402.57 | 0.000 | 70.77% | 99.79% | `{}` |
| filetypes/npm | joint_or_at_fp_0 | 3919 | 4841 | 53.71% | 0 | 0.00 | 61863.37 | 0.000 | 69.89% | 79.29% | `{"filetypes/npm": 0.9902626276016235}` |
| filetypes/pe | joint_or_at_fp_0 | 1372040 | 193854 | 51.70% | 0 | 0.00 | 1545.34 | 0.000 | 68.16% | 57.68% | `{"filegroups/native": 0.9993832111358643, "filetypes/pe": 0.9985507130622864, "general": 0.9996362328529358}` |
| filetypes/vsix | joint_or_at_fp_0 | 92 | 2643 | 51.09% | 0 | 0.00 | 113281.69 | 0.000 | 67.63% | 98.35% | `{"filetypes/vsix": 0.8797798156738281}` |
| filetypes/python | joint_or_at_fp_0 | 23080 | 537061 | 49.60% | 0 | 0.00 | 557.80 | 0.000 | 66.31% | 97.92% | `{"filegroups/scripts": 0.9940980672836304, "filetypes/python": 0.995585560798645, "general": 0.9936510920524597}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8408 | 48.18% | 0 | 0.00 | 35623.20 | 0.000 | 65.03% | 99.33% | `{"filetypes/clojure": 0.9913700819015503}` |
| filetypes/vbs | joint_or_at_fp_0 | 12184 | 3552 | 47.23% | 0 | 0.00 | 84303.75 | 0.000 | 64.16% | 59.14% | `{"filetypes/vbs": 0.9974977374076843, "general": 0.9967108368873596}` |
| filetypes/whl | joint_or_at_fp_0 | 3446 | 5889 | 46.98% | 0 | 0.00 | 50857.03 | 0.000 | 63.93% | 80.43% | `{"filetypes/whl": 0.9912952184677124, "general": 0.9701977372169495}` |
| filetypes/crate | joint_or_at_fp_0 | 84 | 5123 | 46.43% | 0 | 0.00 | 58459.04 | 0.000 | 63.41% | 99.14% | `{"filetypes/crate": 0.9908349514007568, "general": 0.343439519405365}` |
| filetypes/crx | joint_or_at_fp_0 | 1588 | 2405 | 42.19% | 0 | 0.00 | 124485.13 | 0.000 | 59.34% | 77.01% | `{"filetypes/crx": 0.9365206360816956, "general": 0.9752326011657715}` |
| filetypes/php | joint_or_at_fp_0 | 6050 | 549825 | 41.42% | 0 | 0.00 | 544.85 | 0.000 | 58.58% | 99.36% | `{"filegroups/scripts": 0.9762095808982849, "filetypes/php": 0.9958129525184631}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 828 | 97.90% | 0 | 0.00 | 361149.69 | 0.000 | 98.94% | 98.15% | `{"filetypes/rtf": 0.0524369478225708}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.86% | 0 | 0.00 | 18783.79 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9956018924713135}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10622 | 12444 | 95.52% | 0 | 0.00 | 24070.81 | 0.000 | 97.71% | 97.94% | `{"filetypes/pkg_info": 0.9434366226196289, "general": 0.9962251782417297}` |
| filetypes/gem | joint_or_at_fp_0 | 880 | 2393 | 93.52% | 0 | 0.00 | 125108.98 | 0.000 | 96.65% | 98.26% | `{"filetypes/gem": 0.8199471831321716}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 458 | 93.10% | 0 | 0.00 | 651955.50 | 0.000 | 96.43% | 99.22% | `{"filetypes/applescript": 0.7366812229156494}` |
| filetypes/elf | joint_or_at_fp_0 | 191237 | 444331 | 90.09% | 0 | 0.00 | 674.21 | 0.000 | 94.79% | 97.02% | `{"filegroups/native": 0.9917224049568176, "filetypes/elf": 0.9997132420539856, "general": 0.9837158918380737}` |
| filetypes/asar | joint_or_at_fp_0 | 181 | 77 | 89.50% | 0 | 0.00 | 3815851.07 | 0.000 | 94.46% | 92.64% | `{"filetypes/asar": 0.8219209909439087, "general": 0.8244945406913757}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87515 | 30698 | 88.04% | 0 | 0.00 | 9758.25 | 0.000 | 93.64% | 91.14% | `{"filetypes/ole_doc": 0.9859822988510132}` |
| filetypes/package.json | joint_or_at_fp_0 | 20270 | 47358 | 86.68% | 0 | 0.00 | 6325.52 | 0.000 | 92.86% | 96.01% | `{"filegroups/config": 0.9996541738510132, "filetypes/package.json": 0.9977337121963501, "general": 0.9972124695777893}` |
| filetypes/tar | filetype_only_at_fp_0 | 33886 | 62411 | 77.97% | 0 | 0.00 | 4799.89 | 0.000 | 87.62% | 92.25% | `{"filetypes/tar": 0.9939283132553101}` |
| filetypes/macho | joint_or_at_fp_0 | 2806 | 21649 | 73.56% | 0 | 0.00 | 13836.78 | 0.000 | 84.76% | 96.97% | `{"filegroups/native": 0.9603014588356018, "filetypes/macho": 0.9615113735198975, "general": 0.9726599454879761}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25815 | 72.64% | 0 | 0.00 | 11603.95 | 0.000 | 84.15% | 99.89% | `{"filegroups/scripts": 0.9432601928710938, "filetypes/lua": 0.6346017122268677}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 27559 | 71.31% | 0 | 0.00 | 10869.66 | 0.000 | 83.25% | 75.14% | `{"filegroups/documents": 0.8146635890007019, "filetypes/pdf": 0.975774884223938}` |
| filetypes/lnk | joint_or_at_fp_0 | 4624 | 1070 | 66.35% | 0 | 0.00 | 279583.41 | 0.000 | 79.77% | 72.67% | `{"filetypes/lnk": 0.9951815009117126, "general": 0.9965935945510864}` |
| filetypes/shell | joint_or_at_fp_0 | 17897 | 131541 | 63.82% | 0 | 0.00 | 2277.39 | 0.000 | 77.92% | 95.67% | `{"filegroups/scripts": 0.9875808954238892, "filetypes/shell": 0.979455828666687, "general": 0.9930244088172913}` |
| filetypes/swift | joint_or_at_fp_0 | 65 | 38577 | 63.08% | 0 | 0.00 | 7765.29 | 0.000 | 77.36% | 99.94% | `{"filegroups/source": 0.010843515396118164}` |
| filetypes/powershell | joint_or_at_fp_0 | 5972 | 4541 | 56.61% | 0 | 0.00 | 65949.01 | 0.000 | 72.30% | 75.35% | `{"filegroups/scripts": 0.9920329451560974, "filetypes/powershell": 0.9225752949714661, "general": 0.988877534866333}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 67210 | 56.00% | 0 | 0.00 | 4457.17 | 0.000 | 71.79% | 99.74% | `{"filegroups/scripts": 0.9831438660621643, "filetypes/perl": 0.9813404679298401}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32383 | 73209 | 55.57% | 0 | 0.00 | 4091.94 | 0.000 | 71.44% | 86.37% | `{"filegroups/source": 0.9821229577064514, "filetypes/kotlin": 0.9196711778640747, "general": 0.9678019881248474}` |
| filetypes/python_bytecode | learned_blend_at_fp_0 | 3497 | 744155 | 54.76% | 0 | 0.00 | 402.57 | 0.000 | 70.77% | 99.79% | `{}` |
| filetypes/npm | joint_or_at_fp_0 | 3919 | 4841 | 53.71% | 0 | 0.00 | 61863.37 | 0.000 | 69.89% | 79.29% | `{"filetypes/npm": 0.9902626276016235}` |
| filetypes/pe | joint_or_at_fp_0 | 1372040 | 193854 | 51.70% | 0 | 0.00 | 1545.34 | 0.000 | 68.16% | 57.68% | `{"filegroups/native": 0.9993832111358643, "filetypes/pe": 0.9985507130622864, "general": 0.9996362328529358}` |
| filetypes/vsix | joint_or_at_fp_0 | 92 | 2643 | 51.09% | 0 | 0.00 | 113281.69 | 0.000 | 67.63% | 98.35% | `{"filetypes/vsix": 0.8797798156738281}` |
| filetypes/python | joint_or_at_fp_0 | 23080 | 537061 | 49.60% | 0 | 0.00 | 557.80 | 0.000 | 66.31% | 97.92% | `{"filegroups/scripts": 0.9940980672836304, "filetypes/python": 0.995585560798645, "general": 0.9936510920524597}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8408 | 48.18% | 0 | 0.00 | 35623.20 | 0.000 | 65.03% | 99.33% | `{"filetypes/clojure": 0.9913700819015503}` |
| filetypes/vbs | joint_or_at_fp_0 | 12184 | 3552 | 47.23% | 0 | 0.00 | 84303.75 | 0.000 | 64.16% | 59.14% | `{"filetypes/vbs": 0.9974977374076843, "general": 0.9967108368873596}` |
| filetypes/whl | joint_or_at_fp_0 | 3446 | 5889 | 46.98% | 0 | 0.00 | 50857.03 | 0.000 | 63.93% | 80.43% | `{"filetypes/whl": 0.9912952184677124, "general": 0.9701977372169495}` |
| filetypes/crate | joint_or_at_fp_0 | 84 | 5123 | 46.43% | 0 | 0.00 | 58459.04 | 0.000 | 63.41% | 99.14% | `{"filetypes/crate": 0.9908349514007568, "general": 0.343439519405365}` |
| filetypes/crx | joint_or_at_fp_0 | 1588 | 2405 | 42.19% | 0 | 0.00 | 124485.13 | 0.000 | 59.34% | 77.01% | `{"filetypes/crx": 0.9365206360816956, "general": 0.9752326011657715}` |
| filetypes/php | joint_or_at_fp_0 | 6050 | 549825 | 41.42% | 0 | 0.00 | 544.85 | 0.000 | 58.58% | 99.36% | `{"filegroups/scripts": 0.9762095808982849, "filetypes/php": 0.9958129525184631}` |
