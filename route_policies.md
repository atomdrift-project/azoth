# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3898247616`
- Rows: 17606816 (2679214 malware, 14927602 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 97.02% | 0 | 0.00 | 337928.55 | 0.000 | 98.49% | 97.39% | `{"filegroups/documents": 0.9724808931350708, "filetypes/rtf": 0.9957445859909058}` |
| filetypes/asar | learned_blend_at_fp_0 | 189 | 238 | 96.30% | 0 | 0.00 | 1250822.40 | 0.000 | 98.11% | 98.36% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8861338496208191}` |
| filetypes/gem | joint_or_at_fp_0 | 1014 | 8008 | 91.32% | 0 | 0.00 | 37402.25 | 0.000 | 95.46% | 99.02% | `{"filetypes/gem": 0.9655035734176636, "general": 0.9661470055580139}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 91.14% | 0 | 0.00 | 977399.40 | 0.000 | 95.37% | 91.43% | `{"filetypes/7z": 0.7612612843513489, "general": 0.962293803691864}` |
| filetypes/elf | joint_or_at_fp_0 | 196623 | 811136 | 86.44% | 0 | 0.00 | 369.32 | 0.000 | 92.73% | 97.35% | `{"filegroups/native": 0.9967040419578552, "filetypes/elf": 0.9998567700386047, "general": 0.9938178658485413}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 54 | 85.66% | 0 | 0.00 | 5396576.71 | 0.000 | 92.27% | 88.26% | `{"filetypes/chm": 0.8770419955253601, "general": 0.1106354147195816}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 9785 | 16667 | 82.26% | 0 | 0.00 | 17972.42 | 0.000 | 90.27% | 93.44% | `{"filetypes/pkg_info": 0.9991616010665894, "general": 0.9919121861457825}` |
| filetypes/tar | joint_or_at_fp_0 | 33944 | 76545 | 68.03% | 0 | 0.00 | 3913.61 | 0.000 | 80.98% | 90.18% | `{"filetypes/tar": 0.9988718628883362, "general": 0.994055986404419}` |
| filetypes/shell | joint_or_at_fp_0 | 18634 | 160276 | 65.36% | 0 | 0.00 | 1869.09 | 0.000 | 79.05% | 96.39% | `{"filegroups/scripts": 0.998590350151062, "filetypes/shell": 0.9962584376335144, "general": 0.9967576265335083}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 81473 | 61.46% | 0 | 0.00 | 3676.90 | 0.000 | 76.13% | 99.85% | `{"filegroups/documents": 0.9966591000556946, "filetypes/html": 0.9998118877410889, "general": 0.9547045230865479}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 97 | 699 | 56.70% | 0 | 0.00 | 427656.93 | 0.000 | 72.37% | 94.72% | `{"filetypes/python_sdist": 0.9656785130500793, "general": 0.8977712988853455}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 31885 | 55.30% | 0 | 0.00 | 9394.99 | 0.000 | 71.22% | 96.36% | `{"filegroups/native": 0.9799849987030029, "filetypes/macho": 0.994746744632721}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27681 | 52.83% | 0 | 0.00 | 10821.76 | 0.000 | 69.14% | 99.82% | `{"filegroups/scripts": 0.9919057488441467, "filetypes/lua": 0.8092215061187744, "general": 0.9587276577949524}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.18934482336044312}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32349 | 83775 | 51.06% | 0 | 0.00 | 3575.86 | 0.000 | 67.61% | 86.37% | `{"filegroups/source": 0.9963423013687134, "filetypes/kotlin": 0.9562828540802002, "general": 0.9827173352241516}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5518 | 50.55% | 0 | 0.00 | 54275.45 | 0.000 | 67.15% | 74.16% | `{"filegroups/scripts": 0.9980414509773254, "filetypes/powershell": 0.996881902217865, "general": 0.9911803007125854}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87705 | 31279 | 48.57% | 0 | 0.00 | 9577.00 | 0.000 | 65.39% | 62.09% | `{"filetypes/ole_doc": 0.9997215867042542, "general": 0.9985950589179993}` |
| filetypes/javascript | joint_or_at_fp_0 | 142052 | 1646711 | 42.92% | 0 | 0.00 | 181.92 | 0.000 | 60.06% | 95.47% | `{"filegroups/scripts": 0.998309850692749, "filetypes/javascript": 0.9986488223075867, "general": 0.9987262487411499}` |
| filetypes/pe | joint_or_at_fp_0 | 1379170 | 234371 | 41.36% | 0 | 0.00 | 1278.19 | 0.000 | 58.52% | 49.88% | `{"filegroups/native": 0.9997913837432861, "filetypes/pe": 0.9995637536048889, "general": 0.999668538570404}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9477 | 40.91% | 0 | 0.00 | 31605.56 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984038472175598, "general": 0.0375126488506794}` |
| filetypes/php | joint_or_at_fp_0 | 6785 | 613602 | 39.03% | 0 | 0.00 | 488.22 | 0.000 | 56.14% | 99.33% | `{"filegroups/scripts": 0.9988213181495667, "filetypes/php": 0.9948346018791199, "general": 0.9876881241798401}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78169 | 38.64% | 0 | 0.00 | 3832.31 | 0.000 | 55.74% | 99.69% | `{"filetypes/perl": 0.9998233318328857, "general": 0.9787614941596985}` |
| filetypes/npm | joint_or_at_fp_0 | 7335 | 30873 | 38.53% | 0 | 0.00 | 9702.93 | 0.000 | 55.62% | 88.20% | `{"filetypes/npm": 0.9982548952102661, "general": 0.9989631175994873}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1152 | 37.32% | 0 | 0.00 | 259708.38 | 0.000 | 54.35% | 49.68% | `{"filetypes/lnk": 0.9950228333473206, "general": 0.9986004829406738}` |
| filetypes/ruby | joint_or_at_fp_0 | 400 | 179282 | 37.25% | 0 | 0.00 | 1670.95 | 0.000 | 54.28% | 99.86% | `{"filegroups/scripts": 0.97286456823349, "filetypes/ruby": 0.9967503547668457, "general": 0.9322119355201721}` |
| filetypes/python | joint_or_at_fp_0 | 23168 | 643774 | 36.57% | 0 | 0.00 | 465.34 | 0.000 | 53.56% | 97.80% | `{"filegroups/scripts": 0.9984909892082214, "filetypes/python": 0.9991809725761414, "general": 0.997084379196167}` |
| filetypes/jar | joint_or_at_fp_0 | 3936 | 29175 | 31.91% | 0 | 0.00 | 10267.62 | 0.000 | 48.38% | 91.91% | `{"filetypes/jar": 0.998358964920044, "general": 0.9729921817779541}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67991 | 3118 | 30.46% | 0 | 0.00 | 96032.51 | 0.000 | 46.70% | 33.51% | `{"filetypes/ooxml": 0.9964986443519592, "general": 0.9937747120857239}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2897 | 226 | 30.34% | 0 | 0.00 | 1316798.59 | 0.000 | 46.56% | 35.38% | `{"filetypes/apk_android": 0.9193950891494751, "general": 0.3447378873825073}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 97.02% | 0 | 0.00 | 337928.55 | 0.000 | 98.49% | 97.39% | `{"filegroups/documents": 0.9724808931350708, "filetypes/rtf": 0.9957445859909058}` |
| filetypes/asar | learned_blend_at_fp_0 | 189 | 238 | 96.30% | 0 | 0.00 | 1250822.40 | 0.000 | 98.11% | 98.36% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8861338496208191}` |
| filetypes/gem | joint_or_at_fp_0 | 1014 | 8008 | 91.32% | 0 | 0.00 | 37402.25 | 0.000 | 95.46% | 99.02% | `{"filetypes/gem": 0.9655035734176636, "general": 0.9661470055580139}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 91.14% | 0 | 0.00 | 977399.40 | 0.000 | 95.37% | 91.43% | `{"filetypes/7z": 0.7612612843513489, "general": 0.962293803691864}` |
| filetypes/elf | joint_or_at_fp_0 | 196623 | 811136 | 86.44% | 0 | 0.00 | 369.32 | 0.000 | 92.73% | 97.35% | `{"filegroups/native": 0.9967040419578552, "filetypes/elf": 0.9998567700386047, "general": 0.9938178658485413}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 54 | 85.66% | 0 | 0.00 | 5396576.71 | 0.000 | 92.27% | 88.26% | `{"filetypes/chm": 0.8770419955253601, "general": 0.1106354147195816}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 9785 | 16667 | 82.26% | 0 | 0.00 | 17972.42 | 0.000 | 90.27% | 93.44% | `{"filetypes/pkg_info": 0.9991616010665894, "general": 0.9919121861457825}` |
| filetypes/tar | joint_or_at_fp_0 | 33944 | 76545 | 68.03% | 0 | 0.00 | 3913.61 | 0.000 | 80.98% | 90.18% | `{"filetypes/tar": 0.9988718628883362, "general": 0.994055986404419}` |
| filetypes/shell | joint_or_at_fp_0 | 18634 | 160276 | 65.36% | 0 | 0.00 | 1869.09 | 0.000 | 79.05% | 96.39% | `{"filegroups/scripts": 0.998590350151062, "filetypes/shell": 0.9962584376335144, "general": 0.9967576265335083}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 81473 | 61.46% | 0 | 0.00 | 3676.90 | 0.000 | 76.13% | 99.85% | `{"filegroups/documents": 0.9966591000556946, "filetypes/html": 0.9998118877410889, "general": 0.9547045230865479}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 97 | 699 | 56.70% | 0 | 0.00 | 427656.93 | 0.000 | 72.37% | 94.72% | `{"filetypes/python_sdist": 0.9656785130500793, "general": 0.8977712988853455}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 31885 | 55.30% | 0 | 0.00 | 9394.99 | 0.000 | 71.22% | 96.36% | `{"filegroups/native": 0.9799849987030029, "filetypes/macho": 0.994746744632721}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27681 | 52.83% | 0 | 0.00 | 10821.76 | 0.000 | 69.14% | 99.82% | `{"filegroups/scripts": 0.9919057488441467, "filetypes/lua": 0.8092215061187744, "general": 0.9587276577949524}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.18934482336044312}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32349 | 83775 | 51.06% | 0 | 0.00 | 3575.86 | 0.000 | 67.61% | 86.37% | `{"filegroups/source": 0.9963423013687134, "filetypes/kotlin": 0.9562828540802002, "general": 0.9827173352241516}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5518 | 50.55% | 0 | 0.00 | 54275.45 | 0.000 | 67.15% | 74.16% | `{"filegroups/scripts": 0.9980414509773254, "filetypes/powershell": 0.996881902217865, "general": 0.9911803007125854}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87705 | 31279 | 48.57% | 0 | 0.00 | 9577.00 | 0.000 | 65.39% | 62.09% | `{"filetypes/ole_doc": 0.9997215867042542, "general": 0.9985950589179993}` |
| filetypes/javascript | joint_or_at_fp_0 | 142052 | 1646711 | 42.92% | 0 | 0.00 | 181.92 | 0.000 | 60.06% | 95.47% | `{"filegroups/scripts": 0.998309850692749, "filetypes/javascript": 0.9986488223075867, "general": 0.9987262487411499}` |
| filetypes/pe | joint_or_at_fp_0 | 1379170 | 234371 | 41.36% | 0 | 0.00 | 1278.19 | 0.000 | 58.52% | 49.88% | `{"filegroups/native": 0.9997913837432861, "filetypes/pe": 0.9995637536048889, "general": 0.999668538570404}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9477 | 40.91% | 0 | 0.00 | 31605.56 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984038472175598, "general": 0.0375126488506794}` |
| filetypes/php | joint_or_at_fp_0 | 6785 | 613602 | 39.03% | 0 | 0.00 | 488.22 | 0.000 | 56.14% | 99.33% | `{"filegroups/scripts": 0.9988213181495667, "filetypes/php": 0.9948346018791199, "general": 0.9876881241798401}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78169 | 38.64% | 0 | 0.00 | 3832.31 | 0.000 | 55.74% | 99.69% | `{"filetypes/perl": 0.9998233318328857, "general": 0.9787614941596985}` |
| filetypes/npm | joint_or_at_fp_0 | 7335 | 30873 | 38.53% | 0 | 0.00 | 9702.93 | 0.000 | 55.62% | 88.20% | `{"filetypes/npm": 0.9982548952102661, "general": 0.9989631175994873}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1152 | 37.32% | 0 | 0.00 | 259708.38 | 0.000 | 54.35% | 49.68% | `{"filetypes/lnk": 0.9950228333473206, "general": 0.9986004829406738}` |
| filetypes/ruby | joint_or_at_fp_0 | 400 | 179282 | 37.25% | 0 | 0.00 | 1670.95 | 0.000 | 54.28% | 99.86% | `{"filegroups/scripts": 0.97286456823349, "filetypes/ruby": 0.9967503547668457, "general": 0.9322119355201721}` |
| filetypes/python | joint_or_at_fp_0 | 23168 | 643774 | 36.57% | 0 | 0.00 | 465.34 | 0.000 | 53.56% | 97.80% | `{"filegroups/scripts": 0.9984909892082214, "filetypes/python": 0.9991809725761414, "general": 0.997084379196167}` |
| filetypes/rar | calibrate_inherited | 22199 | 44 | 33.70% | 0 | 0.00 | 6581877.11 | 0.000 | 50.41% | 33.83% | `{"general": 0.999324603972282}` |
| filetypes/jar | joint_or_at_fp_0 | 3936 | 29175 | 31.91% | 0 | 0.00 | 10267.62 | 0.000 | 48.38% | 91.91% | `{"filetypes/jar": 0.998358964920044, "general": 0.9729921817779541}` |
| filetypes/zst | calibrate_inherited | 10473 | 334639 | 30.79% | 0 | 0.00 | 895.21 | 0.000 | 47.09% | 97.90% | `{"general": 0.999324603972282}` |
