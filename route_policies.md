# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `6309383805`
- Rows: 2645885 (382558 malware, 2263327 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/swift | calibrate_inherited | 3 | 5562 | 100.00% | 0 | 0.00 | 53846.20 | 0.000 | 100.00% | 100.00% | `{"filegroups/source": 0.9945505429240177, "general": 0.999001722392357}` |
| filetypes/rtf | joint_or_at_fp_0 | 786 | 135 | 99.11% | 0 | 0.00 | 2194620.90 | 0.000 | 99.55% | 99.24% | `{"filetypes/rtf": 0.31953164935112}` |
| filetypes/cab | learned_blend_at_fp_0 | 107 | 13 | 99.07% | 0 | 0.00 | 20581666.52 | 0.000 | 99.53% | 99.17% | `{}` |
| filetypes/bmp | calibrate_inherited | 16 | 34 | 93.75% | 0 | 0.00 | 8433964.34 | 0.000 | 96.77% | 98.00% | `{"filegroups/media": 0.9546170105794783, "general": 0.999001722392357}` |
| filetypes/asar | calibrate_inherited | 35 | 51 | 91.43% | 0 | 0.00 | 5704795.24 | 0.000 | 95.52% | 96.51% | `{"filetypes/asar": 0.6106093857624622, "general": 0.9992479141105999}` |
| filetypes/mp3 | calibrate_inherited | 21 | 39 | 90.48% | 0 | 0.00 | 7393758.89 | 0.000 | 95.00% | 96.67% | `{"filegroups/media": 0.9546170105794783, "general": 0.999001722392357}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 11920 | 3952 | 88.91% | 0 | 0.00 | 75774.22 | 0.000 | 94.13% | 91.67% | `{"filegroups/documents": 0.9442936182022095, "filetypes/ole_doc": 0.977667510509491, "general": 0.9701006412506104}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 364 | 1351 | 86.26% | 0 | 0.00 | 221496.18 | 0.000 | 92.63% | 97.08% | `{"filegroups/archive": 0.6409810185432434, "filetypes/python_sdist": 0.8464486598968506, "general": 0.5086701512336731}` |
| filetypes/elf | joint_or_at_fp_0 | 24894 | 112996 | 83.98% | 0 | 0.00 | 2651.15 | 0.000 | 91.29% | 97.11% | `{"filegroups/native": 0.9948229193687439, "filetypes/elf": 0.819688618183136, "general": 0.9909234642982483}` |
| filetypes/lua | calibrate_inherited | 6 | 3620 | 83.33% | 0 | 0.00 | 82720.80 | 0.000 | 90.91% | 99.97% | `{"filegroups/scripts": 0.9984193809837814, "filetypes/lua": 0.886187556734192, "general": 0.9992479141105999}` |
| filetypes/7z | joint_or_at_fp_0 | 1075 | 46 | 82.33% | 0 | 0.00 | 6304930.17 | 0.000 | 90.31% | 83.05% | `{"filegroups/archive": 0.9924879670143127, "general": 0.8940103054046631}` |
| filetypes/groovy | calibrate_inherited | 10 | 1332 | 80.00% | 0 | 0.00 | 224652.10 | 0.000 | 88.89% | 99.85% | `{"filetypes/groovy": 0.8981806855050581, "general": 0.9992479141105999}` |
| filetypes/registry | joint_or_at_fp_0 | 56 | 13839 | 75.00% | 0 | 0.00 | 21644.69 | 0.000 | 85.71% | 99.90% | `{"filetypes/registry": 0.9943466782569885}` |
| filetypes/pdf | joint_or_at_fp_0 | 22297 | 3705 | 74.59% | 0 | 0.00 | 80823.79 | 0.000 | 85.45% | 78.21% | `{"filegroups/documents": 0.9308114051818848, "filetypes/pdf": 0.6961154341697693}` |
| filetypes/rar | calibrate_inherited | 2816 | 7 | 73.72% | 0 | 0.00 | 34816365.51 | 0.000 | 84.87% | 73.79% | `{"filegroups/archive": 0.9988536446966875, "general": 0.999001722392357}` |
| filetypes/ruby | calibrate_inherited | 37 | 25009 | 72.97% | 0 | 0.00 | 11977.90 | 0.000 | 84.37% | 99.96% | `{"filegroups/scripts": 0.9984193809837814, "filetypes/ruby": 0.9601736387940446, "general": 0.9992479141105999}` |
| filetypes/perl | joint_or_at_fp_0 | 53 | 10229 | 71.70% | 0 | 0.00 | 29282.37 | 0.000 | 83.52% | 99.85% | `{"filegroups/scripts": 0.9795204401016235, "filetypes/perl": 0.9948238134384155, "general": 0.9339204430580139}` |
| filetypes/lnk | joint_or_at_fp_0 | 628 | 148 | 70.54% | 0 | 0.00 | 2003795.17 | 0.000 | 82.73% | 76.16% | `{"filetypes/lnk": 0.4320516586303711, "general": 0.9829287528991699}` |
| filetypes/ico | calibrate_inherited | 30 | 103 | 70.00% | 0 | 0.00 | 2866588.81 | 0.000 | 82.35% | 93.23% | `{"filetypes/ico": 0.01684813184624256, "general": 0.9992479141105999}` |
| filetypes/package.json | joint_or_at_fp_0 | 2762 | 9657 | 69.88% | 0 | 0.00 | 31016.54 | 0.000 | 82.27% | 93.30% | `{"filegroups/config": 0.991320788860321, "filetypes/package.json": 0.9660317897796631, "general": 0.9958635568618774}` |
| filetypes/php | joint_or_at_fp_0 | 802 | 79215 | 68.95% | 0 | 0.00 | 3781.70 | 0.000 | 81.62% | 99.69% | `{"filegroups/scripts": 0.952701985836029, "filetypes/php": 0.9951038956642151, "general": 0.8427647948265076}` |
| filetypes/dex | calibrate_inherited | 16 | 32 | 68.75% | 0 | 0.00 | 8936819.90 | 0.000 | 81.48% | 89.58% | `{"filegroups/portable": 0.9999998999999999, "general": 0.999001722392357}` |
| filetypes/html | joint_or_at_fp_0 | 11563 | 53897 | 67.90% | 0 | 0.00 | 5558.10 | 0.000 | 80.88% | 94.33% | `{"filegroups/documents": 0.9962656497955322, "filetypes/html": 0.9877099990844727, "general": 0.9757505655288696}` |
| filetypes/nupkg | calibrate_inherited | 9 | 1407 | 66.67% | 0 | 0.00 | 212689.79 | 0.000 | 80.00% | 99.79% | `{"filegroups/archive": 0.9990741143390331, "filetypes/nupkg": 0.31742321655130784, "general": 0.9992479141105999}` |
| filetypes/jar | learned_blend_at_fp_0 | 493 | 5119 | 65.52% | 0 | 0.00 | 58504.71 | 0.000 | 79.17% | 96.97% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 370 | 4706 | 62.70% | 0 | 0.00 | 63637.46 | 0.000 | 77.08% | 97.28% | `{"filegroups/native": 0.8575772643089294, "filetypes/macho": 0.9679098129272461, "general": 0.989465057849884}` |
| filetypes/tar | joint_or_at_fp_0 | 1935 | 13294 | 61.40% | 0 | 0.00 | 22531.93 | 0.000 | 76.08% | 95.09% | `{"filegroups/archive": 0.9747467041015625, "filetypes/tar": 0.973667562007904, "general": 0.98807293176651}` |
| filetypes/pkg_info | calibrate_inherited | 33 | 2288 | 60.61% | 0 | 0.00 | 130846.68 | 0.000 | 75.47% | 99.44% | `{"filetypes/pkg_info": 0.9973031818501382, "general": 0.9992479141105999}` |
| filetypes/xpi | calibrate_inherited | 12 | 631 | 58.33% | 0 | 0.00 | 473634.27 | 0.000 | 73.68% | 99.22% | `{"filegroups/archive": 0.9990741143390331, "filetypes/xpi": 0.7403514843013144, "general": 0.9992479141105999}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 448 | 154515 | 57.59% | 0 | 0.00 | 1938.78 | 0.000 | 73.09% | 99.88% | `{"filetypes/python_bytecode": 0.9907791614532471, "general": 0.931919276714325}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/swift | calibrate_inherited | 3 | 5562 | 100.00% | 0 | 0.00 | 53846.20 | 0.000 | 100.00% | 100.00% | `{"filegroups/source": 0.9941732139630163, "general": 0.9977660167409671}` |
| filetypes/rtf | joint_or_at_fp_0 | 786 | 135 | 99.11% | 0 | 0.00 | 2194620.90 | 0.000 | 99.55% | 99.24% | `{"filetypes/rtf": 0.31953164935112}` |
| filetypes/cab | learned_blend_at_fp_0 | 107 | 13 | 99.07% | 0 | 0.00 | 20581666.52 | 0.000 | 99.53% | 99.17% | `{}` |
| filetypes/bmp | calibrate_inherited | 16 | 34 | 93.75% | 0 | 0.00 | 8433964.34 | 0.000 | 96.77% | 98.00% | `{"filegroups/media": 0.9545595369897354, "general": 0.9977660167409671}` |
| filetypes/asar | calibrate_inherited | 35 | 51 | 91.43% | 0 | 0.00 | 5704795.24 | 0.000 | 95.52% | 96.51% | `{"filetypes/asar": 0.6106093857624622, "general": 0.9992479141105999}` |
| filetypes/mp3 | calibrate_inherited | 21 | 39 | 90.48% | 0 | 0.00 | 7393758.89 | 0.000 | 95.00% | 96.67% | `{"filegroups/media": 0.9545595369897354, "general": 0.9977660167409671}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 11920 | 3952 | 88.91% | 0 | 0.00 | 75774.22 | 0.000 | 94.13% | 91.67% | `{"filegroups/documents": 0.9442936182022095, "filetypes/ole_doc": 0.977667510509491, "general": 0.9701006412506104}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 364 | 1351 | 86.26% | 0 | 0.00 | 221496.18 | 0.000 | 92.63% | 97.08% | `{"filegroups/archive": 0.6409810185432434, "filetypes/python_sdist": 0.8464486598968506, "general": 0.5086701512336731}` |
| filetypes/elf | joint_or_at_fp_0 | 24894 | 112996 | 83.98% | 0 | 0.00 | 2651.15 | 0.000 | 91.29% | 97.11% | `{"filegroups/native": 0.9948229193687439, "filetypes/elf": 0.819688618183136, "general": 0.9909234642982483}` |
| filetypes/lua | calibrate_inherited | 6 | 3620 | 83.33% | 0 | 0.00 | 82720.80 | 0.000 | 90.91% | 99.97% | `{"filegroups/scripts": 0.9984193809837814, "filetypes/lua": 0.886187556734192, "general": 0.9992479141105999}` |
| filetypes/7z | joint_or_at_fp_0 | 1075 | 46 | 82.33% | 0 | 0.00 | 6304930.17 | 0.000 | 90.31% | 83.05% | `{"filegroups/archive": 0.9924879670143127, "general": 0.8940103054046631}` |
| filetypes/groovy | calibrate_inherited | 10 | 1332 | 80.00% | 0 | 0.00 | 224652.10 | 0.000 | 88.89% | 99.85% | `{"filetypes/groovy": 0.8981806855050581, "general": 0.9992479141105999}` |
| filetypes/rar | calibrate_inherited | 2816 | 7 | 79.62% | 0 | 0.00 | 34816365.51 | 0.000 | 88.65% | 79.67% | `{"filegroups/archive": 0.9985975732544553, "general": 0.9977660167409671}` |
| filetypes/registry | joint_or_at_fp_0 | 56 | 13839 | 75.00% | 0 | 0.00 | 21644.69 | 0.000 | 85.71% | 99.90% | `{"filetypes/registry": 0.9943466782569885}` |
| filetypes/pdf | joint_or_at_fp_0 | 22297 | 3705 | 74.59% | 0 | 0.00 | 80823.79 | 0.000 | 85.45% | 78.21% | `{"filegroups/documents": 0.9308114051818848, "filetypes/pdf": 0.6961154341697693}` |
| filetypes/ruby | calibrate_inherited | 37 | 25009 | 72.97% | 0 | 0.00 | 11977.90 | 0.000 | 84.37% | 99.96% | `{"filegroups/scripts": 0.9984193809837814, "filetypes/ruby": 0.9601736387940446, "general": 0.9992479141105999}` |
| filetypes/perl | joint_or_at_fp_0 | 53 | 10229 | 71.70% | 0 | 0.00 | 29282.37 | 0.000 | 83.52% | 99.85% | `{"filegroups/scripts": 0.9795204401016235, "filetypes/perl": 0.9948238134384155, "general": 0.9339204430580139}` |
| filetypes/lnk | joint_or_at_fp_0 | 628 | 148 | 70.54% | 0 | 0.00 | 2003795.17 | 0.000 | 82.73% | 76.16% | `{"filetypes/lnk": 0.4320516586303711, "general": 0.9829287528991699}` |
| filetypes/ico | calibrate_inherited | 30 | 103 | 70.00% | 0 | 0.00 | 2866588.81 | 0.000 | 82.35% | 93.23% | `{"filetypes/ico": 0.01684813184624256, "general": 0.9992479141105999}` |
| filetypes/package.json | joint_or_at_fp_0 | 2762 | 9657 | 69.88% | 0 | 0.00 | 31016.54 | 0.000 | 82.27% | 93.30% | `{"filegroups/config": 0.991320788860321, "filetypes/package.json": 0.9660317897796631, "general": 0.9958635568618774}` |
| filetypes/php | joint_or_at_fp_0 | 802 | 79215 | 68.95% | 0 | 0.00 | 3781.70 | 0.000 | 81.62% | 99.69% | `{"filegroups/scripts": 0.952701985836029, "filetypes/php": 0.9951038956642151, "general": 0.8427647948265076}` |
| filetypes/dex | calibrate_inherited | 16 | 32 | 68.75% | 0 | 0.00 | 8936819.90 | 0.000 | 81.48% | 89.58% | `{"filegroups/portable": 0.9999998999999999, "general": 0.9977660167409671}` |
| filetypes/html | joint_or_at_fp_0 | 11563 | 53897 | 67.90% | 0 | 0.00 | 5558.10 | 0.000 | 80.88% | 94.33% | `{"filegroups/documents": 0.9962656497955322, "filetypes/html": 0.9877099990844727, "general": 0.9757505655288696}` |
| filetypes/nupkg | calibrate_inherited | 9 | 1407 | 66.67% | 0 | 0.00 | 212689.79 | 0.000 | 80.00% | 99.79% | `{"filegroups/archive": 0.9990741143390331, "filetypes/nupkg": 0.31742321655130784, "general": 0.9992479141105999}` |
| filetypes/jar | learned_blend_at_fp_0 | 493 | 5119 | 65.52% | 0 | 0.00 | 58504.71 | 0.000 | 79.17% | 96.97% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 370 | 4706 | 62.70% | 0 | 0.00 | 63637.46 | 0.000 | 77.08% | 97.28% | `{"filegroups/native": 0.8575772643089294, "filetypes/macho": 0.9679098129272461, "general": 0.989465057849884}` |
| filetypes/tar | joint_or_at_fp_0 | 1935 | 13294 | 61.40% | 0 | 0.00 | 22531.93 | 0.000 | 76.08% | 95.09% | `{"filegroups/archive": 0.9747467041015625, "filetypes/tar": 0.973667562007904, "general": 0.98807293176651}` |
| filetypes/pkg_info | calibrate_inherited | 33 | 2288 | 60.61% | 0 | 0.00 | 130846.68 | 0.000 | 75.47% | 99.44% | `{"filetypes/pkg_info": 0.9973031818501382, "general": 0.9992479141105999}` |
| filetypes/xpi | calibrate_inherited | 12 | 631 | 58.33% | 0 | 0.00 | 473634.27 | 0.000 | 73.68% | 99.22% | `{"filegroups/archive": 0.9990741143390331, "filetypes/xpi": 0.7403514843013144, "general": 0.9992479141105999}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 448 | 154515 | 57.59% | 0 | 0.00 | 1938.78 | 0.000 | 73.09% | 99.88% | `{"filetypes/python_bytecode": 0.9907791614532471, "general": 0.931919276714325}` |
