# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1658771605`
- Rows: 6720544 (2496311 malware, 4224233 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 10847 | 100.00% | 0 | 0.00 | 27614.26 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9985048770904541, "general": 0.8964168429374695}` |
| filetypes/rtf | joint_or_at_fp_0 | 5868 | 502 | 98.45% | 0 | 0.00 | 594982.34 | 0.000 | 99.22% | 98.57% | `{"filegroups/documents": 0.5882152318954468, "filetypes/rtf": 0.28342515230178833}` |
| filetypes/elf | learned_blend_at_fp_0 | 179066 | 163841 | 90.60% | 0 | 0.00 | 1828.42 | 0.000 | 95.07% | 95.09% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 18416 | 20479 | 88.81% | 0 | 0.00 | 14627.24 | 0.000 | 94.08% | 94.70% | `{"filegroups/config": 0.9997701644897461, "filetypes/package.json": 0.9980536699295044, "general": 0.9986539483070374}` |
| filetypes/shell | learned_blend_at_fp_0 | 14317 | 58949 | 85.35% | 0 | 0.00 | 5081.78 | 0.000 | 92.10% | 97.14% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 37084 | 20747 | 84.08% | 0 | 0.00 | 14438.31 | 0.000 | 91.35% | 89.79% | `{"filegroups/documents": 0.9975226521492004, "filetypes/xls": 0.9867926836013794, "general": 0.9995529055595398}` |
| filetypes/tar | joint_or_at_fp_0 | 31066 | 22449 | 78.34% | 0 | 0.00 | 13343.72 | 0.000 | 87.85% | 87.42% | `{"filetypes/tar": 0.9982911944389343, "general": 0.9975740909576416}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2724 | 87288 | 73.42% | 0 | 0.00 | 3431.95 | 0.000 | 84.67% | 99.20% | `{"filetypes/python-bytecode": 0.9989191293716431, "general": 0.9844789505004883}` |
| filetypes/clojure | joint_or_at_fp_0 | 121 | 5189 | 71.90% | 0 | 0.00 | 57715.70 | 0.000 | 83.65% | 99.36% | `{"general": 0.020301494747400284}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 64 | 448 | 71.88% | 0 | 0.00 | 666459.48 | 0.000 | 83.64% | 96.48% | `{"filetypes/chrome-manifest": 0.9250487089157104}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10641 | 1798 | 70.44% | 0 | 0.00 | 166475.97 | 0.000 | 82.66% | 74.72% | `{"general": 0.9948397874832153}` |
| filetypes/crx | learned_blend_at_fp_0 | 643 | 79 | 64.54% | 0 | 0.00 | 3721067.61 | 0.000 | 78.45% | 68.42% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 2584 | 11581 | 63.82% | 0 | 0.00 | 25864.30 | 0.000 | 77.91% | 93.40% | `{"filegroups/native": 0.9987778067588806, "filetypes/macho": 0.995280921459198, "general": 0.9831417202949524}` |
| filetypes/perl | learned_blend_at_fp_0 | 316 | 39244 | 62.97% | 0 | 0.00 | 7633.31 | 0.000 | 77.28% | 99.70% | `{}` |
| filetypes/javascript | joint_or_at_fp_0 | 117620 | 582691 | 61.37% | 0 | 0.00 | 514.12 | 0.000 | 76.06% | 93.51% | `{"filegroups/scripts": 0.9993817806243896, "filetypes/javascript": 0.9740317463874817, "general": 0.9994640946388245}` |
| filetypes/java_class | joint_or_at_fp_0 | 1638 | 704991 | 61.11% | 0 | 0.00 | 424.93 | 0.000 | 75.86% | 99.91% | `{"filetypes/java_class": 0.972117006778717, "general": 0.9854030013084412}` |
| filetypes/powershell | joint_or_at_fp_0 | 5236 | 2370 | 55.81% | 0 | 0.00 | 126322.35 | 0.000 | 71.64% | 69.58% | `{"filegroups/scripts": 0.9985805749893188, "filetypes/powershell": 0.9950449466705322, "general": 0.9980418086051941}` |
| filetypes/lnk | joint_or_at_fp_0 | 4347 | 1055 | 55.58% | 0 | 0.00 | 283552.89 | 0.000 | 71.45% | 64.25% | `{"filetypes/lnk": 0.9943863153457642, "general": 0.9990662932395935}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32587 | 51272 | 53.62% | 0 | 0.00 | 5842.65 | 0.000 | 69.81% | 81.98% | `{"filegroups/source": 0.8878219127655029, "filetypes/kotlin": 0.8020543456077576, "general": 0.9644496440887451}` |
| filetypes/ruby | joint_or_at_fp_0 | 118 | 24970 | 48.31% | 0 | 0.00 | 11996.61 | 0.000 | 65.14% | 99.76% | `{"filegroups/scripts": 0.9955379962921143, "filetypes/ruby": 0.9998736381530762, "general": 0.9734157919883728}` |
| filetypes/docx | joint_or_at_fp_0 | 4759 | 433 | 47.68% | 0 | 0.00 | 689467.22 | 0.000 | 64.57% | 52.04% | `{"filegroups/documents": 0.9979186654090881, "filetypes/docx": 0.9876461625099182, "general": 0.9829313158988953}` |
| filetypes/jar | learned_blend_at_fp_0 | 3402 | 3743 | 47.38% | 0 | 0.00 | 80003.57 | 0.000 | 64.30% | 74.95% | `{}` |
| filetypes/doc | calibrate_inherited | 32643 | 76 | 46.43% | 0 | 0.00 | 3865076.67 | 0.000 | 63.42% | 46.56% | `{"filegroups/documents": 0.9985501170158386, "general": 0.9998894929885864}` |
| filetypes/php | joint_or_at_fp_0 | 4811 | 145642 | 46.00% | 0 | 0.00 | 2056.89 | 0.000 | 63.01% | 98.27% | `{"filegroups/scripts": 0.998264729976654, "filetypes/php": 0.998719334602356, "general": 0.9766716361045837}` |
| filetypes/ole | joint_or_at_fp_0 | 6892 | 6219 | 45.59% | 0 | 0.00 | 48159.04 | 0.000 | 62.63% | 71.40% | `{"filegroups/documents": 0.9971538782119751, "filetypes/ole": 0.9978785514831543, "general": 0.9993857145309448}` |
| filetypes/msi | joint_or_at_fp_0 | 5307 | 172 | 43.51% | 0 | 0.00 | 1726624.81 | 0.000 | 60.64% | 45.28% | `{"filetypes/msi": 0.9261299967765808, "general": 0.9945985078811646}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18299 | 43.30% | 0 | 0.00 | 16369.68 | 0.000 | 60.43% | 99.70% | `{"filegroups/scripts": 0.9782118797302246, "filetypes/lua": 0.9987921118736267, "general": 0.97865229845047}` |
| filetypes/vbs | joint_or_at_fp_0 | 11088 | 3293 | 41.61% | 0 | 0.00 | 90931.37 | 0.000 | 58.77% | 54.98% | `{"filetypes/vbs": 0.9825754165649414, "general": 0.9964069724082947}` |
| filetypes/python | joint_or_at_fp_0 | 19388 | 182351 | 39.73% | 0 | 0.00 | 1642.82 | 0.000 | 56.86% | 94.21% | `{"filegroups/scripts": 0.9993232488632202, "filetypes/python": 0.9998348951339722, "general": 0.9986805319786072}` |
| filetypes/pe | learned_blend_at_fp_0 | 1325881 | 159682 | 36.30% | 0 | 0.00 | 1876.04 | 0.000 | 53.27% | 43.15% | `{}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 10847 | 100.00% | 0 | 0.00 | 27614.26 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9985048770904541, "general": 0.8964168429374695}` |
| filetypes/rtf | joint_or_at_fp_0 | 5868 | 502 | 98.45% | 0 | 0.00 | 594982.34 | 0.000 | 99.22% | 98.57% | `{"filegroups/documents": 0.5882152318954468, "filetypes/rtf": 0.28342515230178833}` |
| filetypes/elf | learned_blend_at_fp_0 | 179066 | 163841 | 90.60% | 0 | 0.00 | 1828.42 | 0.000 | 95.07% | 95.09% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 18416 | 20479 | 88.81% | 0 | 0.00 | 14627.24 | 0.000 | 94.08% | 94.70% | `{"filegroups/config": 0.9997701644897461, "filetypes/package.json": 0.9980536699295044, "general": 0.9986539483070374}` |
| filetypes/shell | learned_blend_at_fp_0 | 14317 | 58949 | 85.35% | 0 | 0.00 | 5081.78 | 0.000 | 92.10% | 97.14% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 37084 | 20747 | 84.08% | 0 | 0.00 | 14438.31 | 0.000 | 91.35% | 89.79% | `{"filegroups/documents": 0.9975226521492004, "filetypes/xls": 0.9867926836013794, "general": 0.9995529055595398}` |
| filetypes/tar | joint_or_at_fp_0 | 31066 | 22449 | 78.34% | 0 | 0.00 | 13343.72 | 0.000 | 87.85% | 87.42% | `{"filetypes/tar": 0.9982911944389343, "general": 0.9975740909576416}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2724 | 87288 | 73.42% | 0 | 0.00 | 3431.95 | 0.000 | 84.67% | 99.20% | `{"filetypes/python-bytecode": 0.9989191293716431, "general": 0.9844789505004883}` |
| filetypes/clojure | joint_or_at_fp_0 | 121 | 5189 | 71.90% | 0 | 0.00 | 57715.70 | 0.000 | 83.65% | 99.36% | `{"general": 0.020301494747400284}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 64 | 448 | 71.88% | 0 | 0.00 | 666459.48 | 0.000 | 83.64% | 96.48% | `{"filetypes/chrome-manifest": 0.9250487089157104}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10641 | 1798 | 70.44% | 0 | 0.00 | 166475.97 | 0.000 | 82.66% | 74.72% | `{"general": 0.9948397874832153}` |
| filetypes/crx | learned_blend_at_fp_0 | 643 | 79 | 64.54% | 0 | 0.00 | 3721067.61 | 0.000 | 78.45% | 68.42% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 2584 | 11581 | 63.82% | 0 | 0.00 | 25864.30 | 0.000 | 77.91% | 93.40% | `{"filegroups/native": 0.9987778067588806, "filetypes/macho": 0.995280921459198, "general": 0.9831417202949524}` |
| filetypes/perl | learned_blend_at_fp_0 | 316 | 39244 | 62.97% | 0 | 0.00 | 7633.31 | 0.000 | 77.28% | 99.70% | `{}` |
| filetypes/javascript | joint_or_at_fp_0 | 117620 | 582691 | 61.37% | 0 | 0.00 | 514.12 | 0.000 | 76.06% | 93.51% | `{"filegroups/scripts": 0.9993817806243896, "filetypes/javascript": 0.9740317463874817, "general": 0.9994640946388245}` |
| filetypes/java_class | joint_or_at_fp_0 | 1638 | 704991 | 61.11% | 0 | 0.00 | 424.93 | 0.000 | 75.86% | 99.91% | `{"filetypes/java_class": 0.972117006778717, "general": 0.9854030013084412}` |
| filetypes/powershell | joint_or_at_fp_0 | 5236 | 2370 | 55.81% | 0 | 0.00 | 126322.35 | 0.000 | 71.64% | 69.58% | `{"filegroups/scripts": 0.9985805749893188, "filetypes/powershell": 0.9950449466705322, "general": 0.9980418086051941}` |
| filetypes/lnk | joint_or_at_fp_0 | 4347 | 1055 | 55.58% | 0 | 0.00 | 283552.89 | 0.000 | 71.45% | 64.25% | `{"filetypes/lnk": 0.9943863153457642, "general": 0.9990662932395935}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32587 | 51272 | 53.62% | 0 | 0.00 | 5842.65 | 0.000 | 69.81% | 81.98% | `{"filegroups/source": 0.8878219127655029, "filetypes/kotlin": 0.8020543456077576, "general": 0.9644496440887451}` |
| filetypes/ruby | joint_or_at_fp_0 | 118 | 24970 | 48.31% | 0 | 0.00 | 11996.61 | 0.000 | 65.14% | 99.76% | `{"filegroups/scripts": 0.9955379962921143, "filetypes/ruby": 0.9998736381530762, "general": 0.9734157919883728}` |
| filetypes/docx | joint_or_at_fp_0 | 4759 | 433 | 47.68% | 0 | 0.00 | 689467.22 | 0.000 | 64.57% | 52.04% | `{"filegroups/documents": 0.9979186654090881, "filetypes/docx": 0.9876461625099182, "general": 0.9829313158988953}` |
| filetypes/jar | learned_blend_at_fp_0 | 3402 | 3743 | 47.38% | 0 | 0.00 | 80003.57 | 0.000 | 64.30% | 74.95% | `{}` |
| filetypes/doc | calibrate_inherited | 32643 | 76 | 46.46% | 0 | 0.00 | 3865076.67 | 0.000 | 63.45% | 46.59% | `{"filegroups/documents": 0.9985501170158386, "general": 0.9998229742050171}` |
| filetypes/php | joint_or_at_fp_0 | 4811 | 145642 | 46.00% | 0 | 0.00 | 2056.89 | 0.000 | 63.01% | 98.27% | `{"filegroups/scripts": 0.998264729976654, "filetypes/php": 0.998719334602356, "general": 0.9766716361045837}` |
| filetypes/ole | joint_or_at_fp_0 | 6892 | 6219 | 45.59% | 0 | 0.00 | 48159.04 | 0.000 | 62.63% | 71.40% | `{"filegroups/documents": 0.9971538782119751, "filetypes/ole": 0.9978785514831543, "general": 0.9993857145309448}` |
| filetypes/msi | joint_or_at_fp_0 | 5307 | 172 | 43.51% | 0 | 0.00 | 1726624.81 | 0.000 | 60.64% | 45.28% | `{"filetypes/msi": 0.9261299967765808, "general": 0.9945985078811646}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18299 | 43.30% | 0 | 0.00 | 16369.68 | 0.000 | 60.43% | 99.70% | `{"filegroups/scripts": 0.9782118797302246, "filetypes/lua": 0.9987921118736267, "general": 0.97865229845047}` |
| filetypes/vbs | joint_or_at_fp_0 | 11088 | 3293 | 41.61% | 0 | 0.00 | 90931.37 | 0.000 | 58.77% | 54.98% | `{"filetypes/vbs": 0.9825754165649414, "general": 0.9964069724082947}` |
| filetypes/python | joint_or_at_fp_0 | 19388 | 182351 | 39.73% | 0 | 0.00 | 1642.82 | 0.000 | 56.86% | 94.21% | `{"filegroups/scripts": 0.9993232488632202, "filetypes/python": 0.9998348951339722, "general": 0.9986805319786072}` |
| filetypes/pe | learned_blend_at_fp_0 | 1325881 | 159682 | 36.30% | 0 | 0.00 | 1876.04 | 0.000 | 53.27% | 43.15% | `{}` |
