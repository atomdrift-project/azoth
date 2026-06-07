# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1670971082`
- Rows: 6899010 (2511611 malware, 4387399 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11019 | 100.00% | 0 | 0.00 | 27183.28 | 0.000 | 100.00% | 100.00% | `{"general": 0.8486545085906982}` |
| filetypes/rtf | learned_blend_at_fp_3 | 5888 | 507 | 98.42% | 0 | 0.00 | 589131.99 | 0.000 | 99.20% | 98.55% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 179697 | 170249 | 91.07% | 0 | 0.00 | 1759.60 | 0.000 | 95.33% | 95.41% | `{"filegroups/native": 0.9972769618034363, "filetypes/elf": 0.9987571239471436, "general": 0.9920915365219116}` |
| filetypes/package.json | joint_or_at_fp_0 | 18438 | 21473 | 87.69% | 0 | 0.00 | 13950.19 | 0.000 | 93.44% | 94.31% | `{"filegroups/config": 0.9996994733810425, "filetypes/package.json": 0.9991149306297302, "general": 0.9965143203735352}` |
| filetypes/xls | joint_or_at_fp_0 | 37236 | 20747 | 84.70% | 0 | 0.00 | 14438.31 | 0.000 | 91.72% | 90.18% | `{"filegroups/documents": 0.9942182302474976, "filetypes/xls": 0.999415397644043, "general": 0.9996998906135559}` |
| filetypes/tar | joint_or_at_fp_0 | 31218 | 23953 | 76.05% | 0 | 0.00 | 12505.93 | 0.000 | 86.39% | 86.45% | `{"filetypes/tar": 0.998883068561554, "general": 0.9968093633651733}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10644 | 1924 | 75.88% | 0 | 0.00 | 155582.19 | 0.000 | 86.29% | 79.58% | `{"general": 0.993628978729248}` |
| filetypes/clojure | joint_or_at_fp_0 | 125 | 5341 | 70.40% | 0 | 0.00 | 56073.62 | 0.000 | 82.63% | 99.32% | `{"general": 0.043752480298280716}` |
| filetypes/macho | joint_or_at_fp_0 | 2591 | 11727 | 66.23% | 0 | 0.00 | 25542.34 | 0.000 | 79.68% | 93.89% | `{"filegroups/native": 0.9836515784263611, "filetypes/macho": 0.9941095113754272, "general": 0.9895058274269104}` |
| filetypes/doc | calibrate_inherited | 32732 | 76 | 62.66% | 0 | 0.00 | 3865076.67 | 0.000 | 77.05% | 62.75% | `{"filegroups/documents": 0.9953503325661722, "general": 0.9997914462662045}` |
| filetypes/perl | learned_blend_at_fp_0 | 333 | 39777 | 54.95% | 0 | 0.00 | 7531.03 | 0.000 | 70.93% | 99.63% | `{}` |
| filetypes/docx | joint_or_at_fp_0 | 4775 | 434 | 52.46% | 0 | 0.00 | 687884.06 | 0.000 | 68.82% | 56.42% | `{"filegroups/documents": 0.9954180717468262, "filetypes/docx": 0.986842930316925, "general": 0.9804851412773132}` |
| filetypes/kotlin | learned_blend_at_fp_0 | 32747 | 52001 | 47.45% | 0 | 0.00 | 5760.75 | 0.000 | 64.36% | 79.69% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18432 | 47.42% | 0 | 0.00 | 16251.57 | 0.000 | 64.34% | 99.72% | `{"filegroups/scripts": 0.9945775270462036, "filetypes/lua": 0.991586446762085, "general": 0.9892932176589966}` |
| filetypes/python | joint_or_at_fp_0 | 20622 | 197433 | 47.31% | 0 | 0.00 | 1517.33 | 0.000 | 64.23% | 95.02% | `{"filegroups/scripts": 0.9987706542015076, "filetypes/python": 0.9998964071273804, "general": 0.9968591928482056}` |
| filetypes/jar | learned_blend_at_fp_0 | 3442 | 3781 | 46.02% | 0 | 0.00 | 79199.84 | 0.000 | 63.03% | 74.28% | `{}` |
| filetypes/pe | learned_blend_at_fp_0 | 1329010 | 160061 | 45.62% | 0 | 0.00 | 1871.60 | 0.000 | 62.65% | 51.46% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 5068 | 147446 | 44.97% | 0 | 0.00 | 2031.73 | 0.000 | 62.04% | 98.17% | `{"filegroups/scripts": 0.9976862668991089, "filetypes/php": 0.9987418055534363, "general": 0.9855610728263855}` |
| filetypes/lnk | joint_or_at_fp_0 | 4362 | 1055 | 43.37% | 0 | 0.00 | 283552.89 | 0.000 | 60.51% | 54.40% | `{"filetypes/lnk": 0.9956138134002686, "general": 0.9993582963943481}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2887 | 122401 | 40.35% | 0 | 0.00 | 2447.44 | 0.000 | 57.50% | 98.63% | `{"filetypes/python-bytecode": 0.9999654293060303, "general": 0.9913012981414795}` |
| filetypes/powershell | joint_or_at_fp_0 | 5372 | 2394 | 39.45% | 0 | 0.00 | 125056.75 | 0.000 | 56.57% | 58.11% | `{"filegroups/scripts": 0.9989961981773376, "filetypes/powershell": 0.9971664547920227, "general": 0.9973734617233276}` |
| filetypes/shell | joint_or_at_fp_0 | 14519 | 60292 | 37.93% | 0 | 0.00 | 4968.58 | 0.000 | 55.00% | 87.95% | `{"filegroups/scripts": 0.9984991550445557, "filetypes/shell": 0.9977509379386902, "general": 0.9895119071006775}` |
| filetypes/crx | learned_blend_at_fp_0 | 694 | 79 | 36.89% | 0 | 0.00 | 3721067.61 | 0.000 | 53.89% | 43.34% | `{}` |
| filetypes/ruby | learned_blend_at_fp_0 | 154 | 25671 | 36.36% | 0 | 0.00 | 11669.03 | 0.000 | 53.33% | 99.62% | `{}` |
| filetypes/javascript | learned_blend_at_fp_0 | 118857 | 605997 | 35.92% | 0 | 0.00 | 494.35 | 0.000 | 52.86% | 89.49% | `{}` |
| filetypes/rar | calibrate_inherited | 20647 | 4 | 32.97% | 0 | 0.00 | 52712919.55 | 0.000 | 49.59% | 32.98% | `{"general": 0.9997914462662045}` |
| filetypes/msi | joint_or_at_fp_0 | 5328 | 179 | 31.17% | 0 | 0.00 | 1659666.67 | 0.000 | 47.53% | 33.41% | `{"filetypes/msi": 0.9261299967765808, "general": 0.997367799282074}` |
| filetypes/vbs | joint_or_at_fp_0 | 11183 | 3306 | 30.23% | 0 | 0.00 | 90573.97 | 0.000 | 46.43% | 46.15% | `{"filetypes/vbs": 0.9958441853523254, "general": 0.996894359588623}` |
| filetypes/zip | joint_or_at_fp_0 | 101833 | 12246 | 29.03% | 0 | 0.00 | 24459.95 | 0.000 | 45.00% | 36.65% | `{"filetypes/zip": 0.998457670211792, "general": 0.9996304512023926}` |
| filetypes/xlsx | joint_or_at_fp_0 | 58624 | 1839 | 28.91% | 0 | 0.00 | 162767.46 | 0.000 | 44.86% | 31.08% | `{"filegroups/documents": 0.9945617318153381, "filetypes/xlsx": 0.991746187210083, "general": 0.9982468485832214}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 11019 | 100.00% | 0 | 0.00 | 27183.28 | 0.000 | 100.00% | 100.00% | `{"general": 0.8486545085906982}` |
| filetypes/rtf | learned_blend_at_fp_3 | 5888 | 507 | 98.42% | 0 | 0.00 | 589131.99 | 0.000 | 99.20% | 98.55% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 179697 | 170249 | 91.07% | 0 | 0.00 | 1759.60 | 0.000 | 95.33% | 95.41% | `{"filegroups/native": 0.9972769618034363, "filetypes/elf": 0.9987571239471436, "general": 0.9920915365219116}` |
| filetypes/package.json | joint_or_at_fp_0 | 18438 | 21473 | 87.69% | 0 | 0.00 | 13950.19 | 0.000 | 93.44% | 94.31% | `{"filegroups/config": 0.9996994733810425, "filetypes/package.json": 0.9991149306297302, "general": 0.9965143203735352}` |
| filetypes/xls | joint_or_at_fp_0 | 37236 | 20747 | 84.70% | 0 | 0.00 | 14438.31 | 0.000 | 91.72% | 90.18% | `{"filegroups/documents": 0.9942182302474976, "filetypes/xls": 0.999415397644043, "general": 0.9996998906135559}` |
| filetypes/tar | joint_or_at_fp_0 | 31218 | 23953 | 76.05% | 0 | 0.00 | 12505.93 | 0.000 | 86.39% | 86.45% | `{"filetypes/tar": 0.998883068561554, "general": 0.9968093633651733}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10644 | 1924 | 75.88% | 0 | 0.00 | 155582.19 | 0.000 | 86.29% | 79.58% | `{"general": 0.993628978729248}` |
| filetypes/clojure | joint_or_at_fp_0 | 125 | 5341 | 70.40% | 0 | 0.00 | 56073.62 | 0.000 | 82.63% | 99.32% | `{"general": 0.043752480298280716}` |
| filetypes/macho | joint_or_at_fp_0 | 2591 | 11727 | 66.23% | 0 | 0.00 | 25542.34 | 0.000 | 79.68% | 93.89% | `{"filegroups/native": 0.9836515784263611, "filetypes/macho": 0.9941095113754272, "general": 0.9895058274269104}` |
| filetypes/doc | calibrate_inherited | 32732 | 76 | 62.70% | 0 | 0.00 | 3865076.67 | 0.000 | 77.08% | 62.79% | `{"filegroups/documents": 0.9953281909387715, "general": 0.99973283035052}` |
| filetypes/perl | learned_blend_at_fp_0 | 333 | 39777 | 54.95% | 0 | 0.00 | 7531.03 | 0.000 | 70.93% | 99.63% | `{}` |
| filetypes/docx | joint_or_at_fp_0 | 4775 | 434 | 52.46% | 0 | 0.00 | 687884.06 | 0.000 | 68.82% | 56.42% | `{"filegroups/documents": 0.9954180717468262, "filetypes/docx": 0.986842930316925, "general": 0.9804851412773132}` |
| filetypes/kotlin | learned_blend_at_fp_0 | 32747 | 52001 | 47.45% | 0 | 0.00 | 5760.75 | 0.000 | 64.36% | 79.69% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18432 | 47.42% | 0 | 0.00 | 16251.57 | 0.000 | 64.34% | 99.72% | `{"filegroups/scripts": 0.9945775270462036, "filetypes/lua": 0.991586446762085, "general": 0.9892932176589966}` |
| filetypes/python | joint_or_at_fp_0 | 20622 | 197433 | 47.31% | 0 | 0.00 | 1517.33 | 0.000 | 64.23% | 95.02% | `{"filegroups/scripts": 0.9987706542015076, "filetypes/python": 0.9998964071273804, "general": 0.9968591928482056}` |
| filetypes/jar | learned_blend_at_fp_0 | 3442 | 3781 | 46.02% | 0 | 0.00 | 79199.84 | 0.000 | 63.03% | 74.28% | `{}` |
| filetypes/pe | learned_blend_at_fp_0 | 1329010 | 160061 | 45.62% | 0 | 0.00 | 1871.60 | 0.000 | 62.65% | 51.46% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 5068 | 147446 | 44.97% | 0 | 0.00 | 2031.73 | 0.000 | 62.04% | 98.17% | `{"filegroups/scripts": 0.9976862668991089, "filetypes/php": 0.9987418055534363, "general": 0.9855610728263855}` |
| filetypes/lnk | joint_or_at_fp_0 | 4362 | 1055 | 43.37% | 0 | 0.00 | 283552.89 | 0.000 | 60.51% | 54.40% | `{"filetypes/lnk": 0.9956138134002686, "general": 0.9993582963943481}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2887 | 122401 | 40.35% | 0 | 0.00 | 2447.44 | 0.000 | 57.50% | 98.63% | `{"filetypes/python-bytecode": 0.9999654293060303, "general": 0.9913012981414795}` |
| filetypes/rar | calibrate_inherited | 20647 | 4 | 39.81% | 0 | 0.00 | 52712919.55 | 0.000 | 56.95% | 39.82% | `{"general": 0.99973283035052}` |
| filetypes/powershell | joint_or_at_fp_0 | 5372 | 2394 | 39.45% | 0 | 0.00 | 125056.75 | 0.000 | 56.57% | 58.11% | `{"filegroups/scripts": 0.9989961981773376, "filetypes/powershell": 0.9971664547920227, "general": 0.9973734617233276}` |
| filetypes/shell | joint_or_at_fp_0 | 14519 | 60292 | 37.93% | 0 | 0.00 | 4968.58 | 0.000 | 55.00% | 87.95% | `{"filegroups/scripts": 0.9984991550445557, "filetypes/shell": 0.9977509379386902, "general": 0.9895119071006775}` |
| filetypes/crx | learned_blend_at_fp_0 | 694 | 79 | 36.89% | 0 | 0.00 | 3721067.61 | 0.000 | 53.89% | 43.34% | `{}` |
| filetypes/ruby | learned_blend_at_fp_0 | 154 | 25671 | 36.36% | 0 | 0.00 | 11669.03 | 0.000 | 53.33% | 99.62% | `{}` |
| filetypes/javascript | learned_blend_at_fp_0 | 118857 | 605997 | 35.92% | 0 | 0.00 | 494.35 | 0.000 | 52.86% | 89.49% | `{}` |
| filetypes/msi | joint_or_at_fp_0 | 5328 | 179 | 31.17% | 0 | 0.00 | 1659666.67 | 0.000 | 47.53% | 33.41% | `{"filetypes/msi": 0.9261299967765808, "general": 0.997367799282074}` |
| filetypes/vbs | joint_or_at_fp_0 | 11183 | 3306 | 30.23% | 0 | 0.00 | 90573.97 | 0.000 | 46.43% | 46.15% | `{"filetypes/vbs": 0.9958441853523254, "general": 0.996894359588623}` |
| filetypes/7z | calibrate_inherited | 6970 | 112 | 29.63% | 0 | 0.00 | 2639306.04 | 0.000 | 45.71% | 30.74% | `{"general": 0.99973283035052}` |
| filetypes/zip | joint_or_at_fp_0 | 101833 | 12246 | 29.03% | 0 | 0.00 | 24459.95 | 0.000 | 45.00% | 36.65% | `{"filetypes/zip": 0.998457670211792, "general": 0.9996304512023926}` |
