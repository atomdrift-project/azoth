# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `5502527281`
- Rows: 19811828 (2960816 malware, 16851012 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 546 | 92.86% | 0 | 0.00 | 547166.48 | 0.000 | 96.30% | 99.34% | `{"filetypes/applescript": 0.6672536730766296, "general": 0.9812393188476562}` |
| filetypes/mp3 | learned_blend_at_fp_3 | 196 | 321 | 91.84% | 0 | 0.00 | 928908.67 | 0.000 | 95.74% | 96.91% | `{}` |
| filetypes/asar | joint_or_at_fp_0 | 198 | 364 | 83.33% | 0 | 0.00 | 819625.97 | 0.000 | 90.91% | 94.13% | `{"filetypes/asar": 0.916981041431427, "general": 0.7868103981018066}` |
| filetypes/cab | joint_or_at_fp_0 | 868 | 96 | 83.06% | 0 | 0.00 | 3072367.68 | 0.000 | 90.75% | 84.75% | `{"filetypes/cab": 0.934256374835968, "general": 0.7260110974311829}` |
| filetypes/elf | joint_or_at_fp_0 | 197663 | 896853 | 82.68% | 0 | 0.00 | 334.03 | 0.000 | 90.52% | 96.87% | `{"filegroups/native": 0.9984847903251648, "filetypes/elf": 0.9998248219490051, "general": 0.9980757236480713}` |
| filetypes/bmp | joint_or_at_fp_0 | 156 | 180 | 82.05% | 0 | 0.00 | 1650522.82 | 0.000 | 90.14% | 91.67% | `{"filetypes/bmp": 0.8909065127372742, "general": 0.9464058876037598}` |
| filetypes/7z | joint_or_at_fp_0 | 8769 | 389 | 72.60% | 0 | 0.00 | 767153.37 | 0.000 | 84.12% | 73.76% | `{"filetypes/7z": 0.9947394728660583, "general": 0.9907695055007935}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 2968 | 8068 | 68.94% | 0 | 0.00 | 37124.15 | 0.000 | 81.61% | 91.65% | `{"filetypes/python_sdist": 0.9994333982467651, "general": 0.9592176675796509}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 192938 | 65.76% | 0 | 0.00 | 1552.68 | 0.000 | 79.34% | 99.95% | `{"filegroups/scripts": 0.9770316481590271, "general": 0.9434360861778259}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 583 | 64.02% | 0 | 0.00 | 512529.79 | 0.000 | 78.06% | 88.78% | `{}` |
| filetypes/html | learned_blend_at_fp_0 | 341 | 276186 | 63.34% | 0 | 0.00 | 1084.67 | 0.000 | 77.56% | 99.95% | `{}` |
| filetypes/tar | joint_or_at_fp_0 | 25335 | 88654 | 63.25% | 0 | 0.00 | 3379.07 | 0.000 | 77.49% | 91.83% | `{"filetypes/tar": 0.9976098537445068, "general": 0.9910573363304138}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 58.08% | 0 | 0.00 | 2980667.38 | 0.000 | 73.48% | 70.73% | `{"filetypes/chm": 0.8754045367240906, "general": 0.994156002998352}` |
| filetypes/shell | joint_or_at_fp_0 | 18929 | 164501 | 57.77% | 0 | 0.00 | 1821.09 | 0.000 | 73.24% | 95.64% | `{"filegroups/scripts": 0.9967795014381409, "filetypes/shell": 0.997643768787384, "general": 0.9903899431228638}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 265 | 56.32% | 0 | 0.00 | 1124099.26 | 0.000 | 72.06% | 89.20% | `{"filetypes/dex": 0.9210683107376099, "general": 0.9402864575386047}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44768 | 55.93% | 0 | 0.00 | 6691.46 | 0.000 | 71.74% | 99.94% | `{"general": 0.12415570765733719}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27330 | 83662 | 48.74% | 0 | 0.00 | 3580.69 | 0.000 | 65.54% | 87.38% | `{"filegroups/source": 0.9782391786575317, "filetypes/kotlin": 0.9158329367637634, "general": 0.9913703203201294}` |
| filetypes/perl | joint_or_at_fp_0 | 417 | 80328 | 48.68% | 0 | 0.00 | 3729.31 | 0.000 | 65.48% | 99.73% | `{"filegroups/scripts": 0.9897246956825256, "filetypes/perl": 0.9941628575325012, "general": 0.9928662180900574}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3432 | 1198104 | 48.43% | 0 | 0.00 | 250.04 | 0.000 | 65.25% | 99.85% | `{"filetypes/python_bytecode": 0.9999735355377197, "general": 0.9880291819572449}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28481 | 47.13% | 0 | 0.00 | 10517.80 | 0.000 | 64.06% | 99.84% | `{"filegroups/scripts": 0.9915432929992676, "filetypes/lua": 0.9953327178955078}` |
| filetypes/lnk | joint_or_at_fp_0 | 4731 | 1169 | 46.06% | 0 | 0.00 | 255936.45 | 0.000 | 63.07% | 56.75% | `{"filetypes/lnk": 0.9947395920753479, "general": 0.9979907274246216}` |
| filetypes/xpi | joint_or_at_fp_0 | 62 | 2934 | 45.16% | 0 | 0.00 | 102051.92 | 0.000 | 62.22% | 98.87% | `{"filetypes/xpi": 0.967981219291687, "general": 0.9222540855407715}` |
| filetypes/powershell | joint_or_at_fp_0 | 5866 | 6132 | 44.75% | 0 | 0.00 | 48842.15 | 0.000 | 61.83% | 72.99% | `{"filegroups/scripts": 0.9983214735984802, "filetypes/powershell": 0.9947130084037781, "general": 0.9988604784011841}` |
| filetypes/npm | joint_or_at_fp_0 | 23691 | 196002 | 44.11% | 0 | 0.00 | 1528.41 | 0.000 | 61.21% | 93.97% | `{"filetypes/npm": 0.9999237060546875, "general": 0.9993281364440918}` |
| filetypes/macho | joint_or_at_fp_0 | 2729 | 37298 | 42.14% | 0 | 0.00 | 8031.56 | 0.000 | 59.29% | 96.06% | `{"filetypes/macho": 0.9898137450218201, "general": 0.9859268069267273}` |
| filetypes/jar | joint_or_at_fp_0 | 3789 | 40929 | 40.38% | 0 | 0.00 | 7319.07 | 0.000 | 57.53% | 94.95% | `{"filetypes/jar": 0.9967347979545593, "general": 0.9990941882133484}` |
| filetypes/python | joint_or_at_fp_0 | 23546 | 676019 | 40.37% | 0 | 0.00 | 443.14 | 0.000 | 57.52% | 97.99% | `{"filegroups/scripts": 0.9984248280525208, "filetypes/python": 0.9993975758552551, "general": 0.9915330410003662}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 40.23% | 0 | 0.00 | 292981.55 | 0.000 | 57.38% | 48.79% | `{"filegroups/documents": 0.9999374747276306, "filetypes/rtf": 0.9931700229644775, "general": 0.9987450838088989}` |
| filetypes/zip | joint_or_at_fp_0 | 107315 | 89487 | 38.81% | 0 | 0.00 | 3347.62 | 0.000 | 55.91% | 66.63% | `{"filetypes/zip": 0.9991477727890015, "general": 0.9978575110435486}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 38.64% | 0 | 0.00 | 5495548.85 | 0.000 | 55.74% | 38.79% | `{"general": 0.9993209970765327}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 546 | 92.86% | 0 | 0.00 | 547166.48 | 0.000 | 96.30% | 99.34% | `{"filetypes/applescript": 0.6672536730766296, "general": 0.9812393188476562}` |
| filetypes/mp3 | learned_blend_at_fp_3 | 196 | 321 | 91.84% | 0 | 0.00 | 928908.67 | 0.000 | 95.74% | 96.91% | `{}` |
| filetypes/asar | joint_or_at_fp_0 | 198 | 364 | 83.33% | 0 | 0.00 | 819625.97 | 0.000 | 90.91% | 94.13% | `{"filetypes/asar": 0.916981041431427, "general": 0.7868103981018066}` |
| filetypes/cab | joint_or_at_fp_0 | 868 | 96 | 83.06% | 0 | 0.00 | 3072367.68 | 0.000 | 90.75% | 84.75% | `{"filetypes/cab": 0.934256374835968, "general": 0.7260110974311829}` |
| filetypes/elf | joint_or_at_fp_0 | 197663 | 896853 | 82.68% | 0 | 0.00 | 334.03 | 0.000 | 90.52% | 96.87% | `{"filegroups/native": 0.9984847903251648, "filetypes/elf": 0.9998248219490051, "general": 0.9980757236480713}` |
| filetypes/bmp | joint_or_at_fp_0 | 156 | 180 | 82.05% | 0 | 0.00 | 1650522.82 | 0.000 | 90.14% | 91.67% | `{"filetypes/bmp": 0.8909065127372742, "general": 0.9464058876037598}` |
| filetypes/7z | joint_or_at_fp_0 | 8769 | 389 | 72.60% | 0 | 0.00 | 767153.37 | 0.000 | 84.12% | 73.76% | `{"filetypes/7z": 0.9947394728660583, "general": 0.9907695055007935}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 2968 | 8068 | 68.94% | 0 | 0.00 | 37124.15 | 0.000 | 81.61% | 91.65% | `{"filetypes/python_sdist": 0.9994333982467651, "general": 0.9592176675796509}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 192938 | 65.76% | 0 | 0.00 | 1552.68 | 0.000 | 79.34% | 99.95% | `{"filegroups/scripts": 0.9770316481590271, "general": 0.9434360861778259}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 583 | 64.02% | 0 | 0.00 | 512529.79 | 0.000 | 78.06% | 88.78% | `{}` |
| filetypes/html | learned_blend_at_fp_0 | 341 | 276186 | 63.34% | 0 | 0.00 | 1084.67 | 0.000 | 77.56% | 99.95% | `{}` |
| filetypes/tar | joint_or_at_fp_0 | 25335 | 88654 | 63.25% | 0 | 0.00 | 3379.07 | 0.000 | 77.49% | 91.83% | `{"filetypes/tar": 0.9976098537445068, "general": 0.9910573363304138}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 58.08% | 0 | 0.00 | 2980667.38 | 0.000 | 73.48% | 70.73% | `{"filetypes/chm": 0.8754045367240906, "general": 0.994156002998352}` |
| filetypes/shell | joint_or_at_fp_0 | 18929 | 164501 | 57.77% | 0 | 0.00 | 1821.09 | 0.000 | 73.24% | 95.64% | `{"filegroups/scripts": 0.9967795014381409, "filetypes/shell": 0.997643768787384, "general": 0.9903899431228638}` |
| filetypes/dex | joint_or_at_fp_0 | 87 | 265 | 56.32% | 0 | 0.00 | 1124099.26 | 0.000 | 72.06% | 89.20% | `{"filetypes/dex": 0.9210683107376099, "general": 0.9402864575386047}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44768 | 55.93% | 0 | 0.00 | 6691.46 | 0.000 | 71.74% | 99.94% | `{"general": 0.12415570765733719}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27330 | 83662 | 48.74% | 0 | 0.00 | 3580.69 | 0.000 | 65.54% | 87.38% | `{"filegroups/source": 0.9782391786575317, "filetypes/kotlin": 0.9158329367637634, "general": 0.9913703203201294}` |
| filetypes/perl | joint_or_at_fp_0 | 417 | 80328 | 48.68% | 0 | 0.00 | 3729.31 | 0.000 | 65.48% | 99.73% | `{"filegroups/scripts": 0.9897246956825256, "filetypes/perl": 0.9941628575325012, "general": 0.9928662180900574}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3432 | 1198104 | 48.43% | 0 | 0.00 | 250.04 | 0.000 | 65.25% | 99.85% | `{"filetypes/python_bytecode": 0.9999735355377197, "general": 0.9880291819572449}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28481 | 47.13% | 0 | 0.00 | 10517.80 | 0.000 | 64.06% | 99.84% | `{"filegroups/scripts": 0.9915432929992676, "filetypes/lua": 0.9953327178955078}` |
| filetypes/lnk | joint_or_at_fp_0 | 4731 | 1169 | 46.06% | 0 | 0.00 | 255936.45 | 0.000 | 63.07% | 56.75% | `{"filetypes/lnk": 0.9947395920753479, "general": 0.9979907274246216}` |
| filetypes/xpi | joint_or_at_fp_0 | 62 | 2934 | 45.16% | 0 | 0.00 | 102051.92 | 0.000 | 62.22% | 98.87% | `{"filetypes/xpi": 0.967981219291687, "general": 0.9222540855407715}` |
| filetypes/powershell | joint_or_at_fp_0 | 5866 | 6132 | 44.75% | 0 | 0.00 | 48842.15 | 0.000 | 61.83% | 72.99% | `{"filegroups/scripts": 0.9983214735984802, "filetypes/powershell": 0.9947130084037781, "general": 0.9988604784011841}` |
| filetypes/npm | joint_or_at_fp_0 | 23691 | 196002 | 44.11% | 0 | 0.00 | 1528.41 | 0.000 | 61.21% | 93.97% | `{"filetypes/npm": 0.9999237060546875, "general": 0.9993281364440918}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 43.64% | 0 | 0.00 | 5495548.85 | 0.000 | 60.77% | 43.78% | `{"general": 0.999119428152808}` |
| filetypes/macho | joint_or_at_fp_0 | 2729 | 37298 | 42.14% | 0 | 0.00 | 8031.56 | 0.000 | 59.29% | 96.06% | `{"filetypes/macho": 0.9898137450218201, "general": 0.9859268069267273}` |
| filetypes/jar | joint_or_at_fp_0 | 3789 | 40929 | 40.38% | 0 | 0.00 | 7319.07 | 0.000 | 57.53% | 94.95% | `{"filetypes/jar": 0.9967347979545593, "general": 0.9990941882133484}` |
| filetypes/python | joint_or_at_fp_0 | 23546 | 676019 | 40.37% | 0 | 0.00 | 443.14 | 0.000 | 57.52% | 97.99% | `{"filegroups/scripts": 0.9984248280525208, "filetypes/python": 0.9993975758552551, "general": 0.9915330410003662}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 40.23% | 0 | 0.00 | 292981.55 | 0.000 | 57.38% | 48.79% | `{"filegroups/documents": 0.9999374747276306, "filetypes/rtf": 0.9931700229644775, "general": 0.9987450838088989}` |
| filetypes/zip | joint_or_at_fp_0 | 107315 | 89487 | 38.81% | 0 | 0.00 | 3347.62 | 0.000 | 55.91% | 66.63% | `{"filetypes/zip": 0.9991477727890015, "general": 0.9978575110435486}` |
