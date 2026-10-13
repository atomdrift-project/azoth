# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `5922715835`
- Rows: 20801151 (3078117 malware, 17723034 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 127 | 275 | 99.21% | 0 | 0.00 | 1083445.18 | 0.000 | 99.60% | 99.75% | `{"filegroups/media": 0.9433440566062927, "filetypes/bmp": 0.9416564702987671, "general": 0.9807073473930359}` |
| filetypes/jsp | joint_or_at_fp_0 | 264 | 80 | 98.11% | 0 | 0.00 | 3675419.78 | 0.000 | 99.04% | 98.55% | `{"filetypes/jsp": 0.7447940707206726, "general": 0.9927338361740112}` |
| filetypes/applescript | learned_blend_at_fp_0 | 55 | 598 | 96.36% | 0 | 0.00 | 499705.87 | 0.000 | 98.15% | 99.69% | `{}` |
| filetypes/mp3 | joint_or_at_fp_0 | 196 | 356 | 91.84% | 0 | 0.00 | 837967.15 | 0.000 | 95.74% | 97.10% | `{"filegroups/media": 0.3404707610607147, "filetypes/mp3": 0.518356442451477}` |
| filetypes/dex | joint_or_at_fp_0 | 104 | 269 | 87.50% | 0 | 0.00 | 1107476.94 | 0.000 | 93.33% | 96.51% | `{"filetypes/dex": 0.8393434286117554, "general": 0.9548897743225098}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 100 | 85.35% | 0 | 0.00 | 2951304.96 | 0.000 | 92.10% | 86.87% | `{"filetypes/cab": 0.7533257603645325, "general": 0.6897558569908142}` |
| filetypes/elf | joint_or_at_fp_0 | 197908 | 907448 | 84.20% | 0 | 0.00 | 330.13 | 0.000 | 91.42% | 97.17% | `{"filegroups/native": 0.9954860806465149, "filetypes/elf": 0.9997566342353821, "general": 0.9986891150474548}` |
| filetypes/asar | joint_or_at_fp_0 | 201 | 366 | 76.62% | 0 | 0.00 | 815165.45 | 0.000 | 86.76% | 91.71% | `{"filetypes/asar": 0.9673223495483398, "general": 0.7085074782371521}` |
| filetypes/dos_com | joint_or_at_fp_0 | 6255 | 187 | 76.04% | 0 | 0.00 | 1589232.16 | 0.000 | 86.39% | 76.73% | `{"filetypes/dos_com": 0.5287858247756958}` |
| filetypes/asp | joint_or_at_fp_0 | 286 | 67 | 73.08% | 0 | 0.00 | 4372755.48 | 0.000 | 84.44% | 78.19% | `{"general": 0.9933769702911377}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 96 | 72.05% | 0 | 0.00 | 3072367.68 | 0.000 | 83.76% | 80.31% | `{"filetypes/chm": 0.865106999874115, "general": 0.995146632194519}` |
| filetypes/7z | joint_or_at_fp_0 | 8773 | 403 | 71.96% | 0 | 0.00 | 740601.81 | 0.000 | 83.69% | 73.19% | `{"filetypes/7z": 0.9964820146560669, "general": 0.9844080209732056}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3380 | 9150 | 71.54% | 0 | 0.00 | 32734.88 | 0.000 | 83.41% | 92.32% | `{"filetypes/python_sdist": 0.9991787075996399, "general": 0.9668827652931213}` |
| filetypes/ruby | joint_or_at_fp_0 | 260 | 197362 | 66.92% | 0 | 0.00 | 1517.88 | 0.000 | 80.18% | 99.96% | `{"filegroups/scripts": 0.9887321591377258, "general": 0.9141725301742554}` |
| filetypes/swift | joint_or_at_fp_0 | 58 | 44785 | 65.52% | 0 | 0.00 | 6688.92 | 0.000 | 79.17% | 99.96% | `{"general": 0.3926757872104645}` |
| filetypes/ico | joint_or_at_fp_0 | 265 | 722 | 63.77% | 0 | 0.00 | 414061.76 | 0.000 | 77.88% | 90.27% | `{"filetypes/ico": 0.6936132907867432}` |
| filetypes/tar | joint_or_at_fp_0 | 24039 | 91343 | 61.41% | 0 | 0.00 | 3279.60 | 0.000 | 76.09% | 91.96% | `{"filetypes/tar": 0.9971569180488586, "general": 0.9922420978546143}` |
| filetypes/groovy | learned_blend_at_fp_0 | 76 | 10896 | 57.89% | 0 | 0.00 | 27490.09 | 0.000 | 73.33% | 99.71% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4735 | 1208 | 56.83% | 0 | 0.00 | 247683.84 | 0.000 | 72.48% | 65.61% | `{"filetypes/lnk": 0.9764344692230225, "general": 0.9963150024414062}` |
| filetypes/xpi | learned_blend_at_fp_0 | 90 | 4828 | 56.67% | 0 | 0.00 | 62029.89 | 0.000 | 72.34% | 99.21% | `{}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3450 | 1227661 | 50.75% | 0 | 0.00 | 244.02 | 0.000 | 67.33% | 99.86% | `{"filetypes/python_bytecode": 0.9999144673347473, "general": 0.9909624457359314}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27513 | 83805 | 46.60% | 0 | 0.00 | 3574.58 | 0.000 | 63.57% | 86.80% | `{"filegroups/source": 0.9598856568336487, "filetypes/kotlin": 0.9669460654258728, "general": 0.9973267912864685}` |
| filetypes/python | joint_or_at_fp_0 | 23635 | 679755 | 46.57% | 0 | 0.00 | 440.71 | 0.000 | 63.55% | 98.20% | `{"filegroups/scripts": 0.9971794486045837, "filetypes/python": 0.9960105419158936, "general": 0.995683491230011}` |
| filetypes/html | joint_or_at_fp_0 | 91714 | 428507 | 45.61% | 0 | 0.00 | 699.11 | 0.000 | 62.65% | 90.41% | `{"filegroups/documents": 0.9991175532341003, "filetypes/html": 0.999921441078186, "general": 0.9957936406135559}` |
| filetypes/npm | joint_or_at_fp_0 | 25502 | 235224 | 44.88% | 0 | 0.00 | 1273.56 | 0.000 | 61.96% | 94.61% | `{"filetypes/npm": 0.9999179840087891, "general": 0.9992259740829468}` |
| filetypes/pdf | joint_or_at_fp_0 | 178761 | 29911 | 44.68% | 0 | 0.00 | 10014.99 | 0.000 | 61.76% | 52.61% | `{"filegroups/documents": 0.9975168704986572, "filetypes/pdf": 0.975563645362854, "general": 0.9851721525192261}` |
| filetypes/perl | joint_or_at_fp_0 | 448 | 81115 | 43.08% | 0 | 0.00 | 3693.12 | 0.000 | 60.22% | 99.69% | `{"filegroups/scripts": 0.9909111261367798, "filetypes/perl": 0.9942907691001892, "general": 0.9985353350639343}` |
| filetypes/rtf | joint_or_at_fp_0 | 6124 | 1021 | 41.98% | 0 | 0.00 | 292981.55 | 0.000 | 59.14% | 50.27% | `{"filegroups/documents": 0.999854564666748, "filetypes/rtf": 0.992590069770813, "general": 0.9986187815666199}` |
| filetypes/powershell | joint_or_at_fp_0 | 6283 | 6230 | 41.84% | 0 | 0.00 | 48074.03 | 0.000 | 59.00% | 70.80% | `{"filegroups/scripts": 0.9986525177955627, "filetypes/powershell": 0.992750346660614, "general": 0.9980500936508179}` |
| filetypes/jar | joint_or_at_fp_0 | 3821 | 41669 | 37.79% | 0 | 0.00 | 7189.10 | 0.000 | 54.85% | 94.77% | `{"filetypes/jar": 0.9971730709075928, "general": 0.9988665580749512}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 127 | 275 | 99.21% | 0 | 0.00 | 1083445.18 | 0.000 | 99.60% | 99.75% | `{"filegroups/media": 0.9433440566062927, "filetypes/bmp": 0.9416564702987671, "general": 0.9807073473930359}` |
| filetypes/jsp | joint_or_at_fp_0 | 264 | 80 | 98.11% | 0 | 0.00 | 3675419.78 | 0.000 | 99.04% | 98.55% | `{"filetypes/jsp": 0.7447940707206726, "general": 0.9927338361740112}` |
| filetypes/applescript | learned_blend_at_fp_0 | 55 | 598 | 96.36% | 0 | 0.00 | 499705.87 | 0.000 | 98.15% | 99.69% | `{}` |
| filetypes/mp3 | joint_or_at_fp_0 | 196 | 356 | 91.84% | 0 | 0.00 | 837967.15 | 0.000 | 95.74% | 97.10% | `{"filegroups/media": 0.3404707610607147, "filetypes/mp3": 0.518356442451477}` |
| filetypes/dex | joint_or_at_fp_0 | 104 | 269 | 87.50% | 0 | 0.00 | 1107476.94 | 0.000 | 93.33% | 96.51% | `{"filetypes/dex": 0.8393434286117554, "general": 0.9548897743225098}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 100 | 85.35% | 0 | 0.00 | 2951304.96 | 0.000 | 92.10% | 86.87% | `{"filetypes/cab": 0.7533257603645325, "general": 0.6897558569908142}` |
| filetypes/elf | joint_or_at_fp_0 | 197908 | 907448 | 84.20% | 0 | 0.00 | 330.13 | 0.000 | 91.42% | 97.17% | `{"filegroups/native": 0.9954860806465149, "filetypes/elf": 0.9997566342353821, "general": 0.9986891150474548}` |
| filetypes/asar | joint_or_at_fp_0 | 201 | 366 | 76.62% | 0 | 0.00 | 815165.45 | 0.000 | 86.76% | 91.71% | `{"filetypes/asar": 0.9673223495483398, "general": 0.7085074782371521}` |
| filetypes/dos_com | joint_or_at_fp_0 | 6255 | 187 | 76.04% | 0 | 0.00 | 1589232.16 | 0.000 | 86.39% | 76.73% | `{"filetypes/dos_com": 0.5287858247756958}` |
| filetypes/asp | joint_or_at_fp_0 | 286 | 67 | 73.08% | 0 | 0.00 | 4372755.48 | 0.000 | 84.44% | 78.19% | `{"general": 0.9933769702911377}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 96 | 72.05% | 0 | 0.00 | 3072367.68 | 0.000 | 83.76% | 80.31% | `{"filetypes/chm": 0.865106999874115, "general": 0.995146632194519}` |
| filetypes/7z | joint_or_at_fp_0 | 8773 | 403 | 71.96% | 0 | 0.00 | 740601.81 | 0.000 | 83.69% | 73.19% | `{"filetypes/7z": 0.9964820146560669, "general": 0.9844080209732056}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 3380 | 9150 | 71.54% | 0 | 0.00 | 32734.88 | 0.000 | 83.41% | 92.32% | `{"filetypes/python_sdist": 0.9991787075996399, "general": 0.9668827652931213}` |
| filetypes/ruby | joint_or_at_fp_0 | 260 | 197362 | 66.92% | 0 | 0.00 | 1517.88 | 0.000 | 80.18% | 99.96% | `{"filegroups/scripts": 0.9887321591377258, "general": 0.9141725301742554}` |
| filetypes/swift | joint_or_at_fp_0 | 58 | 44785 | 65.52% | 0 | 0.00 | 6688.92 | 0.000 | 79.17% | 99.96% | `{"general": 0.3926757872104645}` |
| filetypes/ico | joint_or_at_fp_0 | 265 | 722 | 63.77% | 0 | 0.00 | 414061.76 | 0.000 | 77.88% | 90.27% | `{"filetypes/ico": 0.6936132907867432}` |
| filetypes/tar | joint_or_at_fp_0 | 24039 | 91343 | 61.41% | 0 | 0.00 | 3279.60 | 0.000 | 76.09% | 91.96% | `{"filetypes/tar": 0.9971569180488586, "general": 0.9922420978546143}` |
| filetypes/groovy | learned_blend_at_fp_0 | 76 | 10896 | 57.89% | 0 | 0.00 | 27490.09 | 0.000 | 73.33% | 99.71% | `{}` |
| filetypes/lnk | joint_or_at_fp_0 | 4735 | 1208 | 56.83% | 0 | 0.00 | 247683.84 | 0.000 | 72.48% | 65.61% | `{"filetypes/lnk": 0.9764344692230225, "general": 0.9963150024414062}` |
| filetypes/xpi | learned_blend_at_fp_0 | 90 | 4828 | 56.67% | 0 | 0.00 | 62029.89 | 0.000 | 72.34% | 99.21% | `{}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3450 | 1227661 | 50.75% | 0 | 0.00 | 244.02 | 0.000 | 67.33% | 99.86% | `{"filetypes/python_bytecode": 0.9999144673347473, "general": 0.9909624457359314}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27513 | 83805 | 46.60% | 0 | 0.00 | 3574.58 | 0.000 | 63.57% | 86.80% | `{"filegroups/source": 0.9598856568336487, "filetypes/kotlin": 0.9669460654258728, "general": 0.9973267912864685}` |
| filetypes/python | joint_or_at_fp_0 | 23635 | 679755 | 46.57% | 0 | 0.00 | 440.71 | 0.000 | 63.55% | 98.20% | `{"filegroups/scripts": 0.9971794486045837, "filetypes/python": 0.9960105419158936, "general": 0.995683491230011}` |
| filetypes/html | joint_or_at_fp_0 | 91714 | 428507 | 45.61% | 0 | 0.00 | 699.11 | 0.000 | 62.65% | 90.41% | `{"filegroups/documents": 0.9991175532341003, "filetypes/html": 0.999921441078186, "general": 0.9957936406135559}` |
| filetypes/npm | joint_or_at_fp_0 | 25502 | 235224 | 44.88% | 0 | 0.00 | 1273.56 | 0.000 | 61.96% | 94.61% | `{"filetypes/npm": 0.9999179840087891, "general": 0.9992259740829468}` |
| filetypes/pdf | joint_or_at_fp_0 | 178761 | 29911 | 44.68% | 0 | 0.00 | 10014.99 | 0.000 | 61.76% | 52.61% | `{"filegroups/documents": 0.9975168704986572, "filetypes/pdf": 0.975563645362854, "general": 0.9851721525192261}` |
| filetypes/perl | joint_or_at_fp_0 | 448 | 81115 | 43.08% | 0 | 0.00 | 3693.12 | 0.000 | 60.22% | 99.69% | `{"filegroups/scripts": 0.9909111261367798, "filetypes/perl": 0.9942907691001892, "general": 0.9985353350639343}` |
| filetypes/rtf | joint_or_at_fp_0 | 6124 | 1021 | 41.98% | 0 | 0.00 | 292981.55 | 0.000 | 59.14% | 50.27% | `{"filegroups/documents": 0.999854564666748, "filetypes/rtf": 0.992590069770813, "general": 0.9986187815666199}` |
| filetypes/powershell | joint_or_at_fp_0 | 6283 | 6230 | 41.84% | 0 | 0.00 | 48074.03 | 0.000 | 59.00% | 70.80% | `{"filegroups/scripts": 0.9986525177955627, "filetypes/powershell": 0.992750346660614, "general": 0.9980500936508179}` |
| filetypes/jar | joint_or_at_fp_0 | 3821 | 41669 | 37.79% | 0 | 0.00 | 7189.10 | 0.000 | 54.85% | 94.77% | `{"filetypes/jar": 0.9971730709075928, "general": 0.9988665580749512}` |
