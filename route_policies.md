# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2538267239`
- Rows: 14692357 (2661661 malware, 12030696 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6255 | 836 | 97.87% | 0 | 0.00 | 357699.91 | 0.000 | 98.93% | 98.12% | `{"filetypes/rtf": 0.6468079090118408, "general": 0.8232688307762146}` |
| filetypes/html | joint_or_at_fp_0 | 256 | 19607 | 96.88% | 0 | 0.00 | 15277.72 | 0.000 | 98.41% | 99.96% | `{"filegroups/documents": 0.8392195105552673, "filetypes/html": 0.9926033616065979}` |
| filetypes/asar | learned_blend_at_fp_0 | 184 | 137 | 95.11% | 0 | 0.00 | 2162931.67 | 0.000 | 97.49% | 97.20% | `{}` |
| filetypes/applescript | learned_blend_at_fp_0 | 59 | 479 | 93.22% | 0 | 0.00 | 623462.19 | 0.000 | 96.49% | 99.26% | `{}` |
| filetypes/gem | joint_or_at_fp_0 | 899 | 2521 | 92.21% | 0 | 0.00 | 118760.53 | 0.000 | 95.95% | 97.95% | `{"filetypes/gem": 0.9528699517250061, "general": 0.9256792068481445}` |
| filetypes/elf | joint_or_at_fp_0 | 193492 | 583176 | 89.48% | 0 | 0.00 | 513.69 | 0.000 | 94.45% | 97.38% | `{"filegroups/native": 0.9873352646827698, "filetypes/elf": 0.9995372295379639, "general": 0.9858866930007935}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 14168 | 66.72% | 0 | 0.00 | 21142.12 | 0.000 | 80.04% | 85.74% | `{"filetypes/pkg_info": 0.9979959726333618, "general": 0.997741162776947}` |
| filetypes/tar | filetype_only_at_fp_0 | 34106 | 65778 | 65.30% | 0 | 0.00 | 4554.20 | 0.000 | 79.01% | 88.15% | `{"filetypes/tar": 0.9989815354347229}` |
| filetypes/macho | joint_or_at_fp_0 | 2830 | 25180 | 63.00% | 0 | 0.00 | 11896.56 | 0.000 | 77.30% | 96.26% | `{"filegroups/native": 0.985181987285614, "filetypes/macho": 0.9809927344322205, "general": 0.9740698337554932}` |
| filetypes/package.json | joint_or_at_fp_0 | 20466 | 51554 | 60.15% | 0 | 0.00 | 5810.69 | 0.000 | 75.12% | 88.68% | `{"filegroups/config": 0.9999792575836182, "filetypes/package.json": 0.9990144968032837, "general": 0.9993634223937988}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 43153 | 56.52% | 0 | 0.00 | 6941.88 | 0.000 | 72.22% | 99.93% | `{"general": 0.14112278819084167}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32375 | 76501 | 52.90% | 0 | 0.00 | 3915.86 | 0.000 | 69.19% | 85.99% | `{"filegroups/source": 0.9794977903366089, "filetypes/kotlin": 0.9953703284263611, "general": 0.9715583324432373}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 26639 | 52.83% | 0 | 0.00 | 11245.03 | 0.000 | 69.14% | 99.81% | `{"filegroups/scripts": 0.9929566383361816, "filetypes/lua": 0.9100056886672974}` |
| filetypes/powershell | joint_or_at_fp_0 | 6042 | 4697 | 51.59% | 0 | 0.00 | 63759.36 | 0.000 | 68.06% | 72.76% | `{"filegroups/scripts": 0.9990767240524292, "filetypes/powershell": 0.9883687496185303, "general": 0.9923271536827087}` |
| filetypes/lnk | joint_or_at_fp_0 | 4650 | 1096 | 50.34% | 0 | 0.00 | 272960.02 | 0.000 | 66.97% | 59.82% | `{"filetypes/lnk": 0.987561047077179, "general": 0.9969716668128967}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 72429 | 48.75% | 0 | 0.00 | 4136.01 | 0.000 | 65.55% | 99.72% | `{"filegroups/scripts": 0.9977385997772217, "filetypes/perl": 0.999428927898407, "general": 0.9916024208068848}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87624 | 31003 | 47.77% | 0 | 0.00 | 9662.25 | 0.000 | 64.65% | 61.42% | `{"filetypes/ole_doc": 0.9994445443153381, "general": 0.9991963505744934}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8857 | 46.36% | 0 | 0.00 | 33817.61 | 0.000 | 63.35% | 99.34% | `{"filetypes/clojure": 0.9948443174362183, "general": 0.018343601375818253}` |
| filetypes/shell | joint_or_at_fp_0 | 18340 | 142475 | 43.63% | 0 | 0.00 | 2102.62 | 0.000 | 60.75% | 93.57% | `{"filegroups/scripts": 0.9992824196815491, "filetypes/shell": 0.9950643181800842, "general": 0.9917590618133545}` |
| filetypes/python | joint_or_at_fp_0 | 23138 | 578000 | 42.58% | 0 | 0.00 | 518.29 | 0.000 | 59.73% | 97.79% | `{"filegroups/scripts": 0.9993942975997925, "filetypes/python": 0.9982618689537048, "general": 0.993467390537262}` |
| filetypes/jar | joint_or_at_fp_0 | 3895 | 24052 | 42.21% | 0 | 0.00 | 12454.46 | 0.000 | 59.36% | 91.95% | `{"filetypes/jar": 0.9937415719032288, "general": 0.9873312711715698}` |
| filetypes/php | joint_or_at_fp_0 | 6303 | 584942 | 40.62% | 0 | 0.00 | 512.14 | 0.000 | 57.77% | 99.37% | `{"filegroups/scripts": 0.998042106628418, "filetypes/php": 0.9985159039497375, "general": 0.9986376166343689}` |
| filetypes/ruby | joint_or_at_fp_0 | 398 | 176297 | 39.95% | 0 | 0.00 | 1699.24 | 0.000 | 57.09% | 99.86% | `{"filegroups/scripts": 0.9880242943763733, "filetypes/ruby": 0.9997207522392273, "general": 0.9432785511016846}` |
| filetypes/javascript | joint_or_at_fp_0 | 140535 | 1360564 | 38.01% | 0 | 0.00 | 220.18 | 0.000 | 55.09% | 94.20% | `{"filegroups/scripts": 0.9990561604499817, "filetypes/javascript": 0.9986953139305115, "general": 0.999198853969574}` |
| filetypes/whl | joint_or_at_fp_0 | 3663 | 7095 | 36.58% | 0 | 0.00 | 42214.23 | 0.000 | 53.57% | 78.41% | `{"filetypes/whl": 0.9954438209533691, "general": 0.9805386662483215}` |
| filetypes/npm | joint_or_at_fp_0 | 4830 | 6122 | 35.30% | 0 | 0.00 | 48921.91 | 0.000 | 52.18% | 71.47% | `{"filetypes/npm": 0.9982442855834961, "general": 0.9976679086685181}` |
| filetypes/crate | joint_or_at_fp_0 | 89 | 5191 | 33.71% | 0 | 0.00 | 57693.47 | 0.000 | 50.42% | 98.88% | `{"filetypes/crate": 0.9982860684394836, "general": 0.3485773503780365}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 28871 | 32.78% | 0 | 0.00 | 10375.73 | 0.000 | 49.37% | 42.13% | `{"filegroups/documents": 0.9978501796722412, "filetypes/pdf": 0.9982852339744568, "general": 0.9957180619239807}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3503 | 835176 | 32.26% | 0 | 0.00 | 358.69 | 0.000 | 48.78% | 99.72% | `{"filetypes/python_bytecode": 0.9999985694885254, "general": 0.9747756719589233}` |
| filetypes/pe | joint_or_at_fp_0 | 1374383 | 204554 | 31.67% | 0 | 0.00 | 1464.51 | 0.000 | 48.11% | 40.52% | `{"filegroups/native": 0.9997369647026062, "filetypes/pe": 0.9994865655899048, "general": 0.9996653199195862}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6255 | 836 | 97.87% | 0 | 0.00 | 357699.91 | 0.000 | 98.93% | 98.12% | `{"filetypes/rtf": 0.6468079090118408, "general": 0.8232688307762146}` |
| filetypes/html | joint_or_at_fp_0 | 256 | 19607 | 96.88% | 0 | 0.00 | 15277.72 | 0.000 | 98.41% | 99.96% | `{"filegroups/documents": 0.8392195105552673, "filetypes/html": 0.9926033616065979}` |
| filetypes/asar | learned_blend_at_fp_0 | 184 | 137 | 95.11% | 0 | 0.00 | 2162931.67 | 0.000 | 97.49% | 97.20% | `{}` |
| filetypes/applescript | learned_blend_at_fp_0 | 59 | 479 | 93.22% | 0 | 0.00 | 623462.19 | 0.000 | 96.49% | 99.26% | `{}` |
| filetypes/gem | joint_or_at_fp_0 | 899 | 2521 | 92.21% | 0 | 0.00 | 118760.53 | 0.000 | 95.95% | 97.95% | `{"filetypes/gem": 0.9528699517250061, "general": 0.9256792068481445}` |
| filetypes/elf | joint_or_at_fp_0 | 193492 | 583176 | 89.48% | 0 | 0.00 | 513.69 | 0.000 | 94.45% | 97.38% | `{"filegroups/native": 0.9873352646827698, "filetypes/elf": 0.9995372295379639, "general": 0.9858866930007935}` |
| filetypes/pkg_info | joint_or_at_fp_0 | 10623 | 14168 | 66.72% | 0 | 0.00 | 21142.12 | 0.000 | 80.04% | 85.74% | `{"filetypes/pkg_info": 0.9979959726333618, "general": 0.997741162776947}` |
| filetypes/tar | filetype_only_at_fp_0 | 34106 | 65778 | 65.30% | 0 | 0.00 | 4554.20 | 0.000 | 79.01% | 88.15% | `{"filetypes/tar": 0.9989815354347229}` |
| filetypes/macho | joint_or_at_fp_0 | 2830 | 25180 | 63.00% | 0 | 0.00 | 11896.56 | 0.000 | 77.30% | 96.26% | `{"filegroups/native": 0.985181987285614, "filetypes/macho": 0.9809927344322205, "general": 0.9740698337554932}` |
| filetypes/package.json | joint_or_at_fp_0 | 20466 | 51554 | 60.15% | 0 | 0.00 | 5810.69 | 0.000 | 75.12% | 88.68% | `{"filegroups/config": 0.9999792575836182, "filetypes/package.json": 0.9990144968032837, "general": 0.9993634223937988}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 43153 | 56.52% | 0 | 0.00 | 6941.88 | 0.000 | 72.22% | 99.93% | `{"general": 0.14112278819084167}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32375 | 76501 | 52.90% | 0 | 0.00 | 3915.86 | 0.000 | 69.19% | 85.99% | `{"filegroups/source": 0.9794977903366089, "filetypes/kotlin": 0.9953703284263611, "general": 0.9715583324432373}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 26639 | 52.83% | 0 | 0.00 | 11245.03 | 0.000 | 69.14% | 99.81% | `{"filegroups/scripts": 0.9929566383361816, "filetypes/lua": 0.9100056886672974}` |
| filetypes/powershell | joint_or_at_fp_0 | 6042 | 4697 | 51.59% | 0 | 0.00 | 63759.36 | 0.000 | 68.06% | 72.76% | `{"filegroups/scripts": 0.9990767240524292, "filetypes/powershell": 0.9883687496185303, "general": 0.9923271536827087}` |
| filetypes/lnk | joint_or_at_fp_0 | 4650 | 1096 | 50.34% | 0 | 0.00 | 272960.02 | 0.000 | 66.97% | 59.82% | `{"filetypes/lnk": 0.987561047077179, "general": 0.9969716668128967}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 72429 | 48.75% | 0 | 0.00 | 4136.01 | 0.000 | 65.55% | 99.72% | `{"filegroups/scripts": 0.9977385997772217, "filetypes/perl": 0.999428927898407, "general": 0.9916024208068848}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 87624 | 31003 | 47.77% | 0 | 0.00 | 9662.25 | 0.000 | 64.65% | 61.42% | `{"filetypes/ole_doc": 0.9994445443153381, "general": 0.9991963505744934}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8857 | 46.36% | 0 | 0.00 | 33817.61 | 0.000 | 63.35% | 99.34% | `{"filetypes/clojure": 0.9948443174362183, "general": 0.018343601375818253}` |
| filetypes/shell | joint_or_at_fp_0 | 18340 | 142475 | 43.63% | 0 | 0.00 | 2102.62 | 0.000 | 60.75% | 93.57% | `{"filegroups/scripts": 0.9992824196815491, "filetypes/shell": 0.9950643181800842, "general": 0.9917590618133545}` |
| filetypes/python | joint_or_at_fp_0 | 23138 | 578000 | 42.58% | 0 | 0.00 | 518.29 | 0.000 | 59.73% | 97.79% | `{"filegroups/scripts": 0.9993942975997925, "filetypes/python": 0.9982618689537048, "general": 0.993467390537262}` |
| filetypes/jar | joint_or_at_fp_0 | 3895 | 24052 | 42.21% | 0 | 0.00 | 12454.46 | 0.000 | 59.36% | 91.95% | `{"filetypes/jar": 0.9937415719032288, "general": 0.9873312711715698}` |
| filetypes/php | joint_or_at_fp_0 | 6303 | 584942 | 40.62% | 0 | 0.00 | 512.14 | 0.000 | 57.77% | 99.37% | `{"filegroups/scripts": 0.998042106628418, "filetypes/php": 0.9985159039497375, "general": 0.9986376166343689}` |
| filetypes/ruby | joint_or_at_fp_0 | 398 | 176297 | 39.95% | 0 | 0.00 | 1699.24 | 0.000 | 57.09% | 99.86% | `{"filegroups/scripts": 0.9880242943763733, "filetypes/ruby": 0.9997207522392273, "general": 0.9432785511016846}` |
| filetypes/zst | calibrate_inherited | 10473 | 253039 | 38.92% | 0 | 0.00 | 1183.89 | 0.000 | 56.03% | 97.57% | `{"general": 0.9993570797461253}` |
| filetypes/javascript | joint_or_at_fp_0 | 140535 | 1360564 | 38.01% | 0 | 0.00 | 220.18 | 0.000 | 55.09% | 94.20% | `{"filegroups/scripts": 0.9990561604499817, "filetypes/javascript": 0.9986953139305115, "general": 0.999198853969574}` |
| filetypes/whl | joint_or_at_fp_0 | 3663 | 7095 | 36.58% | 0 | 0.00 | 42214.23 | 0.000 | 53.57% | 78.41% | `{"filetypes/whl": 0.9954438209533691, "general": 0.9805386662483215}` |
| filetypes/npm | joint_or_at_fp_0 | 4830 | 6122 | 35.30% | 0 | 0.00 | 48921.91 | 0.000 | 52.18% | 71.47% | `{"filetypes/npm": 0.9982442855834961, "general": 0.9976679086685181}` |
| filetypes/crate | joint_or_at_fp_0 | 89 | 5191 | 33.71% | 0 | 0.00 | 57693.47 | 0.000 | 50.42% | 98.88% | `{"filetypes/crate": 0.9982860684394836, "general": 0.3485773503780365}` |
| filetypes/7z | calibrate_inherited | 8995 | 218 | 32.78% | 0 | 0.00 | 1364790.24 | 0.000 | 49.38% | 34.38% | `{"general": 0.9993570797461253}` |
| filetypes/pdf | joint_or_at_fp_0 | 178644 | 28871 | 32.78% | 0 | 0.00 | 10375.73 | 0.000 | 49.37% | 42.13% | `{"filegroups/documents": 0.9978501796722412, "filetypes/pdf": 0.9982852339744568, "general": 0.9957180619239807}` |
