# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2659794449`
- Rows: 16054337 (2665816 malware, 13388521 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 869 | 97.87% | 0 | 0.00 | 344139.77 | 0.000 | 98.93% | 98.13% | `{"filegroups/documents": 0.9559474587440491, "filetypes/rtf": 0.6845533847808838}` |
| filetypes/asar | joint_or_at_fp_0 | 184 | 157 | 95.65% | 0 | 0.00 | 1890020.55 | 0.000 | 97.78% | 97.65% | `{"filetypes/asar": 0.7545366287231445, "general": 0.6989313960075378}` |
| filetypes/html | joint_or_at_fp_0 | 256 | 63361 | 94.53% | 0 | 0.00 | 4727.93 | 0.000 | 97.19% | 99.98% | `{"filetypes/html": 0.9998005628585815, "general": 0.9694483280181885}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 527 | 92.86% | 0 | 0.00 | 566837.53 | 0.000 | 96.30% | 99.31% | `{"general": 0.8431389927864075}` |
| filetypes/gem | joint_or_at_fp_0 | 900 | 2961 | 92.00% | 0 | 0.00 | 101121.83 | 0.000 | 95.83% | 98.14% | `{"filetypes/gem": 0.9333531856536865, "general": 0.9741047024726868}` |
| filetypes/elf | joint_or_at_fp_0 | 194112 | 721371 | 89.06% | 0 | 0.00 | 415.28 | 0.000 | 94.21% | 97.68% | `{"filegroups/native": 0.991648256778717, "filetypes/elf": 0.9996354579925537, "general": 0.9937245845794678}` |
| filetypes/7z | joint_or_at_fp_0 | 8998 | 248 | 88.33% | 0 | 0.00 | 1200690.05 | 0.000 | 93.80% | 88.64% | `{"filetypes/7z": 0.9079958200454712, "general": 0.9887274503707886}` |
| filetypes/tar | joint_or_at_fp_0 | 34231 | 69815 | 67.61% | 0 | 0.00 | 4290.87 | 0.000 | 80.67% | 89.34% | `{"filetypes/tar": 0.998904824256897, "general": 0.9956712126731873}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 15604 | 62.44% | 0 | 0.00 | 19196.65 | 0.000 | 76.88% | 84.79% | `{"filetypes/pkg_info": 0.9978606700897217, "general": 0.9982554316520691}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 892744 | 61.05% | 0 | 0.00 | 335.56 | 0.000 | 75.81% | 99.85% | `{"filetypes/python_bytecode": 0.99205482006073, "general": 0.9795911908149719}` |
| filetypes/macho | joint_or_at_fp_0 | 2822 | 27632 | 59.53% | 0 | 0.00 | 10840.94 | 0.000 | 74.63% | 96.25% | `{"filegroups/native": 0.978805422782898, "filetypes/macho": 0.987602949142456, "general": 0.9804026484489441}` |
| filetypes/shell | joint_or_at_fp_0 | 18411 | 153209 | 59.02% | 0 | 0.00 | 1955.30 | 0.000 | 74.23% | 95.60% | `{"filetypes/shell": 0.996673583984375, "general": 0.9955992698669434}` |
| filetypes/package.json | joint_or_at_fp_0 | 20499 | 52816 | 57.08% | 0 | 0.00 | 5671.86 | 0.000 | 72.67% | 88.00% | `{"filegroups/config": 0.9999856352806091, "filetypes/package.json": 0.9998021125793457, "general": 0.9986355900764465}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27112 | 53.77% | 0 | 0.00 | 11048.86 | 0.000 | 69.94% | 99.82% | `{"filegroups/scripts": 0.9872527718544006, "filetypes/lua": 0.9392476677894592}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 43183 | 52.17% | 0 | 0.00 | 6937.05 | 0.000 | 68.57% | 99.92% | `{"filegroups/source": 0.0546562485396862}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32373 | 83159 | 50.94% | 0 | 0.00 | 3602.35 | 0.000 | 67.50% | 86.25% | `{"filegroups/source": 0.9956105351448059, "filetypes/kotlin": 0.9944589734077454, "general": 0.9823554754257202}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87638 | 31161 | 46.64% | 0 | 0.00 | 9613.26 | 0.000 | 63.61% | 60.64% | `{"filetypes/ole_doc": 0.9994144439697266, "general": 0.9993598461151123}` |
| filetypes/perl | joint_or_at_fp_0 | 398 | 75259 | 46.23% | 0 | 0.00 | 3980.48 | 0.000 | 63.23% | 99.72% | `{"filegroups/scripts": 0.995851993560791, "filetypes/perl": 0.9990823268890381, "general": 0.9901401996612549}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9135 | 45.45% | 0 | 0.00 | 32788.63 | 0.000 | 62.50% | 99.35% | `{"filetypes/clojure": 0.9935770630836487, "general": 0.038632649928331375}` |
| filetypes/powershell | joint_or_at_fp_0 | 6047 | 4847 | 44.50% | 0 | 0.00 | 61786.81 | 0.000 | 61.59% | 69.19% | `{"filegroups/scripts": 0.9981575608253479, "filetypes/powershell": 0.9989431500434875, "general": 0.9923400282859802}` |
| filetypes/python | joint_or_at_fp_0 | 23114 | 613966 | 43.97% | 0 | 0.00 | 487.93 | 0.000 | 61.08% | 97.97% | `{"filegroups/scripts": 0.998746395111084, "filetypes/python": 0.9956305623054504, "general": 0.99421226978302}` |
| filetypes/lnk | joint_or_at_fp_0 | 4659 | 1107 | 43.61% | 0 | 0.00 | 270251.35 | 0.000 | 60.74% | 54.44% | `{"filetypes/lnk": 0.9895011782646179, "general": 0.9984167814254761}` |
| filetypes/ruby | learned_blend_at_fp_0 | 398 | 177341 | 40.95% | 0 | 0.00 | 1689.24 | 0.000 | 58.11% | 99.87% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 6453 | 597497 | 39.78% | 0 | 0.00 | 501.38 | 0.000 | 56.92% | 99.36% | `{"filegroups/scripts": 0.9985790848731995, "filetypes/php": 0.9990136623382568, "general": 0.9801896214485168}` |
| filetypes/javascript | joint_or_at_fp_0 | 140535 | 1447513 | 39.15% | 0 | 0.00 | 206.96 | 0.000 | 56.27% | 94.62% | `{"filegroups/scripts": 0.998687744140625, "filetypes/javascript": 0.9989517331123352, "general": 0.9988614916801453}` |
| filetypes/pe | joint_or_at_fp_0 | 1375283 | 211523 | 36.40% | 0 | 0.00 | 1416.26 | 0.000 | 53.38% | 44.88% | `{"filegroups/native": 0.9997379779815674, "filetypes/pe": 0.9996015429496765, "general": 0.9998400807380676}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2863 | 132 | 34.54% | 0 | 0.00 | 2243934.85 | 0.000 | 51.35% | 37.43% | `{"filetypes/apk_android": 0.7859998941421509, "general": 0.3841687738895416}` |
| filetypes/npm | joint_or_at_fp_0 | 5172 | 6894 | 33.80% | 0 | 0.00 | 43444.76 | 0.000 | 50.52% | 71.62% | `{"filetypes/npm": 0.9974836111068726, "general": 0.9988263845443726}` |
| filetypes/pdf | joint_or_at_fp_0 | 178640 | 29250 | 32.88% | 0 | 0.00 | 10241.30 | 0.000 | 49.49% | 42.32% | `{"filegroups/documents": 0.9982286095619202, "filetypes/pdf": 0.9981079697608948, "general": 0.985171377658844}` |
| filetypes/vbs | joint_or_at_fp_0 | 12359 | 3650 | 32.00% | 0 | 0.00 | 82041.18 | 0.000 | 48.49% | 47.50% | `{"filetypes/vbs": 0.9891085624694824, "general": 0.9909103512763977}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 869 | 97.87% | 0 | 0.00 | 344139.77 | 0.000 | 98.93% | 98.13% | `{"filegroups/documents": 0.9559474587440491, "filetypes/rtf": 0.6845533847808838}` |
| filetypes/asar | joint_or_at_fp_0 | 184 | 157 | 95.65% | 0 | 0.00 | 1890020.55 | 0.000 | 97.78% | 97.65% | `{"filetypes/asar": 0.7545366287231445, "general": 0.6989313960075378}` |
| filetypes/html | joint_or_at_fp_0 | 256 | 63361 | 94.53% | 0 | 0.00 | 4727.93 | 0.000 | 97.19% | 99.98% | `{"filetypes/html": 0.9998005628585815, "general": 0.9694483280181885}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 527 | 92.86% | 0 | 0.00 | 566837.53 | 0.000 | 96.30% | 99.31% | `{"general": 0.8431389927864075}` |
| filetypes/gem | joint_or_at_fp_0 | 900 | 2961 | 92.00% | 0 | 0.00 | 101121.83 | 0.000 | 95.83% | 98.14% | `{"filetypes/gem": 0.9333531856536865, "general": 0.9741047024726868}` |
| filetypes/elf | joint_or_at_fp_0 | 194112 | 721371 | 89.06% | 0 | 0.00 | 415.28 | 0.000 | 94.21% | 97.68% | `{"filegroups/native": 0.991648256778717, "filetypes/elf": 0.9996354579925537, "general": 0.9937245845794678}` |
| filetypes/7z | joint_or_at_fp_0 | 8998 | 248 | 88.33% | 0 | 0.00 | 1200690.05 | 0.000 | 93.80% | 88.64% | `{"filetypes/7z": 0.9079958200454712, "general": 0.9887274503707886}` |
| filetypes/tar | joint_or_at_fp_0 | 34231 | 69815 | 67.61% | 0 | 0.00 | 4290.87 | 0.000 | 80.67% | 89.34% | `{"filetypes/tar": 0.998904824256897, "general": 0.9956712126731873}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 15604 | 62.44% | 0 | 0.00 | 19196.65 | 0.000 | 76.88% | 84.79% | `{"filetypes/pkg_info": 0.9978606700897217, "general": 0.9982554316520691}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 892744 | 61.05% | 0 | 0.00 | 335.56 | 0.000 | 75.81% | 99.85% | `{"filetypes/python_bytecode": 0.99205482006073, "general": 0.9795911908149719}` |
| filetypes/macho | joint_or_at_fp_0 | 2822 | 27632 | 59.53% | 0 | 0.00 | 10840.94 | 0.000 | 74.63% | 96.25% | `{"filegroups/native": 0.978805422782898, "filetypes/macho": 0.987602949142456, "general": 0.9804026484489441}` |
| filetypes/shell | joint_or_at_fp_0 | 18411 | 153209 | 59.02% | 0 | 0.00 | 1955.30 | 0.000 | 74.23% | 95.60% | `{"filetypes/shell": 0.996673583984375, "general": 0.9955992698669434}` |
| filetypes/package.json | joint_or_at_fp_0 | 20499 | 52816 | 57.08% | 0 | 0.00 | 5671.86 | 0.000 | 72.67% | 88.00% | `{"filegroups/config": 0.9999856352806091, "filetypes/package.json": 0.9998021125793457, "general": 0.9986355900764465}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27112 | 53.77% | 0 | 0.00 | 11048.86 | 0.000 | 69.94% | 99.82% | `{"filegroups/scripts": 0.9872527718544006, "filetypes/lua": 0.9392476677894592}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 43183 | 52.17% | 0 | 0.00 | 6937.05 | 0.000 | 68.57% | 99.92% | `{"filegroups/source": 0.0546562485396862}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32373 | 83159 | 50.94% | 0 | 0.00 | 3602.35 | 0.000 | 67.50% | 86.25% | `{"filegroups/source": 0.9956105351448059, "filetypes/kotlin": 0.9944589734077454, "general": 0.9823554754257202}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87638 | 31161 | 46.64% | 0 | 0.00 | 9613.26 | 0.000 | 63.61% | 60.64% | `{"filetypes/ole_doc": 0.9994144439697266, "general": 0.9993598461151123}` |
| filetypes/perl | joint_or_at_fp_0 | 398 | 75259 | 46.23% | 0 | 0.00 | 3980.48 | 0.000 | 63.23% | 99.72% | `{"filegroups/scripts": 0.995851993560791, "filetypes/perl": 0.9990823268890381, "general": 0.9901401996612549}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9135 | 45.45% | 0 | 0.00 | 32788.63 | 0.000 | 62.50% | 99.35% | `{"filetypes/clojure": 0.9935770630836487, "general": 0.038632649928331375}` |
| filetypes/powershell | joint_or_at_fp_0 | 6047 | 4847 | 44.50% | 0 | 0.00 | 61786.81 | 0.000 | 61.59% | 69.19% | `{"filegroups/scripts": 0.9981575608253479, "filetypes/powershell": 0.9989431500434875, "general": 0.9923400282859802}` |
| filetypes/python | joint_or_at_fp_0 | 23114 | 613966 | 43.97% | 0 | 0.00 | 487.93 | 0.000 | 61.08% | 97.97% | `{"filegroups/scripts": 0.998746395111084, "filetypes/python": 0.9956305623054504, "general": 0.99421226978302}` |
| filetypes/lnk | joint_or_at_fp_0 | 4659 | 1107 | 43.61% | 0 | 0.00 | 270251.35 | 0.000 | 60.74% | 54.44% | `{"filetypes/lnk": 0.9895011782646179, "general": 0.9984167814254761}` |
| filetypes/ruby | learned_blend_at_fp_0 | 398 | 177341 | 40.95% | 0 | 0.00 | 1689.24 | 0.000 | 58.11% | 99.87% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 6453 | 597497 | 39.78% | 0 | 0.00 | 501.38 | 0.000 | 56.92% | 99.36% | `{"filegroups/scripts": 0.9985790848731995, "filetypes/php": 0.9990136623382568, "general": 0.9801896214485168}` |
| filetypes/javascript | joint_or_at_fp_0 | 140535 | 1447513 | 39.15% | 0 | 0.00 | 206.96 | 0.000 | 56.27% | 94.62% | `{"filegroups/scripts": 0.998687744140625, "filetypes/javascript": 0.9989517331123352, "general": 0.9988614916801453}` |
| filetypes/pe | joint_or_at_fp_0 | 1375283 | 211523 | 36.40% | 0 | 0.00 | 1416.26 | 0.000 | 53.38% | 44.88% | `{"filegroups/native": 0.9997379779815674, "filetypes/pe": 0.9996015429496765, "general": 0.9998400807380676}` |
| filetypes/zst | calibrate_inherited | 10472 | 305292 | 35.37% | 0 | 0.00 | 981.26 | 0.000 | 52.26% | 97.86% | `{"general": 0.9992812251457481}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2863 | 132 | 34.54% | 0 | 0.00 | 2243934.85 | 0.000 | 51.35% | 37.43% | `{"filetypes/apk_android": 0.7859998941421509, "general": 0.3841687738895416}` |
| filetypes/npm | joint_or_at_fp_0 | 5172 | 6894 | 33.80% | 0 | 0.00 | 43444.76 | 0.000 | 50.52% | 71.62% | `{"filetypes/npm": 0.9974836111068726, "general": 0.9988263845443726}` |
| filetypes/rar | calibrate_inherited | 22184 | 13 | 33.01% | 0 | 0.00 | 20581666.52 | 0.000 | 49.64% | 33.05% | `{"general": 0.9992812251457481}` |
