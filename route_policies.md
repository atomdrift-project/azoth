# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1755420090`
- Rows: 8168688 (2620539 malware, 5548149 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.996795117855072}` |
| filetypes/crx | joint_or_at_fp_0 | 884 | 86 | 98.53% | 0 | 0.00 | 3423437.28 | 0.000 | 99.26% | 98.66% | `{"filetypes/crx": 0.4664289951324463, "general": 0.9838255643844604}` |
| filetypes/rtf | joint_or_at_fp_0 | 6241 | 524 | 97.88% | 0 | 0.00 | 570073.51 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.8088999390602112, "filetypes/rtf": 0.733421802520752}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2719 | 96.87% | 0 | 0.00 | 110117.05 | 0.000 | 98.41% | 97.51% | `{"filetypes/pkg-info": 0.3348732590675354, "general": 0.9938700199127197}` |
| filetypes/doc | calibrate_inherited | 34612 | 85 | 96.18% | 0 | 0.00 | 3463007.50 | 0.000 | 98.05% | 96.19% | `{"filegroups/documents": 0.15216702222824097, "general": 0.9994695269024342}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.34% | 0 | 0.00 | 14427.88 | 0.000 | 97.09% | 96.28% | `{"filegroups/documents": 0.8898531198501587, "filetypes/xls": 0.9140002131462097}` |
| filetypes/gem | joint_or_at_fp_0 | 228 | 712 | 92.98% | 0 | 0.00 | 419865.01 | 0.000 | 96.36% | 98.30% | `{"filetypes/gem": 0.8426432609558105}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 96 | 285 | 92.71% | 0 | 0.00 | 1045629.02 | 0.000 | 96.22% | 98.16% | `{"filetypes/chrome-manifest": 0.835390567779541}` |
| filetypes/elf | joint_or_at_fp_0 | 189137 | 197530 | 91.51% | 0 | 0.00 | 1516.58 | 0.000 | 95.57% | 95.85% | `{"filegroups/native": 0.9669767022132874, "filetypes/elf": 0.9961905479431152, "general": 0.9955655932426453}` |
| filetypes/package.json | joint_or_at_fp_0 | 19116 | 25573 | 90.83% | 0 | 0.00 | 11713.75 | 0.000 | 95.19% | 96.08% | `{"filegroups/config": 0.999666690826416, "filetypes/package.json": 0.9983581900596619, "general": 0.9983990788459778}` |
| filetypes/tar | joint_or_at_fp_0 | 31257 | 44435 | 85.16% | 0 | 0.00 | 6741.60 | 0.000 | 91.98% | 93.87% | `{"filetypes/tar": 0.9940686225891113, "general": 0.9938685297966003}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 287 | 81.29% | 0 | 0.00 | 1038380.37 | 0.000 | 89.68% | 82.29% | `{"filegroups/documents": 0.7808955311775208, "filetypes/docx": 0.9834258556365967}` |
| filetypes/macho | joint_or_at_fp_0 | 2657 | 13098 | 79.79% | 0 | 0.00 | 22869.06 | 0.000 | 88.76% | 96.59% | `{"filegroups/native": 0.9084113836288452, "filetypes/macho": 0.9895059466362, "general": 0.9819565415382385}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 205 | 79.34% | 0 | 0.00 | 1450707.17 | 0.000 | 88.48% | 80.07% | `{"filetypes/msi": 0.5905947685241699, "general": 0.9850572943687439}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6611 | 78.90% | 0 | 0.00 | 45304.09 | 0.000 | 88.21% | 88.87% | `{"filegroups/documents": 0.42404335737228394, "filetypes/ole": 0.9987844824790955}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3391 | 323271 | 75.76% | 0 | 0.00 | 926.69 | 0.000 | 86.21% | 99.75% | `{"filetypes/python-bytecode": 0.9996669292449951, "general": 0.9757524728775024}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5929 | 75.57% | 0 | 0.00 | 50514.01 | 0.000 | 86.09% | 99.47% | `{"filetypes/clojure": 0.32156461477279663}` |
| filetypes/npm | joint_or_at_fp_0 | 1301 | 255 | 75.33% | 0 | 0.00 | 1167923.17 | 0.000 | 85.93% | 79.37% | `{"filetypes/npm": 0.643890917301178}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24578 | 73.81% | 0 | 0.00 | 12187.93 | 0.000 | 84.93% | 76.98% | `{"filegroups/documents": 0.9957650899887085, "filetypes/pdf": 0.9411760568618774, "general": 0.9833977818489075}` |
| filetypes/lnk | joint_or_at_fp_0 | 4601 | 1065 | 73.74% | 0 | 0.00 | 280894.17 | 0.000 | 84.89% | 78.68% | `{"filetypes/lnk": 0.9755615592002869, "general": 0.9989781379699707}` |
| filetypes/shell | joint_or_at_fp_0 | 15674 | 70676 | 60.89% | 0 | 0.00 | 4238.59 | 0.000 | 75.69% | 92.90% | `{"filegroups/scripts": 0.9880514144897461, "filetypes/shell": 0.9923882484436035, "general": 0.9519121050834656}` |
| filetypes/perl | joint_or_at_fp_0 | 374 | 44707 | 58.02% | 0 | 0.00 | 6700.59 | 0.000 | 73.43% | 99.65% | `{"filegroups/scripts": 0.9224196672439575, "filetypes/perl": 0.9928609728813171}` |
| filetypes/pe | learned_blend_at_fp_0 | 1368602 | 169132 | 57.40% | 0 | 0.00 | 1771.22 | 0.000 | 72.93% | 62.08% | `{}` |
| filetypes/whl | joint_or_at_fp_0 | 837 | 4542 | 55.91% | 0 | 0.00 | 65934.49 | 0.000 | 71.72% | 93.14% | `{"filetypes/whl": 0.9772860407829285, "general": 0.9701237082481384}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19080 | 55.88% | 0 | 0.00 | 15699.67 | 0.000 | 71.70% | 99.77% | `{"filegroups/scripts": 0.9712689518928528, "filetypes/lua": 0.800583004951477}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32525 | 58960 | 53.06% | 0 | 0.00 | 5080.83 | 0.000 | 69.33% | 83.31% | `{"filegroups/source": 0.9540346264839172, "filetypes/kotlin": 0.8037535548210144, "general": 0.9030658602714539}` |
| filetypes/powershell | joint_or_at_fp_0 | 5854 | 2574 | 52.55% | 0 | 0.00 | 116316.61 | 0.000 | 68.89% | 67.04% | `{"filegroups/scripts": 0.9935622215270996, "filetypes/powershell": 0.9980806112289429, "general": 0.9949795603752136}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1950 | 824031 | 49.59% | 0 | 0.00 | 363.55 | 0.000 | 66.30% | 99.88% | `{}` |
| filetypes/vbs | joint_or_at_fp_0 | 12004 | 3351 | 47.78% | 0 | 0.00 | 89358.21 | 0.000 | 64.67% | 59.18% | `{"filetypes/vbs": 0.9868960976600647, "general": 0.9913517236709595}` |
| filetypes/python | joint_or_at_fp_0 | 23364 | 245802 | 47.20% | 0 | 0.00 | 1218.75 | 0.000 | 64.13% | 95.42% | `{"filegroups/scripts": 0.9951194524765015, "filetypes/python": 0.9997473359107971, "general": 0.9959601163864136}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.996795117855072}` |
| filetypes/crx | joint_or_at_fp_0 | 884 | 86 | 98.53% | 0 | 0.00 | 3423437.28 | 0.000 | 99.26% | 98.66% | `{"filetypes/crx": 0.4664289951324463, "general": 0.9838255643844604}` |
| filetypes/rtf | joint_or_at_fp_0 | 6241 | 524 | 97.88% | 0 | 0.00 | 570073.51 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.8088999390602112, "filetypes/rtf": 0.733421802520752}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2719 | 96.87% | 0 | 0.00 | 110117.05 | 0.000 | 98.41% | 97.51% | `{"filetypes/pkg-info": 0.3348732590675354, "general": 0.9938700199127197}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.34% | 0 | 0.00 | 14427.88 | 0.000 | 97.09% | 96.28% | `{"filegroups/documents": 0.8898531198501587, "filetypes/xls": 0.9140002131462097}` |
| filetypes/gem | joint_or_at_fp_0 | 228 | 712 | 92.98% | 0 | 0.00 | 419865.01 | 0.000 | 96.36% | 98.30% | `{"filetypes/gem": 0.8426432609558105}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 96 | 285 | 92.71% | 0 | 0.00 | 1045629.02 | 0.000 | 96.22% | 98.16% | `{"filetypes/chrome-manifest": 0.835390567779541}` |
| filetypes/elf | joint_or_at_fp_0 | 189137 | 197530 | 91.51% | 0 | 0.00 | 1516.58 | 0.000 | 95.57% | 95.85% | `{"filegroups/native": 0.9669767022132874, "filetypes/elf": 0.9961905479431152, "general": 0.9955655932426453}` |
| filetypes/package.json | joint_or_at_fp_0 | 19116 | 25573 | 90.83% | 0 | 0.00 | 11713.75 | 0.000 | 95.19% | 96.08% | `{"filegroups/config": 0.999666690826416, "filetypes/package.json": 0.9983581900596619, "general": 0.9983990788459778}` |
| filetypes/tar | joint_or_at_fp_0 | 31257 | 44435 | 85.16% | 0 | 0.00 | 6741.60 | 0.000 | 91.98% | 93.87% | `{"filetypes/tar": 0.9940686225891113, "general": 0.9938685297966003}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 287 | 81.29% | 0 | 0.00 | 1038380.37 | 0.000 | 89.68% | 82.29% | `{"filegroups/documents": 0.7808955311775208, "filetypes/docx": 0.9834258556365967}` |
| filetypes/macho | joint_or_at_fp_0 | 2657 | 13098 | 79.79% | 0 | 0.00 | 22869.06 | 0.000 | 88.76% | 96.59% | `{"filegroups/native": 0.9084113836288452, "filetypes/macho": 0.9895059466362, "general": 0.9819565415382385}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 205 | 79.34% | 0 | 0.00 | 1450707.17 | 0.000 | 88.48% | 80.07% | `{"filetypes/msi": 0.5905947685241699, "general": 0.9850572943687439}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6611 | 78.90% | 0 | 0.00 | 45304.09 | 0.000 | 88.21% | 88.87% | `{"filegroups/documents": 0.42404335737228394, "filetypes/ole": 0.9987844824790955}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3391 | 323271 | 75.76% | 0 | 0.00 | 926.69 | 0.000 | 86.21% | 99.75% | `{"filetypes/python-bytecode": 0.9996669292449951, "general": 0.9757524728775024}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5929 | 75.57% | 0 | 0.00 | 50514.01 | 0.000 | 86.09% | 99.47% | `{"filetypes/clojure": 0.32156461477279663}` |
| filetypes/npm | joint_or_at_fp_0 | 1301 | 255 | 75.33% | 0 | 0.00 | 1167923.17 | 0.000 | 85.93% | 79.37% | `{"filetypes/npm": 0.643890917301178}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24578 | 73.81% | 0 | 0.00 | 12187.93 | 0.000 | 84.93% | 76.98% | `{"filegroups/documents": 0.9957650899887085, "filetypes/pdf": 0.9411760568618774, "general": 0.9833977818489075}` |
| filetypes/lnk | joint_or_at_fp_0 | 4601 | 1065 | 73.74% | 0 | 0.00 | 280894.17 | 0.000 | 84.89% | 78.68% | `{"filetypes/lnk": 0.9755615592002869, "general": 0.9989781379699707}` |
| filetypes/shell | joint_or_at_fp_0 | 15674 | 70676 | 60.89% | 0 | 0.00 | 4238.59 | 0.000 | 75.69% | 92.90% | `{"filegroups/scripts": 0.9880514144897461, "filetypes/shell": 0.9923882484436035, "general": 0.9519121050834656}` |
| filetypes/perl | joint_or_at_fp_0 | 374 | 44707 | 58.02% | 0 | 0.00 | 6700.59 | 0.000 | 73.43% | 99.65% | `{"filegroups/scripts": 0.9224196672439575, "filetypes/perl": 0.9928609728813171}` |
| filetypes/pe | learned_blend_at_fp_0 | 1368602 | 169132 | 57.40% | 0 | 0.00 | 1771.22 | 0.000 | 72.93% | 62.08% | `{}` |
| filetypes/whl | joint_or_at_fp_0 | 837 | 4542 | 55.91% | 0 | 0.00 | 65934.49 | 0.000 | 71.72% | 93.14% | `{"filetypes/whl": 0.9772860407829285, "general": 0.9701237082481384}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19080 | 55.88% | 0 | 0.00 | 15699.67 | 0.000 | 71.70% | 99.77% | `{"filegroups/scripts": 0.9712689518928528, "filetypes/lua": 0.800583004951477}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32525 | 58960 | 53.06% | 0 | 0.00 | 5080.83 | 0.000 | 69.33% | 83.31% | `{"filegroups/source": 0.9540346264839172, "filetypes/kotlin": 0.8037535548210144, "general": 0.9030658602714539}` |
| filetypes/powershell | joint_or_at_fp_0 | 5854 | 2574 | 52.55% | 0 | 0.00 | 116316.61 | 0.000 | 68.89% | 67.04% | `{"filegroups/scripts": 0.9935622215270996, "filetypes/powershell": 0.9980806112289429, "general": 0.9949795603752136}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1950 | 824031 | 49.59% | 0 | 0.00 | 363.55 | 0.000 | 66.30% | 99.88% | `{}` |
| filetypes/vbs | joint_or_at_fp_0 | 12004 | 3351 | 47.78% | 0 | 0.00 | 89358.21 | 0.000 | 64.67% | 59.18% | `{"filetypes/vbs": 0.9868960976600647, "general": 0.9913517236709595}` |
| filetypes/python | joint_or_at_fp_0 | 23364 | 245802 | 47.20% | 0 | 0.00 | 1218.75 | 0.000 | 64.13% | 95.42% | `{"filegroups/scripts": 0.9951194524765015, "filetypes/python": 0.9997473359107971, "general": 0.9959601163864136}` |
| filetypes/jar | joint_or_at_fp_0 | 3681 | 6749 | 46.62% | 0 | 0.00 | 44377.94 | 0.000 | 63.59% | 81.16% | `{"filetypes/jar": 0.9760871529579163, "general": 0.969596803188324}` |
