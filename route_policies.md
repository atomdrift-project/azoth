# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `5659125162`
- Rows: 20074839 (2965462 malware, 17109377 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | learned_blend_at_fp_1 | 130 | 273 | 98.46% | 0 | 0.00 | 1091339.04 | 0.000 | 99.22% | 99.50% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 573 | 92.86% | 0 | 0.00 | 521451.10 | 0.000 | 96.30% | 99.36% | `{"general": 0.9515527486801147}` |
| filetypes/mp3 | joint_or_at_fp_0 | 196 | 347 | 91.84% | 0 | 0.00 | 859607.49 | 0.000 | 95.74% | 97.05% | `{"filetypes/mp3": 0.35080841183662415}` |
| filetypes/asar | joint_or_at_fp_0 | 200 | 364 | 86.00% | 0 | 0.00 | 819625.97 | 0.000 | 92.47% | 95.04% | `{"filetypes/asar": 0.9106354117393494, "general": 0.7690014839172363}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 97 | 82.70% | 0 | 0.00 | 3041180.40 | 0.000 | 90.53% | 84.44% | `{"filetypes/cab": 0.9173753261566162, "general": 0.7928454279899597}` |
| filetypes/elf | joint_or_at_fp_0 | 197676 | 903333 | 82.40% | 0 | 0.00 | 331.63 | 0.000 | 90.35% | 96.84% | `{"filegroups/native": 0.9967737197875977, "filetypes/elf": 0.9998582601547241, "general": 0.9982624053955078}` |
| filetypes/html | learned_blend_at_fp_0 | 355 | 297736 | 78.31% | 0 | 0.00 | 1006.17 | 0.000 | 87.84% | 99.97% | `{}` |
| filetypes/dos_com | learned_blend_at_fp_0 | 6038 | 164 | 76.78% | 0 | 0.00 | 1810083.60 | 0.000 | 86.87% | 77.39% | `{}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3349 | 8604 | 73.28% | 0 | 0.00 | 34811.84 | 0.000 | 84.58% | 92.51% | `{"filetypes/python_sdist": 0.9996329545974731, "general": 0.9397236108779907}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 195310 | 70.43% | 0 | 0.00 | 1533.82 | 0.000 | 82.65% | 99.96% | `{"filegroups/scripts": 0.9482586979866028, "filetypes/ruby": 0.849793016910553, "general": 0.9058483839035034}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 401 | 67.26% | 0 | 0.00 | 744281.81 | 0.000 | 80.43% | 68.70% | `{"filetypes/7z": 0.9957177042961121, "general": 0.997365415096283}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 656 | 64.02% | 0 | 0.00 | 455625.37 | 0.000 | 78.06% | 89.67% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 57.38% | 0 | 0.00 | 255936.45 | 0.000 | 72.92% | 65.82% | `{"filetypes/lnk": 0.9913544654846191, "general": 0.9959377646446228}` |
| filetypes/tar | joint_or_at_fp_0 | 24243 | 88782 | 56.32% | 0 | 0.00 | 3374.20 | 0.000 | 72.06% | 90.63% | `{"filetypes/tar": 0.9986011981964111, "general": 0.9964267611503601}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44784 | 55.93% | 0 | 0.00 | 6689.07 | 0.000 | 71.74% | 99.94% | `{"general": 0.1371200978755951}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 267 | 54.02% | 0 | 0.00 | 1115726.19 | 0.000 | 70.15% | 88.70% | `{"filetypes/dex": 0.8569322228431702, "general": 0.9737224578857422}` |
| filetypes/shell | joint_or_at_fp_0 | 18942 | 164411 | 52.63% | 0 | 0.00 | 1822.08 | 0.000 | 68.97% | 95.11% | `{"filegroups/scripts": 0.996167778968811, "filetypes/shell": 0.996054470539093, "general": 0.9964048862457275}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 99 | 50.41% | 0 | 0.00 | 2980667.38 | 0.000 | 67.03% | 64.72% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9923793077468872}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3449 | 1226152 | 49.03% | 0 | 0.00 | 244.32 | 0.000 | 65.80% | 99.86% | `{"filetypes/python_bytecode": 0.9999752640724182, "general": 0.9857680797576904}` |
| filetypes/python | joint_or_at_fp_0 | 23536 | 677610 | 47.79% | 0 | 0.00 | 442.10 | 0.000 | 64.68% | 98.25% | `{"filegroups/scripts": 0.9972382187843323, "filetypes/python": 0.9947623610496521, "general": 0.995690643787384}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27343 | 83208 | 47.36% | 0 | 0.00 | 3600.23 | 0.000 | 64.28% | 86.98% | `{"filegroups/source": 0.9799506068229675, "filetypes/kotlin": 0.9814198017120361, "general": 0.9982767105102539}` |
| filetypes/perl | joint_or_at_fp_0 | 439 | 80399 | 43.96% | 0 | 0.00 | 3726.01 | 0.000 | 61.08% | 99.70% | `{"filegroups/scripts": 0.9929059743881226, "filetypes/perl": 0.9967522025108337, "general": 0.9962106943130493}` |
| filetypes/npm | joint_or_at_fp_0 | 24495 | 203554 | 43.68% | 0 | 0.00 | 1471.70 | 0.000 | 60.80% | 93.95% | `{"filetypes/npm": 0.9999449253082275, "general": 0.9993087649345398}` |
| filetypes/xpi | learned_blend_at_fp_0 | 72 | 4575 | 43.06% | 0 | 0.00 | 65459.05 | 0.000 | 60.19% | 99.12% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6133 | 1021 | 39.85% | 0 | 0.00 | 292981.55 | 0.000 | 56.99% | 48.43% | `{"filegroups/documents": 0.9998971223831177, "filetypes/rtf": 0.9931366443634033, "general": 0.9985930919647217}` |
| filetypes/lua | joint_or_at_fp_0 | 92 | 28737 | 39.13% | 0 | 0.00 | 10424.11 | 0.000 | 56.25% | 99.81% | `{"filegroups/scripts": 0.9936493635177612, "filetypes/lua": 0.998979389667511, "general": 0.9848855137825012}` |
| filetypes/rar | calibrate_inherited | 22194 | 53 | 37.78% | 0 | 0.00 | 5495548.85 | 0.000 | 54.84% | 37.92% | `{"general": 0.9994269422516724}` |
| filetypes/powershell | joint_or_at_fp_0 | 5952 | 6164 | 37.62% | 0 | 0.00 | 48588.65 | 0.000 | 54.67% | 69.35% | `{"filegroups/scripts": 0.9984310865402222, "filetypes/powershell": 0.9960401058197021, "general": 0.9981516599655151}` |
| filetypes/zip | joint_or_at_fp_0 | 107347 | 100672 | 36.94% | 0 | 0.00 | 2975.69 | 0.000 | 53.95% | 67.46% | `{"filetypes/zip": 0.9994208216667175, "general": 0.9973596930503845}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 253 | 17899 | 30.04% | 0 | 0.00 | 16735.47 | 0.000 | 46.20% | 99.02% | `{"filetypes/pkg_info": 0.996900737285614, "general": 0.9904680252075195}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | learned_blend_at_fp_1 | 130 | 273 | 98.46% | 0 | 0.00 | 1091339.04 | 0.000 | 99.22% | 99.50% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 573 | 92.86% | 0 | 0.00 | 521451.10 | 0.000 | 96.30% | 99.36% | `{"general": 0.9515527486801147}` |
| filetypes/mp3 | joint_or_at_fp_0 | 196 | 347 | 91.84% | 0 | 0.00 | 859607.49 | 0.000 | 95.74% | 97.05% | `{"filetypes/mp3": 0.35080841183662415}` |
| filetypes/asar | joint_or_at_fp_0 | 200 | 364 | 86.00% | 0 | 0.00 | 819625.97 | 0.000 | 92.47% | 95.04% | `{"filetypes/asar": 0.9106354117393494, "general": 0.7690014839172363}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 97 | 82.70% | 0 | 0.00 | 3041180.40 | 0.000 | 90.53% | 84.44% | `{"filetypes/cab": 0.9173753261566162, "general": 0.7928454279899597}` |
| filetypes/elf | joint_or_at_fp_0 | 197676 | 903333 | 82.40% | 0 | 0.00 | 331.63 | 0.000 | 90.35% | 96.84% | `{"filegroups/native": 0.9967737197875977, "filetypes/elf": 0.9998582601547241, "general": 0.9982624053955078}` |
| filetypes/html | learned_blend_at_fp_0 | 355 | 297736 | 78.31% | 0 | 0.00 | 1006.17 | 0.000 | 87.84% | 99.97% | `{}` |
| filetypes/dos_com | learned_blend_at_fp_0 | 6038 | 164 | 76.78% | 0 | 0.00 | 1810083.60 | 0.000 | 86.87% | 77.39% | `{}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3349 | 8604 | 73.28% | 0 | 0.00 | 34811.84 | 0.000 | 84.58% | 92.51% | `{"filetypes/python_sdist": 0.9996329545974731, "general": 0.9397236108779907}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 195310 | 70.43% | 0 | 0.00 | 1533.82 | 0.000 | 82.65% | 99.96% | `{"filegroups/scripts": 0.9482586979866028, "filetypes/ruby": 0.849793016910553, "general": 0.9058483839035034}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 401 | 67.26% | 0 | 0.00 | 744281.81 | 0.000 | 80.43% | 68.70% | `{"filetypes/7z": 0.9957177042961121, "general": 0.997365415096283}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 656 | 64.02% | 0 | 0.00 | 455625.37 | 0.000 | 78.06% | 89.67% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 57.38% | 0 | 0.00 | 255936.45 | 0.000 | 72.92% | 65.82% | `{"filetypes/lnk": 0.9913544654846191, "general": 0.9959377646446228}` |
| filetypes/tar | joint_or_at_fp_0 | 24243 | 88782 | 56.32% | 0 | 0.00 | 3374.20 | 0.000 | 72.06% | 90.63% | `{"filetypes/tar": 0.9986011981964111, "general": 0.9964267611503601}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44784 | 55.93% | 0 | 0.00 | 6689.07 | 0.000 | 71.74% | 99.94% | `{"general": 0.1371200978755951}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 267 | 54.02% | 0 | 0.00 | 1115726.19 | 0.000 | 70.15% | 88.70% | `{"filetypes/dex": 0.8569322228431702, "general": 0.9737224578857422}` |
| filetypes/shell | joint_or_at_fp_0 | 18942 | 164411 | 52.63% | 0 | 0.00 | 1822.08 | 0.000 | 68.97% | 95.11% | `{"filegroups/scripts": 0.996167778968811, "filetypes/shell": 0.996054470539093, "general": 0.9964048862457275}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 99 | 50.41% | 0 | 0.00 | 2980667.38 | 0.000 | 67.03% | 64.72% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9923793077468872}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3449 | 1226152 | 49.03% | 0 | 0.00 | 244.32 | 0.000 | 65.80% | 99.86% | `{"filetypes/python_bytecode": 0.9999752640724182, "general": 0.9857680797576904}` |
| filetypes/python | joint_or_at_fp_0 | 23536 | 677610 | 47.79% | 0 | 0.00 | 442.10 | 0.000 | 64.68% | 98.25% | `{"filegroups/scripts": 0.9972382187843323, "filetypes/python": 0.9947623610496521, "general": 0.995690643787384}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27343 | 83208 | 47.36% | 0 | 0.00 | 3600.23 | 0.000 | 64.28% | 86.98% | `{"filegroups/source": 0.9799506068229675, "filetypes/kotlin": 0.9814198017120361, "general": 0.9982767105102539}` |
| filetypes/perl | joint_or_at_fp_0 | 439 | 80399 | 43.96% | 0 | 0.00 | 3726.01 | 0.000 | 61.08% | 99.70% | `{"filegroups/scripts": 0.9929059743881226, "filetypes/perl": 0.9967522025108337, "general": 0.9962106943130493}` |
| filetypes/npm | joint_or_at_fp_0 | 24495 | 203554 | 43.68% | 0 | 0.00 | 1471.70 | 0.000 | 60.80% | 93.95% | `{"filetypes/npm": 0.9999449253082275, "general": 0.9993087649345398}` |
| filetypes/xpi | learned_blend_at_fp_0 | 72 | 4575 | 43.06% | 0 | 0.00 | 65459.05 | 0.000 | 60.19% | 99.12% | `{}` |
| filetypes/rar | calibrate_inherited | 22194 | 53 | 42.87% | 0 | 0.00 | 5495548.85 | 0.000 | 60.01% | 43.00% | `{"general": 0.9992508387410434}` |
| filetypes/rtf | joint_or_at_fp_0 | 6133 | 1021 | 39.85% | 0 | 0.00 | 292981.55 | 0.000 | 56.99% | 48.43% | `{"filegroups/documents": 0.9998971223831177, "filetypes/rtf": 0.9931366443634033, "general": 0.9985930919647217}` |
| filetypes/lua | joint_or_at_fp_0 | 92 | 28737 | 39.13% | 0 | 0.00 | 10424.11 | 0.000 | 56.25% | 99.81% | `{"filegroups/scripts": 0.9936493635177612, "filetypes/lua": 0.998979389667511, "general": 0.9848855137825012}` |
| filetypes/powershell | joint_or_at_fp_0 | 5952 | 6164 | 37.62% | 0 | 0.00 | 48588.65 | 0.000 | 54.67% | 69.35% | `{"filegroups/scripts": 0.9984310865402222, "filetypes/powershell": 0.9960401058197021, "general": 0.9981516599655151}` |
| filetypes/zip | joint_or_at_fp_0 | 107347 | 100672 | 36.94% | 0 | 0.00 | 2975.69 | 0.000 | 53.95% | 67.46% | `{"filetypes/zip": 0.9994208216667175, "general": 0.9973596930503845}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 253 | 17899 | 30.04% | 0 | 0.00 | 16735.47 | 0.000 | 46.20% | 99.02% | `{"filetypes/pkg_info": 0.996900737285614, "general": 0.9904680252075195}` |
