# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1685037226`
- Rows: 7416064 (2543560 malware, 4872504 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"general": 0.530778706073761}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.37% | 0 | 0.00 | 577769.77 | 0.000 | 99.18% | 98.50% | `{"filegroups/documents": 0.47177785634994507, "filetypes/rtf": 0.30079102516174316}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 91.02% | 0 | 0.00 | 1671.88 | 0.000 | 95.30% | 95.48% | `{"filegroups/native": 0.9954081177711487, "filetypes/elf": 0.9982566237449646, "general": 0.9776919484138489}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 82.61% | 0 | 0.00 | 14428.57 | 0.000 | 90.48% | 88.79% | `{"filegroups/documents": 0.9980289340019226, "filetypes/xls": 0.9991683959960938, "general": 0.9978118538856506}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 78.86% | 0 | 0.00 | 13046.76 | 0.000 | 88.18% | 90.54% | `{"filegroups/config": 0.9997286200523376, "filetypes/package.json": 0.9998397827148438, "general": 0.99217689037323}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 76.69% | 0 | 0.00 | 133232.58 | 0.000 | 86.81% | 80.75% | `{"filetypes/pkg-info": 0.9949275255203247, "general": 0.9819479584693909}` |
| filetypes/tar | joint_or_at_fp_0 | 31332 | 26900 | 70.60% | 0 | 0.00 | 11135.93 | 0.000 | 82.76% | 84.18% | `{"filetypes/tar": 0.9988242983818054, "general": 0.9971198439598083}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"general": 0.01516978070139885}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/doc | calibrate_inherited | 33092 | 81 | 52.78% | 0 | 0.00 | 3630878.21 | 0.000 | 69.09% | 52.90% | `{"filegroups/documents": 0.9980102845019126, "general": 0.9996674518317141}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 52.70% | 0 | 0.00 | 24332.80 | 0.000 | 69.03% | 91.73% | `{"filegroups/native": 0.9760146737098694, "filetypes/macho": 0.9980702996253967, "general": 0.9595746994018555}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 52.07% | 0 | 0.00 | 1540208.46 | 0.000 | 68.48% | 53.73% | `{"filetypes/msi": 0.9261299967765808, "general": 0.9746996760368347}` |
| filetypes/perl | joint_or_at_fp_0 | 358 | 42499 | 47.49% | 0 | 0.00 | 7048.70 | 0.000 | 64.39% | 99.56% | `{"filegroups/scripts": 0.987190306186676, "general": 0.8967370986938477}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 47.06% | 0 | 0.00 | 1918.69 | 0.000 | 64.01% | 98.23% | `{"filegroups/scripts": 0.99444580078125, "filetypes/php": 0.987824559211731, "general": 0.9004867076873779}` |
| filetypes/python-bytecode | learned_blend_at_fp_0 | 3159 | 194703 | 44.89% | 0 | 0.00 | 1538.60 | 0.000 | 61.96% | 99.12% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 44.75% | 0 | 0.00 | 281157.79 | 0.000 | 61.83% | 55.46% | `{"filetypes/lnk": 0.9920518398284912, "general": 0.9974807500839233}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 43.78% | 0 | 0.00 | 664980.11 | 0.000 | 60.90% | 48.56% | `{"filegroups/documents": 0.9946826100349426, "filetypes/docx": 0.9868107438087463, "general": 0.9837183952331543}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 43.32% | 0 | 0.00 | 73469.86 | 0.000 | 60.45% | 73.75% | `{"filetypes/jar": 0.9532655477523804, "general": 0.9894456267356873}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 42.47% | 0 | 0.00 | 1372.10 | 0.000 | 59.62% | 94.62% | `{"filegroups/scripts": 0.9988719820976257, "filetypes/python": 0.99922776222229, "general": 0.991783082485199}` |
| filetypes/whl | joint_or_at_fp_0 | 202 | 758 | 40.59% | 0 | 0.00 | 394435.39 | 0.000 | 57.75% | 87.50% | `{"filetypes/whl": 0.8871507048606873, "general": 0.9503666162490845}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32997 | 55207 | 38.43% | 0 | 0.00 | 5426.22 | 0.000 | 55.52% | 76.97% | `{"filegroups/source": 0.9971801042556763, "filetypes/kotlin": 0.9960784316062927, "general": 0.8662064671516418}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 34.95% | 0 | 0.00 | 121951.33 | 0.000 | 51.79% | 54.81% | `{"filegroups/scripts": 0.9983980059623718, "filetypes/powershell": 0.9970914125442505, "general": 0.9944437146186829}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 30.61% | 0 | 0.00 | 15932.63 | 0.000 | 46.87% | 99.64% | `{"filegroups/scripts": 0.9849173426628113, "filetypes/lua": 0.9990267753601074, "general": 0.9173932671546936}` |
| filetypes/xlsx | joint_or_at_fp_0 | 59283 | 1861 | 29.60% | 0 | 0.00 | 160844.84 | 0.000 | 45.68% | 31.74% | `{"filegroups/documents": 0.9934386610984802, "filetypes/xlsx": 0.9886250495910645, "general": 0.9901142716407776}` |
| filetypes/ruby | learned_blend_at_fp_0 | 220 | 28744 | 29.55% | 0 | 0.00 | 10421.57 | 0.000 | 45.61% | 99.46% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 141 | 353 | 28.37% | 0 | 0.00 | 845058.51 | 0.000 | 44.20% | 79.55% | `{"filetypes/applescript": 0.747204065322876}` |
| filetypes/zip | joint_or_at_fp_0 | 102558 | 13076 | 28.19% | 0 | 0.00 | 22907.53 | 0.000 | 43.98% | 36.31% | `{"filetypes/zip": 0.9992372989654541, "general": 0.99899822473526}` |
| filetypes/javascript | joint_or_at_fp_0 | 121123 | 643321 | 27.20% | 0 | 0.00 | 465.67 | 0.000 | 42.77% | 88.47% | `{"filegroups/scripts": 0.9989528656005859, "filetypes/javascript": 0.9999535083770752, "general": 0.9987738728523254}` |
| filetypes/java_class | joint_or_at_fp_0 | 1785 | 786063 | 24.59% | 0 | 0.00 | 381.11 | 0.000 | 39.48% | 99.83% | `{"filetypes/java_class": 0.9999946355819702, "general": 0.95779949426651}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 79 | 450 | 24.05% | 0 | 0.00 | 663507.29 | 0.000 | 38.78% | 88.66% | `{"filetypes/chrome-manifest": 0.966305136680603, "general": 0.92038893699646}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"general": 0.530778706073761}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.37% | 0 | 0.00 | 577769.77 | 0.000 | 99.18% | 98.50% | `{"filegroups/documents": 0.47177785634994507, "filetypes/rtf": 0.30079102516174316}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 91.02% | 0 | 0.00 | 1671.88 | 0.000 | 95.30% | 95.48% | `{"filegroups/native": 0.9954081177711487, "filetypes/elf": 0.9982566237449646, "general": 0.9776919484138489}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 82.61% | 0 | 0.00 | 14428.57 | 0.000 | 90.48% | 88.79% | `{"filegroups/documents": 0.9980289340019226, "filetypes/xls": 0.9991683959960938, "general": 0.9978118538856506}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 78.86% | 0 | 0.00 | 13046.76 | 0.000 | 88.18% | 90.54% | `{"filegroups/config": 0.9997286200523376, "filetypes/package.json": 0.9998397827148438, "general": 0.99217689037323}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 76.69% | 0 | 0.00 | 133232.58 | 0.000 | 86.81% | 80.75% | `{"filetypes/pkg-info": 0.9949275255203247, "general": 0.9819479584693909}` |
| filetypes/tar | joint_or_at_fp_0 | 31332 | 26900 | 70.60% | 0 | 0.00 | 11135.93 | 0.000 | 82.76% | 84.18% | `{"filetypes/tar": 0.9988242983818054, "general": 0.9971198439598083}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"general": 0.01516978070139885}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/doc | calibrate_inherited | 33092 | 81 | 53.23% | 0 | 0.00 | 3630878.21 | 0.000 | 69.48% | 53.34% | `{"filegroups/documents": 0.9979929463040805, "general": 0.9992784860547762}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 52.70% | 0 | 0.00 | 24332.80 | 0.000 | 69.03% | 91.73% | `{"filegroups/native": 0.9760146737098694, "filetypes/macho": 0.9980702996253967, "general": 0.9595746994018555}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 52.07% | 0 | 0.00 | 1540208.46 | 0.000 | 68.48% | 53.73% | `{"filetypes/msi": 0.9261299967765808, "general": 0.9746996760368347}` |
| filetypes/perl | joint_or_at_fp_0 | 358 | 42499 | 47.49% | 0 | 0.00 | 7048.70 | 0.000 | 64.39% | 99.56% | `{"filegroups/scripts": 0.987190306186676, "general": 0.8967370986938477}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 47.06% | 0 | 0.00 | 1918.69 | 0.000 | 64.01% | 98.23% | `{"filegroups/scripts": 0.99444580078125, "filetypes/php": 0.987824559211731, "general": 0.9004867076873779}` |
| filetypes/python-bytecode | learned_blend_at_fp_0 | 3159 | 194703 | 44.89% | 0 | 0.00 | 1538.60 | 0.000 | 61.96% | 99.12% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 44.75% | 0 | 0.00 | 281157.79 | 0.000 | 61.83% | 55.46% | `{"filetypes/lnk": 0.9920518398284912, "general": 0.9974807500839233}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 43.78% | 0 | 0.00 | 664980.11 | 0.000 | 60.90% | 48.56% | `{"filegroups/documents": 0.9946826100349426, "filetypes/docx": 0.9868107438087463, "general": 0.9837183952331543}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 43.32% | 0 | 0.00 | 73469.86 | 0.000 | 60.45% | 73.75% | `{"filetypes/jar": 0.9532655477523804, "general": 0.9894456267356873}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 42.47% | 0 | 0.00 | 1372.10 | 0.000 | 59.62% | 94.62% | `{"filegroups/scripts": 0.9988719820976257, "filetypes/python": 0.99922776222229, "general": 0.991783082485199}` |
| filetypes/whl | joint_or_at_fp_0 | 202 | 758 | 40.59% | 0 | 0.00 | 394435.39 | 0.000 | 57.75% | 87.50% | `{"filetypes/whl": 0.8871507048606873, "general": 0.9503666162490845}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32997 | 55207 | 38.43% | 0 | 0.00 | 5426.22 | 0.000 | 55.52% | 76.97% | `{"filegroups/source": 0.9971801042556763, "filetypes/kotlin": 0.9960784316062927, "general": 0.8662064671516418}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 34.95% | 0 | 0.00 | 121951.33 | 0.000 | 51.79% | 54.81% | `{"filegroups/scripts": 0.9983980059623718, "filetypes/powershell": 0.9970914125442505, "general": 0.9944437146186829}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 30.61% | 0 | 0.00 | 15932.63 | 0.000 | 46.87% | 99.64% | `{"filegroups/scripts": 0.9849173426628113, "filetypes/lua": 0.9990267753601074, "general": 0.9173932671546936}` |
| filetypes/xlsx | joint_or_at_fp_0 | 59283 | 1861 | 29.60% | 0 | 0.00 | 160844.84 | 0.000 | 45.68% | 31.74% | `{"filegroups/documents": 0.9934386610984802, "filetypes/xlsx": 0.9886250495910645, "general": 0.9901142716407776}` |
| filetypes/7z | calibrate_inherited | 8281 | 120 | 29.55% | 0 | 0.00 | 2465540.11 | 0.000 | 45.62% | 30.56% | `{"general": 0.9992784860547762}` |
| filetypes/ruby | learned_blend_at_fp_0 | 220 | 28744 | 29.55% | 0 | 0.00 | 10421.57 | 0.000 | 45.61% | 99.46% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 141 | 353 | 28.37% | 0 | 0.00 | 845058.51 | 0.000 | 44.20% | 79.55% | `{"filetypes/applescript": 0.747204065322876}` |
| filetypes/zip | joint_or_at_fp_0 | 102558 | 13076 | 28.19% | 0 | 0.00 | 22907.53 | 0.000 | 43.98% | 36.31% | `{"filetypes/zip": 0.9992372989654541, "general": 0.99899822473526}` |
| filetypes/rar | calibrate_inherited | 20890 | 5 | 28.10% | 0 | 0.00 | 45071972.83 | 0.000 | 43.88% | 28.12% | `{"general": 0.9992784860547762}` |
| filetypes/javascript | joint_or_at_fp_0 | 121123 | 643321 | 27.20% | 0 | 0.00 | 465.67 | 0.000 | 42.77% | 88.47% | `{"filegroups/scripts": 0.9989528656005859, "filetypes/javascript": 0.9999535083770752, "general": 0.9987738728523254}` |
