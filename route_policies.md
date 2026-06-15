# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1727088862`
- Rows: 7920730 (2613468 malware, 5307262 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6238 | 524 | 97.90% | 0 | 0.00 | 570073.51 | 0.000 | 98.94% | 98.06% | `{"filetypes/rtf": 0.7203809022903442, "general": 0.011222563683986664}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2543 | 96.87% | 0 | 0.00 | 117733.72 | 0.000 | 98.41% | 97.48% | `{"filetypes/pkg-info": 0.6525869369506836, "general": 0.978059709072113}` |
| filetypes/xls | joint_or_at_fp_0 | 39581 | 20762 | 94.28% | 0 | 0.00 | 14427.88 | 0.000 | 97.05% | 96.25% | `{"filegroups/documents": 0.9993836879730225, "filetypes/xls": 0.905364453792572}` |
| filetypes/elf | joint_or_at_fp_0 | 189085 | 191055 | 93.01% | 0 | 0.00 | 1567.98 | 0.000 | 96.38% | 96.52% | `{"filegroups/native": 0.9172187447547913, "filetypes/elf": 0.9908542633056641, "general": 0.9873099327087402}` |
| filetypes/package.json | joint_or_at_fp_0 | 19082 | 24529 | 91.52% | 0 | 0.00 | 12212.28 | 0.000 | 95.57% | 96.29% | `{"filegroups/config": 0.9996548891067505, "filetypes/package.json": 0.9968649744987488, "general": 0.9888683557510376}` |
| filetypes/tar | joint_or_at_fp_0 | 31220 | 40803 | 90.74% | 0 | 0.00 | 7341.67 | 0.000 | 95.15% | 95.99% | `{"filetypes/tar": 0.9708203077316284, "general": 0.9795634746551514}` |
| filetypes/gem | filetype_only_at_fp_0 | 220 | 451 | 87.73% | 0 | 0.00 | 662040.98 | 0.000 | 93.46% | 95.98% | `{"filetypes/gem": 0.8297737240791321}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 204 | 81.60% | 0 | 0.00 | 1457766.39 | 0.000 | 89.87% | 82.24% | `{"filetypes/msi": 0.4432210922241211, "general": 0.9497512578964233}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 457 | 81.32% | 0 | 0.00 | 653377.43 | 0.000 | 89.70% | 96.90% | `{"filetypes/chrome-manifest": 0.9023540616035461}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6568 | 79.00% | 0 | 0.00 | 45600.63 | 0.000 | 88.27% | 88.88% | `{"filegroups/documents": 0.4871273636817932, "filetypes/ole": 0.4742516279220581}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 273790 | 77.98% | 0 | 0.00 | 1094.17 | 0.000 | 87.63% | 99.73% | `{"filetypes/python-bytecode": 0.999248206615448, "general": 0.9378916025161743}` |
| filetypes/macho | joint_or_at_fp_0 | 2643 | 12787 | 74.65% | 0 | 0.00 | 23425.21 | 0.000 | 85.49% | 95.66% | `{"filegroups/native": 0.4734219014644623, "filetypes/macho": 0.9959020018577576, "general": 0.9391813278198242}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 461 | 73.16% | 0 | 0.00 | 647726.61 | 0.000 | 84.50% | 75.40% | `{"filegroups/documents": 0.955623984336853, "filetypes/docx": 0.9688920378684998, "general": 0.9892902970314026}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.11% | 0 | 0.00 | 280894.17 | 0.000 | 84.47% | 78.16% | `{"filetypes/lnk": 0.9818357229232788, "general": 0.9971070289611816}` |
| filetypes/pdf | joint_or_at_fp_0 | 178630 | 24557 | 71.68% | 0 | 0.00 | 12198.35 | 0.000 | 83.51% | 75.10% | `{"filegroups/documents": 0.6956265568733215, "filetypes/pdf": 0.9445086121559143, "general": 0.9697330594062805}` |
| filetypes/npm | filetype_only_at_fp_0 | 1217 | 137 | 67.21% | 0 | 0.00 | 2162931.67 | 0.000 | 80.39% | 70.53% | `{"filetypes/npm": 0.8038899302482605}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5998 | 67.18% | 0 | 0.00 | 49933.05 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.962000846862793, "general": 0.0228868518024683}` |
| filetypes/crx | joint_or_at_fp_0 | 880 | 96 | 67.05% | 0 | 0.00 | 3072367.68 | 0.000 | 80.27% | 70.29% | `{"filetypes/crx": 0.8663125038146973, "general": 0.8931023478507996}` |
| filetypes/java_class | joint_or_at_fp_0 | 1945 | 794416 | 61.23% | 0 | 0.00 | 377.10 | 0.000 | 75.96% | 99.91% | `{"filegroups/portable": 0.9765889644622803, "filetypes/java_class": 0.9685042500495911, "general": 0.9419178366661072}` |
| filetypes/jar | joint_or_at_fp_0 | 3680 | 4426 | 58.02% | 0 | 0.00 | 67661.97 | 0.000 | 73.43% | 80.94% | `{"filetypes/jar": 0.8075616955757141, "general": 0.9626635909080505}` |
| filetypes/whl | filetype_only_at_fp_0 | 732 | 4452 | 57.38% | 0 | 0.00 | 67266.95 | 0.000 | 72.92% | 93.98% | `{"filetypes/whl": 0.9696301817893982}` |
| filetypes/pe | joint_or_at_fp_0 | 1368083 | 165386 | 57.34% | 0 | 0.00 | 1811.34 | 0.000 | 72.89% | 61.94% | `{"filegroups/native": 0.9975659847259521, "filetypes/pe": 0.9990491271018982, "general": 0.99977707862854}` |
| filetypes/perl | joint_or_at_fp_0 | 375 | 43487 | 56.53% | 0 | 0.00 | 6888.56 | 0.000 | 72.23% | 99.63% | `{"filegroups/scripts": 0.9664208292961121, "filetypes/perl": 0.9973215460777283, "general": 0.7609468698501587}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32655 | 58487 | 52.49% | 0 | 0.00 | 5121.92 | 0.000 | 68.84% | 82.98% | `{"filegroups/source": 0.7614274621009827, "filetypes/kotlin": 0.93508380651474, "general": 0.8157554864883423}` |
| filetypes/php | joint_or_at_fp_0 | 5652 | 165637 | 48.09% | 0 | 0.00 | 1808.60 | 0.000 | 64.95% | 98.29% | `{"filegroups/scripts": 0.993687093257904, "filetypes/php": 0.9665976166725159, "general": 0.9240117073059082}` |
| filetypes/shell | joint_or_at_fp_0 | 15626 | 68542 | 46.77% | 0 | 0.00 | 4370.56 | 0.000 | 63.74% | 90.12% | `{"filegroups/scripts": 0.9955518841743469, "filetypes/shell": 0.9747353792190552, "general": 0.9919736981391907}` |
| filetypes/powershell | joint_or_at_fp_0 | 5845 | 2561 | 46.57% | 0 | 0.00 | 116906.71 | 0.000 | 63.55% | 62.85% | `{"filegroups/scripts": 0.994948148727417, "filetypes/powershell": 0.9890862107276917, "general": 0.9942713975906372}` |
| filetypes/python | joint_or_at_fp_0 | 23298 | 237192 | 44.76% | 0 | 0.00 | 1262.99 | 0.000 | 61.84% | 95.06% | `{"filegroups/scripts": 0.996512234210968, "filetypes/python": 0.9969419836997986, "general": 0.994095504283905}` |
| filetypes/vbs | joint_or_at_fp_0 | 11917 | 3342 | 42.60% | 0 | 0.00 | 89598.74 | 0.000 | 59.75% | 55.17% | `{"filetypes/vbs": 0.9957180619239807, "general": 0.9904896020889282}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6238 | 524 | 97.90% | 0 | 0.00 | 570073.51 | 0.000 | 98.94% | 98.06% | `{"filetypes/rtf": 0.7203809022903442, "general": 0.011222563683986664}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2543 | 96.87% | 0 | 0.00 | 117733.72 | 0.000 | 98.41% | 97.48% | `{"filetypes/pkg-info": 0.6525869369506836, "general": 0.978059709072113}` |
| filetypes/xls | joint_or_at_fp_0 | 39581 | 20762 | 94.28% | 0 | 0.00 | 14427.88 | 0.000 | 97.05% | 96.25% | `{"filegroups/documents": 0.9993836879730225, "filetypes/xls": 0.905364453792572}` |
| filetypes/elf | joint_or_at_fp_0 | 189085 | 191055 | 93.01% | 0 | 0.00 | 1567.98 | 0.000 | 96.38% | 96.52% | `{"filegroups/native": 0.9172187447547913, "filetypes/elf": 0.9908542633056641, "general": 0.9873099327087402}` |
| filetypes/package.json | joint_or_at_fp_0 | 19082 | 24529 | 91.52% | 0 | 0.00 | 12212.28 | 0.000 | 95.57% | 96.29% | `{"filegroups/config": 0.9996548891067505, "filetypes/package.json": 0.9968649744987488, "general": 0.9888683557510376}` |
| filetypes/tar | joint_or_at_fp_0 | 31220 | 40803 | 90.74% | 0 | 0.00 | 7341.67 | 0.000 | 95.15% | 95.99% | `{"filetypes/tar": 0.9708203077316284, "general": 0.9795634746551514}` |
| filetypes/gem | filetype_only_at_fp_0 | 220 | 451 | 87.73% | 0 | 0.00 | 662040.98 | 0.000 | 93.46% | 95.98% | `{"filetypes/gem": 0.8297737240791321}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 204 | 81.60% | 0 | 0.00 | 1457766.39 | 0.000 | 89.87% | 82.24% | `{"filetypes/msi": 0.4432210922241211, "general": 0.9497512578964233}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 457 | 81.32% | 0 | 0.00 | 653377.43 | 0.000 | 89.70% | 96.90% | `{"filetypes/chrome-manifest": 0.9023540616035461}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6568 | 79.00% | 0 | 0.00 | 45600.63 | 0.000 | 88.27% | 88.88% | `{"filegroups/documents": 0.4871273636817932, "filetypes/ole": 0.4742516279220581}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 273790 | 77.98% | 0 | 0.00 | 1094.17 | 0.000 | 87.63% | 99.73% | `{"filetypes/python-bytecode": 0.999248206615448, "general": 0.9378916025161743}` |
| filetypes/macho | joint_or_at_fp_0 | 2643 | 12787 | 74.65% | 0 | 0.00 | 23425.21 | 0.000 | 85.49% | 95.66% | `{"filegroups/native": 0.4734219014644623, "filetypes/macho": 0.9959020018577576, "general": 0.9391813278198242}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 461 | 73.16% | 0 | 0.00 | 647726.61 | 0.000 | 84.50% | 75.40% | `{"filegroups/documents": 0.955623984336853, "filetypes/docx": 0.9688920378684998, "general": 0.9892902970314026}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.11% | 0 | 0.00 | 280894.17 | 0.000 | 84.47% | 78.16% | `{"filetypes/lnk": 0.9818357229232788, "general": 0.9971070289611816}` |
| filetypes/pdf | joint_or_at_fp_0 | 178630 | 24557 | 71.68% | 0 | 0.00 | 12198.35 | 0.000 | 83.51% | 75.10% | `{"filegroups/documents": 0.6956265568733215, "filetypes/pdf": 0.9445086121559143, "general": 0.9697330594062805}` |
| filetypes/npm | filetype_only_at_fp_0 | 1217 | 137 | 67.21% | 0 | 0.00 | 2162931.67 | 0.000 | 80.39% | 70.53% | `{"filetypes/npm": 0.8038899302482605}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5998 | 67.18% | 0 | 0.00 | 49933.05 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.962000846862793, "general": 0.0228868518024683}` |
| filetypes/crx | joint_or_at_fp_0 | 880 | 96 | 67.05% | 0 | 0.00 | 3072367.68 | 0.000 | 80.27% | 70.29% | `{"filetypes/crx": 0.8663125038146973, "general": 0.8931023478507996}` |
| filetypes/java_class | joint_or_at_fp_0 | 1945 | 794416 | 61.23% | 0 | 0.00 | 377.10 | 0.000 | 75.96% | 99.91% | `{"filegroups/portable": 0.9765889644622803, "filetypes/java_class": 0.9685042500495911, "general": 0.9419178366661072}` |
| filetypes/jar | joint_or_at_fp_0 | 3680 | 4426 | 58.02% | 0 | 0.00 | 67661.97 | 0.000 | 73.43% | 80.94% | `{"filetypes/jar": 0.8075616955757141, "general": 0.9626635909080505}` |
| filetypes/whl | filetype_only_at_fp_0 | 732 | 4452 | 57.38% | 0 | 0.00 | 67266.95 | 0.000 | 72.92% | 93.98% | `{"filetypes/whl": 0.9696301817893982}` |
| filetypes/pe | joint_or_at_fp_0 | 1368083 | 165386 | 57.34% | 0 | 0.00 | 1811.34 | 0.000 | 72.89% | 61.94% | `{"filegroups/native": 0.9975659847259521, "filetypes/pe": 0.9990491271018982, "general": 0.99977707862854}` |
| filetypes/perl | joint_or_at_fp_0 | 375 | 43487 | 56.53% | 0 | 0.00 | 6888.56 | 0.000 | 72.23% | 99.63% | `{"filegroups/scripts": 0.9664208292961121, "filetypes/perl": 0.9973215460777283, "general": 0.7609468698501587}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32655 | 58487 | 52.49% | 0 | 0.00 | 5121.92 | 0.000 | 68.84% | 82.98% | `{"filegroups/source": 0.7614274621009827, "filetypes/kotlin": 0.93508380651474, "general": 0.8157554864883423}` |
| filetypes/php | joint_or_at_fp_0 | 5652 | 165637 | 48.09% | 0 | 0.00 | 1808.60 | 0.000 | 64.95% | 98.29% | `{"filegroups/scripts": 0.993687093257904, "filetypes/php": 0.9665976166725159, "general": 0.9240117073059082}` |
| filetypes/shell | joint_or_at_fp_0 | 15626 | 68542 | 46.77% | 0 | 0.00 | 4370.56 | 0.000 | 63.74% | 90.12% | `{"filegroups/scripts": 0.9955518841743469, "filetypes/shell": 0.9747353792190552, "general": 0.9919736981391907}` |
| filetypes/powershell | joint_or_at_fp_0 | 5845 | 2561 | 46.57% | 0 | 0.00 | 116906.71 | 0.000 | 63.55% | 62.85% | `{"filegroups/scripts": 0.994948148727417, "filetypes/powershell": 0.9890862107276917, "general": 0.9942713975906372}` |
| filetypes/python | joint_or_at_fp_0 | 23298 | 237192 | 44.76% | 0 | 0.00 | 1262.99 | 0.000 | 61.84% | 95.06% | `{"filegroups/scripts": 0.996512234210968, "filetypes/python": 0.9969419836997986, "general": 0.994095504283905}` |
| filetypes/vbs | joint_or_at_fp_0 | 11917 | 3342 | 42.60% | 0 | 0.00 | 89598.74 | 0.000 | 59.75% | 55.17% | `{"filetypes/vbs": 0.9957180619239807, "general": 0.9904896020889282}` |
