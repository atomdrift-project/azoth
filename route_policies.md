# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3915237856`
- Rows: 17626984 (2679336 malware, 14947648 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 886 | 97.01% | 0 | 0.00 | 337547.79 | 0.000 | 98.48% | 97.38% | `{"filegroups/documents": 0.9785115122795105, "general": 0.8000980019569397}` |
| filetypes/asar | joint_or_at_fp_0 | 189 | 242 | 96.83% | 0 | 0.00 | 1230275.36 | 0.000 | 98.39% | 98.61% | `{"filetypes/asar": 0.8862689137458801, "general": 0.7814375758171082}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8671037554740906}` |
| filetypes/gem | joint_or_at_fp_0 | 1016 | 9147 | 91.83% | 0 | 0.00 | 32745.62 | 0.000 | 95.74% | 99.18% | `{"filetypes/gem": 0.956017255783081, "general": 0.9946852922439575}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 91.02% | 0 | 0.00 | 977399.40 | 0.000 | 95.30% | 91.31% | `{"filetypes/7z": 0.7383724451065063, "general": 0.9796754717826843}` |
| filetypes/elf | joint_or_at_fp_0 | 196623 | 812461 | 87.35% | 0 | 0.00 | 368.72 | 0.000 | 93.25% | 97.54% | `{"filegroups/native": 0.9947758913040161, "filetypes/elf": 0.9998685121536255, "general": 0.9935932755470276}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 9786 | 16671 | 86.03% | 0 | 0.00 | 17968.11 | 0.000 | 92.49% | 94.83% | `{"filetypes/pkg_info": 0.9993069767951965, "general": 0.9882398843765259}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 55 | 85.25% | 0 | 0.00 | 5301105.50 | 0.000 | 92.04% | 87.96% | `{"general": 0.11045839637517929}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 81893 | 78.03% | 0 | 0.00 | 3658.04 | 0.000 | 87.66% | 99.92% | `{"filegroups/documents": 0.9982190132141113, "filetypes/html": 0.9993913173675537, "general": 0.9630559086799622}` |
| filetypes/tar | joint_or_at_fp_0 | 33924 | 76784 | 69.45% | 0 | 0.00 | 3901.43 | 0.000 | 81.97% | 90.64% | `{"filetypes/tar": 0.9985204935073853, "general": 0.9902130365371704}` |
| filetypes/shell | joint_or_at_fp_0 | 18634 | 160277 | 67.35% | 0 | 0.00 | 1869.08 | 0.000 | 80.49% | 96.60% | `{"filegroups/scripts": 0.9987488985061646, "filetypes/shell": 0.9955040216445923, "general": 0.9968917965888977}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 31960 | 61.63% | 0 | 0.00 | 9372.94 | 0.000 | 76.26% | 96.88% | `{"filegroups/native": 0.9718145728111267, "filetypes/macho": 0.9891033172607422}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 120 | 700 | 58.33% | 0 | 0.00 | 427047.30 | 0.000 | 73.68% | 93.90% | `{"filetypes/python_sdist": 0.9732751846313477, "general": 0.9086434841156006}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32348 | 83775 | 52.46% | 0 | 0.00 | 3575.86 | 0.000 | 68.82% | 86.76% | `{"filegroups/source": 0.9937808513641357, "filetypes/kotlin": 0.9682171940803528, "general": 0.9706523418426514}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5524 | 52.20% | 0 | 0.00 | 54216.51 | 0.000 | 68.60% | 75.04% | `{"filegroups/scripts": 0.9982003569602966, "filetypes/powershell": 0.9966208338737488, "general": 0.9926496148109436}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.13856308162212372}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27682 | 50.94% | 0 | 0.00 | 10821.36 | 0.000 | 67.50% | 99.81% | `{"filegroups/scripts": 0.9930986762046814, "filetypes/lua": 0.8260788917541504}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1152 | 49.01% | 0 | 0.00 | 259708.38 | 0.000 | 65.78% | 59.07% | `{"filetypes/lnk": 0.9949785470962524, "general": 0.9956615567207336}` |
| filetypes/python | joint_or_at_fp_0 | 23175 | 643821 | 42.35% | 0 | 0.00 | 465.30 | 0.000 | 59.50% | 98.00% | `{"filegroups/scripts": 0.999068021774292, "filetypes/python": 0.9982236623764038, "general": 0.9958907961845398}` |
| filetypes/javascript | joint_or_at_fp_0 | 142062 | 1647413 | 42.00% | 0 | 0.00 | 181.84 | 0.000 | 59.16% | 95.40% | `{"filegroups/scripts": 0.9988699555397034, "filetypes/javascript": 0.9988254308700562, "general": 0.9984552264213562}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78287 | 41.41% | 0 | 0.00 | 3826.53 | 0.000 | 58.57% | 99.71% | `{"filegroups/scripts": 0.9966161847114563, "filetypes/perl": 0.9993878602981567, "general": 0.9881097078323364}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9481 | 40.91% | 0 | 0.00 | 31592.23 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984393119812012, "general": 0.015421613119542599}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87705 | 31281 | 40.75% | 0 | 0.00 | 9576.38 | 0.000 | 57.91% | 56.33% | `{"filetypes/ole_doc": 0.9996963739395142, "general": 0.9991683959960938}` |
| filetypes/pe | joint_or_at_fp_0 | 1379180 | 236186 | 38.55% | 0 | 0.00 | 1268.37 | 0.000 | 55.64% | 47.53% | `{"filegroups/native": 0.9997479319572449, "filetypes/pe": 0.9995982050895691, "general": 0.9997740387916565}` |
| filetypes/npm | joint_or_at_fp_0 | 7373 | 34266 | 38.25% | 0 | 0.00 | 8742.20 | 0.000 | 55.33% | 89.07% | `{"filetypes/npm": 0.9984840154647827, "general": 0.9988051652908325}` |
| filetypes/php | joint_or_at_fp_0 | 6785 | 613773 | 33.31% | 0 | 0.00 | 488.08 | 0.000 | 49.97% | 99.27% | `{"filegroups/scripts": 0.9992731809616089, "filetypes/php": 0.9941284656524658, "general": 0.9951510429382324}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67991 | 3123 | 30.71% | 0 | 0.00 | 95878.83 | 0.000 | 46.99% | 33.75% | `{"filetypes/ooxml": 0.9967771768569946, "general": 0.9910301566123962}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2897 | 227 | 29.55% | 0 | 0.00 | 1311035.91 | 0.000 | 45.62% | 34.67% | `{"filetypes/apk_android": 0.9203695058822632, "general": 0.5272229909896851}` |
| filetypes/package.json | joint_or_at_fp_0 | 20921 | 65766 | 28.31% | 0 | 0.00 | 4555.03 | 0.000 | 44.13% | 82.70% | `{"filegroups/config": 0.99998939037323, "filetypes/package.json": 0.9999204277992249, "general": 0.9992169737815857}` |
| filetypes/zip | joint_or_at_fp_0 | 108035 | 42174 | 28.07% | 0 | 0.00 | 7103.02 | 0.000 | 43.83% | 48.27% | `{"filetypes/zip": 0.9988338947296143, "general": 0.9975054264068604}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 886 | 97.01% | 0 | 0.00 | 337547.79 | 0.000 | 98.48% | 97.38% | `{"filegroups/documents": 0.9785115122795105, "general": 0.8000980019569397}` |
| filetypes/asar | joint_or_at_fp_0 | 189 | 242 | 96.83% | 0 | 0.00 | 1230275.36 | 0.000 | 98.39% | 98.61% | `{"filetypes/asar": 0.8862689137458801, "general": 0.7814375758171082}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8671037554740906}` |
| filetypes/gem | joint_or_at_fp_0 | 1016 | 9147 | 91.83% | 0 | 0.00 | 32745.62 | 0.000 | 95.74% | 99.18% | `{"filetypes/gem": 0.956017255783081, "general": 0.9946852922439575}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 91.02% | 0 | 0.00 | 977399.40 | 0.000 | 95.30% | 91.31% | `{"filetypes/7z": 0.7383724451065063, "general": 0.9796754717826843}` |
| filetypes/elf | joint_or_at_fp_0 | 196623 | 812461 | 87.35% | 0 | 0.00 | 368.72 | 0.000 | 93.25% | 97.54% | `{"filegroups/native": 0.9947758913040161, "filetypes/elf": 0.9998685121536255, "general": 0.9935932755470276}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 9786 | 16671 | 86.03% | 0 | 0.00 | 17968.11 | 0.000 | 92.49% | 94.83% | `{"filetypes/pkg_info": 0.9993069767951965, "general": 0.9882398843765259}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 55 | 85.25% | 0 | 0.00 | 5301105.50 | 0.000 | 92.04% | 87.96% | `{"general": 0.11045839637517929}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 81893 | 78.03% | 0 | 0.00 | 3658.04 | 0.000 | 87.66% | 99.92% | `{"filegroups/documents": 0.9982190132141113, "filetypes/html": 0.9993913173675537, "general": 0.9630559086799622}` |
| filetypes/tar | joint_or_at_fp_0 | 33924 | 76784 | 69.45% | 0 | 0.00 | 3901.43 | 0.000 | 81.97% | 90.64% | `{"filetypes/tar": 0.9985204935073853, "general": 0.9902130365371704}` |
| filetypes/shell | joint_or_at_fp_0 | 18634 | 160277 | 67.35% | 0 | 0.00 | 1869.08 | 0.000 | 80.49% | 96.60% | `{"filegroups/scripts": 0.9987488985061646, "filetypes/shell": 0.9955040216445923, "general": 0.9968917965888977}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 31960 | 61.63% | 0 | 0.00 | 9372.94 | 0.000 | 76.26% | 96.88% | `{"filegroups/native": 0.9718145728111267, "filetypes/macho": 0.9891033172607422}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 120 | 700 | 58.33% | 0 | 0.00 | 427047.30 | 0.000 | 73.68% | 93.90% | `{"filetypes/python_sdist": 0.9732751846313477, "general": 0.9086434841156006}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32348 | 83775 | 52.46% | 0 | 0.00 | 3575.86 | 0.000 | 68.82% | 86.76% | `{"filegroups/source": 0.9937808513641357, "filetypes/kotlin": 0.9682171940803528, "general": 0.9706523418426514}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5524 | 52.20% | 0 | 0.00 | 54216.51 | 0.000 | 68.60% | 75.04% | `{"filegroups/scripts": 0.9982003569602966, "filetypes/powershell": 0.9966208338737488, "general": 0.9926496148109436}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.13856308162212372}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27682 | 50.94% | 0 | 0.00 | 10821.36 | 0.000 | 67.50% | 99.81% | `{"filegroups/scripts": 0.9930986762046814, "filetypes/lua": 0.8260788917541504}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1152 | 49.01% | 0 | 0.00 | 259708.38 | 0.000 | 65.78% | 59.07% | `{"filetypes/lnk": 0.9949785470962524, "general": 0.9956615567207336}` |
| filetypes/python | joint_or_at_fp_0 | 23175 | 643821 | 42.35% | 0 | 0.00 | 465.30 | 0.000 | 59.50% | 98.00% | `{"filegroups/scripts": 0.999068021774292, "filetypes/python": 0.9982236623764038, "general": 0.9958907961845398}` |
| filetypes/javascript | joint_or_at_fp_0 | 142062 | 1647413 | 42.00% | 0 | 0.00 | 181.84 | 0.000 | 59.16% | 95.40% | `{"filegroups/scripts": 0.9988699555397034, "filetypes/javascript": 0.9988254308700562, "general": 0.9984552264213562}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78287 | 41.41% | 0 | 0.00 | 3826.53 | 0.000 | 58.57% | 99.71% | `{"filegroups/scripts": 0.9966161847114563, "filetypes/perl": 0.9993878602981567, "general": 0.9881097078323364}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9481 | 40.91% | 0 | 0.00 | 31592.23 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984393119812012, "general": 0.015421613119542599}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87705 | 31281 | 40.75% | 0 | 0.00 | 9576.38 | 0.000 | 57.91% | 56.33% | `{"filetypes/ole_doc": 0.9996963739395142, "general": 0.9991683959960938}` |
| filetypes/pe | joint_or_at_fp_0 | 1379180 | 236186 | 38.55% | 0 | 0.00 | 1268.37 | 0.000 | 55.64% | 47.53% | `{"filegroups/native": 0.9997479319572449, "filetypes/pe": 0.9995982050895691, "general": 0.9997740387916565}` |
| filetypes/npm | joint_or_at_fp_0 | 7373 | 34266 | 38.25% | 0 | 0.00 | 8742.20 | 0.000 | 55.33% | 89.07% | `{"filetypes/npm": 0.9984840154647827, "general": 0.9988051652908325}` |
| filetypes/php | joint_or_at_fp_0 | 6785 | 613773 | 33.31% | 0 | 0.00 | 488.08 | 0.000 | 49.97% | 99.27% | `{"filegroups/scripts": 0.9992731809616089, "filetypes/php": 0.9941284656524658, "general": 0.9951510429382324}` |
| filetypes/rar | calibrate_inherited | 22199 | 44 | 31.41% | 0 | 0.00 | 6581877.11 | 0.000 | 47.80% | 31.54% | `{"general": 0.999333238404696}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67991 | 3123 | 30.71% | 0 | 0.00 | 95878.83 | 0.000 | 46.99% | 33.75% | `{"filetypes/ooxml": 0.9967771768569946, "general": 0.9910301566123962}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2897 | 227 | 29.55% | 0 | 0.00 | 1311035.91 | 0.000 | 45.62% | 34.67% | `{"filetypes/apk_android": 0.9203695058822632, "general": 0.5272229909896851}` |
| filetypes/package.json | joint_or_at_fp_0 | 20921 | 65766 | 28.31% | 0 | 0.00 | 4555.03 | 0.000 | 44.13% | 82.70% | `{"filegroups/config": 0.99998939037323, "filetypes/package.json": 0.9999204277992249, "general": 0.9992169737815857}` |
