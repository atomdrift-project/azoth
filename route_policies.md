# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1634431848`
- Rows: 6488381 (2337508 malware, 4150873 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf† | max_rule | 4975 | 494 | 98.99% | 0 | 0.00 | 604588.50 | 0.000 | 99.49% | 99.09% | `{"filegroups/documents": 0.06965661026222993, "filetypes/rtf": 0.06965661026222993, "general": 0.06965661026222993}` |
| filetypes/doc | calibrate_inherited | 27966 | 69 | 98.98% | 0 | 0.00 | 4248741.05 | 0.000 | 99.49% | 98.98% | `{"filegroups/documents": 0.4212825298309326, "general": 0.9988263282117197}` |
| filetypes/batch | joint_or_at_fp_0 | 175702 | 4447 | 98.15% | 0 | 0.00 | 67342.56 | 0.000 | 99.07% | 98.20% | `{"filegroups/scripts": 0.9966678023338318, "filetypes/batch": 0.9945307374000549, "general": 0.9803351163864136}` |
| filetypes/tar | joint_or_at_fp_0 | 1343 | 502 | 95.90% | 0 | 0.00 | 594982.34 | 0.000 | 97.91% | 97.02% | `{"filetypes/tar": 0.43667858839035034}` |
| filetypes/xls | joint_or_at_fp_0 | 31543 | 20738 | 92.48% | 0 | 0.00 | 14444.57 | 0.000 | 96.09% | 95.46% | `{"filegroups/documents": 0.9324073791503906, "filetypes/xls": 0.9646434783935547}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2599 | 73348 | 91.57% | 0 | 0.00 | 4084.19 | 0.000 | 95.60% | 99.71% | `{"filetypes/python-bytecode": 0.9989367127418518, "general": 0.8539602160453796}` |
| filetypes/package.json | joint_or_at_fp_0 | 18301 | 16200 | 90.40% | 0 | 0.00 | 18490.46 | 0.000 | 94.96% | 94.91% | `{"filegroups/config": 0.9997290968894958, "filetypes/package.json": 0.9985221028327942, "general": 0.9948236346244812}` |
| filetypes/elf | joint_or_at_fp_0 | 159096 | 162960 | 89.12% | 0 | 0.00 | 1838.31 | 0.000 | 94.25% | 94.63% | `{"filegroups/native": 0.9989792704582214, "filetypes/elf": 0.999691367149353, "general": 0.9748407602310181}` |
| filetypes/clojure† | specialist_primary_with_escape | 121 | 2923 | 86.78% | 0 | 0.00 | 102435.77 | 0.000 | 92.92% | 99.47% | `{"filetypes/clojure": 0.8532039059670549, "general": 0.10475176584915337}` |
| filetypes/docx | joint_or_at_fp_0 | 4107 | 401 | 85.56% | 0 | 0.00 | 744281.81 | 0.000 | 92.22% | 86.85% | `{"filegroups/documents": 0.7308213710784912, "filetypes/docx": 0.44649940729141235}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10636 | 1396 | 85.43% | 0 | 0.00 | 214363.91 | 0.000 | 92.14% | 87.12% | `{"filetypes/pkg-info": 0.9707927107810974, "general": 0.983626663684845}` |
| filetypes/crx | joint_or_at_fp_0 | 377 | 79 | 79.31% | 0 | 0.00 | 3721067.61 | 0.000 | 88.46% | 82.89% | `{"filetypes/crx": 0.9172199964523315, "general": 0.9354330897331238}` |
| filetypes/html | joint_or_at_fp_0 | 220 | 25636 | 77.27% | 0 | 0.00 | 11684.96 | 0.000 | 87.18% | 99.81% | `{"filetypes/html": 0.9039939045906067}` |
| filetypes/lnk† | filetype_only | 3913 | 1055 | 72.68% | 0 | 0.00 | 283552.89 | 0.000 | 84.18% | 78.48% | `{"filetypes/lnk": 0.9410658580790215}` |
| filetypes/macho | joint_or_at_fp_0 | 2445 | 11300 | 66.87% | 0 | 0.00 | 26507.39 | 0.000 | 80.15% | 94.11% | `{"filegroups/native": 0.9972110390663147, "filetypes/macho": 0.9924077987670898, "general": 0.9419607520103455}` |
| filetypes/perl | joint_or_at_fp_0 | 309 | 33047 | 64.40% | 0 | 0.00 | 9064.65 | 0.000 | 78.35% | 99.67% | `{"filetypes/perl": 0.995048463344574}` |
| filetypes/jar | joint_or_at_fp_0 | 2981 | 3536 | 61.93% | 0 | 0.00 | 84685.06 | 0.000 | 76.49% | 82.58% | `{"filetypes/jar": 0.7626144289970398, "general": 0.9791368842124939}` |
| filetypes/vbs | joint_or_at_fp_0 | 9357 | 3301 | 61.33% | 0 | 0.00 | 90711.10 | 0.000 | 76.03% | 71.42% | `{"filetypes/vbs": 0.997384250164032, "general": 0.977258026599884}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 29783 | 15018 | 58.06% | 0 | 0.00 | 19945.62 | 0.000 | 73.46% | 72.12% | `{"filetypes/tar.gz": 0.9988204836845398, "general": 0.9966519474983215}` |
| filetypes/java_class | learned_blend_at_fp_3 | 1593 | 665596 | 56.18% | 0 | 0.00 | 450.08 | 0.000 | 71.95% | 99.90% | `{}` |
| filetypes/powershell | joint_or_at_fp_0 | 4739 | 2233 | 49.63% | 0 | 0.00 | 134067.34 | 0.000 | 66.34% | 65.76% | `{"filegroups/scripts": 0.9980271458625793, "filetypes/powershell": 0.9755569100379944, "general": 0.9836516976356506}` |
| filetypes/python | joint_or_at_fp_0 | 18625 | 161067 | 48.08% | 0 | 0.00 | 1859.91 | 0.000 | 64.94% | 94.62% | `{"filegroups/scripts": 0.9990915060043335, "filetypes/python": 0.9998544454574585, "general": 0.9914819002151489}` |
| filetypes/pptx | joint_or_at_fp_0 | 433 | 192 | 47.58% | 0 | 0.00 | 1548167.96 | 0.000 | 64.48% | 63.68% | `{"filegroups/documents": 0.5943199992179871, "filetypes/pptx": 0.08845603466033936}` |
| filetypes/javascript | joint_or_at_fp_0 | 98603 | 554036 | 46.94% | 0 | 0.00 | 540.71 | 0.000 | 63.89% | 91.98% | `{"filegroups/scripts": 0.9971467852592468, "filetypes/javascript": 0.9986768364906311, "general": 0.9988792538642883}` |
| filetypes/lua | joint_or_at_fp_0 | 88 | 18000 | 46.59% | 0 | 0.00 | 16641.57 | 0.000 | 63.57% | 99.74% | `{"filegroups/scripts": 0.980327308177948, "filetypes/lua": 0.9551162123680115}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32798 | 50324 | 46.16% | 0 | 0.00 | 5952.71 | 0.000 | 63.16% | 78.76% | `{"filegroups/source": 0.936838686466217, "filetypes/kotlin": 0.629711389541626, "general": 0.9800496101379395}` |
| filetypes/ole | joint_or_at_fp_0 | 5866 | 5812 | 43.83% | 0 | 0.00 | 51530.63 | 0.000 | 60.95% | 71.78% | `{"filegroups/documents": 0.9658700227737427, "filetypes/ole": 0.994615375995636, "general": 0.9872515201568604}` |
| filetypes/php | joint_or_at_fp_0 | 4221 | 117803 | 41.77% | 0 | 0.00 | 2542.97 | 0.000 | 58.92% | 97.99% | `{"filegroups/scripts": 0.9974150657653809, "filetypes/php": 0.9997287392616272, "general": 0.9898976683616638}` |
| filetypes/pe† | specialist_primary_with_escape | 1242847 | 159898 | 40.67% | 0 | 0.00 | 1873.51 | 0.000 | 57.82% | 47.43% | `{"filegroups/native": 0.999673764630868, "filetypes/pe": 0.9997772674535989, "general": 0.9993650758143114}` |
| filetypes/rar | calibrate_inherited | 17551 | 4 | 36.52% | 0 | 0.00 | 52712919.55 | 0.000 | 53.50% | 36.53% | `{"general": 0.9988263282117197}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf† | max_rule | 4975 | 494 | 98.99% | 0 | 0.00 | 604588.50 | 0.000 | 99.49% | 99.09% | `{"filegroups/documents": 0.06964219836121616, "filetypes/rtf": 0.06964219836121616, "general": 0.06964219836121616}` |
| filetypes/doc | calibrate_inherited | 27966 | 69 | 98.98% | 0 | 0.00 | 4248741.05 | 0.000 | 99.49% | 98.98% | `{"filegroups/documents": 0.4212825298309326, "general": 0.998809710281674}` |
| filetypes/batch | joint_or_at_fp_0 | 175702 | 4447 | 98.15% | 0 | 0.00 | 67342.56 | 0.000 | 99.07% | 98.20% | `{"filegroups/scripts": 0.9966678023338318, "filetypes/batch": 0.9945307374000549, "general": 0.9803351163864136}` |
| filetypes/tar | joint_or_at_fp_0 | 1343 | 502 | 95.90% | 0 | 0.00 | 594982.34 | 0.000 | 97.91% | 97.02% | `{"filetypes/tar": 0.43667858839035034}` |
| filetypes/xls | joint_or_at_fp_0 | 31543 | 20738 | 92.48% | 0 | 0.00 | 14444.57 | 0.000 | 96.09% | 95.46% | `{"filegroups/documents": 0.9324073791503906, "filetypes/xls": 0.9646434783935547}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2599 | 73348 | 91.57% | 0 | 0.00 | 4084.19 | 0.000 | 95.60% | 99.71% | `{"filetypes/python-bytecode": 0.9989367127418518, "general": 0.8539602160453796}` |
| filetypes/package.json | joint_or_at_fp_0 | 18301 | 16200 | 90.40% | 0 | 0.00 | 18490.46 | 0.000 | 94.96% | 94.91% | `{"filegroups/config": 0.9997290968894958, "filetypes/package.json": 0.9985221028327942, "general": 0.9948236346244812}` |
| filetypes/elf | joint_or_at_fp_0 | 159096 | 162960 | 89.12% | 0 | 0.00 | 1838.31 | 0.000 | 94.25% | 94.63% | `{"filegroups/native": 0.9989792704582214, "filetypes/elf": 0.999691367149353, "general": 0.9748407602310181}` |
| filetypes/clojure† | specialist_primary_with_escape | 121 | 2923 | 86.78% | 0 | 0.00 | 102435.77 | 0.000 | 92.92% | 99.47% | `{"filetypes/clojure": 0.852524952100254, "general": 0.06975183565600786}` |
| filetypes/docx | joint_or_at_fp_0 | 4107 | 401 | 85.56% | 0 | 0.00 | 744281.81 | 0.000 | 92.22% | 86.85% | `{"filegroups/documents": 0.7308213710784912, "filetypes/docx": 0.44649940729141235}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10636 | 1396 | 85.43% | 0 | 0.00 | 214363.91 | 0.000 | 92.14% | 87.12% | `{"filetypes/pkg-info": 0.9707927107810974, "general": 0.983626663684845}` |
| filetypes/crx | joint_or_at_fp_0 | 377 | 79 | 79.31% | 0 | 0.00 | 3721067.61 | 0.000 | 88.46% | 82.89% | `{"filetypes/crx": 0.9172199964523315, "general": 0.9354330897331238}` |
| filetypes/html | joint_or_at_fp_0 | 220 | 25636 | 77.27% | 0 | 0.00 | 11684.96 | 0.000 | 87.18% | 99.81% | `{"filetypes/html": 0.9039939045906067}` |
| filetypes/lnk† | filetype_only | 3913 | 1055 | 72.96% | 0 | 0.00 | 283552.89 | 0.000 | 84.37% | 78.70% | `{"filetypes/lnk": 0.9394227275257974}` |
| filetypes/macho | joint_or_at_fp_0 | 2445 | 11300 | 66.87% | 0 | 0.00 | 26507.39 | 0.000 | 80.15% | 94.11% | `{"filegroups/native": 0.9972110390663147, "filetypes/macho": 0.9924077987670898, "general": 0.9419607520103455}` |
| filetypes/perl | joint_or_at_fp_0 | 309 | 33047 | 64.40% | 0 | 0.00 | 9064.65 | 0.000 | 78.35% | 99.67% | `{"filetypes/perl": 0.995048463344574}` |
| filetypes/jar | joint_or_at_fp_0 | 2981 | 3536 | 61.93% | 0 | 0.00 | 84685.06 | 0.000 | 76.49% | 82.58% | `{"filetypes/jar": 0.7626144289970398, "general": 0.9791368842124939}` |
| filetypes/vbs | joint_or_at_fp_0 | 9357 | 3301 | 61.33% | 0 | 0.00 | 90711.10 | 0.000 | 76.03% | 71.42% | `{"filetypes/vbs": 0.997384250164032, "general": 0.977258026599884}` |
| filetypes/tar.gz | joint_or_at_fp_0 | 29783 | 15018 | 58.06% | 0 | 0.00 | 19945.62 | 0.000 | 73.46% | 72.12% | `{"filetypes/tar.gz": 0.9988204836845398, "general": 0.9966519474983215}` |
| filetypes/java_class | learned_blend_at_fp_3 | 1593 | 665596 | 56.18% | 0 | 0.00 | 450.08 | 0.000 | 71.95% | 99.90% | `{}` |
| filetypes/powershell | joint_or_at_fp_0 | 4739 | 2233 | 49.63% | 0 | 0.00 | 134067.34 | 0.000 | 66.34% | 65.76% | `{"filegroups/scripts": 0.9980271458625793, "filetypes/powershell": 0.9755569100379944, "general": 0.9836516976356506}` |
| filetypes/python | joint_or_at_fp_0 | 18625 | 161067 | 48.08% | 0 | 0.00 | 1859.91 | 0.000 | 64.94% | 94.62% | `{"filegroups/scripts": 0.9990915060043335, "filetypes/python": 0.9998544454574585, "general": 0.9914819002151489}` |
| filetypes/pe | learned_blend_at_fp_0 | 1242847 | 159898 | 48.04% | 0 | 0.00 | 1873.51 | 0.000 | 64.90% | 53.96% | `{}` |
| filetypes/pptx | joint_or_at_fp_0 | 433 | 192 | 47.58% | 0 | 0.00 | 1548167.96 | 0.000 | 64.48% | 63.68% | `{"filegroups/documents": 0.5943199992179871, "filetypes/pptx": 0.08845603466033936}` |
| filetypes/javascript | joint_or_at_fp_0 | 98603 | 554036 | 46.94% | 0 | 0.00 | 540.71 | 0.000 | 63.89% | 91.98% | `{"filegroups/scripts": 0.9971467852592468, "filetypes/javascript": 0.9986768364906311, "general": 0.9988792538642883}` |
| filetypes/lua | joint_or_at_fp_0 | 88 | 18000 | 46.59% | 0 | 0.00 | 16641.57 | 0.000 | 63.57% | 99.74% | `{"filegroups/scripts": 0.980327308177948, "filetypes/lua": 0.9551162123680115}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32798 | 50324 | 46.16% | 0 | 0.00 | 5952.71 | 0.000 | 63.16% | 78.76% | `{"filegroups/source": 0.936838686466217, "filetypes/kotlin": 0.629711389541626, "general": 0.9800496101379395}` |
| filetypes/ole | joint_or_at_fp_0 | 5866 | 5812 | 43.83% | 0 | 0.00 | 51530.63 | 0.000 | 60.95% | 71.78% | `{"filegroups/documents": 0.9658700227737427, "filetypes/ole": 0.994615375995636, "general": 0.9872515201568604}` |
| filetypes/php | joint_or_at_fp_0 | 4221 | 117803 | 41.77% | 0 | 0.00 | 2542.97 | 0.000 | 58.92% | 97.99% | `{"filegroups/scripts": 0.9974150657653809, "filetypes/php": 0.9997287392616272, "general": 0.9898976683616638}` |
| filetypes/bz2† | or_general_primary | 34 | 11326 | 38.24% | 0 | 0.00 | 26446.55 | 0.000 | 55.32% | 99.82% | `{"general": 0.31482233905786333}` |
