# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3450504705`
- Rows: 17132677 (2673344 malware, 14459333 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 879 | 97.87% | 0 | 0.00 | 340231.30 | 0.000 | 98.93% | 98.14% | `{"filegroups/documents": 0.975637674331665, "filetypes/rtf": 0.7046968936920166}` |
| filetypes/asar | joint_or_at_fp_0 | 185 | 224 | 97.30% | 0 | 0.00 | 1328477.28 | 0.000 | 98.63% | 98.78% | `{"filetypes/asar": 0.7306756377220154, "general": 0.6601081490516663}` |
| filetypes/html | joint_or_at_fp_0 | 262 | 67496 | 92.37% | 0 | 0.00 | 4438.29 | 0.000 | 96.03% | 99.97% | `{"filetypes/html": 0.9998939633369446, "general": 0.9424716234207153}` |
| filetypes/gem | joint_or_at_fp_0 | 932 | 3538 | 91.52% | 0 | 0.00 | 84637.21 | 0.000 | 95.57% | 98.23% | `{"filetypes/gem": 0.9810687899589539, "general": 0.9516155123710632}` |
| filetypes/applescript | joint_or_at_fp_0 | 57 | 527 | 91.23% | 0 | 0.00 | 566837.53 | 0.000 | 95.41% | 99.14% | `{"general": 0.9165362119674683}` |
| filetypes/7z | joint_or_at_fp_0 | 9010 | 297 | 90.72% | 0 | 0.00 | 1003594.11 | 0.000 | 95.14% | 91.02% | `{"filetypes/7z": 0.8370134830474854, "general": 0.9753223657608032}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16287 | 90.01% | 0 | 0.00 | 18391.70 | 0.000 | 94.74% | 96.06% | `{"filetypes/pkg_info": 0.9963082671165466, "general": 0.9941892623901367}` |
| filetypes/elf | joint_or_at_fp_0 | 195453 | 784391 | 86.75% | 0 | 0.00 | 381.92 | 0.000 | 92.90% | 97.36% | `{"filegroups/native": 0.9958385825157166, "filetypes/elf": 0.9997966885566711, "general": 0.9937453269958496}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 50 | 85.25% | 0 | 0.00 | 5815507.91 | 0.000 | 92.04% | 87.76% | `{"filetypes/chm": 0.8650705218315125, "general": 0.1885560154914856}` |
| filetypes/tar | joint_or_at_fp_0 | 34318 | 73563 | 72.00% | 0 | 0.00 | 4072.25 | 0.000 | 83.72% | 91.09% | `{"filetypes/tar": 0.998378574848175, "general": 0.9940339922904968}` |
| filetypes/package.json | joint_or_at_fp_0 | 20662 | 62503 | 62.02% | 0 | 0.00 | 4792.83 | 0.000 | 76.56% | 90.56% | `{"filegroups/config": 0.9999741911888123, "filetypes/package.json": 0.9998231530189514, "general": 0.9993354082107544}` |
| filetypes/shell | joint_or_at_fp_0 | 18579 | 157630 | 58.15% | 0 | 0.00 | 1900.47 | 0.000 | 73.53% | 95.59% | `{"filegroups/scripts": 0.9994414448738098, "filetypes/shell": 0.9974471926689148, "general": 0.9960634708404541}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44522 | 52.17% | 0 | 0.00 | 6728.43 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.12992624938488007}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32363 | 83308 | 52.02% | 0 | 0.00 | 3595.91 | 0.000 | 68.44% | 86.58% | `{"filegroups/source": 0.9971853494644165, "filetypes/kotlin": 0.9353815317153931, "general": 0.9806024432182312}` |
| filetypes/macho | joint_or_at_fp_0 | 2825 | 31153 | 51.93% | 0 | 0.00 | 9615.73 | 0.000 | 68.36% | 96.00% | `{"filegroups/native": 0.9857239127159119, "filetypes/macho": 0.9956993460655212, "general": 0.9968633651733398}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3512 | 1014811 | 51.65% | 0 | 0.00 | 295.20 | 0.000 | 68.12% | 99.83% | `{"filetypes/python_bytecode": 0.9999443888664246, "general": 0.9865643978118896}` |
| filetypes/dmg | joint_or_at_fp_0 | 62 | 241 | 51.61% | 0 | 0.00 | 1235348.58 | 0.000 | 68.09% | 90.10% | `{"filetypes/dmg": 0.8412267565727234, "general": 0.9566053152084351}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27666 | 50.94% | 0 | 0.00 | 10827.62 | 0.000 | 67.50% | 99.81% | `{"filegroups/scripts": 0.996650755405426, "filetypes/lua": 0.863678514957428}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 75 | 272 | 45.33% | 0 | 0.00 | 1095329.26 | 0.000 | 62.39% | 88.18% | `{"filetypes/python_sdist": 0.9296724796295166, "general": 0.9576486945152283}` |
| filetypes/python | joint_or_at_fp_0 | 23148 | 637265 | 45.01% | 0 | 0.00 | 470.09 | 0.000 | 62.07% | 98.07% | `{"filegroups/scripts": 0.9990367889404297, "filetypes/python": 0.9969910979270935, "general": 0.9931808710098267}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 76141 | 44.08% | 0 | 0.00 | 3934.38 | 0.000 | 61.19% | 99.71% | `{"filegroups/scripts": 0.9981914758682251, "filetypes/perl": 0.999664843082428, "general": 0.9806804656982422}` |
| filetypes/javascript | joint_or_at_fp_0 | 141304 | 1611995 | 44.01% | 0 | 0.00 | 185.84 | 0.000 | 61.12% | 95.49% | `{"filegroups/scripts": 0.9987635612487793, "filetypes/javascript": 0.9986634254455566, "general": 0.9988200068473816}` |
| filetypes/powershell | joint_or_at_fp_0 | 6063 | 5268 | 42.29% | 0 | 0.00 | 56850.43 | 0.000 | 59.44% | 69.12% | `{"filegroups/scripts": 0.9987106919288635, "filetypes/powershell": 0.9985373616218567, "general": 0.9957389831542969}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9264 | 40.91% | 0 | 0.00 | 32332.12 | 0.000 | 58.06% | 99.31% | `{"filetypes/clojure": 0.9970583319664001, "general": 0.02364300936460495}` |
| filetypes/zst | calibrate_inherited | 10473 | 325483 | 39.85% | 0 | 0.00 | 920.39 | 0.000 | 56.99% | 98.13% | `{"general": 0.9993479127347483}` |
| filetypes/pdf | joint_or_at_fp_0 | 178640 | 29364 | 39.05% | 0 | 0.00 | 10201.54 | 0.000 | 56.17% | 47.65% | `{"filegroups/documents": 0.9981157183647156, "filetypes/pdf": 0.9986247420310974, "general": 0.9961258172988892}` |
| filetypes/php | joint_or_at_fp_0 | 6652 | 611948 | 38.73% | 0 | 0.00 | 489.54 | 0.000 | 55.83% | 99.34% | `{"filegroups/scripts": 0.9988862872123718, "filetypes/php": 0.9965444803237915, "general": 0.9782417416572571}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1119 | 37.08% | 0 | 0.00 | 267357.09 | 0.000 | 54.10% | 49.21% | `{"filetypes/lnk": 0.996296226978302, "general": 0.9986103177070618}` |
| filetypes/pe | joint_or_at_fp_0 | 1377225 | 228402 | 35.67% | 0 | 0.00 | 1311.60 | 0.000 | 52.58% | 44.82% | `{"filegroups/native": 0.9997637271881104, "filetypes/pe": 0.9996781349182129, "general": 0.9996814727783203}` |
| filetypes/ruby | joint_or_at_fp_0 | 397 | 179076 | 33.50% | 0 | 0.00 | 1672.87 | 0.000 | 50.19% | 99.85% | `{"filetypes/ruby": 0.9766124486923218, "general": 0.922759473323822}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6254 | 879 | 97.87% | 0 | 0.00 | 340231.30 | 0.000 | 98.93% | 98.14% | `{"filegroups/documents": 0.975637674331665, "filetypes/rtf": 0.7046968936920166}` |
| filetypes/asar | joint_or_at_fp_0 | 185 | 224 | 97.30% | 0 | 0.00 | 1328477.28 | 0.000 | 98.63% | 98.78% | `{"filetypes/asar": 0.7306756377220154, "general": 0.6601081490516663}` |
| filetypes/html | joint_or_at_fp_0 | 262 | 67496 | 92.37% | 0 | 0.00 | 4438.29 | 0.000 | 96.03% | 99.97% | `{"filetypes/html": 0.9998939633369446, "general": 0.9424716234207153}` |
| filetypes/gem | joint_or_at_fp_0 | 932 | 3538 | 91.52% | 0 | 0.00 | 84637.21 | 0.000 | 95.57% | 98.23% | `{"filetypes/gem": 0.9810687899589539, "general": 0.9516155123710632}` |
| filetypes/applescript | joint_or_at_fp_0 | 57 | 527 | 91.23% | 0 | 0.00 | 566837.53 | 0.000 | 95.41% | 99.14% | `{"general": 0.9165362119674683}` |
| filetypes/7z | joint_or_at_fp_0 | 9010 | 297 | 90.72% | 0 | 0.00 | 1003594.11 | 0.000 | 95.14% | 91.02% | `{"filetypes/7z": 0.8370134830474854, "general": 0.9753223657608032}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16287 | 90.01% | 0 | 0.00 | 18391.70 | 0.000 | 94.74% | 96.06% | `{"filetypes/pkg_info": 0.9963082671165466, "general": 0.9941892623901367}` |
| filetypes/elf | joint_or_at_fp_0 | 195453 | 784391 | 86.75% | 0 | 0.00 | 381.92 | 0.000 | 92.90% | 97.36% | `{"filegroups/native": 0.9958385825157166, "filetypes/elf": 0.9997966885566711, "general": 0.9937453269958496}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 50 | 85.25% | 0 | 0.00 | 5815507.91 | 0.000 | 92.04% | 87.76% | `{"filetypes/chm": 0.8650705218315125, "general": 0.1885560154914856}` |
| filetypes/tar | joint_or_at_fp_0 | 34318 | 73563 | 72.00% | 0 | 0.00 | 4072.25 | 0.000 | 83.72% | 91.09% | `{"filetypes/tar": 0.998378574848175, "general": 0.9940339922904968}` |
| filetypes/package.json | joint_or_at_fp_0 | 20662 | 62503 | 62.02% | 0 | 0.00 | 4792.83 | 0.000 | 76.56% | 90.56% | `{"filegroups/config": 0.9999741911888123, "filetypes/package.json": 0.9998231530189514, "general": 0.9993354082107544}` |
| filetypes/shell | joint_or_at_fp_0 | 18579 | 157630 | 58.15% | 0 | 0.00 | 1900.47 | 0.000 | 73.53% | 95.59% | `{"filegroups/scripts": 0.9994414448738098, "filetypes/shell": 0.9974471926689148, "general": 0.9960634708404541}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44522 | 52.17% | 0 | 0.00 | 6728.43 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.12992624938488007}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32363 | 83308 | 52.02% | 0 | 0.00 | 3595.91 | 0.000 | 68.44% | 86.58% | `{"filegroups/source": 0.9971853494644165, "filetypes/kotlin": 0.9353815317153931, "general": 0.9806024432182312}` |
| filetypes/macho | joint_or_at_fp_0 | 2825 | 31153 | 51.93% | 0 | 0.00 | 9615.73 | 0.000 | 68.36% | 96.00% | `{"filegroups/native": 0.9857239127159119, "filetypes/macho": 0.9956993460655212, "general": 0.9968633651733398}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3512 | 1014811 | 51.65% | 0 | 0.00 | 295.20 | 0.000 | 68.12% | 99.83% | `{"filetypes/python_bytecode": 0.9999443888664246, "general": 0.9865643978118896}` |
| filetypes/dmg | joint_or_at_fp_0 | 62 | 241 | 51.61% | 0 | 0.00 | 1235348.58 | 0.000 | 68.09% | 90.10% | `{"filetypes/dmg": 0.8412267565727234, "general": 0.9566053152084351}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27666 | 50.94% | 0 | 0.00 | 10827.62 | 0.000 | 67.50% | 99.81% | `{"filegroups/scripts": 0.996650755405426, "filetypes/lua": 0.863678514957428}` |
| filetypes/zst | calibrate_inherited | 10473 | 325483 | 47.45% | 0 | 0.00 | 920.39 | 0.000 | 64.36% | 98.36% | `{"general": 0.9992232846470547}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 75 | 272 | 45.33% | 0 | 0.00 | 1095329.26 | 0.000 | 62.39% | 88.18% | `{"filetypes/python_sdist": 0.9296724796295166, "general": 0.9576486945152283}` |
| filetypes/python | joint_or_at_fp_0 | 23148 | 637265 | 45.01% | 0 | 0.00 | 470.09 | 0.000 | 62.07% | 98.07% | `{"filegroups/scripts": 0.9990367889404297, "filetypes/python": 0.9969910979270935, "general": 0.9931808710098267}` |
| filetypes/perl | joint_or_at_fp_0 | 397 | 76141 | 44.08% | 0 | 0.00 | 3934.38 | 0.000 | 61.19% | 99.71% | `{"filegroups/scripts": 0.9981914758682251, "filetypes/perl": 0.999664843082428, "general": 0.9806804656982422}` |
| filetypes/javascript | joint_or_at_fp_0 | 141304 | 1611995 | 44.01% | 0 | 0.00 | 185.84 | 0.000 | 61.12% | 95.49% | `{"filegroups/scripts": 0.9987635612487793, "filetypes/javascript": 0.9986634254455566, "general": 0.9988200068473816}` |
| filetypes/powershell | joint_or_at_fp_0 | 6063 | 5268 | 42.29% | 0 | 0.00 | 56850.43 | 0.000 | 59.44% | 69.12% | `{"filegroups/scripts": 0.9987106919288635, "filetypes/powershell": 0.9985373616218567, "general": 0.9957389831542969}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9264 | 40.91% | 0 | 0.00 | 32332.12 | 0.000 | 58.06% | 99.31% | `{"filetypes/clojure": 0.9970583319664001, "general": 0.02364300936460495}` |
| filetypes/pdf | joint_or_at_fp_0 | 178640 | 29364 | 39.05% | 0 | 0.00 | 10201.54 | 0.000 | 56.17% | 47.65% | `{"filegroups/documents": 0.9981157183647156, "filetypes/pdf": 0.9986247420310974, "general": 0.9961258172988892}` |
| filetypes/php | joint_or_at_fp_0 | 6652 | 611948 | 38.73% | 0 | 0.00 | 489.54 | 0.000 | 55.83% | 99.34% | `{"filegroups/scripts": 0.9988862872123718, "filetypes/php": 0.9965444803237915, "general": 0.9782417416572571}` |
| filetypes/lnk | joint_or_at_fp_0 | 4687 | 1119 | 37.08% | 0 | 0.00 | 267357.09 | 0.000 | 54.10% | 49.21% | `{"filetypes/lnk": 0.996296226978302, "general": 0.9986103177070618}` |
| filetypes/pe | joint_or_at_fp_0 | 1377225 | 228402 | 35.67% | 0 | 0.00 | 1311.60 | 0.000 | 52.58% | 44.82% | `{"filegroups/native": 0.9997637271881104, "filetypes/pe": 0.9996781349182129, "general": 0.9996814727783203}` |
| filetypes/ruby | joint_or_at_fp_0 | 397 | 179076 | 33.50% | 0 | 0.00 | 1672.87 | 0.000 | 50.19% | 99.85% | `{"filetypes/ruby": 0.9766124486923218, "general": 0.922759473323822}` |
