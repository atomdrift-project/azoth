# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2037843653`
- Rows: 12910342 (2642872 malware, 10267470 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 826 | 97.90% | 0 | 0.00 | 362022.56 | 0.000 | 98.94% | 98.15% | `{"filetypes/rtf": 0.06724709272384644}` |
| filetypes/html | learned_blend_at_fp_0 | 254 | 15944 | 96.85% | 0 | 0.00 | 18787.32 | 0.000 | 98.40% | 99.95% | `{}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10619 | 10663 | 95.49% | 0 | 0.00 | 28090.70 | 0.000 | 97.69% | 97.75% | `{"filetypes/pkg_info": 0.9864152073860168, "general": 0.997292697429657}` |
| filetypes/gem | joint_or_at_fp_0 | 863 | 2251 | 95.02% | 0 | 0.00 | 132995.99 | 0.000 | 97.45% | 98.62% | `{"filetypes/gem": 0.38464033603668213}` |
| filetypes/elf | joint_or_at_fp_0 | 190908 | 390774 | 89.75% | 0 | 0.00 | 766.61 | 0.000 | 94.60% | 96.64% | `{"filegroups/native": 0.9869804978370667, "filetypes/elf": 0.9997420907020569, "general": 0.9999980330467224}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87490 | 30609 | 84.95% | 0 | 0.00 | 9786.62 | 0.000 | 91.86% | 88.85% | `{"filetypes/ole_doc": 0.991094172000885}` |
| filetypes/package.json | joint_or_at_fp_0 | 20189 | 43427 | 83.46% | 0 | 0.00 | 6898.08 | 0.000 | 90.98% | 94.75% | `{"filegroups/config": 0.9994163513183594}` |
| filetypes/tar | filetype_only_at_fp_0 | 32128 | 57199 | 82.37% | 0 | 0.00 | 5237.25 | 0.000 | 90.34% | 93.66% | `{"filetypes/tar": 0.9740726947784424}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 64816 | 67.25% | 0 | 0.00 | 4621.80 | 0.000 | 80.42% | 99.80% | `{"filetypes/perl": 0.978473961353302}` |
| filetypes/scala | calibrate_inherited | 3 | 40414 | 66.67% | 0 | 0.00 | 7412.34 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9818880732342707, "general": 0.9991210862018159}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25530 | 66.04% | 0 | 0.00 | 11733.48 | 0.000 | 79.55% | 99.86% | `{"filetypes/lua": 0.9192374348640442}` |
| filetypes/pdf | joint_or_at_fp_0 | 178645 | 27488 | 64.74% | 0 | 0.00 | 10897.73 | 0.000 | 78.60% | 69.44% | `{"filegroups/documents": 0.9951966404914856, "filetypes/pdf": 0.3511354327201843}` |
| filetypes/lnk | joint_or_at_fp_0 | 4623 | 1070 | 61.22% | 0 | 0.00 | 279583.41 | 0.000 | 75.94% | 68.51% | `{"filetypes/lnk": 0.9220167398452759, "general": 0.9987412691116333}` |
| filetypes/pe | joint_or_at_fp_0 | 1371496 | 189120 | 58.55% | 0 | 0.00 | 1584.03 | 0.000 | 73.86% | 63.58% | `{"filegroups/native": 0.9998159408569336, "filetypes/pe": 0.9974667429924011, "general": 0.9999971985816956}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3497 | 657343 | 58.05% | 0 | 0.00 | 455.73 | 0.000 | 73.46% | 99.78% | `{"filetypes/python_bytecode": 0.9999929666519165}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32386 | 72124 | 57.95% | 0 | 0.00 | 4153.50 | 0.000 | 73.38% | 86.97% | `{"filegroups/source": 0.9746145606040955, "filetypes/kotlin": 0.5068297386169434}` |
| filetypes/macho | joint_or_at_fp_0 | 2792 | 21347 | 54.19% | 0 | 0.00 | 14032.52 | 0.000 | 70.29% | 94.70% | `{"filegroups/native": 0.911315381526947, "filetypes/macho": 0.987328052520752}` |
| filetypes/java_class | joint_or_at_fp_0 | 2111 | 1509053 | 53.01% | 0 | 0.00 | 198.52 | 0.000 | 69.29% | 99.93% | `{"filegroups/portable": 0.9615174531936646, "filetypes/java_class": 0.9539626240730286, "general": 0.9999915361404419}` |
| filetypes/swift | calibrate_inherited | 63 | 37365 | 50.79% | 0 | 0.00 | 8017.16 | 0.000 | 67.37% | 99.92% | `{"filegroups/source": 0.9818880732342707, "general": 0.9991210862018159}` |
| filetypes/npm | joint_or_at_fp_0 | 3287 | 4311 | 50.65% | 0 | 0.00 | 69466.29 | 0.000 | 67.25% | 78.65% | `{"filetypes/npm": 0.9673994779586792}` |
| filetypes/python | learned_blend_at_fp_0 | 23025 | 495959 | 50.02% | 0 | 0.00 | 604.03 | 0.000 | 66.68% | 97.78% | `{}` |
| filetypes/crate | joint_or_at_fp_0 | 62 | 5097 | 50.00% | 0 | 0.00 | 58757.15 | 0.000 | 66.67% | 99.40% | `{"filetypes/crate": 0.9264771938323975}` |
| filetypes/shell | joint_or_at_fp_0 | 17794 | 128263 | 49.17% | 0 | 0.00 | 2335.59 | 0.000 | 65.93% | 93.81% | `{"filegroups/scripts": 0.9838855266571045, "filetypes/shell": 0.9636064767837524}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8183 | 49.09% | 0 | 0.00 | 36602.52 | 0.000 | 65.85% | 99.32% | `{"filetypes/clojure": 0.998830258846283, "general": 0.26186588406562805}` |
| filetypes/whl | joint_or_at_fp_0 | 2874 | 5100 | 48.09% | 0 | 0.00 | 58722.60 | 0.000 | 64.94% | 81.29% | `{"filetypes/whl": 0.9942296743392944}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 106 | 906 | 45.28% | 0 | 0.00 | 330108.72 | 0.000 | 62.34% | 94.27% | `{"filetypes/chrome_manifest": 0.992759108543396}` |
| filetypes/jar | joint_or_at_fp_0 | 3805 | 13123 | 43.71% | 0 | 0.00 | 22825.50 | 0.000 | 60.83% | 87.35% | `{"filetypes/jar": 0.9737594127655029}` |
| filetypes/vbs | joint_or_at_fp_0 | 12167 | 3539 | 41.07% | 0 | 0.00 | 84613.30 | 0.000 | 58.23% | 54.35% | `{"filetypes/vbs": 0.9904431700706482}` |
| filetypes/php | joint_or_at_fp_0 | 6047 | 539315 | 40.71% | 0 | 0.00 | 555.47 | 0.000 | 57.87% | 99.34% | `{"filegroups/scripts": 0.9849788546562195, "filetypes/php": 0.98636394739151}` |
| filetypes/rar | calibrate_inherited | 22054 | 13 | 39.59% | 0 | 0.00 | 20581666.52 | 0.000 | 56.73% | 39.63% | `{"general": 0.9991210862018159}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 826 | 97.90% | 0 | 0.00 | 362022.56 | 0.000 | 98.94% | 98.15% | `{"filetypes/rtf": 0.06724709272384644}` |
| filetypes/html | learned_blend_at_fp_0 | 254 | 15944 | 96.85% | 0 | 0.00 | 18787.32 | 0.000 | 98.40% | 99.95% | `{}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10619 | 10663 | 95.49% | 0 | 0.00 | 28090.70 | 0.000 | 97.69% | 97.75% | `{"filetypes/pkg_info": 0.9864152073860168, "general": 0.997292697429657}` |
| filetypes/gem | joint_or_at_fp_0 | 863 | 2251 | 95.02% | 0 | 0.00 | 132995.99 | 0.000 | 97.45% | 98.62% | `{"filetypes/gem": 0.38464033603668213}` |
| filetypes/elf | joint_or_at_fp_0 | 190908 | 390774 | 89.75% | 0 | 0.00 | 766.61 | 0.000 | 94.60% | 96.64% | `{"filegroups/native": 0.9869804978370667, "filetypes/elf": 0.9997420907020569, "general": 0.9999980330467224}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87490 | 30609 | 84.95% | 0 | 0.00 | 9786.62 | 0.000 | 91.86% | 88.85% | `{"filetypes/ole_doc": 0.991094172000885}` |
| filetypes/package.json | joint_or_at_fp_0 | 20189 | 43427 | 83.46% | 0 | 0.00 | 6898.08 | 0.000 | 90.98% | 94.75% | `{"filegroups/config": 0.9994163513183594}` |
| filetypes/tar | filetype_only_at_fp_0 | 32128 | 57199 | 82.37% | 0 | 0.00 | 5237.25 | 0.000 | 90.34% | 93.66% | `{"filetypes/tar": 0.9740726947784424}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 64816 | 67.25% | 0 | 0.00 | 4621.80 | 0.000 | 80.42% | 99.80% | `{"filetypes/perl": 0.978473961353302}` |
| filetypes/scala | calibrate_inherited | 3 | 40414 | 66.67% | 0 | 0.00 | 7412.34 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9818346849054098, "general": 0.9989275459837801}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 25530 | 66.04% | 0 | 0.00 | 11733.48 | 0.000 | 79.55% | 99.86% | `{"filetypes/lua": 0.9192374348640442}` |
| filetypes/pdf | joint_or_at_fp_0 | 178645 | 27488 | 64.74% | 0 | 0.00 | 10897.73 | 0.000 | 78.60% | 69.44% | `{"filegroups/documents": 0.9951966404914856, "filetypes/pdf": 0.3511354327201843}` |
| filetypes/lnk | joint_or_at_fp_0 | 4623 | 1070 | 61.22% | 0 | 0.00 | 279583.41 | 0.000 | 75.94% | 68.51% | `{"filetypes/lnk": 0.9220167398452759, "general": 0.9987412691116333}` |
| filetypes/pe | joint_or_at_fp_0 | 1371496 | 189120 | 58.55% | 0 | 0.00 | 1584.03 | 0.000 | 73.86% | 63.58% | `{"filegroups/native": 0.9998159408569336, "filetypes/pe": 0.9974667429924011, "general": 0.9999971985816956}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3497 | 657343 | 58.05% | 0 | 0.00 | 455.73 | 0.000 | 73.46% | 99.78% | `{"filetypes/python_bytecode": 0.9999929666519165}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32386 | 72124 | 57.95% | 0 | 0.00 | 4153.50 | 0.000 | 73.38% | 86.97% | `{"filegroups/source": 0.9746145606040955, "filetypes/kotlin": 0.5068297386169434}` |
| filetypes/macho | joint_or_at_fp_0 | 2792 | 21347 | 54.19% | 0 | 0.00 | 14032.52 | 0.000 | 70.29% | 94.70% | `{"filegroups/native": 0.911315381526947, "filetypes/macho": 0.987328052520752}` |
| filetypes/java_class | joint_or_at_fp_0 | 2111 | 1509053 | 53.01% | 0 | 0.00 | 198.52 | 0.000 | 69.29% | 99.93% | `{"filegroups/portable": 0.9615174531936646, "filetypes/java_class": 0.9539626240730286, "general": 0.9999915361404419}` |
| filetypes/swift | calibrate_inherited | 63 | 37365 | 50.79% | 0 | 0.00 | 8017.16 | 0.000 | 67.37% | 99.92% | `{"filegroups/source": 0.9818346849054098, "general": 0.9989275459837801}` |
| filetypes/npm | joint_or_at_fp_0 | 3287 | 4311 | 50.65% | 0 | 0.00 | 69466.29 | 0.000 | 67.25% | 78.65% | `{"filetypes/npm": 0.9673994779586792}` |
| filetypes/python | learned_blend_at_fp_0 | 23025 | 495959 | 50.02% | 0 | 0.00 | 604.03 | 0.000 | 66.68% | 97.78% | `{}` |
| filetypes/crate | joint_or_at_fp_0 | 62 | 5097 | 50.00% | 0 | 0.00 | 58757.15 | 0.000 | 66.67% | 99.40% | `{"filetypes/crate": 0.9264771938323975}` |
| filetypes/shell | joint_or_at_fp_0 | 17794 | 128263 | 49.17% | 0 | 0.00 | 2335.59 | 0.000 | 65.93% | 93.81% | `{"filegroups/scripts": 0.9838855266571045, "filetypes/shell": 0.9636064767837524}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8183 | 49.09% | 0 | 0.00 | 36602.52 | 0.000 | 65.85% | 99.32% | `{"filetypes/clojure": 0.998830258846283, "general": 0.26186588406562805}` |
| filetypes/whl | joint_or_at_fp_0 | 2874 | 5100 | 48.09% | 0 | 0.00 | 58722.60 | 0.000 | 64.94% | 81.29% | `{"filetypes/whl": 0.9942296743392944}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 106 | 906 | 45.28% | 0 | 0.00 | 330108.72 | 0.000 | 62.34% | 94.27% | `{"filetypes/chrome_manifest": 0.992759108543396}` |
| filetypes/jar | joint_or_at_fp_0 | 3805 | 13123 | 43.71% | 0 | 0.00 | 22825.50 | 0.000 | 60.83% | 87.35% | `{"filetypes/jar": 0.9737594127655029}` |
| filetypes/rar | calibrate_inherited | 22054 | 13 | 43.53% | 0 | 0.00 | 20581666.52 | 0.000 | 60.66% | 43.56% | `{"general": 0.9989275459837801}` |
| filetypes/vbs | joint_or_at_fp_0 | 12167 | 3539 | 41.07% | 0 | 0.00 | 84613.30 | 0.000 | 58.23% | 54.35% | `{"filetypes/vbs": 0.9904431700706482}` |
| filetypes/php | joint_or_at_fp_0 | 6047 | 539315 | 40.71% | 0 | 0.00 | 555.47 | 0.000 | 57.87% | 99.34% | `{"filegroups/scripts": 0.9849788546562195, "filetypes/php": 0.98636394739151}` |
