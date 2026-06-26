# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1872261008`
- Rows: 8638497 (2614576 malware, 6023921 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 254 | 15802 | 100.00% | 0 | 0.00 | 18956.13 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9964885711669922}` |
| filetypes/crx | learned_blend_at_fp_0 | 805 | 184 | 98.39% | 0 | 0.00 | 1614933.21 | 0.000 | 99.19% | 98.69% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 526 | 97.89% | 0 | 0.00 | 567912.10 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.058191537857055664}` |
| filetypes/gem | joint_or_at_fp_0 | 772 | 1104 | 97.28% | 0 | 0.00 | 270984.73 | 0.000 | 98.62% | 98.88% | `{"filetypes/gem": 0.29505765438079834, "general": 0.9259820580482483}` |
| filetypes/elf | joint_or_at_fp_0 | 189688 | 283349 | 90.33% | 0 | 0.00 | 1057.25 | 0.000 | 94.92% | 96.12% | `{"filegroups/native": 0.9790063500404358, "filetypes/elf": 0.9984685778617859, "general": 0.986871063709259}` |
| filetypes/tar | joint_or_at_fp_0 | 30706 | 48611 | 85.55% | 0 | 0.00 | 6162.47 | 0.000 | 92.21% | 94.40% | `{"filetypes/tar": 0.993459165096283, "general": 0.9965975284576416}` |
| filetypes/package.json | learned_blend_at_fp_0 | 19404 | 27746 | 83.60% | 0 | 0.00 | 10796.41 | 0.000 | 91.07% | 93.25% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4617 | 1065 | 74.25% | 0 | 0.00 | 280894.17 | 0.000 | 85.22% | 79.07% | `{"filetypes/lnk": 0.9497115015983582, "general": 0.9987188577651978}` |
| filetypes/shell | joint_or_at_fp_0 | 15777 | 77224 | 73.85% | 0 | 0.00 | 3879.20 | 0.000 | 84.96% | 95.56% | `{"filegroups/scripts": 0.9832287430763245, "filetypes/shell": 0.9643027186393738, "general": 0.969433605670929}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24717 | 73.72% | 0 | 0.00 | 12119.39 | 0.000 | 84.87% | 76.91% | `{"filegroups/documents": 0.9885914921760559, "filetypes/pdf": 0.9596382975578308, "general": 0.9770442247390747}` |
| filetypes/macho | joint_or_at_fp_0 | 2698 | 14122 | 67.79% | 0 | 0.00 | 21210.98 | 0.000 | 80.80% | 94.83% | `{"filegroups/native": 0.9560235142707825, "filetypes/macho": 0.989905059337616, "general": 0.9858856797218323}` |
| filetypes/npm | filetype_only_at_fp_0 | 1891 | 1342 | 66.42% | 0 | 0.00 | 222979.96 | 0.000 | 79.82% | 80.36% | `{"filetypes/npm": 0.964945375919342}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45436 | 61.50% | 0 | 0.00 | 6593.08 | 0.000 | 76.16% | 99.67% | `{"filegroups/scripts": 0.966874361038208, "filetypes/perl": 0.9905412793159485}` |
| filetypes/javascript | joint_or_at_fp_0 | 127229 | 740360 | 60.83% | 0 | 0.00 | 404.63 | 0.000 | 75.64% | 94.26% | `{"filegroups/scripts": 0.9934012293815613, "filetypes/javascript": 0.9843078255653381, "general": 0.9985212087631226}` |
| filetypes/whl | joint_or_at_fp_0 | 2525 | 4740 | 59.33% | 0 | 0.00 | 63181.14 | 0.000 | 74.47% | 85.86% | `{"filetypes/whl": 0.9944532513618469, "general": 0.9096306562423706}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 19279 | 53.61% | 0 | 0.00 | 15537.63 | 0.000 | 69.80% | 99.77% | `{"filegroups/scripts": 0.964593768119812, "filetypes/lua": 0.8219956159591675}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32487 | 57866 | 52.31% | 0 | 0.00 | 5176.88 | 0.000 | 68.69% | 82.85% | `{"filegroups/source": 0.8723461627960205, "filetypes/kotlin": 0.8567541241645813, "general": 0.9301852583885193}` |
| filetypes/jar | joint_or_at_fp_0 | 3709 | 9271 | 50.18% | 0 | 0.00 | 32307.72 | 0.000 | 66.82% | 85.76% | `{"filetypes/jar": 0.97544264793396, "general": 0.9724860787391663}` |
| filetypes/scala | calibrate_inherited | 2 | 19272 | 50.00% | 0 | 0.00 | 15543.27 | 0.000 | 66.67% | 99.99% | `{"filegroups/source": 0.9822411564821043, "general": 0.9996190194825575}` |
| filetypes/php | joint_or_at_fp_0 | 5830 | 175559 | 47.91% | 0 | 0.00 | 1706.38 | 0.000 | 64.78% | 98.33% | `{"filegroups/scripts": 0.9867510199546814, "filetypes/php": 0.9919480681419373, "general": 0.9649550914764404}` |
| filetypes/pe | learned_blend_at_fp_0 | 1370421 | 177176 | 46.71% | 0 | 0.00 | 1690.81 | 0.000 | 63.68% | 52.81% | `{}` |
| filetypes/java_class | joint_or_at_fp_0 | 1980 | 835864 | 46.11% | 0 | 0.00 | 358.40 | 0.000 | 63.12% | 99.87% | `{"filegroups/portable": 0.9999483823776245, "filetypes/java_class": 0.9998989105224609, "general": 0.9815715551376343}` |
| filetypes/python | joint_or_at_fp_0 | 20793 | 268879 | 41.01% | 0 | 0.00 | 1114.15 | 0.000 | 58.17% | 95.77% | `{"filegroups/scripts": 0.9973414540290833, "filetypes/python": 0.999884843826294, "general": 0.993659257888794}` |
| filetypes/ruby | joint_or_at_fp_0 | 259 | 39152 | 39.00% | 0 | 0.00 | 7651.25 | 0.000 | 56.11% | 99.60% | `{"filegroups/scripts": 0.9362844824790955, "filetypes/ruby": 0.9952794313430786, "general": 0.9770616292953491}` |
| filetypes/powershell | joint_or_at_fp_0 | 5886 | 2604 | 38.57% | 0 | 0.00 | 114977.33 | 0.000 | 55.66% | 57.41% | `{"filegroups/scripts": 0.9962124824523926, "filetypes/powershell": 0.9969474673271179, "general": 0.9980995059013367}` |
| filetypes/zip | joint_or_at_fp_0 | 103757 | 18990 | 33.78% | 0 | 0.00 | 15774.07 | 0.000 | 50.50% | 44.02% | `{"filetypes/zip": 0.9988564252853394, "general": 0.9975571632385254}` |
| filetypes/vbs | joint_or_at_fp_0 | 12102 | 3394 | 33.03% | 0 | 0.00 | 88226.59 | 0.000 | 49.66% | 47.70% | `{"filetypes/vbs": 0.9890198111534119, "general": 0.9941238760948181}` |
| filetypes/dockerfile | joint_or_at_fp_0 | 69 | 2025 | 27.54% | 0 | 0.00 | 147828.02 | 0.000 | 43.18% | 97.61% | `{"filetypes/dockerfile": 0.9832398295402527, "general": 0.9650478959083557}` |
| filetypes/svg | calibrate_inherited | 34 | 33137 | 23.53% | 0 | 0.00 | 9040.04 | 0.000 | 38.10% | 99.92% | `{"filegroups/media": 0.9988531460508445, "general": 0.9996190194825575}` |
| filetypes/7z | calibrate_inherited | 8962 | 109 | 22.81% | 0 | 0.00 | 2710953.96 | 0.000 | 37.14% | 23.73% | `{"general": 0.9996190194825575}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 254 | 15802 | 100.00% | 0 | 0.00 | 18956.13 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9964885711669922}` |
| filetypes/crx | learned_blend_at_fp_0 | 805 | 184 | 98.39% | 0 | 0.00 | 1614933.21 | 0.000 | 99.19% | 98.69% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 526 | 97.89% | 0 | 0.00 | 567912.10 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.058191537857055664}` |
| filetypes/gem | joint_or_at_fp_0 | 772 | 1104 | 97.28% | 0 | 0.00 | 270984.73 | 0.000 | 98.62% | 98.88% | `{"filetypes/gem": 0.29505765438079834, "general": 0.9259820580482483}` |
| filetypes/elf | joint_or_at_fp_0 | 189688 | 283349 | 90.33% | 0 | 0.00 | 1057.25 | 0.000 | 94.92% | 96.12% | `{"filegroups/native": 0.9790063500404358, "filetypes/elf": 0.9984685778617859, "general": 0.986871063709259}` |
| filetypes/tar | joint_or_at_fp_0 | 30706 | 48611 | 85.55% | 0 | 0.00 | 6162.47 | 0.000 | 92.21% | 94.40% | `{"filetypes/tar": 0.993459165096283, "general": 0.9965975284576416}` |
| filetypes/package.json | learned_blend_at_fp_0 | 19404 | 27746 | 83.60% | 0 | 0.00 | 10796.41 | 0.000 | 91.07% | 93.25% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4617 | 1065 | 74.25% | 0 | 0.00 | 280894.17 | 0.000 | 85.22% | 79.07% | `{"filetypes/lnk": 0.9497115015983582, "general": 0.9987188577651978}` |
| filetypes/shell | joint_or_at_fp_0 | 15777 | 77224 | 73.85% | 0 | 0.00 | 3879.20 | 0.000 | 84.96% | 95.56% | `{"filegroups/scripts": 0.9832287430763245, "filetypes/shell": 0.9643027186393738, "general": 0.969433605670929}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24717 | 73.72% | 0 | 0.00 | 12119.39 | 0.000 | 84.87% | 76.91% | `{"filegroups/documents": 0.9885914921760559, "filetypes/pdf": 0.9596382975578308, "general": 0.9770442247390747}` |
| filetypes/macho | joint_or_at_fp_0 | 2698 | 14122 | 67.79% | 0 | 0.00 | 21210.98 | 0.000 | 80.80% | 94.83% | `{"filegroups/native": 0.9560235142707825, "filetypes/macho": 0.989905059337616, "general": 0.9858856797218323}` |
| filetypes/npm | filetype_only_at_fp_0 | 1891 | 1342 | 66.42% | 0 | 0.00 | 222979.96 | 0.000 | 79.82% | 80.36% | `{"filetypes/npm": 0.964945375919342}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45436 | 61.50% | 0 | 0.00 | 6593.08 | 0.000 | 76.16% | 99.67% | `{"filegroups/scripts": 0.966874361038208, "filetypes/perl": 0.9905412793159485}` |
| filetypes/javascript | joint_or_at_fp_0 | 127229 | 740360 | 60.83% | 0 | 0.00 | 404.63 | 0.000 | 75.64% | 94.26% | `{"filegroups/scripts": 0.9934012293815613, "filetypes/javascript": 0.9843078255653381, "general": 0.9985212087631226}` |
| filetypes/whl | joint_or_at_fp_0 | 2525 | 4740 | 59.33% | 0 | 0.00 | 63181.14 | 0.000 | 74.47% | 85.86% | `{"filetypes/whl": 0.9944532513618469, "general": 0.9096306562423706}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 19279 | 53.61% | 0 | 0.00 | 15537.63 | 0.000 | 69.80% | 99.77% | `{"filegroups/scripts": 0.964593768119812, "filetypes/lua": 0.8219956159591675}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32487 | 57866 | 52.31% | 0 | 0.00 | 5176.88 | 0.000 | 68.69% | 82.85% | `{"filegroups/source": 0.8723461627960205, "filetypes/kotlin": 0.8567541241645813, "general": 0.9301852583885193}` |
| filetypes/jar | joint_or_at_fp_0 | 3709 | 9271 | 50.18% | 0 | 0.00 | 32307.72 | 0.000 | 66.82% | 85.76% | `{"filetypes/jar": 0.97544264793396, "general": 0.9724860787391663}` |
| filetypes/scala | calibrate_inherited | 2 | 19272 | 50.00% | 0 | 0.00 | 15543.27 | 0.000 | 66.67% | 99.99% | `{"filegroups/source": 0.982221072481872, "general": 0.9995949515780225}` |
| filetypes/php | joint_or_at_fp_0 | 5830 | 175559 | 47.91% | 0 | 0.00 | 1706.38 | 0.000 | 64.78% | 98.33% | `{"filegroups/scripts": 0.9867510199546814, "filetypes/php": 0.9919480681419373, "general": 0.9649550914764404}` |
| filetypes/pe | learned_blend_at_fp_0 | 1370421 | 177176 | 46.71% | 0 | 0.00 | 1690.81 | 0.000 | 63.68% | 52.81% | `{}` |
| filetypes/java_class | joint_or_at_fp_0 | 1980 | 835864 | 46.11% | 0 | 0.00 | 358.40 | 0.000 | 63.12% | 99.87% | `{"filegroups/portable": 0.9999483823776245, "filetypes/java_class": 0.9998989105224609, "general": 0.9815715551376343}` |
| filetypes/python | joint_or_at_fp_0 | 20793 | 268879 | 41.01% | 0 | 0.00 | 1114.15 | 0.000 | 58.17% | 95.77% | `{"filegroups/scripts": 0.9973414540290833, "filetypes/python": 0.999884843826294, "general": 0.993659257888794}` |
| filetypes/ruby | joint_or_at_fp_0 | 259 | 39152 | 39.00% | 0 | 0.00 | 7651.25 | 0.000 | 56.11% | 99.60% | `{"filegroups/scripts": 0.9362844824790955, "filetypes/ruby": 0.9952794313430786, "general": 0.9770616292953491}` |
| filetypes/powershell | joint_or_at_fp_0 | 5886 | 2604 | 38.57% | 0 | 0.00 | 114977.33 | 0.000 | 55.66% | 57.41% | `{"filegroups/scripts": 0.9962124824523926, "filetypes/powershell": 0.9969474673271179, "general": 0.9980995059013367}` |
| filetypes/zip | joint_or_at_fp_0 | 103757 | 18990 | 33.78% | 0 | 0.00 | 15774.07 | 0.000 | 50.50% | 44.02% | `{"filetypes/zip": 0.9988564252853394, "general": 0.9975571632385254}` |
| filetypes/vbs | joint_or_at_fp_0 | 12102 | 3394 | 33.03% | 0 | 0.00 | 88226.59 | 0.000 | 49.66% | 47.70% | `{"filetypes/vbs": 0.9890198111534119, "general": 0.9941238760948181}` |
| filetypes/dockerfile | joint_or_at_fp_0 | 69 | 2025 | 27.54% | 0 | 0.00 | 147828.02 | 0.000 | 43.18% | 97.61% | `{"filetypes/dockerfile": 0.9832398295402527, "general": 0.9650478959083557}` |
| filetypes/7z | calibrate_inherited | 8962 | 109 | 23.64% | 0 | 0.00 | 2710953.96 | 0.000 | 38.25% | 24.56% | `{"general": 0.9995949515780225}` |
| filetypes/svg | calibrate_inherited | 34 | 33137 | 23.53% | 0 | 0.00 | 9040.04 | 0.000 | 38.10% | 99.92% | `{"filegroups/media": 0.9987822155445135, "general": 0.9995949515780225}` |
