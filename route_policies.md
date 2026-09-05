# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3998018903`
- Rows: 17755836 (2694836 malware, 15061000 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 189 | 249 | 97.35% | 0 | 0.00 | 1195896.96 | 0.000 | 98.66% | 98.86% | `{"filetypes/asar": 0.8714922666549683, "general": 0.9096137881278992}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 886 | 97.12% | 0 | 0.00 | 337547.79 | 0.000 | 98.54% | 97.48% | `{"filegroups/documents": 0.9582754373550415, "filetypes/rtf": 0.980923056602478, "general": 0.8226900100708008}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8578193783760071}` |
| filetypes/7z | joint_or_at_fp_0 | 9026 | 309 | 91.20% | 0 | 0.00 | 964808.22 | 0.000 | 95.40% | 91.49% | `{"filetypes/7z": 0.7272136211395264, "general": 0.9919013977050781}` |
| filetypes/elf | joint_or_at_fp_0 | 196690 | 820051 | 87.04% | 0 | 0.00 | 365.31 | 0.000 | 93.07% | 97.49% | `{"filegroups/native": 0.996111273765564, "filetypes/elf": 0.999891459941864, "general": 0.992966890335083}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 58 | 86.48% | 0 | 0.00 | 5033933.83 | 0.000 | 92.75% | 89.07% | `{"filetypes/chm": 0.880485475063324, "general": 0.06417316198348999}` |
| filetypes/html | learned_blend_at_fp_0 | 314 | 113748 | 77.71% | 0 | 0.00 | 2633.62 | 0.000 | 87.46% | 99.94% | `{}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 11038 | 16719 | 73.65% | 0 | 0.00 | 17916.53 | 0.000 | 84.83% | 89.52% | `{"filetypes/pkg_info": 0.9994839429855347, "general": 0.9942713379859924}` |
| filetypes/tar | joint_or_at_fp_0 | 33968 | 77321 | 68.56% | 0 | 0.00 | 3874.33 | 0.000 | 81.35% | 90.40% | `{"filetypes/tar": 0.9986763596534729, "general": 0.9949512481689453}` |
| filetypes/shell | joint_or_at_fp_0 | 18672 | 160880 | 65.20% | 0 | 0.00 | 1862.07 | 0.000 | 78.94% | 96.38% | `{"filegroups/scripts": 0.9986487627029419, "filetypes/shell": 0.9967365860939026, "general": 0.9952974915504456}` |
| filetypes/macho | joint_or_at_fp_0 | 2844 | 32232 | 62.06% | 0 | 0.00 | 9293.85 | 0.000 | 76.59% | 96.92% | `{"filegroups/native": 0.9688791036605835, "filetypes/macho": 0.9879056215286255}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87706 | 31288 | 60.49% | 0 | 0.00 | 9574.24 | 0.000 | 75.38% | 70.88% | `{"filetypes/ole_doc": 0.999387800693512, "general": 0.9990237951278687}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27774 | 55.66% | 0 | 0.00 | 10785.52 | 0.000 | 71.52% | 99.83% | `{"filegroups/scripts": 0.9940053820610046, "filetypes/lua": 0.8269254565238953}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 83873 | 54.41% | 0 | 0.00 | 3571.68 | 0.000 | 70.47% | 87.31% | `{"filegroups/source": 0.993887722492218, "filetypes/kotlin": 0.9205230474472046, "general": 0.9730113744735718}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5542 | 53.25% | 0 | 0.00 | 54040.47 | 0.000 | 69.49% | 75.62% | `{"filegroups/scripts": 0.997689962387085, "filetypes/powershell": 0.9975726008415222, "general": 0.9916506409645081}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44580 | 52.17% | 0 | 0.00 | 6719.68 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.09026411920785904}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 737 | 706 | 51.56% | 0 | 0.00 | 423425.70 | 0.000 | 68.04% | 75.26% | `{"filetypes/python_sdist": 0.9855461120605469, "general": 0.9464699625968933}` |
| filetypes/gem | joint_or_at_fp_0 | 2080 | 10182 | 44.95% | 0 | 0.00 | 29417.52 | 0.000 | 62.02% | 90.66% | `{"filetypes/gem": 0.9518187642097473, "general": 0.9938482642173767}` |
| filetypes/lnk | joint_or_at_fp_0 | 4688 | 1152 | 44.60% | 0 | 0.00 | 259708.38 | 0.000 | 61.69% | 55.53% | `{"filetypes/lnk": 0.995326578617096, "general": 0.9981127977371216}` |
| filetypes/javascript | joint_or_at_fp_0 | 142851 | 1662779 | 44.20% | 0 | 0.00 | 180.16 | 0.000 | 61.31% | 95.59% | `{"filegroups/scripts": 0.9986636638641357, "filetypes/javascript": 0.9982583522796631, "general": 0.997397780418396}` |
| filetypes/python | joint_or_at_fp_0 | 23397 | 645373 | 43.53% | 0 | 0.00 | 464.19 | 0.000 | 60.66% | 98.02% | `{"filegroups/scripts": 0.9989362359046936, "filetypes/python": 0.9963087439537048, "general": 0.9962235689163208}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9485 | 40.91% | 0 | 0.00 | 31578.91 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984393119812012, "general": 0.03260482847690582}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78322 | 39.90% | 0 | 0.00 | 3824.82 | 0.000 | 57.04% | 99.70% | `{"filetypes/perl": 0.9996488690376282, "general": 0.9816994071006775}` |
| filetypes/php | joint_or_at_fp_0 | 6794 | 614096 | 39.09% | 0 | 0.00 | 487.83 | 0.000 | 56.21% | 99.33% | `{"filegroups/scripts": 0.9990638494491577, "filetypes/php": 0.996876060962677, "general": 0.9954624772071838}` |
| filetypes/pe | joint_or_at_fp_0 | 1379228 | 236962 | 35.12% | 0 | 0.00 | 1264.22 | 0.000 | 51.98% | 44.63% | `{"filegroups/native": 0.9997800588607788, "filetypes/pe": 0.9997308254241943, "general": 0.9996027946472168}` |
| filetypes/npm | joint_or_at_fp_0 | 10751 | 38580 | 35.00% | 0 | 0.00 | 7764.69 | 0.000 | 51.85% | 85.83% | `{"filetypes/npm": 0.9990649819374084, "general": 0.9996231198310852}` |
| filetypes/jar | joint_or_at_fp_0 | 3937 | 30048 | 32.56% | 0 | 0.00 | 9969.33 | 0.000 | 49.13% | 92.19% | `{"filetypes/jar": 0.995728075504303, "general": 0.9725269079208374}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 264 | 31.75% | 0 | 0.00 | 1128333.10 | 0.000 | 48.19% | 86.85% | `{"filetypes/dmg": 0.9801228642463684, "general": 0.9782789945602417}` |
| filetypes/ruby | joint_or_at_fp_0 | 401 | 179473 | 30.92% | 0 | 0.00 | 1669.17 | 0.000 | 47.24% | 99.85% | `{"filetypes/ruby": 0.9937001466751099, "general": 0.9274932146072388}` |
| filetypes/package.json | joint_or_at_fp_0 | 21386 | 66427 | 30.09% | 0 | 0.00 | 4509.71 | 0.000 | 46.25% | 82.97% | `{"filegroups/config": 0.999991238117218, "filetypes/package.json": 0.9999343156814575, "general": 0.9990639686584473}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 189 | 249 | 97.35% | 0 | 0.00 | 1195896.96 | 0.000 | 98.66% | 98.86% | `{"filetypes/asar": 0.8714922666549683, "general": 0.9096137881278992}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 886 | 97.12% | 0 | 0.00 | 337547.79 | 0.000 | 98.54% | 97.48% | `{"filegroups/documents": 0.9582754373550415, "filetypes/rtf": 0.980923056602478, "general": 0.8226900100708008}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 94.55% | 0 | 0.00 | 566837.53 | 0.000 | 97.20% | 99.48% | `{"general": 0.8578193783760071}` |
| filetypes/7z | joint_or_at_fp_0 | 9026 | 309 | 91.20% | 0 | 0.00 | 964808.22 | 0.000 | 95.40% | 91.49% | `{"filetypes/7z": 0.7272136211395264, "general": 0.9919013977050781}` |
| filetypes/elf | joint_or_at_fp_0 | 196690 | 820051 | 87.04% | 0 | 0.00 | 365.31 | 0.000 | 93.07% | 97.49% | `{"filegroups/native": 0.996111273765564, "filetypes/elf": 0.999891459941864, "general": 0.992966890335083}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 58 | 86.48% | 0 | 0.00 | 5033933.83 | 0.000 | 92.75% | 89.07% | `{"filetypes/chm": 0.880485475063324, "general": 0.06417316198348999}` |
| filetypes/html | learned_blend_at_fp_0 | 314 | 113748 | 77.71% | 0 | 0.00 | 2633.62 | 0.000 | 87.46% | 99.94% | `{}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 11038 | 16719 | 73.65% | 0 | 0.00 | 17916.53 | 0.000 | 84.83% | 89.52% | `{"filetypes/pkg_info": 0.9994839429855347, "general": 0.9942713379859924}` |
| filetypes/tar | joint_or_at_fp_0 | 33968 | 77321 | 68.56% | 0 | 0.00 | 3874.33 | 0.000 | 81.35% | 90.40% | `{"filetypes/tar": 0.9986763596534729, "general": 0.9949512481689453}` |
| filetypes/shell | joint_or_at_fp_0 | 18672 | 160880 | 65.20% | 0 | 0.00 | 1862.07 | 0.000 | 78.94% | 96.38% | `{"filegroups/scripts": 0.9986487627029419, "filetypes/shell": 0.9967365860939026, "general": 0.9952974915504456}` |
| filetypes/macho | joint_or_at_fp_0 | 2844 | 32232 | 62.06% | 0 | 0.00 | 9293.85 | 0.000 | 76.59% | 96.92% | `{"filegroups/native": 0.9688791036605835, "filetypes/macho": 0.9879056215286255}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87706 | 31288 | 60.49% | 0 | 0.00 | 9574.24 | 0.000 | 75.38% | 70.88% | `{"filetypes/ole_doc": 0.999387800693512, "general": 0.9990237951278687}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27774 | 55.66% | 0 | 0.00 | 10785.52 | 0.000 | 71.52% | 99.83% | `{"filegroups/scripts": 0.9940053820610046, "filetypes/lua": 0.8269254565238953}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32343 | 83873 | 54.41% | 0 | 0.00 | 3571.68 | 0.000 | 70.47% | 87.31% | `{"filegroups/source": 0.993887722492218, "filetypes/kotlin": 0.9205230474472046, "general": 0.9730113744735718}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5542 | 53.25% | 0 | 0.00 | 54040.47 | 0.000 | 69.49% | 75.62% | `{"filegroups/scripts": 0.997689962387085, "filetypes/powershell": 0.9975726008415222, "general": 0.9916506409645081}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44580 | 52.17% | 0 | 0.00 | 6719.68 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.09026411920785904}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 737 | 706 | 51.56% | 0 | 0.00 | 423425.70 | 0.000 | 68.04% | 75.26% | `{"filetypes/python_sdist": 0.9855461120605469, "general": 0.9464699625968933}` |
| filetypes/gem | joint_or_at_fp_0 | 2080 | 10182 | 44.95% | 0 | 0.00 | 29417.52 | 0.000 | 62.02% | 90.66% | `{"filetypes/gem": 0.9518187642097473, "general": 0.9938482642173767}` |
| filetypes/lnk | joint_or_at_fp_0 | 4688 | 1152 | 44.60% | 0 | 0.00 | 259708.38 | 0.000 | 61.69% | 55.53% | `{"filetypes/lnk": 0.995326578617096, "general": 0.9981127977371216}` |
| filetypes/javascript | joint_or_at_fp_0 | 142851 | 1662779 | 44.20% | 0 | 0.00 | 180.16 | 0.000 | 61.31% | 95.59% | `{"filegroups/scripts": 0.9986636638641357, "filetypes/javascript": 0.9982583522796631, "general": 0.997397780418396}` |
| filetypes/python | joint_or_at_fp_0 | 23397 | 645373 | 43.53% | 0 | 0.00 | 464.19 | 0.000 | 60.66% | 98.02% | `{"filegroups/scripts": 0.9989362359046936, "filetypes/python": 0.9963087439537048, "general": 0.9962235689163208}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9485 | 40.91% | 0 | 0.00 | 31578.91 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9984393119812012, "general": 0.03260482847690582}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78322 | 39.90% | 0 | 0.00 | 3824.82 | 0.000 | 57.04% | 99.70% | `{"filetypes/perl": 0.9996488690376282, "general": 0.9816994071006775}` |
| filetypes/php | joint_or_at_fp_0 | 6794 | 614096 | 39.09% | 0 | 0.00 | 487.83 | 0.000 | 56.21% | 99.33% | `{"filegroups/scripts": 0.9990638494491577, "filetypes/php": 0.996876060962677, "general": 0.9954624772071838}` |
| filetypes/pe | joint_or_at_fp_0 | 1379228 | 236962 | 35.12% | 0 | 0.00 | 1264.22 | 0.000 | 51.98% | 44.63% | `{"filegroups/native": 0.9997800588607788, "filetypes/pe": 0.9997308254241943, "general": 0.9996027946472168}` |
| filetypes/npm | joint_or_at_fp_0 | 10751 | 38580 | 35.00% | 0 | 0.00 | 7764.69 | 0.000 | 51.85% | 85.83% | `{"filetypes/npm": 0.9990649819374084, "general": 0.9996231198310852}` |
| filetypes/rar | calibrate_inherited | 22199 | 44 | 34.02% | 0 | 0.00 | 6581877.11 | 0.000 | 50.76% | 34.15% | `{"general": 0.9992884898267459}` |
| filetypes/jar | joint_or_at_fp_0 | 3937 | 30048 | 32.56% | 0 | 0.00 | 9969.33 | 0.000 | 49.13% | 92.19% | `{"filetypes/jar": 0.995728075504303, "general": 0.9725269079208374}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 264 | 31.75% | 0 | 0.00 | 1128333.10 | 0.000 | 48.19% | 86.85% | `{"filetypes/dmg": 0.9801228642463684, "general": 0.9782789945602417}` |
| filetypes/ruby | joint_or_at_fp_0 | 401 | 179473 | 30.92% | 0 | 0.00 | 1669.17 | 0.000 | 47.24% | 99.85% | `{"filetypes/ruby": 0.9937001466751099, "general": 0.9274932146072388}` |
