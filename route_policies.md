# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1872261008`
- Rows: 8638497 (2614576 malware, 6023921 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{}` |
| filetypes/crx | learned_blend_at_fp_0 | 805 | 184 | 98.39% | 0 | 0.00 | 1614933.21 | 0.000 | 99.19% | 98.69% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 526 | 97.89% | 0 | 0.00 | 567912.10 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.058191537857055664}` |
| filetypes/gem | joint_or_at_fp_0 | 772 | 1106 | 97.28% | 0 | 0.00 | 270495.37 | 0.000 | 98.62% | 98.88% | `{"filetypes/gem": 0.29505765438079834, "general": 0.9259820580482483}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 3766 | 96.78% | 0 | 0.00 | 79515.16 | 0.000 | 98.36% | 97.63% | `{"filetypes/pkg-info": 0.13838452100753784}` |
| filetypes/doc | calibrate_inherited | 34589 | 86 | 96.46% | 0 | 0.00 | 3423437.28 | 0.000 | 98.20% | 96.46% | `{"filegroups/documents": 0.19414395093917847, "general": 0.9996190194825575}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 90 | 277 | 95.56% | 0 | 0.00 | 1075664.70 | 0.000 | 97.73% | 98.91% | `{"filetypes/chrome-manifest": 0.6607028245925903}` |
| filetypes/xls | joint_or_at_fp_0 | 39677 | 20762 | 94.85% | 0 | 0.00 | 14427.88 | 0.000 | 97.35% | 96.62% | `{"filegroups/documents": 0.8492828011512756, "filetypes/xls": 0.9130752682685852}` |
| filetypes/elf | joint_or_at_fp_0 | 189688 | 283349 | 90.33% | 0 | 0.00 | 1057.25 | 0.000 | 94.92% | 96.12% | `{"filegroups/native": 0.9790063500404358, "filetypes/elf": 0.9984685778617859, "general": 0.986871063709259}` |
| filetypes/tar | joint_or_at_fp_0 | 30722 | 48820 | 85.54% | 0 | 0.00 | 6136.09 | 0.000 | 92.21% | 94.41% | `{"filetypes/tar": 0.993459165096283, "general": 0.9965975284576416}` |
| filetypes/package.json | learned_blend_at_fp_0 | 19404 | 27748 | 83.59% | 0 | 0.00 | 10795.63 | 0.000 | 91.06% | 93.25% | `{}` |
| filetypes/docx | joint_or_at_fp_0 | 4965 | 402 | 82.78% | 0 | 0.00 | 742437.25 | 0.000 | 90.58% | 84.07% | `{"filegroups/documents": 0.9156664609909058, "filetypes/docx": 0.5880919098854065}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6720 | 78.07% | 0 | 0.00 | 44569.41 | 0.000 | 87.69% | 88.51% | `{"filegroups/documents": 0.6700654625892639, "filetypes/ole": 0.9968721270561218}` |
| filetypes/lnk | joint_or_at_fp_0 | 4617 | 1065 | 74.25% | 0 | 0.00 | 280894.17 | 0.000 | 85.22% | 79.07% | `{"filetypes/lnk": 0.9497115015983582, "general": 0.9987188577651978}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3418 | 446251 | 74.05% | 0 | 0.00 | 671.31 | 0.000 | 85.09% | 99.80% | `{"filetypes/python-bytecode": 0.9950478672981262}` |
| filetypes/shell | joint_or_at_fp_0 | 15777 | 77326 | 73.85% | 0 | 0.00 | 3874.08 | 0.000 | 84.96% | 95.57% | `{"filegroups/scripts": 0.9832287430763245, "filetypes/shell": 0.9643027186393738, "general": 0.969433605670929}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24717 | 73.72% | 0 | 0.00 | 12119.39 | 0.000 | 84.87% | 76.91% | `{"filegroups/documents": 0.9885914921760559, "filetypes/pdf": 0.9596382975578308, "general": 0.9770442247390747}` |
| filetypes/macho | joint_or_at_fp_0 | 2698 | 14122 | 67.79% | 0 | 0.00 | 21210.98 | 0.000 | 80.80% | 94.83% | `{"filegroups/native": 0.9560235142707825, "filetypes/macho": 0.989905059337616, "general": 0.9858856797218323}` |
| filetypes/npm | joint_or_at_fp_0 | 1876 | 1152 | 67.16% | 0 | 0.00 | 259708.38 | 0.000 | 80.36% | 79.66% | `{"filetypes/npm": 0.964945375919342, "general": 0.9889031052589417}` |
| filetypes/msi | joint_or_at_fp_0 | 5651 | 226 | 63.95% | 0 | 0.00 | 1316798.59 | 0.000 | 78.01% | 65.34% | `{"filetypes/msi": 0.8605440258979797, "general": 0.9851658344268799}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45437 | 61.50% | 0 | 0.00 | 6592.94 | 0.000 | 76.16% | 99.67% | `{"filegroups/scripts": 0.966874361038208, "filetypes/perl": 0.9905412793159485}` |
| filetypes/javascript | joint_or_at_fp_0 | 127217 | 739006 | 60.83% | 0 | 0.00 | 405.37 | 0.000 | 75.65% | 94.25% | `{"filegroups/scripts": 0.9934012293815613, "filetypes/javascript": 0.9843078255653381, "general": 0.9985212087631226}` |
| filetypes/whl | joint_or_at_fp_0 | 2500 | 4738 | 59.20% | 0 | 0.00 | 63207.80 | 0.000 | 74.37% | 85.91% | `{"filetypes/whl": 0.9944532513618469, "general": 0.9096306562423706}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32497 | 58868 | 52.29% | 0 | 0.00 | 5088.77 | 0.000 | 68.68% | 83.03% | `{"filegroups/source": 0.8723461627960205, "filetypes/kotlin": 0.8567541241645813, "general": 0.9301852583885193}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19285 | 50.98% | 0 | 0.00 | 15532.80 | 0.000 | 67.53% | 99.74% | `{"filegroups/scripts": 0.964593768119812, "filetypes/lua": 0.8219956159591675}` |
| filetypes/jar | joint_or_at_fp_0 | 3711 | 9271 | 50.20% | 0 | 0.00 | 32307.72 | 0.000 | 66.85% | 85.76% | `{"filetypes/jar": 0.97544264793396, "general": 0.9724860787391663}` |
| filetypes/scala | calibrate_inherited | 2 | 19272 | 50.00% | 0 | 0.00 | 15543.27 | 0.000 | 66.67% | 99.99% | `{"filegroups/source": 0.9822411564821043, "general": 0.9996190194825575}` |
| filetypes/php | joint_or_at_fp_0 | 5825 | 175559 | 47.95% | 0 | 0.00 | 1706.38 | 0.000 | 64.82% | 98.33% | `{"filegroups/scripts": 0.9867510199546814, "filetypes/php": 0.9919480681419373, "general": 0.9649550914764404}` |
| filetypes/pe | learned_blend_at_fp_0 | 1370421 | 177179 | 46.71% | 0 | 0.00 | 1690.78 | 0.000 | 63.68% | 52.81% | `{}` |
| filetypes/java_class | joint_or_at_fp_0 | 1980 | 835864 | 46.11% | 0 | 0.00 | 358.40 | 0.000 | 63.12% | 99.87% | `{"filegroups/portable": 0.9999483823776245, "filetypes/java_class": 0.9998989105224609, "general": 0.9815715551376343}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{}` |
| filetypes/crx | learned_blend_at_fp_0 | 805 | 184 | 98.39% | 0 | 0.00 | 1614933.21 | 0.000 | 99.19% | 98.69% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 526 | 97.89% | 0 | 0.00 | 567912.10 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.058191537857055664}` |
| filetypes/gem | joint_or_at_fp_0 | 772 | 1106 | 97.28% | 0 | 0.00 | 270495.37 | 0.000 | 98.62% | 98.88% | `{"filetypes/gem": 0.29505765438079834, "general": 0.9259820580482483}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 3766 | 96.78% | 0 | 0.00 | 79515.16 | 0.000 | 98.36% | 97.63% | `{"filetypes/pkg-info": 0.13838452100753784}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 90 | 277 | 95.56% | 0 | 0.00 | 1075664.70 | 0.000 | 97.73% | 98.91% | `{"filetypes/chrome-manifest": 0.6607028245925903}` |
| filetypes/xls | joint_or_at_fp_0 | 39677 | 20762 | 94.85% | 0 | 0.00 | 14427.88 | 0.000 | 97.35% | 96.62% | `{"filegroups/documents": 0.8492828011512756, "filetypes/xls": 0.9130752682685852}` |
| filetypes/elf | joint_or_at_fp_0 | 189688 | 283349 | 90.33% | 0 | 0.00 | 1057.25 | 0.000 | 94.92% | 96.12% | `{"filegroups/native": 0.9790063500404358, "filetypes/elf": 0.9984685778617859, "general": 0.986871063709259}` |
| filetypes/tar | joint_or_at_fp_0 | 30722 | 48820 | 85.54% | 0 | 0.00 | 6136.09 | 0.000 | 92.21% | 94.41% | `{"filetypes/tar": 0.993459165096283, "general": 0.9965975284576416}` |
| filetypes/package.json | learned_blend_at_fp_0 | 19404 | 27748 | 83.59% | 0 | 0.00 | 10795.63 | 0.000 | 91.06% | 93.25% | `{}` |
| filetypes/docx | joint_or_at_fp_0 | 4965 | 402 | 82.78% | 0 | 0.00 | 742437.25 | 0.000 | 90.58% | 84.07% | `{"filegroups/documents": 0.9156664609909058, "filetypes/docx": 0.5880919098854065}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6720 | 78.07% | 0 | 0.00 | 44569.41 | 0.000 | 87.69% | 88.51% | `{"filegroups/documents": 0.6700654625892639, "filetypes/ole": 0.9968721270561218}` |
| filetypes/lnk | joint_or_at_fp_0 | 4617 | 1065 | 74.25% | 0 | 0.00 | 280894.17 | 0.000 | 85.22% | 79.07% | `{"filetypes/lnk": 0.9497115015983582, "general": 0.9987188577651978}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3418 | 446251 | 74.05% | 0 | 0.00 | 671.31 | 0.000 | 85.09% | 99.80% | `{"filetypes/python-bytecode": 0.9950478672981262}` |
| filetypes/shell | joint_or_at_fp_0 | 15777 | 77326 | 73.85% | 0 | 0.00 | 3874.08 | 0.000 | 84.96% | 95.57% | `{"filegroups/scripts": 0.9832287430763245, "filetypes/shell": 0.9643027186393738, "general": 0.969433605670929}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24717 | 73.72% | 0 | 0.00 | 12119.39 | 0.000 | 84.87% | 76.91% | `{"filegroups/documents": 0.9885914921760559, "filetypes/pdf": 0.9596382975578308, "general": 0.9770442247390747}` |
| filetypes/macho | joint_or_at_fp_0 | 2698 | 14122 | 67.79% | 0 | 0.00 | 21210.98 | 0.000 | 80.80% | 94.83% | `{"filegroups/native": 0.9560235142707825, "filetypes/macho": 0.989905059337616, "general": 0.9858856797218323}` |
| filetypes/npm | joint_or_at_fp_0 | 1876 | 1152 | 67.16% | 0 | 0.00 | 259708.38 | 0.000 | 80.36% | 79.66% | `{"filetypes/npm": 0.964945375919342, "general": 0.9889031052589417}` |
| filetypes/msi | joint_or_at_fp_0 | 5651 | 226 | 63.95% | 0 | 0.00 | 1316798.59 | 0.000 | 78.01% | 65.34% | `{"filetypes/msi": 0.8605440258979797, "general": 0.9851658344268799}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45437 | 61.50% | 0 | 0.00 | 6592.94 | 0.000 | 76.16% | 99.67% | `{"filegroups/scripts": 0.966874361038208, "filetypes/perl": 0.9905412793159485}` |
| filetypes/javascript | joint_or_at_fp_0 | 127217 | 739006 | 60.83% | 0 | 0.00 | 405.37 | 0.000 | 75.65% | 94.25% | `{"filegroups/scripts": 0.9934012293815613, "filetypes/javascript": 0.9843078255653381, "general": 0.9985212087631226}` |
| filetypes/whl | joint_or_at_fp_0 | 2500 | 4738 | 59.20% | 0 | 0.00 | 63207.80 | 0.000 | 74.37% | 85.91% | `{"filetypes/whl": 0.9944532513618469, "general": 0.9096306562423706}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32497 | 58868 | 52.29% | 0 | 0.00 | 5088.77 | 0.000 | 68.68% | 83.03% | `{"filegroups/source": 0.8723461627960205, "filetypes/kotlin": 0.8567541241645813, "general": 0.9301852583885193}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19285 | 50.98% | 0 | 0.00 | 15532.80 | 0.000 | 67.53% | 99.74% | `{"filegroups/scripts": 0.964593768119812, "filetypes/lua": 0.8219956159591675}` |
| filetypes/jar | joint_or_at_fp_0 | 3711 | 9271 | 50.20% | 0 | 0.00 | 32307.72 | 0.000 | 66.85% | 85.76% | `{"filetypes/jar": 0.97544264793396, "general": 0.9724860787391663}` |
| filetypes/scala | calibrate_inherited | 2 | 19272 | 50.00% | 0 | 0.00 | 15543.27 | 0.000 | 66.67% | 99.99% | `{"filegroups/source": 0.982221072481872, "general": 0.9995949515780225}` |
| filetypes/php | joint_or_at_fp_0 | 5825 | 175559 | 47.95% | 0 | 0.00 | 1706.38 | 0.000 | 64.82% | 98.33% | `{"filegroups/scripts": 0.9867510199546814, "filetypes/php": 0.9919480681419373, "general": 0.9649550914764404}` |
| filetypes/pe | learned_blend_at_fp_0 | 1370421 | 177179 | 46.71% | 0 | 0.00 | 1690.78 | 0.000 | 63.68% | 52.81% | `{}` |
| filetypes/java_class | joint_or_at_fp_0 | 1980 | 835864 | 46.11% | 0 | 0.00 | 358.40 | 0.000 | 63.12% | 99.87% | `{"filegroups/portable": 0.9999483823776245, "filetypes/java_class": 0.9998989105224609, "general": 0.9815715551376343}` |
| filetypes/python | joint_or_at_fp_0 | 20794 | 268938 | 41.01% | 0 | 0.00 | 1113.91 | 0.000 | 58.16% | 95.77% | `{"filegroups/scripts": 0.9973414540290833, "filetypes/python": 0.999884843826294, "general": 0.993659257888794}` |
