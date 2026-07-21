# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2448147370`
- Rows: 14395301 (2659504 malware, 11735797 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 836 | 97.94% | 0 | 0.00 | 357699.91 | 0.000 | 98.96% | 98.18% | `{"filetypes/rtf": 0.0404934287071228}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15962 | 96.86% | 0 | 0.00 | 18766.14 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9955982565879822}` |
| filetypes/gem | joint_or_at_fp_0 | 891 | 2498 | 95.17% | 0 | 0.00 | 119853.35 | 0.000 | 97.53% | 98.73% | `{"filetypes/gem": 0.484771192073822}` |
| filetypes/applescript | joint_or_at_fp_0 | 59 | 471 | 93.22% | 0 | 0.00 | 634018.15 | 0.000 | 96.49% | 99.25% | `{"filetypes/applescript": 0.7700080871582031}` |
| filetypes/elf | joint_or_at_fp_0 | 192928 | 535178 | 90.58% | 0 | 0.00 | 559.76 | 0.000 | 95.06% | 97.50% | `{"filegroups/native": 0.9659082293510437, "filetypes/elf": 0.9998036026954651, "general": 0.9871376752853394}` |
| filetypes/asar | joint_or_at_fp_0 | 183 | 115 | 90.16% | 0 | 0.00 | 2571347.57 | 0.000 | 94.83% | 93.96% | `{"filetypes/asar": 0.8965896964073181, "general": 0.696668267250061}` |
| filetypes/package.json | joint_or_at_fp_0 | 20439 | 50362 | 83.14% | 0 | 0.00 | 5948.22 | 0.000 | 90.79% | 95.13% | `{"filegroups/config": 0.9998757839202881, "filetypes/package.json": 0.9987155199050903, "general": 0.9994921684265137}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87600 | 30881 | 83.08% | 0 | 0.00 | 9700.42 | 0.000 | 90.76% | 87.49% | `{"filetypes/ole_doc": 0.9944595098495483}` |
| filetypes/vsix | joint_or_at_fp_0 | 100 | 3249 | 79.00% | 0 | 0.00 | 92162.25 | 0.000 | 88.27% | 99.37% | `{"filetypes/vsix": 0.8790768980979919}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 23467 | 76.03% | 0 | 0.00 | 12764.91 | 0.000 | 86.38% | 97.42% | `{"filegroups/native": 0.7896321415901184, "filetypes/macho": 0.9529614448547363, "general": 0.972654402256012}` |
| filetypes/tar | filetype_only_at_fp_0 | 34050 | 64488 | 73.07% | 0 | 0.00 | 4645.30 | 0.000 | 84.44% | 90.69% | `{"filetypes/tar": 0.9979864358901978}` |
| filetypes/lnk | joint_or_at_fp_0 | 4642 | 1089 | 72.08% | 0 | 0.00 | 274712.17 | 0.000 | 83.78% | 77.39% | `{"filetypes/lnk": 0.9783370494842529, "general": 0.9972060918807983}` |
| filetypes/nupkg | joint_or_at_fp_0 | 82 | 2655 | 71.95% | 0 | 0.00 | 112769.97 | 0.000 | 83.69% | 99.16% | `{"filetypes/nupkg": 0.9802218079566956}` |
| filetypes/vbs | joint_or_at_fp_0 | 12296 | 3593 | 70.94% | 0 | 0.00 | 83342.16 | 0.000 | 83.00% | 77.51% | `{"filetypes/vbs": 0.9895721673965454, "general": 0.9933519959449768}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 26360 | 70.75% | 0 | 0.00 | 11364.04 | 0.000 | 82.87% | 99.88% | `{"filegroups/scripts": 0.8677955269813538, "filetypes/lua": 0.5373945236206055}` |
| filetypes/powershell | joint_or_at_fp_0 | 6007 | 4630 | 67.39% | 0 | 0.00 | 64681.71 | 0.000 | 80.52% | 81.58% | `{"filegroups/scripts": 0.9899453520774841, "filetypes/powershell": 0.9305325746536255, "general": 0.9920415878295898}` |
| filetypes/shell | joint_or_at_fp_0 | 18271 | 136620 | 61.96% | 0 | 0.00 | 2192.72 | 0.000 | 76.51% | 95.51% | `{"filegroups/scripts": 0.9899010062217712, "filetypes/shell": 0.9960921406745911, "general": 0.9922816753387451}` |
| filetypes/npm | joint_or_at_fp_0 | 4705 | 6777 | 57.24% | 0 | 0.00 | 44194.63 | 0.000 | 72.80% | 82.48% | `{"filetypes/npm": 0.9921572208404541, "general": 0.998028576374054}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32377 | 74455 | 56.70% | 0 | 0.00 | 4023.47 | 0.000 | 72.37% | 86.88% | `{"filegroups/source": 0.9757959842681885, "filetypes/kotlin": 0.8162355422973633, "general": 0.9978578090667725}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 71097 | 55.25% | 0 | 0.00 | 4213.50 | 0.000 | 71.18% | 99.75% | `{"filetypes/perl": 0.9967003464698792, "general": 0.9963526725769043}` |
| filetypes/whl | joint_or_at_fp_0 | 3625 | 6784 | 53.49% | 0 | 0.00 | 44149.04 | 0.000 | 69.70% | 83.80% | `{"filetypes/whl": 0.9848321080207825, "general": 0.9858607053756714}` |
| filetypes/pe | joint_or_at_fp_0 | 1373702 | 203004 | 53.30% | 0 | 0.00 | 1475.69 | 0.000 | 69.54% | 59.32% | `{"filegroups/native": 0.9984853863716125, "filetypes/pe": 0.9978228807449341, "general": 0.9996113181114197}` |
| filetypes/jar | joint_or_at_fp_0 | 3887 | 22891 | 50.45% | 0 | 0.00 | 13086.09 | 0.000 | 67.07% | 92.81% | `{"filetypes/jar": 0.9627929329872131, "general": 0.9790080189704895}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8598 | 48.18% | 0 | 0.00 | 34836.13 | 0.000 | 65.03% | 99.35% | `{"filetypes/clojure": 0.9918729662895203}` |
| filetypes/registry | joint_or_at_fp_0 | 624 | 211958 | 45.19% | 0 | 0.00 | 1413.35 | 0.000 | 62.25% | 99.84% | `{"filetypes/registry": 0.9999548196792603, "general": 0.9790661931037903}` |
| filetypes/php | joint_or_at_fp_0 | 6164 | 582024 | 43.87% | 0 | 0.00 | 514.71 | 0.000 | 60.98% | 99.41% | `{"filegroups/scripts": 0.9848021864891052, "filetypes/php": 0.9982240796089172}` |
| filetypes/python | joint_or_at_fp_0 | 23126 | 568150 | 43.57% | 0 | 0.00 | 527.28 | 0.000 | 60.70% | 97.79% | `{"filegroups/scripts": 0.9949315190315247, "filetypes/python": 0.9989088773727417, "general": 0.9950354695320129}` |
| filetypes/javascript | joint_or_at_fp_0 | 140391 | 1336350 | 42.08% | 0 | 0.00 | 224.17 | 0.000 | 59.23% | 94.49% | `{"filegroups/scripts": 0.9934298396110535, "filetypes/javascript": 0.9971555471420288, "general": 0.9987212419509888}` |
| filetypes/xpi | joint_or_at_fp_0 | 111 | 657 | 36.94% | 0 | 0.00 | 454933.46 | 0.000 | 53.95% | 90.89% | `{"filetypes/xpi": 0.9137144088745117, "general": 0.806810200214386}` |
| filetypes/chrome_manifest | joint_or_at_fp_0 | 106 | 954 | 34.91% | 0 | 0.00 | 313525.54 | 0.000 | 51.75% | 93.49% | `{"filetypes/chrome_manifest": 0.9398350715637207}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | joint_or_at_fp_0 | 6252 | 836 | 97.94% | 0 | 0.00 | 357699.91 | 0.000 | 98.96% | 98.18% | `{"filetypes/rtf": 0.0404934287071228}` |
| filetypes/html | joint_or_at_fp_0 | 255 | 15962 | 96.86% | 0 | 0.00 | 18766.14 | 0.000 | 98.41% | 99.95% | `{"filetypes/html": 0.9955982565879822}` |
| filetypes/gem | joint_or_at_fp_0 | 891 | 2498 | 95.17% | 0 | 0.00 | 119853.35 | 0.000 | 97.53% | 98.73% | `{"filetypes/gem": 0.484771192073822}` |
| filetypes/applescript | joint_or_at_fp_0 | 59 | 471 | 93.22% | 0 | 0.00 | 634018.15 | 0.000 | 96.49% | 99.25% | `{"filetypes/applescript": 0.7700080871582031}` |
| filetypes/elf | joint_or_at_fp_0 | 192928 | 535178 | 90.58% | 0 | 0.00 | 559.76 | 0.000 | 95.06% | 97.50% | `{"filegroups/native": 0.9659082293510437, "filetypes/elf": 0.9998036026954651, "general": 0.9871376752853394}` |
| filetypes/asar | joint_or_at_fp_0 | 183 | 115 | 90.16% | 0 | 0.00 | 2571347.57 | 0.000 | 94.83% | 93.96% | `{"filetypes/asar": 0.8965896964073181, "general": 0.696668267250061}` |
| filetypes/package.json | joint_or_at_fp_0 | 20439 | 50362 | 83.14% | 0 | 0.00 | 5948.22 | 0.000 | 90.79% | 95.13% | `{"filegroups/config": 0.9998757839202881, "filetypes/package.json": 0.9987155199050903, "general": 0.9994921684265137}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87600 | 30881 | 83.08% | 0 | 0.00 | 9700.42 | 0.000 | 90.76% | 87.49% | `{"filetypes/ole_doc": 0.9944595098495483}` |
| filetypes/vsix | joint_or_at_fp_0 | 100 | 3249 | 79.00% | 0 | 0.00 | 92162.25 | 0.000 | 88.27% | 99.37% | `{"filetypes/vsix": 0.8790768980979919}` |
| filetypes/macho | joint_or_at_fp_0 | 2828 | 23467 | 76.03% | 0 | 0.00 | 12764.91 | 0.000 | 86.38% | 97.42% | `{"filegroups/native": 0.7896321415901184, "filetypes/macho": 0.9529614448547363, "general": 0.972654402256012}` |
| filetypes/tar | filetype_only_at_fp_0 | 34050 | 64488 | 73.07% | 0 | 0.00 | 4645.30 | 0.000 | 84.44% | 90.69% | `{"filetypes/tar": 0.9979864358901978}` |
| filetypes/lnk | joint_or_at_fp_0 | 4642 | 1089 | 72.08% | 0 | 0.00 | 274712.17 | 0.000 | 83.78% | 77.39% | `{"filetypes/lnk": 0.9783370494842529, "general": 0.9972060918807983}` |
| filetypes/nupkg | joint_or_at_fp_0 | 82 | 2655 | 71.95% | 0 | 0.00 | 112769.97 | 0.000 | 83.69% | 99.16% | `{"filetypes/nupkg": 0.9802218079566956}` |
| filetypes/vbs | joint_or_at_fp_0 | 12296 | 3593 | 70.94% | 0 | 0.00 | 83342.16 | 0.000 | 83.00% | 77.51% | `{"filetypes/vbs": 0.9895721673965454, "general": 0.9933519959449768}` |
| filetypes/lua | joint_or_at_fp_0 | 106 | 26360 | 70.75% | 0 | 0.00 | 11364.04 | 0.000 | 82.87% | 99.88% | `{"filegroups/scripts": 0.8677955269813538, "filetypes/lua": 0.5373945236206055}` |
| filetypes/powershell | joint_or_at_fp_0 | 6007 | 4630 | 67.39% | 0 | 0.00 | 64681.71 | 0.000 | 80.52% | 81.58% | `{"filegroups/scripts": 0.9899453520774841, "filetypes/powershell": 0.9305325746536255, "general": 0.9920415878295898}` |
| filetypes/shell | joint_or_at_fp_0 | 18271 | 136620 | 61.96% | 0 | 0.00 | 2192.72 | 0.000 | 76.51% | 95.51% | `{"filegroups/scripts": 0.9899010062217712, "filetypes/shell": 0.9960921406745911, "general": 0.9922816753387451}` |
| filetypes/npm | joint_or_at_fp_0 | 4705 | 6777 | 57.24% | 0 | 0.00 | 44194.63 | 0.000 | 72.80% | 82.48% | `{"filetypes/npm": 0.9921572208404541, "general": 0.998028576374054}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32377 | 74455 | 56.70% | 0 | 0.00 | 4023.47 | 0.000 | 72.37% | 86.88% | `{"filegroups/source": 0.9757959842681885, "filetypes/kotlin": 0.8162355422973633, "general": 0.9978578090667725}` |
| filetypes/perl | joint_or_at_fp_0 | 400 | 71097 | 55.25% | 0 | 0.00 | 4213.50 | 0.000 | 71.18% | 99.75% | `{"filetypes/perl": 0.9967003464698792, "general": 0.9963526725769043}` |
| filetypes/whl | joint_or_at_fp_0 | 3625 | 6784 | 53.49% | 0 | 0.00 | 44149.04 | 0.000 | 69.70% | 83.80% | `{"filetypes/whl": 0.9848321080207825, "general": 0.9858607053756714}` |
| filetypes/pe | joint_or_at_fp_0 | 1373702 | 203004 | 53.30% | 0 | 0.00 | 1475.69 | 0.000 | 69.54% | 59.32% | `{"filegroups/native": 0.9984853863716125, "filetypes/pe": 0.9978228807449341, "general": 0.9996113181114197}` |
| filetypes/jar | joint_or_at_fp_0 | 3887 | 22891 | 50.45% | 0 | 0.00 | 13086.09 | 0.000 | 67.07% | 92.81% | `{"filetypes/jar": 0.9627929329872131, "general": 0.9790080189704895}` |
| filetypes/clojure | joint_or_at_fp_0 | 110 | 8598 | 48.18% | 0 | 0.00 | 34836.13 | 0.000 | 65.03% | 99.35% | `{"filetypes/clojure": 0.9918729662895203}` |
| filetypes/registry | joint_or_at_fp_0 | 624 | 211958 | 45.19% | 0 | 0.00 | 1413.35 | 0.000 | 62.25% | 99.84% | `{"filetypes/registry": 0.9999548196792603, "general": 0.9790661931037903}` |
| filetypes/php | joint_or_at_fp_0 | 6164 | 582024 | 43.87% | 0 | 0.00 | 514.71 | 0.000 | 60.98% | 99.41% | `{"filegroups/scripts": 0.9848021864891052, "filetypes/php": 0.9982240796089172}` |
| filetypes/python | joint_or_at_fp_0 | 23126 | 568150 | 43.57% | 0 | 0.00 | 527.28 | 0.000 | 60.70% | 97.79% | `{"filegroups/scripts": 0.9949315190315247, "filetypes/python": 0.9989088773727417, "general": 0.9950354695320129}` |
| filetypes/zst | calibrate_inherited | 10473 | 232425 | 42.60% | 0 | 0.00 | 1288.89 | 0.000 | 59.75% | 97.53% | `{"general": 0.9992278860010352}` |
| filetypes/javascript | joint_or_at_fp_0 | 140391 | 1336350 | 42.08% | 0 | 0.00 | 224.17 | 0.000 | 59.23% | 94.49% | `{"filegroups/scripts": 0.9934298396110535, "filetypes/javascript": 0.9971555471420288, "general": 0.9987212419509888}` |
| filetypes/xpi | joint_or_at_fp_0 | 111 | 657 | 36.94% | 0 | 0.00 | 454933.46 | 0.000 | 53.95% | 90.89% | `{"filetypes/xpi": 0.9137144088745117, "general": 0.806810200214386}` |
