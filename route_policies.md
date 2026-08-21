# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3084319633`
- Rows: 17074459 (2672405 malware, 14402054 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 878 | 97.87% | 0 | 0.00 | 340618.15 | 0.000 | 98.93% | 98.14% | `{"filegroups/documents": 0.9729885458946228, "filetypes/rtf": 0.7075628042221069}` |
| filetypes/html | joint_or_at_fp_0 | 262 | 67217 | 95.42% | 0 | 0.00 | 4456.71 | 0.000 | 97.66% | 99.98% | `{"filetypes/html": 0.999888002872467, "general": 0.9100732207298279}` |
| filetypes/asar | joint_or_at_fp_0 | 184 | 221 | 94.57% | 0 | 0.00 | 1346388.96 | 0.000 | 97.21% | 97.53% | `{"filetypes/asar": 0.848507285118103, "general": 0.8347011208534241}` |
| filetypes/gem | joint_or_at_fp_0 | 927 | 3468 | 92.34% | 0 | 0.00 | 86344.83 | 0.000 | 96.02% | 98.38% | `{"filetypes/gem": 0.9057793617248535, "general": 0.9941101670265198}` |
| filetypes/applescript | joint_or_at_fp_0 | 57 | 527 | 91.23% | 0 | 0.00 | 566837.53 | 0.000 | 95.41% | 99.14% | `{"general": 0.9106630086898804}` |
| filetypes/7z | joint_or_at_fp_0 | 9003 | 297 | 90.89% | 0 | 0.00 | 1003594.11 | 0.000 | 95.23% | 91.18% | `{"filetypes/7z": 0.8420525789260864, "general": 0.9790073037147522}` |
| filetypes/elf | joint_or_at_fp_0 | 195272 | 781175 | 88.04% | 0 | 0.00 | 383.49 | 0.000 | 93.64% | 97.61% | `{"filegroups/native": 0.9940590858459473, "filetypes/elf": 0.9997561573982239, "general": 0.9920714497566223}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16200 | 87.24% | 0 | 0.00 | 18490.46 | 0.000 | 93.19% | 94.95% | `{"filetypes/pkg_info": 0.9975733757019043, "general": 0.9934224486351013}` |
| filetypes/tar | joint_or_at_fp_0 | 34299 | 73482 | 72.45% | 0 | 0.00 | 4076.74 | 0.000 | 84.02% | 91.23% | `{"filetypes/tar": 0.9985238313674927, "general": 0.9916430115699768}` |
| filetypes/package.json | joint_or_at_fp_0 | 20655 | 61789 | 58.72% | 0 | 0.00 | 4848.21 | 0.000 | 73.99% | 89.66% | `{"filegroups/config": 0.9999760389328003, "filetypes/package.json": 0.999846875667572, "general": 0.9987754821777344}` |
| filetypes/macho | joint_or_at_fp_0 | 2823 | 30746 | 55.47% | 0 | 0.00 | 9743.01 | 0.000 | 71.36% | 96.26% | `{"filegroups/native": 0.9745824933052063, "filetypes/macho": 0.9914526343345642, "general": 0.9967143535614014}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 32369 | 83237 | 52.65% | 0 | 0.00 | 3598.97 | 0.000 | 68.98% | 86.74% | `{}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44519 | 52.17% | 0 | 0.00 | 6728.88 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.07100141048431396}` |
| filetypes/powershell | joint_or_at_fp_0 | 6062 | 5233 | 50.66% | 0 | 0.00 | 57230.56 | 0.000 | 67.25% | 73.52% | `{"filegroups/scripts": 0.9979398250579834, "filetypes/powershell": 0.996994137763977, "general": 0.9917295575141907}` |
| filetypes/shell | joint_or_at_fp_0 | 18552 | 157467 | 50.24% | 0 | 0.00 | 1902.43 | 0.000 | 66.88% | 94.76% | `{"filegroups/scripts": 0.9995417594909668, "filetypes/shell": 0.9983620047569275, "general": 0.9958887100219727}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3509 | 1012833 | 48.82% | 0 | 0.00 | 295.78 | 0.000 | 65.61% | 99.82% | `{"filetypes/python_bytecode": 0.9999899864196777, "general": 0.9855927228927612}` |
| filetypes/dmg | joint_or_at_fp_0 | 61 | 241 | 47.54% | 0 | 0.00 | 1235348.58 | 0.000 | 64.44% | 89.40% | `{"filetypes/dmg": 0.8415968418121338, "general": 0.9937610030174255}` |
| filetypes/perl | joint_or_at_fp_0 | 398 | 76113 | 47.49% | 0 | 0.00 | 3935.82 | 0.000 | 64.40% | 99.73% | `{"filetypes/perl": 0.9997100830078125, "general": 0.9753663539886475}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87662 | 31240 | 47.20% | 0 | 0.00 | 9588.95 | 0.000 | 64.13% | 61.07% | `{"filetypes/ole_doc": 0.9992230534553528, "general": 0.9988775849342346}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 75 | 262 | 46.67% | 0 | 0.00 | 1136897.18 | 0.000 | 63.64% | 88.13% | `{"filetypes/python_sdist": 0.943884015083313, "general": 0.9294898509979248}` |
| filetypes/python | joint_or_at_fp_0 | 23143 | 632725 | 44.79% | 0 | 0.00 | 473.46 | 0.000 | 61.87% | 98.05% | `{"filegroups/scripts": 0.9990708231925964, "filetypes/python": 0.994676411151886, "general": 0.9950885772705078}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27664 | 43.40% | 0 | 0.00 | 10828.41 | 0.000 | 60.53% | 99.78% | `{"filetypes/lua": 0.8212938904762268, "general": 0.9778561592102051}` |
| filetypes/javascript | joint_or_at_fp_0 | 141200 | 1596758 | 41.20% | 0 | 0.00 | 187.61 | 0.000 | 58.36% | 95.22% | `{"filegroups/scripts": 0.9990209937095642, "filetypes/javascript": 0.9987907409667969, "general": 0.9980453848838806}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9256 | 40.00% | 0 | 0.00 | 32360.06 | 0.000 | 57.14% | 99.30% | `{"filetypes/clojure": 0.9961665272712708, "general": 0.03630353882908821}` |
| filetypes/npm | joint_or_at_fp_0 | 5947 | 7910 | 37.83% | 0 | 0.00 | 37865.55 | 0.000 | 54.90% | 73.32% | `{"filetypes/npm": 0.9965786337852478, "general": 0.9992344975471497}` |
| filetypes/pdf | joint_or_at_fp_0 | 178640 | 29360 | 37.82% | 0 | 0.00 | 10202.93 | 0.000 | 54.88% | 46.60% | `{"filegroups/documents": 0.9985247254371643, "filetypes/pdf": 0.9979481101036072, "general": 0.9887642860412598}` |
| filetypes/php | joint_or_at_fp_0 | 6611 | 611846 | 35.55% | 0 | 0.00 | 489.62 | 0.000 | 52.45% | 99.31% | `{"filegroups/scripts": 0.998884379863739, "filetypes/php": 0.9993404746055603, "general": 0.9843087196350098}` |
| filetypes/pe | joint_or_at_fp_0 | 1376835 | 227568 | 35.33% | 0 | 0.00 | 1316.40 | 0.000 | 52.21% | 44.50% | `{"filegroups/native": 0.9997499585151672, "filetypes/pe": 0.9996539354324341, "general": 0.9996278882026672}` |
| filetypes/lnk | joint_or_at_fp_0 | 4685 | 1119 | 35.05% | 0 | 0.00 | 267357.09 | 0.000 | 51.90% | 47.57% | `{"filetypes/lnk": 0.9938345551490784, "general": 0.9984873533248901}` |
| filetypes/zst | calibrate_inherited | 10473 | 325114 | 32.92% | 0 | 0.00 | 921.44 | 0.000 | 49.54% | 97.91% | `{"general": 0.9994064770465989}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 878 | 97.87% | 0 | 0.00 | 340618.15 | 0.000 | 98.93% | 98.14% | `{"filegroups/documents": 0.9729885458946228, "filetypes/rtf": 0.7075628042221069}` |
| filetypes/html | joint_or_at_fp_0 | 262 | 67217 | 95.42% | 0 | 0.00 | 4456.71 | 0.000 | 97.66% | 99.98% | `{"filetypes/html": 0.999888002872467, "general": 0.9100732207298279}` |
| filetypes/asar | joint_or_at_fp_0 | 184 | 221 | 94.57% | 0 | 0.00 | 1346388.96 | 0.000 | 97.21% | 97.53% | `{"filetypes/asar": 0.848507285118103, "general": 0.8347011208534241}` |
| filetypes/gem | joint_or_at_fp_0 | 927 | 3468 | 92.34% | 0 | 0.00 | 86344.83 | 0.000 | 96.02% | 98.38% | `{"filetypes/gem": 0.9057793617248535, "general": 0.9941101670265198}` |
| filetypes/applescript | joint_or_at_fp_0 | 57 | 527 | 91.23% | 0 | 0.00 | 566837.53 | 0.000 | 95.41% | 99.14% | `{"general": 0.9106630086898804}` |
| filetypes/7z | joint_or_at_fp_0 | 9003 | 297 | 90.89% | 0 | 0.00 | 1003594.11 | 0.000 | 95.23% | 91.18% | `{"filetypes/7z": 0.8420525789260864, "general": 0.9790073037147522}` |
| filetypes/elf | joint_or_at_fp_0 | 195272 | 781175 | 88.04% | 0 | 0.00 | 383.49 | 0.000 | 93.64% | 97.61% | `{"filegroups/native": 0.9940590858459473, "filetypes/elf": 0.9997561573982239, "general": 0.9920714497566223}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16200 | 87.24% | 0 | 0.00 | 18490.46 | 0.000 | 93.19% | 94.95% | `{"filetypes/pkg_info": 0.9975733757019043, "general": 0.9934224486351013}` |
| filetypes/tar | joint_or_at_fp_0 | 34299 | 73482 | 72.45% | 0 | 0.00 | 4076.74 | 0.000 | 84.02% | 91.23% | `{"filetypes/tar": 0.9985238313674927, "general": 0.9916430115699768}` |
| filetypes/package.json | joint_or_at_fp_0 | 20655 | 61789 | 58.72% | 0 | 0.00 | 4848.21 | 0.000 | 73.99% | 89.66% | `{"filegroups/config": 0.9999760389328003, "filetypes/package.json": 0.999846875667572, "general": 0.9987754821777344}` |
| filetypes/macho | joint_or_at_fp_0 | 2823 | 30746 | 55.47% | 0 | 0.00 | 9743.01 | 0.000 | 71.36% | 96.26% | `{"filegroups/native": 0.9745824933052063, "filetypes/macho": 0.9914526343345642, "general": 0.9967143535614014}` |
| filetypes/kotlin | learned_blend_at_fp_3 | 32369 | 83237 | 52.65% | 0 | 0.00 | 3598.97 | 0.000 | 68.98% | 86.74% | `{}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44519 | 52.17% | 0 | 0.00 | 6728.88 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.07100141048431396}` |
| filetypes/powershell | joint_or_at_fp_0 | 6062 | 5233 | 50.66% | 0 | 0.00 | 57230.56 | 0.000 | 67.25% | 73.52% | `{"filegroups/scripts": 0.9979398250579834, "filetypes/powershell": 0.996994137763977, "general": 0.9917295575141907}` |
| filetypes/shell | joint_or_at_fp_0 | 18552 | 157467 | 50.24% | 0 | 0.00 | 1902.43 | 0.000 | 66.88% | 94.76% | `{"filegroups/scripts": 0.9995417594909668, "filetypes/shell": 0.9983620047569275, "general": 0.9958887100219727}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3509 | 1012833 | 48.82% | 0 | 0.00 | 295.78 | 0.000 | 65.61% | 99.82% | `{"filetypes/python_bytecode": 0.9999899864196777, "general": 0.9855927228927612}` |
| filetypes/dmg | joint_or_at_fp_0 | 61 | 241 | 47.54% | 0 | 0.00 | 1235348.58 | 0.000 | 64.44% | 89.40% | `{"filetypes/dmg": 0.8415968418121338, "general": 0.9937610030174255}` |
| filetypes/perl | joint_or_at_fp_0 | 398 | 76113 | 47.49% | 0 | 0.00 | 3935.82 | 0.000 | 64.40% | 99.73% | `{"filetypes/perl": 0.9997100830078125, "general": 0.9753663539886475}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87662 | 31240 | 47.20% | 0 | 0.00 | 9588.95 | 0.000 | 64.13% | 61.07% | `{"filetypes/ole_doc": 0.9992230534553528, "general": 0.9988775849342346}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 75 | 262 | 46.67% | 0 | 0.00 | 1136897.18 | 0.000 | 63.64% | 88.13% | `{"filetypes/python_sdist": 0.943884015083313, "general": 0.9294898509979248}` |
| filetypes/python | joint_or_at_fp_0 | 23143 | 632725 | 44.79% | 0 | 0.00 | 473.46 | 0.000 | 61.87% | 98.05% | `{"filegroups/scripts": 0.9990708231925964, "filetypes/python": 0.994676411151886, "general": 0.9950885772705078}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27664 | 43.40% | 0 | 0.00 | 10828.41 | 0.000 | 60.53% | 99.78% | `{"filetypes/lua": 0.8212938904762268, "general": 0.9778561592102051}` |
| filetypes/zst | calibrate_inherited | 10473 | 325114 | 42.55% | 0 | 0.00 | 921.44 | 0.000 | 59.70% | 98.21% | `{"general": 0.99928453796608}` |
| filetypes/javascript | joint_or_at_fp_0 | 141200 | 1596758 | 41.20% | 0 | 0.00 | 187.61 | 0.000 | 58.36% | 95.22% | `{"filegroups/scripts": 0.9990209937095642, "filetypes/javascript": 0.9987907409667969, "general": 0.9980453848838806}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9256 | 40.00% | 0 | 0.00 | 32360.06 | 0.000 | 57.14% | 99.30% | `{"filetypes/clojure": 0.9961665272712708, "general": 0.03630353882908821}` |
| filetypes/npm | joint_or_at_fp_0 | 5947 | 7910 | 37.83% | 0 | 0.00 | 37865.55 | 0.000 | 54.90% | 73.32% | `{"filetypes/npm": 0.9965786337852478, "general": 0.9992344975471497}` |
| filetypes/pdf | joint_or_at_fp_0 | 178640 | 29360 | 37.82% | 0 | 0.00 | 10202.93 | 0.000 | 54.88% | 46.60% | `{"filegroups/documents": 0.9985247254371643, "filetypes/pdf": 0.9979481101036072, "general": 0.9887642860412598}` |
| filetypes/php | joint_or_at_fp_0 | 6611 | 611846 | 35.55% | 0 | 0.00 | 489.62 | 0.000 | 52.45% | 99.31% | `{"filegroups/scripts": 0.998884379863739, "filetypes/php": 0.9993404746055603, "general": 0.9843087196350098}` |
| filetypes/pe | joint_or_at_fp_0 | 1376835 | 227568 | 35.33% | 0 | 0.00 | 1316.40 | 0.000 | 52.21% | 44.50% | `{"filegroups/native": 0.9997499585151672, "filetypes/pe": 0.9996539354324341, "general": 0.9996278882026672}` |
| filetypes/lnk | joint_or_at_fp_0 | 4685 | 1119 | 35.05% | 0 | 0.00 | 267357.09 | 0.000 | 51.90% | 47.57% | `{"filetypes/lnk": 0.9938345551490784, "general": 0.9984873533248901}` |
