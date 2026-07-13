# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2269663951`
- Rows: 13792064 (2654811 malware, 11137253 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 831 | 98.06% | 0 | 0.00 | 359848.25 | 0.000 | 99.02% | 98.29% | `{"filegroups/documents": 0.018222352489829063, "filetypes/rtf": 0.08900821208953857}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.86% | 0 | 0.00 | 18783.79 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9956018924713135}` |
| filetypes/gem | joint_or_at_fp_0 | 882 | 2419 | 93.54% | 0 | 0.00 | 123765.11 | 0.000 | 96.66% | 98.27% | `{"filetypes/gem": 0.6460350751876831}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 468 | 93.10% | 0 | 0.00 | 638069.37 | 0.000 | 96.43% | 99.24% | `{"filetypes/applescript": 0.810309648513794}` |
| filetypes/asar | joint_or_at_fp_0 | 182 | 92 | 90.66% | 0 | 0.00 | 3203786.32 | 0.000 | 95.10% | 93.80% | `{"filetypes/asar": 0.8254848718643188, "general": 0.6711981892585754}` |
| filetypes/elf | joint_or_at_fp_0 | 191551 | 466024 | 90.45% | 0 | 0.00 | 642.83 | 0.000 | 94.99% | 97.22% | `{"filegroups/native": 0.9653680324554443, "filetypes/elf": 0.999664306640625, "general": 0.9905263185501099}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87524 | 30767 | 87.65% | 0 | 0.00 | 9736.36 | 0.000 | 93.42% | 90.86% | `{"filetypes/ole_doc": 0.9889227151870728}` |
| filetypes/package.json | joint_or_at_fp_0 | 20379 | 48410 | 82.51% | 0 | 0.00 | 6188.06 | 0.000 | 90.42% | 94.82% | `{"filegroups/config": 0.9997947812080383, "filetypes/package.json": 0.9978846907615662, "general": 0.9934601187705994}` |
| filetypes/macho | joint_or_at_fp_0 | 2811 | 21964 | 75.70% | 0 | 0.00 | 13638.35 | 0.000 | 86.17% | 97.24% | `{"filegroups/native": 0.8221607208251953, "filetypes/macho": 0.9700431227684021, "general": 0.9610883593559265}` |
| filetypes/tar | filetype_only_at_fp_0 | 34031 | 62892 | 73.84% | 0 | 0.00 | 4763.18 | 0.000 | 84.95% | 90.81% | `{"filetypes/tar": 0.9980213642120361}` |
| filetypes/scala | calibrate_inherited | 3 | 47161 | 66.67% | 0 | 0.00 | 6351.94 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9544550592865771, "general": 0.9991108880571773}` |
| filetypes/vbs | joint_or_at_fp_0 | 12223 | 3566 | 66.51% | 0 | 0.00 | 83972.92 | 0.000 | 79.89% | 74.08% | `{"filetypes/vbs": 0.9498981237411499, "general": 0.9934083223342896}` |
| filetypes/lnk | joint_or_at_fp_0 | 4627 | 1070 | 66.16% | 0 | 0.00 | 279583.41 | 0.000 | 79.63% | 72.51% | `{"filetypes/lnk": 0.9944460391998291, "general": 0.9978243112564087}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3498 | 765821 | 65.27% | 0 | 0.00 | 391.18 | 0.000 | 78.98% | 99.84% | `{"filetypes/python_bytecode": 0.9996715784072876, "general": 0.9802015423774719}` |
| filetypes/powershell | joint_or_at_fp_0 | 5977 | 4583 | 64.56% | 0 | 0.00 | 65344.83 | 0.000 | 78.47% | 79.94% | `{"filegroups/scripts": 0.9906123280525208, "filetypes/powershell": 0.9478875994682312, "general": 0.9953655004501343}` |
| filetypes/shell | joint_or_at_fp_0 | 17975 | 133004 | 61.34% | 0 | 0.00 | 2252.34 | 0.000 | 76.04% | 95.40% | `{"filegroups/scripts": 0.9912277460098267, "filetypes/shell": 0.9914147257804871, "general": 0.9945436716079712}` |
| filetypes/npm | joint_or_at_fp_0 | 4338 | 5329 | 58.99% | 0 | 0.00 | 56199.86 | 0.000 | 74.21% | 81.60% | `{"filetypes/npm": 0.9892116785049438}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32379 | 73059 | 56.42% | 0 | 0.00 | 4100.34 | 0.000 | 72.14% | 86.62% | `{"filegroups/source": 0.5308534502983093, "filetypes/kotlin": 0.27091148495674133, "general": 0.9967122077941895}` |
| filetypes/vsix | joint_or_at_fp_0 | 95 | 2782 | 55.79% | 0 | 0.00 | 107624.73 | 0.000 | 71.62% | 98.54% | `{"filetypes/vsix": 0.9378865957260132}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 69004 | 53.75% | 0 | 0.00 | 4341.30 | 0.000 | 69.92% | 99.73% | `{"filegroups/scripts": 0.9847646951675415, "filetypes/perl": 0.9974864721298218, "general": 0.9895265102386475}` |
| filetypes/whl | joint_or_at_fp_0 | 3484 | 6035 | 52.81% | 0 | 0.00 | 49626.99 | 0.000 | 69.12% | 82.73% | `{"filetypes/whl": 0.9951545000076294, "general": 0.9677857160568237}` |
| filetypes/python | joint_or_at_fp_0 | 23112 | 543578 | 51.06% | 0 | 0.00 | 551.11 | 0.000 | 67.61% | 98.00% | `{"filegroups/scripts": 0.9936250448226929, "filetypes/python": 0.9881475567817688, "general": 0.9942303895950317}` |
| filetypes/pe | joint_or_at_fp_0 | 1372364 | 195921 | 48.25% | 0 | 0.00 | 1529.04 | 0.000 | 65.09% | 54.72% | `{"filegroups/native": 0.999112069606781, "filetypes/pe": 0.9982747435569763, "general": 0.999631404876709}` |
| filetypes/php | joint_or_at_fp_0 | 6063 | 560315 | 47.57% | 0 | 0.00 | 534.65 | 0.000 | 64.47% | 99.44% | `{"filegroups/scripts": 0.9908904433250427, "filetypes/php": 0.8956148624420166, "general": 0.9976130723953247}` |
| filetypes/ruby | joint_or_at_fp_0 | 398 | 173167 | 42.71% | 0 | 0.00 | 1729.95 | 0.000 | 59.86% | 99.87% | `{"filegroups/scripts": 0.9837116599082947, "filetypes/ruby": 0.9963740706443787, "general": 0.9802253246307373}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 106 | 946 | 40.57% | 0 | 0.00 | 316172.72 | 0.000 | 57.72% | 94.01% | `{"filetypes/chrome_manifest": 0.6136806011199951}` |
| filetypes/registry | joint_or_at_fp_0 | 623 | 128415 | 38.36% | 0 | 0.00 | 2332.83 | 0.000 | 55.45% | 99.70% | `{"filetypes/registry": 0.9999405145645142, "general": 0.9617170095443726}` |
| filetypes/swift | calibrate_inherited | 69 | 42490 | 37.68% | 0 | 0.00 | 7050.19 | 0.000 | 54.74% | 99.90% | `{"filegroups/source": 0.9544550592865771, "general": 0.9991108880571773}` |
| filetypes/7z | calibrate_inherited | 8973 | 200 | 35.71% | 0 | 0.00 | 1486703.92 | 0.000 | 52.62% | 37.11% | `{"general": 0.9991108880571773}` |
| filetypes/zip | joint_or_at_fp_0 | 107012 | 26213 | 35.45% | 0 | 0.00 | 11427.77 | 0.000 | 52.34% | 48.15% | `{"filetypes/zip": 0.9963969588279724, "general": 0.9985396265983582}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 831 | 98.06% | 0 | 0.00 | 359848.25 | 0.000 | 99.02% | 98.29% | `{"filegroups/documents": 0.018222352489829063, "filetypes/rtf": 0.08900821208953857}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15947 | 96.86% | 0 | 0.00 | 18783.79 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9956018924713135}` |
| filetypes/gem | joint_or_at_fp_0 | 882 | 2419 | 93.54% | 0 | 0.00 | 123765.11 | 0.000 | 96.66% | 98.27% | `{"filetypes/gem": 0.6460350751876831}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 468 | 93.10% | 0 | 0.00 | 638069.37 | 0.000 | 96.43% | 99.24% | `{"filetypes/applescript": 0.810309648513794}` |
| filetypes/asar | joint_or_at_fp_0 | 182 | 92 | 90.66% | 0 | 0.00 | 3203786.32 | 0.000 | 95.10% | 93.80% | `{"filetypes/asar": 0.8254848718643188, "general": 0.6711981892585754}` |
| filetypes/elf | joint_or_at_fp_0 | 191551 | 466024 | 90.45% | 0 | 0.00 | 642.83 | 0.000 | 94.99% | 97.22% | `{"filegroups/native": 0.9653680324554443, "filetypes/elf": 0.999664306640625, "general": 0.9905263185501099}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87524 | 30767 | 87.65% | 0 | 0.00 | 9736.36 | 0.000 | 93.42% | 90.86% | `{"filetypes/ole_doc": 0.9889227151870728}` |
| filetypes/package.json | joint_or_at_fp_0 | 20379 | 48410 | 82.51% | 0 | 0.00 | 6188.06 | 0.000 | 90.42% | 94.82% | `{"filegroups/config": 0.9997947812080383, "filetypes/package.json": 0.9978846907615662, "general": 0.9934601187705994}` |
| filetypes/macho | joint_or_at_fp_0 | 2811 | 21964 | 75.70% | 0 | 0.00 | 13638.35 | 0.000 | 86.17% | 97.24% | `{"filegroups/native": 0.8221607208251953, "filetypes/macho": 0.9700431227684021, "general": 0.9610883593559265}` |
| filetypes/tar | filetype_only_at_fp_0 | 34031 | 62892 | 73.84% | 0 | 0.00 | 4763.18 | 0.000 | 84.95% | 90.81% | `{"filetypes/tar": 0.9980213642120361}` |
| filetypes/scala | calibrate_inherited | 3 | 47161 | 66.67% | 0 | 0.00 | 6351.94 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9538112511565212, "general": 0.9988694838427258}` |
| filetypes/vbs | joint_or_at_fp_0 | 12223 | 3566 | 66.51% | 0 | 0.00 | 83972.92 | 0.000 | 79.89% | 74.08% | `{"filetypes/vbs": 0.9498981237411499, "general": 0.9934083223342896}` |
| filetypes/lnk | joint_or_at_fp_0 | 4627 | 1070 | 66.16% | 0 | 0.00 | 279583.41 | 0.000 | 79.63% | 72.51% | `{"filetypes/lnk": 0.9944460391998291, "general": 0.9978243112564087}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3498 | 765821 | 65.27% | 0 | 0.00 | 391.18 | 0.000 | 78.98% | 99.84% | `{"filetypes/python_bytecode": 0.9996715784072876, "general": 0.9802015423774719}` |
| filetypes/powershell | joint_or_at_fp_0 | 5977 | 4583 | 64.56% | 0 | 0.00 | 65344.83 | 0.000 | 78.47% | 79.94% | `{"filegroups/scripts": 0.9906123280525208, "filetypes/powershell": 0.9478875994682312, "general": 0.9953655004501343}` |
| filetypes/shell | joint_or_at_fp_0 | 17975 | 133004 | 61.34% | 0 | 0.00 | 2252.34 | 0.000 | 76.04% | 95.40% | `{"filegroups/scripts": 0.9912277460098267, "filetypes/shell": 0.9914147257804871, "general": 0.9945436716079712}` |
| filetypes/npm | joint_or_at_fp_0 | 4338 | 5329 | 58.99% | 0 | 0.00 | 56199.86 | 0.000 | 74.21% | 81.60% | `{"filetypes/npm": 0.9892116785049438}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32379 | 73059 | 56.42% | 0 | 0.00 | 4100.34 | 0.000 | 72.14% | 86.62% | `{"filegroups/source": 0.5308534502983093, "filetypes/kotlin": 0.27091148495674133, "general": 0.9967122077941895}` |
| filetypes/vsix | joint_or_at_fp_0 | 95 | 2782 | 55.79% | 0 | 0.00 | 107624.73 | 0.000 | 71.62% | 98.54% | `{"filetypes/vsix": 0.9378865957260132}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 69004 | 53.75% | 0 | 0.00 | 4341.30 | 0.000 | 69.92% | 99.73% | `{"filegroups/scripts": 0.9847646951675415, "filetypes/perl": 0.9974864721298218, "general": 0.9895265102386475}` |
| filetypes/whl | joint_or_at_fp_0 | 3484 | 6035 | 52.81% | 0 | 0.00 | 49626.99 | 0.000 | 69.12% | 82.73% | `{"filetypes/whl": 0.9951545000076294, "general": 0.9677857160568237}` |
| filetypes/python | joint_or_at_fp_0 | 23112 | 543578 | 51.06% | 0 | 0.00 | 551.11 | 0.000 | 67.61% | 98.00% | `{"filegroups/scripts": 0.9936250448226929, "filetypes/python": 0.9881475567817688, "general": 0.9942303895950317}` |
| filetypes/pe | joint_or_at_fp_0 | 1372364 | 195921 | 48.25% | 0 | 0.00 | 1529.04 | 0.000 | 65.09% | 54.72% | `{"filegroups/native": 0.999112069606781, "filetypes/pe": 0.9982747435569763, "general": 0.999631404876709}` |
| filetypes/php | joint_or_at_fp_0 | 6063 | 560315 | 47.57% | 0 | 0.00 | 534.65 | 0.000 | 64.47% | 99.44% | `{"filegroups/scripts": 0.9908904433250427, "filetypes/php": 0.8956148624420166, "general": 0.9976130723953247}` |
| filetypes/ruby | joint_or_at_fp_0 | 398 | 173167 | 42.71% | 0 | 0.00 | 1729.95 | 0.000 | 59.86% | 99.87% | `{"filegroups/scripts": 0.9837116599082947, "filetypes/ruby": 0.9963740706443787, "general": 0.9802253246307373}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 106 | 946 | 40.57% | 0 | 0.00 | 316172.72 | 0.000 | 57.72% | 94.01% | `{"filetypes/chrome_manifest": 0.6136806011199951}` |
| filetypes/zst | calibrate_inherited | 10473 | 182984 | 39.61% | 0 | 0.00 | 1637.14 | 0.000 | 56.74% | 96.73% | `{"general": 0.9988694838427258}` |
| filetypes/7z | calibrate_inherited | 8973 | 200 | 39.60% | 0 | 0.00 | 1486703.92 | 0.000 | 56.73% | 40.91% | `{"general": 0.9988694838427258}` |
| filetypes/registry | joint_or_at_fp_0 | 623 | 128415 | 38.36% | 0 | 0.00 | 2332.83 | 0.000 | 55.45% | 99.70% | `{"filetypes/registry": 0.9999405145645142, "general": 0.9617170095443726}` |
| filetypes/swift | calibrate_inherited | 69 | 42490 | 37.68% | 0 | 0.00 | 7050.19 | 0.000 | 54.74% | 99.90% | `{"filegroups/source": 0.9538112511565212, "general": 0.9988694838427258}` |
