# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `4351728144`
- Rows: 18322760 (2682277 malware, 15640483 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 191 | 303 | 96.86% | 0 | 0.00 | 983819.04 | 0.000 | 98.40% | 98.79% | `{"filetypes/asar": 0.89125657081604, "general": 0.8482485413551331}` |
| filetypes/cab | joint_or_at_fp_0 | 880 | 84 | 95.34% | 0 | 0.00 | 3503503.06 | 0.000 | 97.61% | 95.75% | `{"filetypes/cab": 0.8924787044525146, "general": 0.6824786067008972}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 529 | 92.73% | 0 | 0.00 | 564700.54 | 0.000 | 96.23% | 99.32% | `{"filetypes/applescript": 0.9634076952934265, "general": 0.9485079646110535}` |
| filetypes/7z | joint_or_at_fp_0 | 9052 | 340 | 90.64% | 0 | 0.00 | 877227.44 | 0.000 | 95.09% | 90.98% | `{"filetypes/7z": 0.8367222547531128, "general": 0.9841593503952026}` |
| filetypes/elf | joint_or_at_fp_0 | 196854 | 859062 | 87.62% | 0 | 0.00 | 348.72 | 0.000 | 93.40% | 97.69% | `{"filegroups/native": 0.995327353477478, "filetypes/elf": 0.9998093247413635, "general": 0.9947900176048279}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 72 | 85.66% | 0 | 0.00 | 4075368.62 | 0.000 | 92.27% | 88.92% | `{"filetypes/chm": 0.8833631873130798, "general": 0.7534775733947754}` |
| filetypes/shell | joint_or_at_fp_0 | 18794 | 164580 | 66.18% | 0 | 0.00 | 1820.21 | 0.000 | 79.65% | 96.53% | `{"filegroups/scripts": 0.9989709258079529, "filetypes/shell": 0.9950119853019714, "general": 0.9968542456626892}` |
| filetypes/tar | joint_or_at_fp_0 | 34291 | 82766 | 65.43% | 0 | 0.00 | 3619.45 | 0.000 | 79.10% | 89.87% | `{"filetypes/tar": 0.9995710849761963, "general": 0.9918844699859619}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 34534 | 61.20% | 0 | 0.00 | 8674.36 | 0.000 | 75.93% | 97.03% | `{"filegroups/native": 0.9774362444877625, "filetypes/macho": 0.9904804229736328}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 957 | 57.45% | 0 | 0.00 | 312544.24 | 0.000 | 72.98% | 63.10% | `{"filegroups/documents": 0.9998659491539001, "filetypes/rtf": 0.9935286045074463, "general": 0.9991967678070068}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 977 | 1395 | 56.40% | 0 | 0.00 | 214517.42 | 0.000 | 72.12% | 82.04% | `{"filetypes/python_sdist": 0.9895145893096924, "general": 0.9614319205284119}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87713 | 31834 | 54.30% | 0 | 0.00 | 9410.04 | 0.000 | 70.39% | 66.47% | `{"filetypes/ole_doc": 0.9993669986724854, "general": 0.9982293844223022}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27775 | 52.83% | 0 | 0.00 | 10785.13 | 0.000 | 69.14% | 99.82% | `{"filetypes/lua": 0.7376510500907898, "general": 0.9806055426597595}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 324 | 52.38% | 0 | 0.00 | 920347.36 | 0.000 | 68.75% | 92.25% | `{"filetypes/dmg": 0.8825401663780212, "general": 0.9622342586517334}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44607 | 50.72% | 0 | 0.00 | 6715.61 | 0.000 | 67.31% | 99.92% | `{"filegroups/source": 0.9316802024841309}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 5631 | 49.31% | 0 | 0.00 | 53186.57 | 0.000 | 66.05% | 73.75% | `{"filegroups/scripts": 0.9984983801841736, "filetypes/powershell": 0.9950370192527771, "general": 0.9963555335998535}` |
| filetypes/pe | joint_or_at_fp_0 | 1379506 | 251747 | 46.40% | 0 | 0.00 | 1189.97 | 0.000 | 63.38% | 54.67% | `{"filegroups/native": 0.9996936321258545, "filetypes/pe": 0.9994720816612244, "general": 0.999785840511322}` |
| filetypes/package.json | joint_or_at_fp_0 | 22369 | 70855 | 45.86% | 0 | 0.00 | 4227.89 | 0.000 | 62.88% | 87.01% | `{"filegroups/config": 0.9999793767929077, "filetypes/package.json": 0.9998695850372314, "general": 0.9993761777877808}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 84141 | 45.64% | 0 | 0.00 | 3560.31 | 0.000 | 62.67% | 84.91% | `{"filegroups/source": 0.991012692451477, "filetypes/kotlin": 0.9779708385467529, "general": 0.9964229464530945}` |
| filetypes/npm | joint_or_at_fp_0 | 17401 | 104932 | 45.62% | 0 | 0.00 | 2854.89 | 0.000 | 62.65% | 92.26% | `{"filetypes/npm": 0.9993012547492981, "general": 0.9994699954986572}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 185673 | 45.54% | 0 | 0.00 | 1613.43 | 0.000 | 62.58% | 99.91% | `{"filegroups/documents": 0.9979287385940552, "general": 0.9659225940704346}` |
| filetypes/javascript | joint_or_at_fp_0 | 144979 | 1712861 | 43.25% | 0 | 0.00 | 174.90 | 0.000 | 60.39% | 95.57% | `{"filegroups/scripts": 0.9986911416053772, "filetypes/javascript": 0.9988570213317871, "general": 0.994106650352478}` |
| filetypes/gem | joint_or_at_fp_0 | 2111 | 47842 | 43.11% | 0 | 0.00 | 6261.52 | 0.000 | 60.24% | 97.60% | `{"filetypes/gem": 0.999733030796051, "general": 0.9779737591743469}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 78637 | 43.07% | 0 | 0.00 | 3809.50 | 0.000 | 60.21% | 99.71% | `{"filegroups/scripts": 0.9984470009803772, "filetypes/perl": 0.9994779229164124, "general": 0.9901589155197144}` |
| filetypes/python | joint_or_at_fp_0 | 23631 | 661889 | 39.89% | 0 | 0.00 | 452.60 | 0.000 | 57.03% | 97.93% | `{"filegroups/scripts": 0.9988007545471191, "filetypes/python": 0.9986681342124939, "general": 0.9951849579811096}` |
| filetypes/lnk | joint_or_at_fp_0 | 4696 | 1155 | 37.01% | 0 | 0.00 | 259034.68 | 0.000 | 54.03% | 49.44% | `{"filetypes/lnk": 0.9936132431030273, "general": 0.9971751570701599}` |
| filetypes/php | joint_or_at_fp_0 | 7218 | 615929 | 33.00% | 0 | 0.00 | 486.38 | 0.000 | 49.62% | 99.22% | `{"filegroups/scripts": 0.9991531372070312, "filetypes/php": 0.9972749948501587, "general": 0.988580048084259}` |
| filetypes/ruby | joint_or_at_fp_0 | 402 | 183842 | 32.09% | 0 | 0.00 | 1629.50 | 0.000 | 48.59% | 99.85% | `{"filegroups/scripts": 0.9865238666534424, "filetypes/ruby": 0.9992597103118896}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1117 | 30.69% | 0 | 0.00 | 267835.15 | 0.000 | 46.97% | 94.25% | `{"filetypes/chrome_manifest": 0.9806844592094421, "general": 0.9512924551963806}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9515 | 30.00% | 0 | 0.00 | 31479.36 | 0.000 | 46.15% | 99.20% | `{"general": 0.0380796454846859}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 191 | 303 | 96.86% | 0 | 0.00 | 983819.04 | 0.000 | 98.40% | 98.79% | `{"filetypes/asar": 0.89125657081604, "general": 0.8482485413551331}` |
| filetypes/cab | joint_or_at_fp_0 | 880 | 84 | 95.34% | 0 | 0.00 | 3503503.06 | 0.000 | 97.61% | 95.75% | `{"filetypes/cab": 0.8924787044525146, "general": 0.6824786067008972}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 529 | 92.73% | 0 | 0.00 | 564700.54 | 0.000 | 96.23% | 99.32% | `{"filetypes/applescript": 0.9634076952934265, "general": 0.9485079646110535}` |
| filetypes/7z | joint_or_at_fp_0 | 9052 | 340 | 90.64% | 0 | 0.00 | 877227.44 | 0.000 | 95.09% | 90.98% | `{"filetypes/7z": 0.8367222547531128, "general": 0.9841593503952026}` |
| filetypes/elf | joint_or_at_fp_0 | 196854 | 859062 | 87.62% | 0 | 0.00 | 348.72 | 0.000 | 93.40% | 97.69% | `{"filegroups/native": 0.995327353477478, "filetypes/elf": 0.9998093247413635, "general": 0.9947900176048279}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 72 | 85.66% | 0 | 0.00 | 4075368.62 | 0.000 | 92.27% | 88.92% | `{"filetypes/chm": 0.8833631873130798, "general": 0.7534775733947754}` |
| filetypes/shell | joint_or_at_fp_0 | 18794 | 164580 | 66.18% | 0 | 0.00 | 1820.21 | 0.000 | 79.65% | 96.53% | `{"filegroups/scripts": 0.9989709258079529, "filetypes/shell": 0.9950119853019714, "general": 0.9968542456626892}` |
| filetypes/tar | joint_or_at_fp_0 | 34291 | 82766 | 65.43% | 0 | 0.00 | 3619.45 | 0.000 | 79.10% | 89.87% | `{"filetypes/tar": 0.9995710849761963, "general": 0.9918844699859619}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 34534 | 61.20% | 0 | 0.00 | 8674.36 | 0.000 | 75.93% | 97.03% | `{"filegroups/native": 0.9774362444877625, "filetypes/macho": 0.9904804229736328}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 957 | 57.45% | 0 | 0.00 | 312544.24 | 0.000 | 72.98% | 63.10% | `{"filegroups/documents": 0.9998659491539001, "filetypes/rtf": 0.9935286045074463, "general": 0.9991967678070068}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 977 | 1395 | 56.40% | 0 | 0.00 | 214517.42 | 0.000 | 72.12% | 82.04% | `{"filetypes/python_sdist": 0.9895145893096924, "general": 0.9614319205284119}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87713 | 31834 | 54.30% | 0 | 0.00 | 9410.04 | 0.000 | 70.39% | 66.47% | `{"filetypes/ole_doc": 0.9993669986724854, "general": 0.9982293844223022}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27775 | 52.83% | 0 | 0.00 | 10785.13 | 0.000 | 69.14% | 99.82% | `{"filetypes/lua": 0.7376510500907898, "general": 0.9806055426597595}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 324 | 52.38% | 0 | 0.00 | 920347.36 | 0.000 | 68.75% | 92.25% | `{"filetypes/dmg": 0.8825401663780212, "general": 0.9622342586517334}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44607 | 50.72% | 0 | 0.00 | 6715.61 | 0.000 | 67.31% | 99.92% | `{"filegroups/source": 0.9316802024841309}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 5631 | 49.31% | 0 | 0.00 | 53186.57 | 0.000 | 66.05% | 73.75% | `{"filegroups/scripts": 0.9984983801841736, "filetypes/powershell": 0.9950370192527771, "general": 0.9963555335998535}` |
| filetypes/pe | joint_or_at_fp_0 | 1379506 | 251747 | 46.40% | 0 | 0.00 | 1189.97 | 0.000 | 63.38% | 54.67% | `{"filegroups/native": 0.9996936321258545, "filetypes/pe": 0.9994720816612244, "general": 0.999785840511322}` |
| filetypes/package.json | joint_or_at_fp_0 | 22369 | 70855 | 45.86% | 0 | 0.00 | 4227.89 | 0.000 | 62.88% | 87.01% | `{"filegroups/config": 0.9999793767929077, "filetypes/package.json": 0.9998695850372314, "general": 0.9993761777877808}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 84141 | 45.64% | 0 | 0.00 | 3560.31 | 0.000 | 62.67% | 84.91% | `{"filegroups/source": 0.991012692451477, "filetypes/kotlin": 0.9779708385467529, "general": 0.9964229464530945}` |
| filetypes/npm | joint_or_at_fp_0 | 17401 | 104932 | 45.62% | 0 | 0.00 | 2854.89 | 0.000 | 62.65% | 92.26% | `{"filetypes/npm": 0.9993012547492981, "general": 0.9994699954986572}` |
| filetypes/html | joint_or_at_fp_0 | 314 | 185673 | 45.54% | 0 | 0.00 | 1613.43 | 0.000 | 62.58% | 99.91% | `{"filegroups/documents": 0.9979287385940552, "general": 0.9659225940704346}` |
| filetypes/javascript | joint_or_at_fp_0 | 144979 | 1712861 | 43.25% | 0 | 0.00 | 174.90 | 0.000 | 60.39% | 95.57% | `{"filegroups/scripts": 0.9986911416053772, "filetypes/javascript": 0.9988570213317871, "general": 0.994106650352478}` |
| filetypes/gem | joint_or_at_fp_0 | 2111 | 47842 | 43.11% | 0 | 0.00 | 6261.52 | 0.000 | 60.24% | 97.60% | `{"filetypes/gem": 0.999733030796051, "general": 0.9779737591743469}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 78637 | 43.07% | 0 | 0.00 | 3809.50 | 0.000 | 60.21% | 99.71% | `{"filegroups/scripts": 0.9984470009803772, "filetypes/perl": 0.9994779229164124, "general": 0.9901589155197144}` |
| filetypes/python | joint_or_at_fp_0 | 23631 | 661889 | 39.89% | 0 | 0.00 | 452.60 | 0.000 | 57.03% | 97.93% | `{"filegroups/scripts": 0.9988007545471191, "filetypes/python": 0.9986681342124939, "general": 0.9951849579811096}` |
| filetypes/lnk | joint_or_at_fp_0 | 4696 | 1155 | 37.01% | 0 | 0.00 | 259034.68 | 0.000 | 54.03% | 49.44% | `{"filetypes/lnk": 0.9936132431030273, "general": 0.9971751570701599}` |
| filetypes/rar | calibrate_inherited | 22206 | 43 | 33.25% | 0 | 0.00 | 6729675.34 | 0.000 | 49.91% | 33.38% | `{"general": 0.9993280755195791}` |
| filetypes/php | joint_or_at_fp_0 | 7218 | 615929 | 33.00% | 0 | 0.00 | 486.38 | 0.000 | 49.62% | 99.22% | `{"filegroups/scripts": 0.9991531372070312, "filetypes/php": 0.9972749948501587, "general": 0.988580048084259}` |
| filetypes/ruby | joint_or_at_fp_0 | 402 | 183842 | 32.09% | 0 | 0.00 | 1629.50 | 0.000 | 48.59% | 99.85% | `{"filegroups/scripts": 0.9865238666534424, "filetypes/ruby": 0.9992597103118896}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1117 | 30.69% | 0 | 0.00 | 267835.15 | 0.000 | 46.97% | 94.25% | `{"filetypes/chrome_manifest": 0.9806844592094421, "general": 0.9512924551963806}` |
