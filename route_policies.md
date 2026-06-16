# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1727088862`
- Rows: 7920730 (2613468 malware, 5307262 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.996795117855072}` |
| filetypes/rtf | learned_blend_at_fp_0 | 6238 | 524 | 98.35% | 0 | 0.00 | 570073.51 | 0.000 | 99.17% | 98.48% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2543 | 96.87% | 0 | 0.00 | 117733.72 | 0.000 | 98.41% | 97.48% | `{"filetypes/pkg-info": 0.6525869369506836, "general": 0.978059709072113}` |
| filetypes/xls | learned_blend_at_fp_0 | 39581 | 20762 | 94.83% | 0 | 0.00 | 14427.88 | 0.000 | 97.35% | 96.61% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 189085 | 191055 | 93.01% | 0 | 0.00 | 1567.98 | 0.000 | 96.38% | 96.52% | `{"filegroups/native": 0.9172187447547913, "filetypes/elf": 0.9908542633056641, "general": 0.9873099327087402}` |
| filetypes/gem | filetype_only_at_fp_0 | 220 | 451 | 87.73% | 0 | 0.00 | 662040.98 | 0.000 | 93.46% | 95.98% | `{"filetypes/gem": 0.8297737240791321}` |
| filetypes/package.json | joint_or_at_fp_0 | 19082 | 24529 | 82.04% | 0 | 0.00 | 12212.28 | 0.000 | 90.13% | 92.14% | `{"filegroups/config": 0.9996179342269897, "filetypes/package.json": 0.9996460676193237, "general": 0.9887835383415222}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 204 | 81.60% | 0 | 0.00 | 1457766.39 | 0.000 | 89.87% | 82.24% | `{"filetypes/msi": 0.4432210922241211, "general": 0.9497512578964233}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 457 | 81.32% | 0 | 0.00 | 653377.43 | 0.000 | 89.70% | 96.90% | `{"filetypes/chrome-manifest": 0.9023540616035461}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 273790 | 77.98% | 0 | 0.00 | 1094.17 | 0.000 | 87.63% | 99.73% | `{"filetypes/python-bytecode": 0.999248206615448, "general": 0.9378916025161743}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6568 | 77.92% | 0 | 0.00 | 45600.63 | 0.000 | 87.59% | 88.31% | `{"filegroups/documents": 0.22609888017177582, "filetypes/ole": 0.9976373314857483, "general": 0.8952587842941284}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 461 | 75.75% | 0 | 0.00 | 647726.61 | 0.000 | 86.20% | 77.77% | `{"filegroups/documents": 0.36584416031837463, "filetypes/docx": 0.9688920378684998}` |
| filetypes/macho | joint_or_at_fp_0 | 2643 | 12787 | 74.65% | 0 | 0.00 | 23425.21 | 0.000 | 85.49% | 95.66% | `{"filegroups/native": 0.4734219014644623, "filetypes/macho": 0.9959020018577576, "general": 0.9391813278198242}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.11% | 0 | 0.00 | 280894.17 | 0.000 | 84.47% | 78.16% | `{"filetypes/lnk": 0.9818357229232788, "general": 0.9971070289611816}` |
| filetypes/npm | filetype_only_at_fp_0 | 1217 | 137 | 67.21% | 0 | 0.00 | 2162931.67 | 0.000 | 80.39% | 70.53% | `{"filetypes/npm": 0.8038899302482605}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5998 | 67.18% | 0 | 0.00 | 49933.05 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.962000846862793, "general": 0.0228868518024683}` |
| filetypes/crx | joint_or_at_fp_0 | 880 | 96 | 67.05% | 0 | 0.00 | 3072367.68 | 0.000 | 80.27% | 70.29% | `{"filetypes/crx": 0.8663125038146973, "general": 0.8931023478507996}` |
| filetypes/shell | joint_or_at_fp_0 | 15626 | 68542 | 65.29% | 0 | 0.00 | 4370.56 | 0.000 | 79.00% | 93.56% | `{"filegroups/scripts": 0.9628051519393921, "filetypes/shell": 0.9524995684623718}` |
| filetypes/java_class | joint_or_at_fp_0 | 1945 | 794416 | 62.31% | 0 | 0.00 | 377.10 | 0.000 | 76.78% | 99.91% | `{"filegroups/portable": 0.9769918322563171, "filetypes/java_class": 0.9687302112579346, "general": 0.9419178366661072}` |
| filetypes/pe | joint_or_at_fp_0 | 1368083 | 165386 | 61.89% | 0 | 0.00 | 1811.34 | 0.000 | 76.46% | 66.00% | `{"filegroups/native": 0.9975660443305969, "filetypes/pe": 0.9977226257324219, "general": 0.9997783899307251}` |
| filetypes/javascript | filetype_only_at_fp_0 | 127208 | 677336 | 59.30% | 0 | 0.00 | 442.28 | 0.000 | 74.45% | 93.57% | `{"filetypes/javascript": 0.9559124112129211}` |
| filetypes/jar | joint_or_at_fp_0 | 3680 | 4426 | 58.02% | 0 | 0.00 | 67661.97 | 0.000 | 73.43% | 80.94% | `{"filetypes/jar": 0.8075616955757141, "general": 0.9626635909080505}` |
| filetypes/whl | filetype_only_at_fp_0 | 732 | 4452 | 57.38% | 0 | 0.00 | 67266.95 | 0.000 | 72.92% | 93.98% | `{"filetypes/whl": 0.9696301817893982}` |
| filetypes/perl | joint_or_at_fp_0 | 375 | 43487 | 56.27% | 0 | 0.00 | 6888.56 | 0.000 | 72.01% | 99.63% | `{"filegroups/scripts": 0.9567227363586426, "filetypes/perl": 0.9973215460777283, "general": 0.7573856115341187}` |
| filetypes/php | joint_or_at_fp_0 | 5652 | 165637 | 48.71% | 0 | 0.00 | 1808.60 | 0.000 | 65.51% | 98.31% | `{"filegroups/scripts": 0.9787468314170837, "filetypes/php": 0.9672286510467529, "general": 0.9237154722213745}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32655 | 58487 | 47.63% | 0 | 0.00 | 5121.92 | 0.000 | 64.52% | 81.24% | `{"filegroups/source": 0.8955700397491455, "filetypes/kotlin": 0.8694854378700256, "general": 0.8146654367446899}` |
| filetypes/powershell | joint_or_at_fp_0 | 5845 | 2561 | 46.31% | 0 | 0.00 | 116906.71 | 0.000 | 63.31% | 62.67% | `{"filegroups/scripts": 0.9885620474815369, "filetypes/powershell": 0.9919875860214233, "general": 0.9942713975906372}` |
| filetypes/python | joint_or_at_fp_0 | 23298 | 237192 | 46.29% | 0 | 0.00 | 1262.99 | 0.000 | 63.28% | 95.20% | `{"filegroups/scripts": 0.9920116662979126, "filetypes/python": 0.9969084858894348, "general": 0.994207501411438}` |
| filetypes/ruby | joint_or_at_fp_0 | 248 | 29026 | 40.73% | 0 | 0.00 | 10320.33 | 0.000 | 57.88% | 99.50% | `{"filegroups/scripts": 0.9785200357437134, "filetypes/ruby": 0.9925271272659302, "general": 0.9281122088432312}` |
| filetypes/zip | joint_or_at_fp_0 | 104631 | 17561 | 34.06% | 0 | 0.00 | 17057.55 | 0.000 | 50.82% | 43.54% | `{"filetypes/zip": 0.9982025623321533, "general": 0.9977526068687439}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.996795117855072}` |
| filetypes/rtf | learned_blend_at_fp_0 | 6238 | 524 | 98.35% | 0 | 0.00 | 570073.51 | 0.000 | 99.17% | 98.48% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10655 | 2543 | 96.87% | 0 | 0.00 | 117733.72 | 0.000 | 98.41% | 97.48% | `{"filetypes/pkg-info": 0.6525869369506836, "general": 0.978059709072113}` |
| filetypes/xls | learned_blend_at_fp_0 | 39581 | 20762 | 94.83% | 0 | 0.00 | 14427.88 | 0.000 | 97.35% | 96.61% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 189085 | 191055 | 93.01% | 0 | 0.00 | 1567.98 | 0.000 | 96.38% | 96.52% | `{"filegroups/native": 0.9172187447547913, "filetypes/elf": 0.9908542633056641, "general": 0.9873099327087402}` |
| filetypes/gem | filetype_only_at_fp_0 | 220 | 451 | 87.73% | 0 | 0.00 | 662040.98 | 0.000 | 93.46% | 95.98% | `{"filetypes/gem": 0.8297737240791321}` |
| filetypes/package.json | joint_or_at_fp_0 | 19082 | 24529 | 82.04% | 0 | 0.00 | 12212.28 | 0.000 | 90.13% | 92.14% | `{"filegroups/config": 0.9996179342269897, "filetypes/package.json": 0.9996460676193237, "general": 0.9887835383415222}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 204 | 81.60% | 0 | 0.00 | 1457766.39 | 0.000 | 89.87% | 82.24% | `{"filetypes/msi": 0.4432210922241211, "general": 0.9497512578964233}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 457 | 81.32% | 0 | 0.00 | 653377.43 | 0.000 | 89.70% | 96.90% | `{"filetypes/chrome-manifest": 0.9023540616035461}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 273790 | 77.98% | 0 | 0.00 | 1094.17 | 0.000 | 87.63% | 99.73% | `{"filetypes/python-bytecode": 0.999248206615448, "general": 0.9378916025161743}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6568 | 77.92% | 0 | 0.00 | 45600.63 | 0.000 | 87.59% | 88.31% | `{"filegroups/documents": 0.22609888017177582, "filetypes/ole": 0.9976373314857483, "general": 0.8952587842941284}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 461 | 75.75% | 0 | 0.00 | 647726.61 | 0.000 | 86.20% | 77.77% | `{"filegroups/documents": 0.36584416031837463, "filetypes/docx": 0.9688920378684998}` |
| filetypes/macho | joint_or_at_fp_0 | 2643 | 12787 | 74.65% | 0 | 0.00 | 23425.21 | 0.000 | 85.49% | 95.66% | `{"filegroups/native": 0.4734219014644623, "filetypes/macho": 0.9959020018577576, "general": 0.9391813278198242}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.11% | 0 | 0.00 | 280894.17 | 0.000 | 84.47% | 78.16% | `{"filetypes/lnk": 0.9818357229232788, "general": 0.9971070289611816}` |
| filetypes/npm | filetype_only_at_fp_0 | 1217 | 137 | 67.21% | 0 | 0.00 | 2162931.67 | 0.000 | 80.39% | 70.53% | `{"filetypes/npm": 0.8038899302482605}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 5998 | 67.18% | 0 | 0.00 | 49933.05 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.962000846862793, "general": 0.0228868518024683}` |
| filetypes/crx | joint_or_at_fp_0 | 880 | 96 | 67.05% | 0 | 0.00 | 3072367.68 | 0.000 | 80.27% | 70.29% | `{"filetypes/crx": 0.8663125038146973, "general": 0.8931023478507996}` |
| filetypes/shell | joint_or_at_fp_0 | 15626 | 68542 | 65.29% | 0 | 0.00 | 4370.56 | 0.000 | 79.00% | 93.56% | `{"filegroups/scripts": 0.9628051519393921, "filetypes/shell": 0.9524995684623718}` |
| filetypes/java_class | joint_or_at_fp_0 | 1945 | 794416 | 62.31% | 0 | 0.00 | 377.10 | 0.000 | 76.78% | 99.91% | `{"filegroups/portable": 0.9769918322563171, "filetypes/java_class": 0.9687302112579346, "general": 0.9419178366661072}` |
| filetypes/pe | joint_or_at_fp_0 | 1368083 | 165386 | 61.89% | 0 | 0.00 | 1811.34 | 0.000 | 76.46% | 66.00% | `{"filegroups/native": 0.9975660443305969, "filetypes/pe": 0.9977226257324219, "general": 0.9997783899307251}` |
| filetypes/javascript | filetype_only_at_fp_0 | 127208 | 677336 | 59.30% | 0 | 0.00 | 442.28 | 0.000 | 74.45% | 93.57% | `{"filetypes/javascript": 0.9559124112129211}` |
| filetypes/jar | joint_or_at_fp_0 | 3680 | 4426 | 58.02% | 0 | 0.00 | 67661.97 | 0.000 | 73.43% | 80.94% | `{"filetypes/jar": 0.8075616955757141, "general": 0.9626635909080505}` |
| filetypes/whl | filetype_only_at_fp_0 | 732 | 4452 | 57.38% | 0 | 0.00 | 67266.95 | 0.000 | 72.92% | 93.98% | `{"filetypes/whl": 0.9696301817893982}` |
| filetypes/perl | joint_or_at_fp_0 | 375 | 43487 | 56.27% | 0 | 0.00 | 6888.56 | 0.000 | 72.01% | 99.63% | `{"filegroups/scripts": 0.9567227363586426, "filetypes/perl": 0.9973215460777283, "general": 0.7573856115341187}` |
| filetypes/php | joint_or_at_fp_0 | 5652 | 165637 | 48.71% | 0 | 0.00 | 1808.60 | 0.000 | 65.51% | 98.31% | `{"filegroups/scripts": 0.9787468314170837, "filetypes/php": 0.9672286510467529, "general": 0.9237154722213745}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32655 | 58487 | 47.63% | 0 | 0.00 | 5121.92 | 0.000 | 64.52% | 81.24% | `{"filegroups/source": 0.8955700397491455, "filetypes/kotlin": 0.8694854378700256, "general": 0.8146654367446899}` |
| filetypes/powershell | joint_or_at_fp_0 | 5845 | 2561 | 46.31% | 0 | 0.00 | 116906.71 | 0.000 | 63.31% | 62.67% | `{"filegroups/scripts": 0.9885620474815369, "filetypes/powershell": 0.9919875860214233, "general": 0.9942713975906372}` |
| filetypes/python | joint_or_at_fp_0 | 23298 | 237192 | 46.29% | 0 | 0.00 | 1262.99 | 0.000 | 63.28% | 95.20% | `{"filegroups/scripts": 0.9920116662979126, "filetypes/python": 0.9969084858894348, "general": 0.994207501411438}` |
| filetypes/ruby | joint_or_at_fp_0 | 248 | 29026 | 40.73% | 0 | 0.00 | 10320.33 | 0.000 | 57.88% | 99.50% | `{"filegroups/scripts": 0.9785200357437134, "filetypes/ruby": 0.9925271272659302, "general": 0.9281122088432312}` |
| filetypes/zip | joint_or_at_fp_0 | 104631 | 17561 | 34.06% | 0 | 0.00 | 17057.55 | 0.000 | 50.82% | 43.54% | `{"filetypes/zip": 0.9982025623321533, "general": 0.9977526068687439}` |
