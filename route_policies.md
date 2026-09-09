# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `4265996154`
- Rows: 18146634 (2680655 malware, 15465979 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 191 | 287 | 97.38% | 0 | 0.00 | 1038380.37 | 0.000 | 98.67% | 98.95% | `{"filetypes/asar": 0.877382755279541, "general": 0.8244227766990662}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 97.26% | 0 | 0.00 | 337928.55 | 0.000 | 98.61% | 97.60% | `{"filegroups/documents": 0.9444311261177063, "filetypes/rtf": 0.985369086265564}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 92.73% | 0 | 0.00 | 566837.53 | 0.000 | 96.23% | 99.31% | `{"filetypes/applescript": 0.961675226688385, "general": 0.9387657046318054}` |
| filetypes/7z | joint_or_at_fp_0 | 9047 | 329 | 91.89% | 0 | 0.00 | 906423.91 | 0.000 | 95.77% | 92.17% | `{"filetypes/7z": 0.7093846201896667, "general": 0.9723973274230957}` |
| filetypes/elf | joint_or_at_fp_0 | 196805 | 847549 | 88.10% | 0 | 0.00 | 353.46 | 0.000 | 93.67% | 97.76% | `{"filegroups/native": 0.9945619702339172, "filetypes/elf": 0.9998200535774231, "general": 0.9955693483352661}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 71 | 85.66% | 0 | 0.00 | 4131565.87 | 0.000 | 92.27% | 88.89% | `{"filetypes/chm": 0.9045122861862183, "general": 0.37594228982925415}` |
| filetypes/cab | learned_blend_at_fp_0 | 880 | 84 | 80.34% | 0 | 0.00 | 3503503.06 | 0.000 | 89.10% | 82.05% | `{}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 313 | 69.84% | 0 | 0.00 | 952537.31 | 0.000 | 82.24% | 94.95% | `{"filetypes/dmg": 0.953292727470398, "general": 0.9934636354446411}` |
| filetypes/shell | joint_or_at_fp_0 | 18756 | 164166 | 65.55% | 0 | 0.00 | 1824.80 | 0.000 | 79.19% | 96.47% | `{"filegroups/scripts": 0.9991629719734192, "filetypes/shell": 0.9963274002075195, "general": 0.9938265681266785}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 33932 | 61.34% | 0 | 0.00 | 8828.24 | 0.000 | 76.04% | 97.00% | `{"filegroups/native": 0.964705765247345, "filetypes/macho": 0.9877621531486511}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27782 | 61.32% | 0 | 0.00 | 10782.42 | 0.000 | 76.02% | 99.85% | `{"filetypes/lua": 0.6480605602264404}` |
| filetypes/tar | joint_or_at_fp_0 | 34314 | 82193 | 59.72% | 0 | 0.00 | 3644.69 | 0.000 | 74.78% | 88.14% | `{"filetypes/tar": 0.9995732307434082, "general": 0.9971647262573242}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32351 | 84060 | 53.20% | 0 | 0.00 | 3563.74 | 0.000 | 69.46% | 87.00% | `{"filegroups/source": 0.9893109202384949, "filetypes/kotlin": 0.9309629201889038, "general": 0.9947842955589294}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44608 | 52.17% | 0 | 0.00 | 6715.46 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.32530489563941956}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 951 | 806 | 49.95% | 0 | 0.00 | 370989.07 | 0.000 | 66.62% | 72.91% | `{"filetypes/python_sdist": 0.9906394481658936, "general": 0.971674382686615}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87709 | 31328 | 49.31% | 0 | 0.00 | 9562.02 | 0.000 | 66.05% | 62.65% | `{"filetypes/ole_doc": 0.9993537068367004, "general": 0.9989978075027466}` |
| filetypes/pe | joint_or_at_fp_0 | 1379460 | 249378 | 47.17% | 0 | 0.00 | 1201.27 | 0.000 | 64.10% | 55.26% | `{"filegroups/native": 0.9997759461402893, "filetypes/pe": 0.9994805455207825, "general": 0.9995736479759216}` |
| filetypes/python | joint_or_at_fp_0 | 23619 | 650854 | 45.36% | 0 | 0.00 | 460.28 | 0.000 | 62.41% | 98.09% | `{"filegroups/scripts": 0.9993122816085815, "filetypes/python": 0.99659663438797, "general": 0.9914003014564514}` |
| filetypes/gem | joint_or_at_fp_0 | 2105 | 41044 | 45.32% | 0 | 0.00 | 7298.56 | 0.000 | 62.37% | 97.33% | `{"filetypes/gem": 0.997404932975769, "general": 0.955265998840332}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 5611 | 45.00% | 0 | 0.00 | 53376.10 | 0.000 | 62.07% | 71.47% | `{"filegroups/scripts": 0.9985575079917908, "filetypes/powershell": 0.9960235357284546, "general": 0.9981186985969543}` |
| filetypes/npm | joint_or_at_fp_0 | 17444 | 98151 | 44.73% | 0 | 0.00 | 3052.12 | 0.000 | 61.81% | 91.66% | `{"filetypes/npm": 0.9993144869804382, "general": 0.9993318319320679}` |
| filetypes/javascript | joint_or_at_fp_0 | 144939 | 1704828 | 41.81% | 0 | 0.00 | 175.72 | 0.000 | 58.97% | 95.44% | `{"filegroups/scripts": 0.9988857507705688, "filetypes/javascript": 0.9988902807235718, "general": 0.9969733357429504}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9505 | 40.91% | 0 | 0.00 | 31512.47 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9982877969741821, "general": 0.01750543713569641}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 78543 | 30.98% | 0 | 0.00 | 3814.06 | 0.000 | 47.31% | 99.65% | `{"filetypes/perl": 0.9997957348823547, "general": 0.9915205240249634}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2900 | 245 | 29.90% | 0 | 0.00 | 1215302.68 | 0.000 | 46.03% | 35.36% | `{"filetypes/apk_android": 0.9270797967910767, "general": 0.5010213255882263}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67992 | 3136 | 29.82% | 0 | 0.00 | 95481.56 | 0.000 | 45.94% | 32.91% | `{"filetypes/ooxml": 0.9984638690948486, "general": 0.992874026298523}` |
| filetypes/rar | calibrate_inherited | 22206 | 43 | 29.65% | 0 | 0.00 | 6729675.34 | 0.000 | 45.74% | 29.79% | `{"general": 0.9993818992838515}` |
| filetypes/lnk | joint_or_at_fp_0 | 4693 | 1155 | 29.24% | 0 | 0.00 | 259034.68 | 0.000 | 45.24% | 43.21% | `{"filetypes/lnk": 0.9932800531387329, "general": 0.9992448687553406}` |
| filetypes/ruby | learned_blend_at_fp_0 | 402 | 183691 | 28.86% | 0 | 0.00 | 1630.84 | 0.000 | 44.79% | 99.84% | `{}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1114 | 28.71% | 0 | 0.00 | 268555.46 | 0.000 | 44.62% | 94.07% | `{"filetypes/chrome_manifest": 0.9885585904121399, "general": 0.9303878545761108}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/asar | joint_or_at_fp_0 | 191 | 287 | 97.38% | 0 | 0.00 | 1038380.37 | 0.000 | 98.67% | 98.95% | `{"filetypes/asar": 0.877382755279541, "general": 0.8244227766990662}` |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 97.26% | 0 | 0.00 | 337928.55 | 0.000 | 98.61% | 97.60% | `{"filegroups/documents": 0.9444311261177063, "filetypes/rtf": 0.985369086265564}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 527 | 92.73% | 0 | 0.00 | 566837.53 | 0.000 | 96.23% | 99.31% | `{"filetypes/applescript": 0.961675226688385, "general": 0.9387657046318054}` |
| filetypes/7z | joint_or_at_fp_0 | 9047 | 329 | 91.89% | 0 | 0.00 | 906423.91 | 0.000 | 95.77% | 92.17% | `{"filetypes/7z": 0.7093846201896667, "general": 0.9723973274230957}` |
| filetypes/elf | joint_or_at_fp_0 | 196805 | 847549 | 88.10% | 0 | 0.00 | 353.46 | 0.000 | 93.67% | 97.76% | `{"filegroups/native": 0.9945619702339172, "filetypes/elf": 0.9998200535774231, "general": 0.9955693483352661}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 71 | 85.66% | 0 | 0.00 | 4131565.87 | 0.000 | 92.27% | 88.89% | `{"filetypes/chm": 0.9045122861862183, "general": 0.37594228982925415}` |
| filetypes/cab | learned_blend_at_fp_0 | 880 | 84 | 80.34% | 0 | 0.00 | 3503503.06 | 0.000 | 89.10% | 82.05% | `{}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 313 | 69.84% | 0 | 0.00 | 952537.31 | 0.000 | 82.24% | 94.95% | `{"filetypes/dmg": 0.953292727470398, "general": 0.9934636354446411}` |
| filetypes/shell | joint_or_at_fp_0 | 18756 | 164166 | 65.55% | 0 | 0.00 | 1824.80 | 0.000 | 79.19% | 96.47% | `{"filegroups/scripts": 0.9991629719734192, "filetypes/shell": 0.9963274002075195, "general": 0.9938265681266785}` |
| filetypes/macho | joint_or_at_fp_0 | 2858 | 33932 | 61.34% | 0 | 0.00 | 8828.24 | 0.000 | 76.04% | 97.00% | `{"filegroups/native": 0.964705765247345, "filetypes/macho": 0.9877621531486511}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27782 | 61.32% | 0 | 0.00 | 10782.42 | 0.000 | 76.02% | 99.85% | `{"filetypes/lua": 0.6480605602264404}` |
| filetypes/tar | joint_or_at_fp_0 | 34314 | 82193 | 59.72% | 0 | 0.00 | 3644.69 | 0.000 | 74.78% | 88.14% | `{"filetypes/tar": 0.9995732307434082, "general": 0.9971647262573242}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32351 | 84060 | 53.20% | 0 | 0.00 | 3563.74 | 0.000 | 69.46% | 87.00% | `{"filegroups/source": 0.9893109202384949, "filetypes/kotlin": 0.9309629201889038, "general": 0.9947842955589294}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44608 | 52.17% | 0 | 0.00 | 6715.46 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.32530489563941956}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 951 | 806 | 49.95% | 0 | 0.00 | 370989.07 | 0.000 | 66.62% | 72.91% | `{"filetypes/python_sdist": 0.9906394481658936, "general": 0.971674382686615}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87709 | 31328 | 49.31% | 0 | 0.00 | 9562.02 | 0.000 | 66.05% | 62.65% | `{"filetypes/ole_doc": 0.9993537068367004, "general": 0.9989978075027466}` |
| filetypes/pe | joint_or_at_fp_0 | 1379460 | 249378 | 47.17% | 0 | 0.00 | 1201.27 | 0.000 | 64.10% | 55.26% | `{"filegroups/native": 0.9997759461402893, "filetypes/pe": 0.9994805455207825, "general": 0.9995736479759216}` |
| filetypes/python | joint_or_at_fp_0 | 23619 | 650854 | 45.36% | 0 | 0.00 | 460.28 | 0.000 | 62.41% | 98.09% | `{"filegroups/scripts": 0.9993122816085815, "filetypes/python": 0.99659663438797, "general": 0.9914003014564514}` |
| filetypes/gem | joint_or_at_fp_0 | 2105 | 41044 | 45.32% | 0 | 0.00 | 7298.56 | 0.000 | 62.37% | 97.33% | `{"filetypes/gem": 0.997404932975769, "general": 0.955265998840332}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 5611 | 45.00% | 0 | 0.00 | 53376.10 | 0.000 | 62.07% | 71.47% | `{"filegroups/scripts": 0.9985575079917908, "filetypes/powershell": 0.9960235357284546, "general": 0.9981186985969543}` |
| filetypes/npm | joint_or_at_fp_0 | 17444 | 98151 | 44.73% | 0 | 0.00 | 3052.12 | 0.000 | 61.81% | 91.66% | `{"filetypes/npm": 0.9993144869804382, "general": 0.9993318319320679}` |
| filetypes/javascript | joint_or_at_fp_0 | 144939 | 1704828 | 41.81% | 0 | 0.00 | 175.72 | 0.000 | 58.97% | 95.44% | `{"filegroups/scripts": 0.9988857507705688, "filetypes/javascript": 0.9988902807235718, "general": 0.9969733357429504}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9505 | 40.91% | 0 | 0.00 | 31512.47 | 0.000 | 58.06% | 99.32% | `{"filetypes/clojure": 0.9982877969741821, "general": 0.01750543713569641}` |
| filetypes/rar | calibrate_inherited | 22206 | 43 | 34.51% | 0 | 0.00 | 6729675.34 | 0.000 | 51.32% | 34.64% | `{"general": 0.9992355090728172}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 78543 | 30.98% | 0 | 0.00 | 3814.06 | 0.000 | 47.31% | 99.65% | `{"filetypes/perl": 0.9997957348823547, "general": 0.9915205240249634}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2900 | 245 | 29.90% | 0 | 0.00 | 1215302.68 | 0.000 | 46.03% | 35.36% | `{"filetypes/apk_android": 0.9270797967910767, "general": 0.5010213255882263}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67992 | 3136 | 29.82% | 0 | 0.00 | 95481.56 | 0.000 | 45.94% | 32.91% | `{"filetypes/ooxml": 0.9984638690948486, "general": 0.992874026298523}` |
| filetypes/lnk | joint_or_at_fp_0 | 4693 | 1155 | 29.24% | 0 | 0.00 | 259034.68 | 0.000 | 45.24% | 43.21% | `{"filetypes/lnk": 0.9932800531387329, "general": 0.9992448687553406}` |
| filetypes/ruby | learned_blend_at_fp_0 | 402 | 183691 | 28.86% | 0 | 0.00 | 1630.84 | 0.000 | 44.79% | 99.84% | `{}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1114 | 28.71% | 0 | 0.00 | 268555.46 | 0.000 | 44.62% | 94.07% | `{"filetypes/chrome_manifest": 0.9885585904121399, "general": 0.9303878545761108}` |
