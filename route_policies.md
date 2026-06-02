# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1637343931`
- Rows: 6563647 (2373669 malware, 4189978 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf† | max_rule | 5188 | 495 | 99.04% | 0 | 0.00 | 603370.80 | 0.000 | 99.52% | 99.12% | `{"filegroups/documents": 0.059649036397432825, "filetypes/rtf": 0.059649036397432825, "general": 0.059649036397432825}` |
| filetypes/doc | calibrate_inherited | 29009 | 69 | 98.10% | 0 | 0.00 | 4248741.05 | 0.000 | 99.04% | 98.11% | `{"filegroups/documents": 0.7054287195205688, "general": 0.9985769240861829}` |
| filetypes/batch | joint_or_at_fp_0 | 175830 | 4479 | 98.05% | 0 | 0.00 | 66861.59 | 0.000 | 99.01% | 98.10% | `{"filegroups/scripts": 0.9965866804122925, "filetypes/batch": 0.9952186942100525, "general": 0.9728008508682251}` |
| filetypes/tar | joint_or_at_fp_0 | 1358 | 502 | 94.99% | 0 | 0.00 | 594982.34 | 0.000 | 97.43% | 96.34% | `{"filetypes/tar": 0.6570408940315247, "general": 0.802480161190033}` |
| filetypes/xls | learned_blend_at_fp_0 | 32874 | 20740 | 93.97% | 0 | 0.00 | 14443.18 | 0.000 | 96.89% | 96.31% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2632 | 74039 | 93.88% | 0 | 0.00 | 4046.07 | 0.000 | 96.84% | 99.79% | `{"filetypes/python-bytecode": 0.9990511536598206, "general": 0.8666414618492126}` |
| filetypes/package.json | learned_blend_at_fp_0 | 18304 | 16827 | 89.71% | 0 | 0.00 | 17801.54 | 0.000 | 94.57% | 94.64% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 163474 | 164654 | 88.79% | 0 | 0.00 | 1819.39 | 0.000 | 94.06% | 94.42% | `{"filegroups/native": 0.9981070756912231, "filetypes/elf": 0.9996823072433472, "general": 0.98270183801651}` |
| filetypes/clojure | joint_or_at_fp_0 | 121 | 3000 | 86.78% | 0 | 0.00 | 99807.90 | 0.000 | 92.92% | 99.49% | `{"filetypes/clojure": 0.8923954963684082}` |
| filetypes/ole | joint_or_at_fp_0 | 6117 | 5887 | 86.76% | 0 | 0.00 | 50874.30 | 0.000 | 92.91% | 93.25% | `{"filegroups/documents": 0.7791716456413269, "general": 0.9513899087905884}` |
| filetypes/shell | learned_blend_at_fp_0 | 13239 | 54419 | 85.69% | 0 | 0.00 | 5504.79 | 0.000 | 92.29% | 97.20% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10636 | 1420 | 83.40% | 0 | 0.00 | 210744.68 | 0.000 | 90.95% | 85.35% | `{"filetypes/pkg-info": 0.9949578642845154, "general": 0.9842746257781982}` |
| filetypes/html | learned_blend_at_fp_3 | 225 | 25636 | 80.89% | 0 | 0.00 | 11684.96 | 0.000 | 89.43% | 99.83% | `{}` |
| filetypes/docx† | filetype_only | 4268 | 412 | 80.58% | 0 | 0.00 | 724482.37 | 0.000 | 89.24% | 82.29% | `{"filetypes/docx": 0.49349499834883714}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 59 | 435 | 76.27% | 0 | 0.00 | 686308.16 | 0.000 | 86.54% | 97.17% | `{"filetypes/chrome-manifest": 0.9049327373504639}` |
| filetypes/crx | joint_or_at_fp_0 | 379 | 79 | 76.25% | 0 | 0.00 | 3721067.61 | 0.000 | 86.53% | 80.35% | `{"filetypes/crx": 0.9353027939796448, "general": 0.9746719598770142}` |
| filetypes/7z† | or_general_primary | 5809 | 108 | 72.71% | 0 | 0.00 | 2735708.87 | 0.000 | 84.20% | 73.21% | `{"general": 0.9640197665360211}` |
| filetypes/lnk† | filetype_only | 4027 | 1055 | 70.23% | 0 | 0.00 | 283552.89 | 0.000 | 82.51% | 76.41% | `{"filetypes/lnk": 0.9755334746801442}` |
| filetypes/vbs | joint_or_at_fp_0 | 9655 | 3301 | 63.81% | 0 | 0.00 | 90711.10 | 0.000 | 77.91% | 73.03% | `{"filetypes/vbs": 0.9959895014762878, "general": 0.9731259942054749}` |
| filetypes/perl | joint_or_at_fp_0 | 310 | 33185 | 63.23% | 0 | 0.00 | 9026.96 | 0.000 | 77.47% | 99.66% | `{"filegroups/scripts": 0.9813587069511414, "filetypes/perl": 0.9944701194763184}` |
| filetypes/javascript | joint_or_at_fp_0 | 99494 | 559855 | 55.07% | 0 | 0.00 | 535.09 | 0.000 | 71.03% | 93.22% | `{"filegroups/scripts": 0.9977161884307861, "filetypes/javascript": 0.9938919544219971, "general": 0.9983687996864319}` |
| filetypes/jar | joint_or_at_fp_0 | 3083 | 3558 | 54.07% | 0 | 0.00 | 84161.65 | 0.000 | 70.19% | 78.68% | `{"filetypes/jar": 0.9076920747756958, "general": 0.9845328330993652}` |
| filetypes/pe† | max_rule | 1263848 | 159938 | 53.41% | 0 | 0.00 | 1873.04 | 0.000 | 69.63% | 58.64% | `{"filegroups/native": 0.9994085401380736, "filetypes/pe": 0.9994085401380736, "general": 0.9994085401380736}` |
| filetypes/pptx | joint_or_at_fp_0 | 454 | 192 | 52.20% | 0 | 0.00 | 1548167.96 | 0.000 | 68.60% | 66.41% | `{"filegroups/documents": 0.7346557974815369, "filetypes/pptx": 0.09874933958053589}` |
| filetypes/powershell | learned_blend_at_fp_0 | 4850 | 2301 | 46.95% | 0 | 0.00 | 130107.91 | 0.000 | 63.90% | 64.02% | `{}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32813 | 50489 | 46.50% | 0 | 0.00 | 5933.26 | 0.000 | 63.48% | 78.92% | `{"filegroups/source": 0.8264152407646179, "filetypes/kotlin": 0.8846541047096252, "general": 0.9302482008934021}` |
| filetypes/macho† | filetype_only | 2518 | 11373 | 45.31% | 0 | 0.00 | 26337.27 | 0.000 | 62.37% | 90.09% | `{"filetypes/macho": 0.9970421904176612}` |
| filetypes/xlsx | joint_or_at_fp_0 | 51918 | 1585 | 44.47% | 0 | 0.00 | 188826.69 | 0.000 | 61.56% | 46.12% | `{"filegroups/documents": 0.41709890961647034, "filetypes/xlsx": 0.92574143409729}` |
| filetypes/php | joint_or_at_fp_0 | 4233 | 120277 | 43.96% | 0 | 0.00 | 2490.66 | 0.000 | 61.08% | 98.09% | `{"filegroups/scripts": 0.9966230392456055, "filetypes/php": 0.9997223019599915, "general": 0.98988938331604}` |
| filetypes/python | joint_or_at_fp_0 | 18646 | 163686 | 43.70% | 0 | 0.00 | 1830.15 | 0.000 | 60.82% | 94.24% | `{"filegroups/scripts": 0.9982466697692871, "filetypes/python": 0.9998779296875, "general": 0.9953924417495728}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf† | max_rule | 5188 | 495 | 99.04% | 0 | 0.00 | 603370.80 | 0.000 | 99.52% | 99.12% | `{"filegroups/documents": 0.059646826731417205, "filetypes/rtf": 0.059646826731417205, "general": 0.059646826731417205}` |
| filetypes/doc | calibrate_inherited | 29009 | 69 | 98.10% | 0 | 0.00 | 4248741.05 | 0.000 | 99.04% | 98.11% | `{"filegroups/documents": 0.7054287195205688, "general": 0.9985527266621961}` |
| filetypes/batch | joint_or_at_fp_0 | 175830 | 4479 | 98.05% | 0 | 0.00 | 66861.59 | 0.000 | 99.01% | 98.10% | `{"filegroups/scripts": 0.9965866804122925, "filetypes/batch": 0.9952186942100525, "general": 0.9728008508682251}` |
| filetypes/tar | joint_or_at_fp_0 | 1358 | 502 | 94.99% | 0 | 0.00 | 594982.34 | 0.000 | 97.43% | 96.34% | `{"filetypes/tar": 0.6570408940315247, "general": 0.802480161190033}` |
| filetypes/xls | learned_blend_at_fp_0 | 32874 | 20740 | 93.97% | 0 | 0.00 | 14443.18 | 0.000 | 96.89% | 96.31% | `{}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2632 | 74039 | 93.88% | 0 | 0.00 | 4046.07 | 0.000 | 96.84% | 99.79% | `{"filetypes/python-bytecode": 0.9990511536598206, "general": 0.8666414618492126}` |
| filetypes/package.json | learned_blend_at_fp_0 | 18304 | 16827 | 89.71% | 0 | 0.00 | 17801.54 | 0.000 | 94.57% | 94.64% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 163474 | 164654 | 88.79% | 0 | 0.00 | 1819.39 | 0.000 | 94.06% | 94.42% | `{"filegroups/native": 0.9981070756912231, "filetypes/elf": 0.9996823072433472, "general": 0.98270183801651}` |
| filetypes/clojure | joint_or_at_fp_0 | 121 | 3000 | 86.78% | 0 | 0.00 | 99807.90 | 0.000 | 92.92% | 99.49% | `{"filetypes/clojure": 0.8923954963684082}` |
| filetypes/ole | joint_or_at_fp_0 | 6117 | 5887 | 86.76% | 0 | 0.00 | 50874.30 | 0.000 | 92.91% | 93.25% | `{"filegroups/documents": 0.7791716456413269, "general": 0.9513899087905884}` |
| filetypes/shell | learned_blend_at_fp_0 | 13239 | 54419 | 85.69% | 0 | 0.00 | 5504.79 | 0.000 | 92.29% | 97.20% | `{}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10636 | 1420 | 83.40% | 0 | 0.00 | 210744.68 | 0.000 | 90.95% | 85.35% | `{"filetypes/pkg-info": 0.9949578642845154, "general": 0.9842746257781982}` |
| filetypes/html | learned_blend_at_fp_3 | 225 | 25636 | 80.89% | 0 | 0.00 | 11684.96 | 0.000 | 89.43% | 99.83% | `{}` |
| filetypes/docx† | filetype_only | 4268 | 412 | 80.60% | 0 | 0.00 | 724482.37 | 0.000 | 89.26% | 82.31% | `{"filetypes/docx": 0.48797113247748913}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 59 | 435 | 76.27% | 0 | 0.00 | 686308.16 | 0.000 | 86.54% | 97.17% | `{"filetypes/chrome-manifest": 0.9049327373504639}` |
| filetypes/crx | joint_or_at_fp_0 | 379 | 79 | 76.25% | 0 | 0.00 | 3721067.61 | 0.000 | 86.53% | 80.35% | `{"filetypes/crx": 0.9353027939796448, "general": 0.9746719598770142}` |
| filetypes/7z† | or_general_primary | 5809 | 108 | 72.71% | 0 | 0.00 | 2735708.87 | 0.000 | 84.20% | 73.21% | `{"general": 0.96400865753016}` |
| filetypes/lnk† | filetype_only | 4027 | 1055 | 70.60% | 0 | 0.00 | 283552.89 | 0.000 | 82.77% | 76.70% | `{"filetypes/lnk": 0.9666239845440031}` |
| filetypes/vbs | joint_or_at_fp_0 | 9655 | 3301 | 63.81% | 0 | 0.00 | 90711.10 | 0.000 | 77.91% | 73.03% | `{"filetypes/vbs": 0.9959895014762878, "general": 0.9731259942054749}` |
| filetypes/perl | joint_or_at_fp_0 | 310 | 33185 | 63.23% | 0 | 0.00 | 9026.96 | 0.000 | 77.47% | 99.66% | `{"filegroups/scripts": 0.9813587069511414, "filetypes/perl": 0.9944701194763184}` |
| filetypes/pdf† | filetype_only | 178284 | 21735 | 62.15% | 0 | 0.00 | 13782.04 | 0.000 | 76.66% | 66.26% | `{"filetypes/pdf": 0.8455750526143105}` |
| filetypes/macho† | filetype_only | 2518 | 11373 | 55.40% | 0 | 0.00 | 26337.27 | 0.000 | 71.30% | 91.92% | `{"filetypes/macho": 0.9950642199015115}` |
| filetypes/javascript | joint_or_at_fp_0 | 99494 | 559855 | 55.07% | 0 | 0.00 | 535.09 | 0.000 | 71.03% | 93.22% | `{"filegroups/scripts": 0.9977161884307861, "filetypes/javascript": 0.9938919544219971, "general": 0.9983687996864319}` |
| filetypes/jar | joint_or_at_fp_0 | 3083 | 3558 | 54.07% | 0 | 0.00 | 84161.65 | 0.000 | 70.19% | 78.68% | `{"filetypes/jar": 0.9076920747756958, "general": 0.9845328330993652}` |
| filetypes/pe† | max_rule | 1263848 | 159938 | 53.60% | 0 | 0.00 | 1873.04 | 0.000 | 69.79% | 58.81% | `{"filegroups/native": 0.999402974349452, "filetypes/pe": 0.999402974349452, "general": 0.999402974349452}` |
| filetypes/pptx | joint_or_at_fp_0 | 454 | 192 | 52.20% | 0 | 0.00 | 1548167.96 | 0.000 | 68.60% | 66.41% | `{"filegroups/documents": 0.7346557974815369, "filetypes/pptx": 0.09874933958053589}` |
| filetypes/powershell | learned_blend_at_fp_0 | 4850 | 2301 | 46.95% | 0 | 0.00 | 130107.91 | 0.000 | 63.90% | 64.02% | `{}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32813 | 50489 | 46.50% | 0 | 0.00 | 5933.26 | 0.000 | 63.48% | 78.92% | `{"filegroups/source": 0.8264152407646179, "filetypes/kotlin": 0.8846541047096252, "general": 0.9302482008934021}` |
| filetypes/xlsx | joint_or_at_fp_0 | 51918 | 1585 | 44.47% | 0 | 0.00 | 188826.69 | 0.000 | 61.56% | 46.12% | `{"filegroups/documents": 0.41709890961647034, "filetypes/xlsx": 0.92574143409729}` |
| filetypes/php | joint_or_at_fp_0 | 4233 | 120277 | 43.96% | 0 | 0.00 | 2490.66 | 0.000 | 61.08% | 98.09% | `{"filegroups/scripts": 0.9966230392456055, "filetypes/php": 0.9997223019599915, "general": 0.98988938331604}` |
