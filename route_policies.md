# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `3828940278`
- Rows: 17535482 (2678703 malware, 14856779 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 96.99% | 0 | 0.00 | 337928.55 | 0.000 | 98.47% | 97.37% | `{"filegroups/documents": 0.9848322868347168, "general": 0.8436551690101624}` |
| filetypes/asar | joint_or_at_fp_0 | 188 | 235 | 96.81% | 0 | 0.00 | 1266688.79 | 0.000 | 98.38% | 98.58% | `{"filetypes/asar": 0.8564065098762512, "general": 0.8970264196395874}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 530 | 94.55% | 0 | 0.00 | 563638.07 | 0.000 | 97.20% | 99.49% | `{"general": 0.8539895415306091}` |
| filetypes/gem | joint_or_at_fp_0 | 1008 | 4665 | 92.16% | 0 | 0.00 | 64196.58 | 0.000 | 95.92% | 98.61% | `{"filetypes/gem": 0.9423370957374573, "general": 0.9742353558540344}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 90.86% | 0 | 0.00 | 977399.40 | 0.000 | 95.21% | 91.16% | `{"filetypes/7z": 0.7546620965003967, "general": 0.9876203536987305}` |
| filetypes/elf | joint_or_at_fp_0 | 196620 | 808232 | 88.44% | 0 | 0.00 | 370.65 | 0.000 | 93.87% | 97.74% | `{"filegroups/native": 0.9941302537918091, "filetypes/elf": 0.9998213648796082, "general": 0.9892976880073547}` |
| filetypes/html | joint_or_at_fp_0 | 263 | 77662 | 87.83% | 0 | 0.00 | 3857.32 | 0.000 | 93.52% | 99.96% | `{"filegroups/documents": 0.9987590909004211, "filetypes/html": 0.999596118927002, "general": 0.9446626305580139}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 83 | 402 | 86.75% | 0 | 0.00 | 742437.25 | 0.000 | 92.90% | 97.73% | `{"filetypes/python_sdist": 0.8777077198028564}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16644 | 86.43% | 0 | 0.00 | 17997.25 | 0.000 | 92.72% | 94.71% | `{"filetypes/pkg_info": 0.9985552430152893, "general": 0.9901254177093506}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 53 | 84.84% | 0 | 0.00 | 5495548.85 | 0.000 | 91.80% | 87.54% | `{"filetypes/chm": 0.8653669953346252, "general": 0.1371891349554062}` |
| filetypes/tar | joint_or_at_fp_0 | 34261 | 75446 | 68.54% | 0 | 0.00 | 3970.62 | 0.000 | 81.34% | 90.18% | `{"filetypes/tar": 0.9991694092750549, "general": 0.9942576289176941}` |
| filetypes/shell | joint_or_at_fp_0 | 18635 | 160039 | 64.92% | 0 | 0.00 | 1871.86 | 0.000 | 78.73% | 96.34% | `{"filegroups/scripts": 0.9990348815917969, "filetypes/shell": 0.9966918230056763, "general": 0.9922184348106384}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87704 | 31274 | 58.67% | 0 | 0.00 | 9578.53 | 0.000 | 73.95% | 69.53% | `{"filetypes/ole_doc": 0.9996793270111084, "general": 0.9986937046051025}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27678 | 54.72% | 0 | 0.00 | 10822.93 | 0.000 | 70.73% | 99.83% | `{"filegroups/scripts": 0.99515300989151, "filetypes/lua": 0.9064293503761292, "general": 0.9730017185211182}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.11997564882040024}` |
| filetypes/macho | joint_or_at_fp_0 | 2827 | 31794 | 52.10% | 0 | 0.00 | 9421.88 | 0.000 | 68.51% | 96.09% | `{"filegroups/native": 0.9889988899230957, "filetypes/macho": 0.9950132966041565, "general": 0.9955723285675049}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5485 | 51.99% | 0 | 0.00 | 54601.90 | 0.000 | 68.41% | 74.84% | `{"filegroups/scripts": 0.9983050227165222, "filetypes/powershell": 0.9972237348556519, "general": 0.9896460175514221}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32350 | 83759 | 51.79% | 0 | 0.00 | 3576.55 | 0.000 | 68.24% | 86.57% | `{"filegroups/source": 0.9844242930412292, "filetypes/kotlin": 0.9635764360427856, "general": 0.9658637642860413}` |
| filetypes/package.json | joint_or_at_fp_0 | 20832 | 64116 | 49.42% | 0 | 0.00 | 4672.25 | 0.000 | 66.15% | 87.60% | `{"filegroups/config": 0.9999878406524658, "filetypes/package.json": 0.9999068975448608, "general": 0.9987140893936157}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9474 | 47.27% | 0 | 0.00 | 31615.57 | 0.000 | 64.20% | 99.39% | `{"filetypes/clojure": 0.9826399683952332, "general": 0.009953147731721401}` |
| filetypes/javascript | joint_or_at_fp_0 | 141873 | 1632971 | 43.95% | 0 | 0.00 | 183.45 | 0.000 | 61.06% | 95.52% | `{"filegroups/scripts": 0.9989351630210876, "filetypes/javascript": 0.9985103607177734, "general": 0.9969708323478699}` |
| filetypes/python | joint_or_at_fp_0 | 23133 | 643034 | 43.59% | 0 | 0.00 | 465.87 | 0.000 | 60.72% | 98.04% | `{"filegroups/scripts": 0.9989697337150574, "filetypes/python": 0.9952390789985657, "general": 0.9934379458427429}` |
| filetypes/dmg | joint_or_at_fp_0 | 62 | 249 | 43.55% | 0 | 0.00 | 1195896.96 | 0.000 | 60.67% | 88.75% | `{"filetypes/dmg": 0.9168030023574829, "general": 0.9536659121513367}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1061 | 41.58% | 0 | 0.00 | 281951.65 | 0.000 | 58.74% | 94.92% | `{"filetypes/chrome_manifest": 0.7949474453926086, "general": 0.9666340351104736}` |
| filetypes/ruby | joint_or_at_fp_0 | 397 | 179226 | 38.79% | 0 | 0.00 | 1671.47 | 0.000 | 55.90% | 99.86% | `{"filegroups/scripts": 0.9908696413040161, "filetypes/ruby": 0.9749945998191833, "general": 0.9246655106544495}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78129 | 38.64% | 0 | 0.00 | 3834.27 | 0.000 | 55.74% | 99.69% | `{"filetypes/perl": 0.999790608882904, "general": 0.98844975233078}` |
| filetypes/pe | joint_or_at_fp_0 | 1379129 | 233390 | 36.98% | 0 | 0.00 | 1283.57 | 0.000 | 54.00% | 46.10% | `{"filegroups/native": 0.9998283386230469, "filetypes/pe": 0.9996039867401123, "general": 0.9996622204780579}` |
| filetypes/npm | joint_or_at_fp_0 | 7018 | 18706 | 35.24% | 0 | 0.00 | 16013.54 | 0.000 | 52.11% | 82.33% | `{"filetypes/npm": 0.9978756308555603, "general": 0.9977253079414368}` |
| filetypes/zip | joint_or_at_fp_0 | 108029 | 40073 | 32.38% | 0 | 0.00 | 7475.41 | 0.000 | 48.91% | 50.67% | `{"filetypes/zip": 0.999140739440918, "general": 0.9953022599220276}` |
| filetypes/lnk | joint_or_at_fp_0 | 4685 | 1152 | 32.17% | 0 | 0.00 | 259708.38 | 0.000 | 48.68% | 45.55% | `{"filetypes/lnk": 0.9952960014343262, "general": 0.9988121390342712}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 885 | 96.99% | 0 | 0.00 | 337928.55 | 0.000 | 98.47% | 97.37% | `{"filegroups/documents": 0.9848322868347168, "general": 0.8436551690101624}` |
| filetypes/asar | joint_or_at_fp_0 | 188 | 235 | 96.81% | 0 | 0.00 | 1266688.79 | 0.000 | 98.38% | 98.58% | `{"filetypes/asar": 0.8564065098762512, "general": 0.8970264196395874}` |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 530 | 94.55% | 0 | 0.00 | 563638.07 | 0.000 | 97.20% | 99.49% | `{"general": 0.8539895415306091}` |
| filetypes/gem | joint_or_at_fp_0 | 1008 | 4665 | 92.16% | 0 | 0.00 | 64196.58 | 0.000 | 95.92% | 98.61% | `{"filetypes/gem": 0.9423370957374573, "general": 0.9742353558540344}` |
| filetypes/7z | joint_or_at_fp_0 | 9019 | 305 | 90.86% | 0 | 0.00 | 977399.40 | 0.000 | 95.21% | 91.16% | `{"filetypes/7z": 0.7546620965003967, "general": 0.9876203536987305}` |
| filetypes/elf | joint_or_at_fp_0 | 196620 | 808232 | 88.44% | 0 | 0.00 | 370.65 | 0.000 | 93.87% | 97.74% | `{"filegroups/native": 0.9941302537918091, "filetypes/elf": 0.9998213648796082, "general": 0.9892976880073547}` |
| filetypes/html | joint_or_at_fp_0 | 263 | 77662 | 87.83% | 0 | 0.00 | 3857.32 | 0.000 | 93.52% | 99.96% | `{"filegroups/documents": 0.9987590909004211, "filetypes/html": 0.999596118927002, "general": 0.9446626305580139}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 83 | 402 | 86.75% | 0 | 0.00 | 742437.25 | 0.000 | 92.90% | 97.73% | `{"filetypes/python_sdist": 0.8777077198028564}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 16644 | 86.43% | 0 | 0.00 | 17997.25 | 0.000 | 92.72% | 94.71% | `{"filetypes/pkg_info": 0.9985552430152893, "general": 0.9901254177093506}` |
| filetypes/chm | joint_or_at_fp_0 | 244 | 53 | 84.84% | 0 | 0.00 | 5495548.85 | 0.000 | 91.80% | 87.54% | `{"filetypes/chm": 0.8653669953346252, "general": 0.1371891349554062}` |
| filetypes/tar | joint_or_at_fp_0 | 34261 | 75446 | 68.54% | 0 | 0.00 | 3970.62 | 0.000 | 81.34% | 90.18% | `{"filetypes/tar": 0.9991694092750549, "general": 0.9942576289176941}` |
| filetypes/shell | joint_or_at_fp_0 | 18635 | 160039 | 64.92% | 0 | 0.00 | 1871.86 | 0.000 | 78.73% | 96.34% | `{"filegroups/scripts": 0.9990348815917969, "filetypes/shell": 0.9966918230056763, "general": 0.9922184348106384}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87704 | 31274 | 58.67% | 0 | 0.00 | 9578.53 | 0.000 | 73.95% | 69.53% | `{"filetypes/ole_doc": 0.9996793270111084, "general": 0.9986937046051025}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 27678 | 54.72% | 0 | 0.00 | 10822.93 | 0.000 | 70.73% | 99.83% | `{"filegroups/scripts": 0.99515300989151, "filetypes/lua": 0.9064293503761292, "general": 0.9730017185211182}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44573 | 52.17% | 0 | 0.00 | 6720.73 | 0.000 | 68.57% | 99.93% | `{"filegroups/source": 0.11997564882040024}` |
| filetypes/macho | joint_or_at_fp_0 | 2827 | 31794 | 52.10% | 0 | 0.00 | 9421.88 | 0.000 | 68.51% | 96.09% | `{"filegroups/native": 0.9889988899230957, "filetypes/macho": 0.9950132966041565, "general": 0.9955723285675049}` |
| filetypes/powershell | joint_or_at_fp_0 | 6038 | 5485 | 51.99% | 0 | 0.00 | 54601.90 | 0.000 | 68.41% | 74.84% | `{"filegroups/scripts": 0.9983050227165222, "filetypes/powershell": 0.9972237348556519, "general": 0.9896460175514221}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32350 | 83759 | 51.79% | 0 | 0.00 | 3576.55 | 0.000 | 68.24% | 86.57% | `{"filegroups/source": 0.9844242930412292, "filetypes/kotlin": 0.9635764360427856, "general": 0.9658637642860413}` |
| filetypes/package.json | joint_or_at_fp_0 | 20832 | 64116 | 49.42% | 0 | 0.00 | 4672.25 | 0.000 | 66.15% | 87.60% | `{"filegroups/config": 0.9999878406524658, "filetypes/package.json": 0.9999068975448608, "general": 0.9987140893936157}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 9474 | 47.27% | 0 | 0.00 | 31615.57 | 0.000 | 64.20% | 99.39% | `{"filetypes/clojure": 0.9826399683952332, "general": 0.009953147731721401}` |
| filetypes/javascript | joint_or_at_fp_0 | 141873 | 1632971 | 43.95% | 0 | 0.00 | 183.45 | 0.000 | 61.06% | 95.52% | `{"filegroups/scripts": 0.9989351630210876, "filetypes/javascript": 0.9985103607177734, "general": 0.9969708323478699}` |
| filetypes/python | joint_or_at_fp_0 | 23133 | 643034 | 43.59% | 0 | 0.00 | 465.87 | 0.000 | 60.72% | 98.04% | `{"filegroups/scripts": 0.9989697337150574, "filetypes/python": 0.9952390789985657, "general": 0.9934379458427429}` |
| filetypes/dmg | joint_or_at_fp_0 | 62 | 249 | 43.55% | 0 | 0.00 | 1195896.96 | 0.000 | 60.67% | 88.75% | `{"filetypes/dmg": 0.9168030023574829, "general": 0.9536659121513367}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 101 | 1061 | 41.58% | 0 | 0.00 | 281951.65 | 0.000 | 58.74% | 94.92% | `{"filetypes/chrome_manifest": 0.7949474453926086, "general": 0.9666340351104736}` |
| filetypes/ruby | joint_or_at_fp_0 | 397 | 179226 | 38.79% | 0 | 0.00 | 1671.47 | 0.000 | 55.90% | 99.86% | `{"filegroups/scripts": 0.9908696413040161, "filetypes/ruby": 0.9749945998191833, "general": 0.9246655106544495}` |
| filetypes/perl | joint_or_at_fp_0 | 396 | 78129 | 38.64% | 0 | 0.00 | 3834.27 | 0.000 | 55.74% | 99.69% | `{"filetypes/perl": 0.999790608882904, "general": 0.98844975233078}` |
| filetypes/pe | joint_or_at_fp_0 | 1379129 | 233390 | 36.98% | 0 | 0.00 | 1283.57 | 0.000 | 54.00% | 46.10% | `{"filegroups/native": 0.9998283386230469, "filetypes/pe": 0.9996039867401123, "general": 0.9996622204780579}` |
| filetypes/npm | joint_or_at_fp_0 | 7018 | 18706 | 35.24% | 0 | 0.00 | 16013.54 | 0.000 | 52.11% | 82.33% | `{"filetypes/npm": 0.9978756308555603, "general": 0.9977253079414368}` |
| filetypes/rar | calibrate_inherited | 22199 | 43 | 34.86% | 0 | 0.00 | 6729675.34 | 0.000 | 51.70% | 34.99% | `{"general": 0.9992722186377954}` |
| filetypes/zip | joint_or_at_fp_0 | 108029 | 40073 | 32.38% | 0 | 0.00 | 7475.41 | 0.000 | 48.91% | 50.67% | `{"filetypes/zip": 0.999140739440918, "general": 0.9953022599220276}` |
