# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1679491877`
- Rows: 7260408 (2532241 malware, 4728167 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11021 | 100.00% | 0 | 0.00 | 27178.34 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9948320388793945}` |
| filetypes/rtf | learned_blend_at_fp_0 | 5921 | 514 | 98.33% | 0 | 0.00 | 581132.15 | 0.000 | 99.16% | 98.46% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2252 | 95.89% | 0 | 0.00 | 132936.97 | 0.000 | 97.90% | 96.60% | `{"filetypes/pkg-info": 0.9815199971199036, "general": 0.9956156015396118}` |
| filetypes/xls | joint_or_at_fp_0 | 37479 | 20761 | 95.00% | 0 | 0.00 | 14428.57 | 0.000 | 97.43% | 96.78% | `{"filegroups/documents": 0.2136012762784958, "filetypes/xls": 0.7950483560562134}` |
| filetypes/elf | joint_or_at_fp_0 | 180840 | 175951 | 92.03% | 0 | 0.00 | 1702.58 | 0.000 | 95.85% | 95.96% | `{"filegroups/native": 0.9933313727378845, "filetypes/elf": 0.9974352717399597, "general": 0.996862530708313}` |
| filetypes/tar | joint_or_at_fp_0 | 31472 | 26345 | 86.44% | 0 | 0.00 | 11370.51 | 0.000 | 92.73% | 92.62% | `{"filetypes/tar": 0.990632176399231, "general": 0.996157169342041}` |
| filetypes/package.json | joint_or_at_fp_0 | 18546 | 23191 | 84.62% | 0 | 0.00 | 12916.82 | 0.000 | 91.67% | 93.17% | `{"filegroups/config": 0.9996832013130188, "filetypes/package.json": 0.9977713823318481, "general": 0.9976021647453308}` |
| filetypes/ole | joint_or_at_fp_0 | 6998 | 6337 | 82.75% | 0 | 0.00 | 47262.49 | 0.000 | 90.56% | 90.95% | `{"filegroups/documents": 0.21458876132965088, "filetypes/ole": 0.7750661969184875}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3089 | 189284 | 82.62% | 0 | 0.00 | 1582.65 | 0.000 | 90.48% | 99.72% | `{"filetypes/python-bytecode": 0.9987117052078247}` |
| filetypes/macho | joint_or_at_fp_0 | 2605 | 12260 | 78.69% | 0 | 0.00 | 24432.03 | 0.000 | 88.08% | 96.27% | `{"filegroups/native": 0.8213019371032715, "filetypes/macho": 0.9945999383926392, "general": 0.9860457181930542}` |
| filetypes/docx | joint_or_at_fp_0 | 4811 | 445 | 77.90% | 0 | 0.00 | 670937.36 | 0.000 | 87.58% | 79.78% | `{"filegroups/documents": 0.37584617733955383, "filetypes/docx": 0.9829602241516113, "general": 0.9876081943511963}` |
| filetypes/lnk | joint_or_at_fp_0 | 4394 | 1058 | 73.40% | 0 | 0.00 | 282750.01 | 0.000 | 84.66% | 78.56% | `{"filetypes/lnk": 0.9328004717826843, "general": 0.9995412230491638}` |
| filetypes/msi | joint_or_at_fp_0 | 5356 | 187 | 71.19% | 0 | 0.00 | 1589232.16 | 0.000 | 83.17% | 72.16% | `{"filetypes/msi": 0.7899327874183655, "general": 0.9959746599197388}` |
| filetypes/crx | learned_blend_at_fp_0 | 755 | 79 | 69.27% | 0 | 0.00 | 3721067.61 | 0.000 | 81.85% | 72.18% | `{}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5610 | 68.75% | 0 | 0.00 | 53385.61 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.9821199774742126, "general": 0.0419960618019104}` |
| filetypes/shell | joint_or_at_fp_0 | 14822 | 63898 | 66.52% | 0 | 0.00 | 4688.19 | 0.000 | 79.90% | 93.70% | `{"filegroups/scripts": 0.9819706082344055, "filetypes/shell": 0.9551436901092529, "general": 0.9991866946220398}` |
| filetypes/pe | joint_or_at_fp_0 | 1334102 | 161301 | 64.74% | 0 | 0.00 | 1857.21 | 0.000 | 78.60% | 68.54% | `{"filegroups/native": 0.9994445443153381, "filetypes/pe": 0.9975886344909668, "general": 0.9999306201934814}` |
| filetypes/java_class | joint_or_at_fp_0 | 1760 | 749741 | 61.42% | 0 | 0.00 | 399.57 | 0.000 | 76.10% | 99.91% | `{"filegroups/portable": 0.9682957530021667, "filetypes/java_class": 0.9626302123069763, "general": 0.9844369888305664}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 77 | 450 | 59.74% | 0 | 0.00 | 663507.29 | 0.000 | 74.80% | 94.12% | `{"filetypes/chrome-manifest": 0.9235559701919556, "general": 0.9794719219207764}` |
| filetypes/javascript | joint_or_at_fp_0 | 120499 | 632398 | 55.72% | 0 | 0.00 | 473.71 | 0.000 | 71.57% | 92.91% | `{"filegroups/scripts": 0.9945963025093079, "filetypes/javascript": 0.9852455258369446, "general": 0.9993019104003906}` |
| filetypes/jar | joint_or_at_fp_0 | 3495 | 4001 | 53.39% | 0 | 0.00 | 74846.56 | 0.000 | 69.61% | 78.27% | `{"filetypes/jar": 0.8621511459350586}` |
| filetypes/perl | joint_or_at_fp_0 | 346 | 43142 | 51.16% | 0 | 0.00 | 6943.65 | 0.000 | 67.69% | 99.61% | `{"filegroups/scripts": 0.9805095195770264, "filetypes/perl": 0.9985882639884949, "general": 0.9828863143920898}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32923 | 54825 | 51.14% | 0 | 0.00 | 5464.02 | 0.000 | 67.67% | 81.67% | `{"filegroups/source": 0.9576686024665833, "general": 0.9630189538002014}` |
| filetypes/php | joint_or_at_fp_0 | 5338 | 155021 | 49.44% | 0 | 0.00 | 1932.45 | 0.000 | 66.17% | 98.32% | `{"filegroups/scripts": 0.9789575934410095, "filetypes/php": 0.9535987973213196, "general": 0.9809699654579163}` |
| filetypes/powershell | joint_or_at_fp_0 | 5517 | 2447 | 45.15% | 0 | 0.00 | 122349.79 | 0.000 | 62.21% | 62.00% | `{"filegroups/scripts": 0.9916049242019653, "filetypes/powershell": 0.9947660565376282, "general": 0.9964884519577026}` |
| filetypes/python | joint_or_at_fp_0 | 22045 | 215872 | 43.35% | 0 | 0.00 | 1387.73 | 0.000 | 60.48% | 94.75% | `{"filegroups/scripts": 0.9957477450370789, "filetypes/python": 0.9985629916191101, "general": 0.998293399810791}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18595 | 41.24% | 0 | 0.00 | 16109.12 | 0.000 | 58.39% | 99.70% | `{"filegroups/scripts": 0.9691926836967468, "filetypes/lua": 0.9925063252449036, "general": 0.970565140247345}` |
| filetypes/ruby | joint_or_at_fp_0 | 207 | 28402 | 39.61% | 0 | 0.00 | 10547.05 | 0.000 | 56.75% | 99.56% | `{"filegroups/scripts": 0.9900863766670227, "filetypes/ruby": 0.9884610176086426}` |
| filetypes/zip | joint_or_at_fp_0 | 102348 | 12708 | 31.63% | 0 | 0.00 | 23570.82 | 0.000 | 48.06% | 39.19% | `{"filetypes/zip": 0.9985566735267639, "general": 0.9992659687995911}` |
| filetypes/xlsx | joint_or_at_fp_0 | 58982 | 1853 | 30.58% | 0 | 0.00 | 161538.69 | 0.000 | 46.84% | 32.69% | `{"filegroups/documents": 0.2833556830883026, "filetypes/xlsx": 0.962775707244873}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11021 | 100.00% | 0 | 0.00 | 27178.34 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9948320388793945}` |
| filetypes/rtf | learned_blend_at_fp_0 | 5921 | 514 | 98.33% | 0 | 0.00 | 581132.15 | 0.000 | 99.16% | 98.46% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2252 | 95.89% | 0 | 0.00 | 132936.97 | 0.000 | 97.90% | 96.60% | `{"filetypes/pkg-info": 0.9815199971199036, "general": 0.9956156015396118}` |
| filetypes/xls | joint_or_at_fp_0 | 37479 | 20761 | 95.00% | 0 | 0.00 | 14428.57 | 0.000 | 97.43% | 96.78% | `{"filegroups/documents": 0.2136012762784958, "filetypes/xls": 0.7950483560562134}` |
| filetypes/elf | joint_or_at_fp_0 | 180840 | 175951 | 92.03% | 0 | 0.00 | 1702.58 | 0.000 | 95.85% | 95.96% | `{"filegroups/native": 0.9933313727378845, "filetypes/elf": 0.9974352717399597, "general": 0.996862530708313}` |
| filetypes/tar | joint_or_at_fp_0 | 31472 | 26345 | 86.44% | 0 | 0.00 | 11370.51 | 0.000 | 92.73% | 92.62% | `{"filetypes/tar": 0.990632176399231, "general": 0.996157169342041}` |
| filetypes/package.json | joint_or_at_fp_0 | 18546 | 23191 | 84.62% | 0 | 0.00 | 12916.82 | 0.000 | 91.67% | 93.17% | `{"filegroups/config": 0.9996832013130188, "filetypes/package.json": 0.9977713823318481, "general": 0.9976021647453308}` |
| filetypes/ole | joint_or_at_fp_0 | 6998 | 6337 | 82.75% | 0 | 0.00 | 47262.49 | 0.000 | 90.56% | 90.95% | `{"filegroups/documents": 0.21458876132965088, "filetypes/ole": 0.7750661969184875}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3089 | 189284 | 82.62% | 0 | 0.00 | 1582.65 | 0.000 | 90.48% | 99.72% | `{"filetypes/python-bytecode": 0.9987117052078247}` |
| filetypes/macho | joint_or_at_fp_0 | 2605 | 12260 | 78.69% | 0 | 0.00 | 24432.03 | 0.000 | 88.08% | 96.27% | `{"filegroups/native": 0.8213019371032715, "filetypes/macho": 0.9945999383926392, "general": 0.9860457181930542}` |
| filetypes/docx | joint_or_at_fp_0 | 4811 | 445 | 77.90% | 0 | 0.00 | 670937.36 | 0.000 | 87.58% | 79.78% | `{"filegroups/documents": 0.37584617733955383, "filetypes/docx": 0.9829602241516113, "general": 0.9876081943511963}` |
| filetypes/lnk | joint_or_at_fp_0 | 4394 | 1058 | 73.40% | 0 | 0.00 | 282750.01 | 0.000 | 84.66% | 78.56% | `{"filetypes/lnk": 0.9328004717826843, "general": 0.9995412230491638}` |
| filetypes/msi | joint_or_at_fp_0 | 5356 | 187 | 71.19% | 0 | 0.00 | 1589232.16 | 0.000 | 83.17% | 72.16% | `{"filetypes/msi": 0.7899327874183655, "general": 0.9959746599197388}` |
| filetypes/crx | learned_blend_at_fp_0 | 755 | 79 | 69.27% | 0 | 0.00 | 3721067.61 | 0.000 | 81.85% | 72.18% | `{}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5610 | 68.75% | 0 | 0.00 | 53385.61 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.9821199774742126, "general": 0.0419960618019104}` |
| filetypes/shell | joint_or_at_fp_0 | 14822 | 63898 | 66.52% | 0 | 0.00 | 4688.19 | 0.000 | 79.90% | 93.70% | `{"filegroups/scripts": 0.9819706082344055, "filetypes/shell": 0.9551436901092529, "general": 0.9991866946220398}` |
| filetypes/pe | joint_or_at_fp_0 | 1334102 | 161301 | 64.74% | 0 | 0.00 | 1857.21 | 0.000 | 78.60% | 68.54% | `{"filegroups/native": 0.9994445443153381, "filetypes/pe": 0.9975886344909668, "general": 0.9999306201934814}` |
| filetypes/java_class | joint_or_at_fp_0 | 1760 | 749741 | 61.42% | 0 | 0.00 | 399.57 | 0.000 | 76.10% | 99.91% | `{"filegroups/portable": 0.9682957530021667, "filetypes/java_class": 0.9626302123069763, "general": 0.9844369888305664}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 77 | 450 | 59.74% | 0 | 0.00 | 663507.29 | 0.000 | 74.80% | 94.12% | `{"filetypes/chrome-manifest": 0.9235559701919556, "general": 0.9794719219207764}` |
| filetypes/javascript | joint_or_at_fp_0 | 120499 | 632398 | 55.72% | 0 | 0.00 | 473.71 | 0.000 | 71.57% | 92.91% | `{"filegroups/scripts": 0.9945963025093079, "filetypes/javascript": 0.9852455258369446, "general": 0.9993019104003906}` |
| filetypes/jar | joint_or_at_fp_0 | 3495 | 4001 | 53.39% | 0 | 0.00 | 74846.56 | 0.000 | 69.61% | 78.27% | `{"filetypes/jar": 0.8621511459350586}` |
| filetypes/perl | joint_or_at_fp_0 | 346 | 43142 | 51.16% | 0 | 0.00 | 6943.65 | 0.000 | 67.69% | 99.61% | `{"filegroups/scripts": 0.9805095195770264, "filetypes/perl": 0.9985882639884949, "general": 0.9828863143920898}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32923 | 54825 | 51.14% | 0 | 0.00 | 5464.02 | 0.000 | 67.67% | 81.67% | `{"filegroups/source": 0.9576686024665833, "general": 0.9630189538002014}` |
| filetypes/php | joint_or_at_fp_0 | 5338 | 155021 | 49.44% | 0 | 0.00 | 1932.45 | 0.000 | 66.17% | 98.32% | `{"filegroups/scripts": 0.9789575934410095, "filetypes/php": 0.9535987973213196, "general": 0.9809699654579163}` |
| filetypes/powershell | joint_or_at_fp_0 | 5517 | 2447 | 45.15% | 0 | 0.00 | 122349.79 | 0.000 | 62.21% | 62.00% | `{"filegroups/scripts": 0.9916049242019653, "filetypes/powershell": 0.9947660565376282, "general": 0.9964884519577026}` |
| filetypes/python | joint_or_at_fp_0 | 22045 | 215872 | 43.35% | 0 | 0.00 | 1387.73 | 0.000 | 60.48% | 94.75% | `{"filegroups/scripts": 0.9957477450370789, "filetypes/python": 0.9985629916191101, "general": 0.998293399810791}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18595 | 41.24% | 0 | 0.00 | 16109.12 | 0.000 | 58.39% | 99.70% | `{"filegroups/scripts": 0.9691926836967468, "filetypes/lua": 0.9925063252449036, "general": 0.970565140247345}` |
| filetypes/ruby | joint_or_at_fp_0 | 207 | 28402 | 39.61% | 0 | 0.00 | 10547.05 | 0.000 | 56.75% | 99.56% | `{"filegroups/scripts": 0.9900863766670227, "filetypes/ruby": 0.9884610176086426}` |
| filetypes/zip | joint_or_at_fp_0 | 102348 | 12708 | 31.63% | 0 | 0.00 | 23570.82 | 0.000 | 48.06% | 39.19% | `{"filetypes/zip": 0.9985566735267639, "general": 0.9992659687995911}` |
| filetypes/xlsx | joint_or_at_fp_0 | 58982 | 1853 | 30.58% | 0 | 0.00 | 161538.69 | 0.000 | 46.84% | 32.69% | `{"filegroups/documents": 0.2833556830883026, "filetypes/xlsx": 0.962775707244873}` |
