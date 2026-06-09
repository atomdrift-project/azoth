# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1679491877`
- Rows: 7260408 (2532241 malware, 4728167 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11021 | 100.00% | 0 | 0.00 | 27178.34 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9948320388793945}` |
| filetypes/rtf | joint_or_at_fp_0 | 5921 | 514 | 97.99% | 0 | 0.00 | 581132.15 | 0.000 | 98.98% | 98.15% | `{"filetypes/rtf": 0.7592488527297974, "general": 0.09144198149442673}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2252 | 95.89% | 0 | 0.00 | 132936.97 | 0.000 | 97.90% | 96.60% | `{"filetypes/pkg-info": 0.9815199971199036, "general": 0.9956156015396118}` |
| filetypes/xls | joint_or_at_fp_0 | 37479 | 20761 | 94.59% | 0 | 0.00 | 14428.57 | 0.000 | 97.22% | 96.52% | `{"filetypes/xls": 0.8552315831184387}` |
| filetypes/elf | joint_or_at_fp_0 | 180840 | 175951 | 94.24% | 0 | 0.00 | 1702.58 | 0.000 | 97.03% | 97.08% | `{"filegroups/native": 0.9933704137802124, "filetypes/elf": 0.9928072690963745, "general": 0.9969998598098755}` |
| filetypes/package.json | joint_or_at_fp_0 | 18546 | 23191 | 87.38% | 0 | 0.00 | 12916.82 | 0.000 | 93.26% | 94.39% | `{"filegroups/config": 0.9998296499252319, "filetypes/package.json": 0.9977713823318481, "general": 0.9976021647453308}` |
| filetypes/tar | joint_or_at_fp_0 | 31506 | 26345 | 86.45% | 0 | 0.00 | 11370.51 | 0.000 | 92.73% | 92.62% | `{"filetypes/tar": 0.990632176399231, "general": 0.996157169342041}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3089 | 189284 | 82.62% | 0 | 0.00 | 1582.65 | 0.000 | 90.48% | 99.72% | `{"filetypes/python-bytecode": 0.9987117052078247}` |
| filetypes/docx | joint_or_at_fp_0 | 4811 | 445 | 82.44% | 0 | 0.00 | 670937.36 | 0.000 | 90.37% | 83.92% | `{"filegroups/documents": 0.6616628766059875, "filetypes/docx": 0.9832839965820312}` |
| filetypes/lnk | joint_or_at_fp_0 | 4394 | 1058 | 80.91% | 0 | 0.00 | 282750.01 | 0.000 | 89.45% | 84.61% | `{"filetypes/lnk": 0.8684421181678772, "general": 0.9995412230491638}` |
| filetypes/macho | joint_or_at_fp_0 | 2605 | 12260 | 78.69% | 0 | 0.00 | 24432.03 | 0.000 | 88.08% | 96.27% | `{"filegroups/native": 0.8213019371032715, "filetypes/macho": 0.9945999383926392, "general": 0.9860457181930542}` |
| filetypes/msi | joint_or_at_fp_0 | 5356 | 187 | 71.19% | 0 | 0.00 | 1589232.16 | 0.000 | 83.17% | 72.16% | `{"filetypes/msi": 0.7899327874183655, "general": 0.9959746599197388}` |
| filetypes/crx | learned_blend_at_fp_0 | 755 | 79 | 69.27% | 0 | 0.00 | 3721067.61 | 0.000 | 81.85% | 72.18% | `{}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5610 | 68.75% | 0 | 0.00 | 53385.61 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.9821199774742126, "general": 0.0419960618019104}` |
| filetypes/shell | joint_or_at_fp_0 | 14822 | 63898 | 67.78% | 0 | 0.00 | 4688.19 | 0.000 | 80.80% | 93.93% | `{"filegroups/scripts": 0.9912846088409424, "filetypes/shell": 0.9161846041679382, "general": 0.9981441497802734}` |
| filetypes/pe | learned_blend_at_fp_0 | 1334102 | 161301 | 59.84% | 0 | 0.00 | 1857.21 | 0.000 | 74.88% | 64.18% | `{}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 77 | 450 | 59.74% | 0 | 0.00 | 663507.29 | 0.000 | 74.80% | 94.12% | `{"filetypes/chrome-manifest": 0.9235559701919556, "general": 0.9794719219207764}` |
| filetypes/perl | learned_blend_at_fp_0 | 346 | 43142 | 54.34% | 0 | 0.00 | 6943.65 | 0.000 | 70.41% | 99.64% | `{}` |
| filetypes/javascript | joint_or_at_fp_0 | 120499 | 632398 | 53.97% | 0 | 0.00 | 473.71 | 0.000 | 70.10% | 92.63% | `{"filegroups/scripts": 0.9969678521156311, "filetypes/javascript": 0.9960122108459473, "general": 0.9993058443069458}` |
| filetypes/jar | joint_or_at_fp_0 | 3495 | 4001 | 53.39% | 0 | 0.00 | 74846.56 | 0.000 | 69.61% | 78.27% | `{"filetypes/jar": 0.8621511459350586}` |
| filetypes/ole | joint_or_at_fp_0 | 6998 | 6337 | 52.17% | 0 | 0.00 | 47262.49 | 0.000 | 68.57% | 74.90% | `{"filegroups/documents": 0.9913382530212402, "filetypes/ole": 0.998272180557251, "general": 0.9986438751220703}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32923 | 54825 | 52.06% | 0 | 0.00 | 5464.02 | 0.000 | 68.47% | 82.01% | `{"filegroups/source": 0.9576686024665833, "filetypes/kotlin": 0.9667871594429016, "general": 0.9630189538002014}` |
| filetypes/php | joint_or_at_fp_0 | 5338 | 155021 | 49.29% | 0 | 0.00 | 1932.45 | 0.000 | 66.03% | 98.31% | `{"filegroups/scripts": 0.9957072138786316, "filetypes/php": 0.9892904162406921, "general": 0.9807645678520203}` |
| filetypes/powershell | joint_or_at_fp_0 | 5517 | 2447 | 46.84% | 0 | 0.00 | 122349.79 | 0.000 | 63.79% | 63.17% | `{"filegroups/scripts": 0.9976429343223572, "filetypes/powershell": 0.9972008466720581, "general": 0.9964884519577026}` |
| filetypes/python | joint_or_at_fp_0 | 22045 | 215872 | 46.61% | 0 | 0.00 | 1387.73 | 0.000 | 63.59% | 95.05% | `{"filegroups/scripts": 0.9961400628089905, "filetypes/python": 0.9995294809341431, "general": 0.998340368270874}` |
| filetypes/java_class | joint_or_at_fp_0 | 1760 | 749741 | 46.19% | 0 | 0.00 | 399.57 | 0.000 | 63.19% | 99.87% | `{"filetypes/java_class": 0.9999648332595825, "general": 0.9844369888305664}` |
| filetypes/ruby | joint_or_at_fp_0 | 207 | 28402 | 41.55% | 0 | 0.00 | 10547.05 | 0.000 | 58.70% | 99.58% | `{"filegroups/scripts": 0.9643304944038391, "filetypes/ruby": 0.9884610176086426}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18595 | 41.24% | 0 | 0.00 | 16109.12 | 0.000 | 58.39% | 99.70% | `{"filegroups/scripts": 0.9786484837532043, "filetypes/lua": 0.9925063252449036, "general": 0.970565140247345}` |
| filetypes/vbs | joint_or_at_fp_0 | 11317 | 3328 | 37.55% | 0 | 0.00 | 89975.49 | 0.000 | 54.60% | 51.74% | `{"filetypes/vbs": 0.9948980212211609, "general": 0.997754693031311}` |
| filetypes/zip | joint_or_at_fp_0 | 102408 | 12712 | 36.73% | 0 | 0.00 | 23563.40 | 0.000 | 53.72% | 43.71% | `{"filetypes/zip": 0.997256338596344, "general": 0.9992659687995911}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11021 | 100.00% | 0 | 0.00 | 27178.34 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9948320388793945}` |
| filetypes/rtf | joint_or_at_fp_0 | 5921 | 514 | 97.99% | 0 | 0.00 | 581132.15 | 0.000 | 98.98% | 98.15% | `{"filetypes/rtf": 0.7592488527297974, "general": 0.09144198149442673}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2252 | 95.89% | 0 | 0.00 | 132936.97 | 0.000 | 97.90% | 96.60% | `{"filetypes/pkg-info": 0.9815199971199036, "general": 0.9956156015396118}` |
| filetypes/xls | joint_or_at_fp_0 | 37479 | 20761 | 94.59% | 0 | 0.00 | 14428.57 | 0.000 | 97.22% | 96.52% | `{"filetypes/xls": 0.8552315831184387}` |
| filetypes/elf | joint_or_at_fp_0 | 180840 | 175951 | 94.24% | 0 | 0.00 | 1702.58 | 0.000 | 97.03% | 97.08% | `{"filegroups/native": 0.9933704137802124, "filetypes/elf": 0.9928072690963745, "general": 0.9969998598098755}` |
| filetypes/package.json | joint_or_at_fp_0 | 18546 | 23191 | 87.38% | 0 | 0.00 | 12916.82 | 0.000 | 93.26% | 94.39% | `{"filegroups/config": 0.9998296499252319, "filetypes/package.json": 0.9977713823318481, "general": 0.9976021647453308}` |
| filetypes/tar | joint_or_at_fp_0 | 31506 | 26345 | 86.45% | 0 | 0.00 | 11370.51 | 0.000 | 92.73% | 92.62% | `{"filetypes/tar": 0.990632176399231, "general": 0.996157169342041}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3089 | 189284 | 82.62% | 0 | 0.00 | 1582.65 | 0.000 | 90.48% | 99.72% | `{"filetypes/python-bytecode": 0.9987117052078247}` |
| filetypes/docx | joint_or_at_fp_0 | 4811 | 445 | 82.44% | 0 | 0.00 | 670937.36 | 0.000 | 90.37% | 83.92% | `{"filegroups/documents": 0.6616628766059875, "filetypes/docx": 0.9832839965820312}` |
| filetypes/lnk | joint_or_at_fp_0 | 4394 | 1058 | 80.91% | 0 | 0.00 | 282750.01 | 0.000 | 89.45% | 84.61% | `{"filetypes/lnk": 0.8684421181678772, "general": 0.9995412230491638}` |
| filetypes/macho | joint_or_at_fp_0 | 2605 | 12260 | 78.69% | 0 | 0.00 | 24432.03 | 0.000 | 88.08% | 96.27% | `{"filegroups/native": 0.8213019371032715, "filetypes/macho": 0.9945999383926392, "general": 0.9860457181930542}` |
| filetypes/msi | joint_or_at_fp_0 | 5356 | 187 | 71.19% | 0 | 0.00 | 1589232.16 | 0.000 | 83.17% | 72.16% | `{"filetypes/msi": 0.7899327874183655, "general": 0.9959746599197388}` |
| filetypes/crx | learned_blend_at_fp_0 | 755 | 79 | 69.27% | 0 | 0.00 | 3721067.61 | 0.000 | 81.85% | 72.18% | `{}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5610 | 68.75% | 0 | 0.00 | 53385.61 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.9821199774742126, "general": 0.0419960618019104}` |
| filetypes/shell | joint_or_at_fp_0 | 14822 | 63898 | 67.78% | 0 | 0.00 | 4688.19 | 0.000 | 80.80% | 93.93% | `{"filegroups/scripts": 0.9912846088409424, "filetypes/shell": 0.9161846041679382, "general": 0.9981441497802734}` |
| filetypes/pe | learned_blend_at_fp_0 | 1334102 | 161301 | 59.84% | 0 | 0.00 | 1857.21 | 0.000 | 74.88% | 64.18% | `{}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 77 | 450 | 59.74% | 0 | 0.00 | 663507.29 | 0.000 | 74.80% | 94.12% | `{"filetypes/chrome-manifest": 0.9235559701919556, "general": 0.9794719219207764}` |
| filetypes/perl | learned_blend_at_fp_0 | 346 | 43142 | 54.34% | 0 | 0.00 | 6943.65 | 0.000 | 70.41% | 99.64% | `{}` |
| filetypes/javascript | joint_or_at_fp_0 | 120499 | 632398 | 53.97% | 0 | 0.00 | 473.71 | 0.000 | 70.10% | 92.63% | `{"filegroups/scripts": 0.9969678521156311, "filetypes/javascript": 0.9960122108459473, "general": 0.9993058443069458}` |
| filetypes/jar | joint_or_at_fp_0 | 3495 | 4001 | 53.39% | 0 | 0.00 | 74846.56 | 0.000 | 69.61% | 78.27% | `{"filetypes/jar": 0.8621511459350586}` |
| filetypes/ole | joint_or_at_fp_0 | 6998 | 6337 | 52.17% | 0 | 0.00 | 47262.49 | 0.000 | 68.57% | 74.90% | `{"filegroups/documents": 0.9913382530212402, "filetypes/ole": 0.998272180557251, "general": 0.9986438751220703}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32923 | 54825 | 52.06% | 0 | 0.00 | 5464.02 | 0.000 | 68.47% | 82.01% | `{"filegroups/source": 0.9576686024665833, "filetypes/kotlin": 0.9667871594429016, "general": 0.9630189538002014}` |
| filetypes/php | joint_or_at_fp_0 | 5338 | 155021 | 49.29% | 0 | 0.00 | 1932.45 | 0.000 | 66.03% | 98.31% | `{"filegroups/scripts": 0.9957072138786316, "filetypes/php": 0.9892904162406921, "general": 0.9807645678520203}` |
| filetypes/powershell | joint_or_at_fp_0 | 5517 | 2447 | 46.84% | 0 | 0.00 | 122349.79 | 0.000 | 63.79% | 63.17% | `{"filegroups/scripts": 0.9976429343223572, "filetypes/powershell": 0.9972008466720581, "general": 0.9964884519577026}` |
| filetypes/python | joint_or_at_fp_0 | 22045 | 215872 | 46.61% | 0 | 0.00 | 1387.73 | 0.000 | 63.59% | 95.05% | `{"filegroups/scripts": 0.9961400628089905, "filetypes/python": 0.9995294809341431, "general": 0.998340368270874}` |
| filetypes/java_class | joint_or_at_fp_0 | 1760 | 749741 | 46.19% | 0 | 0.00 | 399.57 | 0.000 | 63.19% | 99.87% | `{"filetypes/java_class": 0.9999648332595825, "general": 0.9844369888305664}` |
| filetypes/ruby | joint_or_at_fp_0 | 207 | 28402 | 41.55% | 0 | 0.00 | 10547.05 | 0.000 | 58.70% | 99.58% | `{"filegroups/scripts": 0.9643304944038391, "filetypes/ruby": 0.9884610176086426}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18595 | 41.24% | 0 | 0.00 | 16109.12 | 0.000 | 58.39% | 99.70% | `{"filegroups/scripts": 0.9786484837532043, "filetypes/lua": 0.9925063252449036, "general": 0.970565140247345}` |
| filetypes/vbs | joint_or_at_fp_0 | 11317 | 3328 | 37.55% | 0 | 0.00 | 89975.49 | 0.000 | 54.60% | 51.74% | `{"filetypes/vbs": 0.9948980212211609, "general": 0.997754693031311}` |
| filetypes/zip | joint_or_at_fp_0 | 102408 | 12712 | 36.73% | 0 | 0.00 | 23563.40 | 0.000 | 53.72% | 43.71% | `{"filetypes/zip": 0.997256338596344, "general": 0.9992659687995911}` |
