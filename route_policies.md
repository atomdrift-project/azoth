# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1938482389`
- Rows: 12461279 (2635645 malware, 9825634 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 254 | 15941 | 100.00% | 0 | 0.00 | 18790.86 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 825 | 97.90% | 0 | 0.00 | 362460.58 | 0.000 | 98.94% | 98.15% | `{"filegroups/documents": 0.10112279653549194, "filetypes/rtf": 0.5517976880073547}` |
| filetypes/gem | joint_or_at_fp_0 | 858 | 2116 | 96.74% | 0 | 0.00 | 141475.08 | 0.000 | 98.34% | 99.06% | `{"filetypes/gem": 0.15371638536453247}` |
| filetypes/pkg_info | learned_blend_at_fp_0 | 10618 | 10032 | 96.17% | 0 | 0.00 | 29857.31 | 0.000 | 98.05% | 98.03% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 439 | 93.10% | 0 | 0.00 | 680076.10 | 0.000 | 96.43% | 99.20% | `{"filetypes/applescript": 0.7831297516822815}` |
| filetypes/elf | joint_or_at_fp_0 | 190293 | 380037 | 89.61% | 0 | 0.00 | 788.27 | 0.000 | 94.52% | 96.53% | `{"filegroups/native": 0.9797928333282471, "filetypes/elf": 0.9999781847000122, "general": 0.9999980330467224}` |
| filetypes/tar | filetype_only_at_fp_0 | 31035 | 54382 | 84.44% | 0 | 0.00 | 5508.53 | 0.000 | 91.56% | 94.35% | `{"filetypes/tar": 0.9840909838676453}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87475 | 30464 | 80.97% | 0 | 0.00 | 9833.20 | 0.000 | 89.48% | 85.88% | `{"filetypes/ole_doc": 0.9946728348731995}` |
| filetypes/package.json | joint_or_at_fp_0 | 20126 | 39513 | 74.10% | 0 | 0.00 | 7581.35 | 0.000 | 85.13% | 91.26% | `{"filegroups/config": 0.9998471736907959, "filetypes/package.json": 0.9974556565284729}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 27402 | 73.54% | 0 | 0.00 | 10931.93 | 0.000 | 84.75% | 77.06% | `{"filegroups/documents": 0.983866274356842, "filetypes/pdf": 0.9922099113464355}` |
| filetypes/scala | calibrate_inherited | 3 | 40241 | 66.67% | 0 | 0.00 | 7444.20 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9796748955236774, "general": 0.9991336292264918}` |
| filetypes/jar | joint_or_at_fp_0 | 3785 | 11951 | 61.06% | 0 | 0.00 | 25063.65 | 0.000 | 75.82% | 90.63% | `{"filetypes/jar": 0.9626078009605408, "general": 0.9999957084655762}` |
| filetypes/lnk | joint_or_at_fp_0 | 4619 | 1070 | 61.05% | 0 | 0.00 | 279583.41 | 0.000 | 75.82% | 68.38% | `{"filetypes/lnk": 0.9045023322105408, "general": 0.9987412691116333}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 64383 | 60.25% | 0 | 0.00 | 4652.88 | 0.000 | 75.20% | 99.75% | `{"filegroups/scripts": 0.9848921298980713, "filetypes/perl": 0.9918814301490784}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3492 | 574767 | 58.62% | 0 | 0.00 | 521.21 | 0.000 | 73.91% | 99.75% | `{"filetypes/python_bytecode": 0.9999322891235352}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32518 | 75632 | 55.70% | 0 | 0.00 | 3960.85 | 0.000 | 71.55% | 86.68% | `{"filegroups/source": 0.9543018341064453, "filetypes/kotlin": 0.823935866355896}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8276 | 51.82% | 0 | 0.00 | 36191.28 | 0.000 | 68.26% | 99.37% | `{"filetypes/clojure": 0.9972190856933594, "general": 0.9615685343742371}` |
| filetypes/python | joint_or_at_fp_0 | 22993 | 482785 | 49.90% | 0 | 0.00 | 620.51 | 0.000 | 66.58% | 97.72% | `{"filegroups/scripts": 0.9959927201271057, "filetypes/python": 0.9902048110961914}` |
| filetypes/macho | joint_or_at_fp_0 | 2771 | 20633 | 47.71% | 0 | 0.00 | 14518.08 | 0.000 | 64.60% | 93.81% | `{"filegroups/native": 0.9600578546524048, "filetypes/macho": 0.9995895028114319}` |
| filetypes/pe | joint_or_at_fp_0 | 1370970 | 186041 | 47.45% | 0 | 0.00 | 1610.24 | 0.000 | 64.36% | 53.73% | `{"filegroups/native": 0.9994394183158875, "filetypes/pe": 0.9981478452682495, "general": 0.9999971985816956}` |
| filetypes/registry | joint_or_at_fp_0 | 384 | 33324 | 45.05% | 0 | 0.00 | 8989.31 | 0.000 | 62.12% | 99.37% | `{"filetypes/registry": 0.8450819849967957}` |
| filetypes/npm | joint_or_at_fp_0 | 2556 | 3243 | 44.17% | 0 | 0.00 | 92332.69 | 0.000 | 61.28% | 75.39% | `{"filetypes/npm": 0.9883435964584351}` |
| filetypes/shell | joint_or_at_fp_0 | 17711 | 126320 | 42.19% | 0 | 0.00 | 2371.51 | 0.000 | 59.34% | 92.89% | `{"filegroups/scripts": 0.9939045310020447, "filetypes/shell": 0.9771266579627991}` |
| filetypes/whl | joint_or_at_fp_0 | 2684 | 4853 | 40.31% | 0 | 0.00 | 61710.44 | 0.000 | 57.46% | 78.74% | `{"filetypes/whl": 0.9963556528091431}` |
| filetypes/powershell | joint_or_at_fp_0 | 5946 | 4385 | 39.76% | 0 | 0.00 | 68294.39 | 0.000 | 56.90% | 65.33% | `{"filegroups/scripts": 0.9939286708831787, "filetypes/powershell": 0.9909754395484924, "general": 0.9999769330024719}` |
| filetypes/zip | joint_or_at_fp_0 | 103970 | 19890 | 39.50% | 0 | 0.00 | 15060.37 | 0.000 | 56.63% | 49.22% | `{"filetypes/zip": 0.9982097148895264}` |
| filetypes/rar | calibrate_inherited | 22046 | 13 | 39.41% | 0 | 0.00 | 20581666.52 | 0.000 | 56.54% | 39.44% | `{"general": 0.9991336292264918}` |
| filetypes/lua | learned_blend_at_fp_0 | 110 | 25407 | 39.09% | 0 | 0.00 | 11790.28 | 0.000 | 56.21% | 99.74% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 6041 | 536330 | 35.59% | 0 | 0.00 | 558.56 | 0.000 | 52.50% | 99.28% | `{"filegroups/scripts": 0.9961133003234863, "filetypes/php": 0.9973865151405334}` |
| filetypes/swift | joint_or_at_fp_0 | 63 | 37235 | 33.33% | 0 | 0.00 | 8045.15 | 0.000 | 50.00% | 99.89% | `{"filegroups/source": 0.7385311126708984}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 254 | 15941 | 100.00% | 0 | 0.00 | 18790.86 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 825 | 97.90% | 0 | 0.00 | 362460.58 | 0.000 | 98.94% | 98.15% | `{"filegroups/documents": 0.10112279653549194, "filetypes/rtf": 0.5517976880073547}` |
| filetypes/gem | joint_or_at_fp_0 | 858 | 2116 | 96.74% | 0 | 0.00 | 141475.08 | 0.000 | 98.34% | 99.06% | `{"filetypes/gem": 0.15371638536453247}` |
| filetypes/pkg_info | learned_blend_at_fp_0 | 10618 | 10032 | 96.17% | 0 | 0.00 | 29857.31 | 0.000 | 98.05% | 98.03% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 58 | 439 | 93.10% | 0 | 0.00 | 680076.10 | 0.000 | 96.43% | 99.20% | `{"filetypes/applescript": 0.7831297516822815}` |
| filetypes/elf | joint_or_at_fp_0 | 190293 | 380037 | 89.61% | 0 | 0.00 | 788.27 | 0.000 | 94.52% | 96.53% | `{"filegroups/native": 0.9797928333282471, "filetypes/elf": 0.9999781847000122, "general": 0.9999980330467224}` |
| filetypes/tar | filetype_only_at_fp_0 | 31035 | 54382 | 84.44% | 0 | 0.00 | 5508.53 | 0.000 | 91.56% | 94.35% | `{"filetypes/tar": 0.9840909838676453}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87475 | 30464 | 80.97% | 0 | 0.00 | 9833.20 | 0.000 | 89.48% | 85.88% | `{"filetypes/ole_doc": 0.9946728348731995}` |
| filetypes/package.json | joint_or_at_fp_0 | 20126 | 39513 | 74.10% | 0 | 0.00 | 7581.35 | 0.000 | 85.13% | 91.26% | `{"filegroups/config": 0.9998471736907959, "filetypes/package.json": 0.9974556565284729}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 27402 | 73.54% | 0 | 0.00 | 10931.93 | 0.000 | 84.75% | 77.06% | `{"filegroups/documents": 0.983866274356842, "filetypes/pdf": 0.9922099113464355}` |
| filetypes/scala | calibrate_inherited | 3 | 40241 | 66.67% | 0 | 0.00 | 7444.20 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9790796437237462, "general": 0.9989333860528404}` |
| filetypes/jar | joint_or_at_fp_0 | 3785 | 11951 | 61.06% | 0 | 0.00 | 25063.65 | 0.000 | 75.82% | 90.63% | `{"filetypes/jar": 0.9626078009605408, "general": 0.9999957084655762}` |
| filetypes/lnk | joint_or_at_fp_0 | 4619 | 1070 | 61.05% | 0 | 0.00 | 279583.41 | 0.000 | 75.82% | 68.38% | `{"filetypes/lnk": 0.9045023322105408, "general": 0.9987412691116333}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 64383 | 60.25% | 0 | 0.00 | 4652.88 | 0.000 | 75.20% | 99.75% | `{"filegroups/scripts": 0.9848921298980713, "filetypes/perl": 0.9918814301490784}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3492 | 574767 | 58.62% | 0 | 0.00 | 521.21 | 0.000 | 73.91% | 99.75% | `{"filetypes/python_bytecode": 0.9999322891235352}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32518 | 75632 | 55.70% | 0 | 0.00 | 3960.85 | 0.000 | 71.55% | 86.68% | `{"filegroups/source": 0.9543018341064453, "filetypes/kotlin": 0.823935866355896}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8276 | 51.82% | 0 | 0.00 | 36191.28 | 0.000 | 68.26% | 99.37% | `{"filetypes/clojure": 0.9972190856933594, "general": 0.9615685343742371}` |
| filetypes/python | joint_or_at_fp_0 | 22993 | 482785 | 49.90% | 0 | 0.00 | 620.51 | 0.000 | 66.58% | 97.72% | `{"filegroups/scripts": 0.9959927201271057, "filetypes/python": 0.9902048110961914}` |
| filetypes/macho | joint_or_at_fp_0 | 2771 | 20633 | 47.71% | 0 | 0.00 | 14518.08 | 0.000 | 64.60% | 93.81% | `{"filegroups/native": 0.9600578546524048, "filetypes/macho": 0.9995895028114319}` |
| filetypes/pe | joint_or_at_fp_0 | 1370970 | 186041 | 47.45% | 0 | 0.00 | 1610.24 | 0.000 | 64.36% | 53.73% | `{"filegroups/native": 0.9994394183158875, "filetypes/pe": 0.9981478452682495, "general": 0.9999971985816956}` |
| filetypes/registry | joint_or_at_fp_0 | 384 | 33324 | 45.05% | 0 | 0.00 | 8989.31 | 0.000 | 62.12% | 99.37% | `{"filetypes/registry": 0.8450819849967957}` |
| filetypes/npm | joint_or_at_fp_0 | 2556 | 3243 | 44.17% | 0 | 0.00 | 92332.69 | 0.000 | 61.28% | 75.39% | `{"filetypes/npm": 0.9883435964584351}` |
| filetypes/rar | calibrate_inherited | 22046 | 13 | 43.44% | 0 | 0.00 | 20581666.52 | 0.000 | 60.57% | 43.47% | `{"general": 0.9989333860528404}` |
| filetypes/shell | joint_or_at_fp_0 | 17711 | 126320 | 42.19% | 0 | 0.00 | 2371.51 | 0.000 | 59.34% | 92.89% | `{"filegroups/scripts": 0.9939045310020447, "filetypes/shell": 0.9771266579627991}` |
| filetypes/whl | joint_or_at_fp_0 | 2684 | 4853 | 40.31% | 0 | 0.00 | 61710.44 | 0.000 | 57.46% | 78.74% | `{"filetypes/whl": 0.9963556528091431}` |
| filetypes/powershell | joint_or_at_fp_0 | 5946 | 4385 | 39.76% | 0 | 0.00 | 68294.39 | 0.000 | 56.90% | 65.33% | `{"filegroups/scripts": 0.9939286708831787, "filetypes/powershell": 0.9909754395484924, "general": 0.9999769330024719}` |
| filetypes/zip | joint_or_at_fp_0 | 103970 | 19890 | 39.50% | 0 | 0.00 | 15060.37 | 0.000 | 56.63% | 49.22% | `{"filetypes/zip": 0.9982097148895264}` |
| filetypes/lua | learned_blend_at_fp_0 | 110 | 25407 | 39.09% | 0 | 0.00 | 11790.28 | 0.000 | 56.21% | 99.74% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 6041 | 536330 | 35.59% | 0 | 0.00 | 558.56 | 0.000 | 52.50% | 99.28% | `{"filegroups/scripts": 0.9961133003234863, "filetypes/php": 0.9973865151405334}` |
| filetypes/swift | joint_or_at_fp_0 | 63 | 37235 | 33.33% | 0 | 0.00 | 8045.15 | 0.000 | 50.00% | 99.89% | `{"filegroups/source": 0.7385311126708984}` |
