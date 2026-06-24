# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1841440894`
- Rows: 8434434 (2612902 malware, 5821532 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{"filetypes/html": 0.9971267580986023}` |
| filetypes/crx | learned_blend_at_fp_0 | 802 | 184 | 98.13% | 0 | 0.00 | 1614933.21 | 0.000 | 99.06% | 98.48% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 525 | 97.98% | 0 | 0.00 | 568990.75 | 0.000 | 98.98% | 98.14% | `{"filegroups/documents": 0.07487976551055908, "filetypes/rtf": 0.1712195873260498}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 3243 | 96.76% | 0 | 0.00 | 92332.69 | 0.000 | 98.35% | 97.52% | `{"filetypes/pkg-info": 0.11785441637039185}` |
| filetypes/gem | joint_or_at_fp_0 | 769 | 1099 | 95.58% | 0 | 0.00 | 272215.92 | 0.000 | 97.74% | 98.18% | `{"filetypes/gem": 0.9908872842788696, "general": 0.9284250140190125}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 90 | 273 | 94.44% | 0 | 0.00 | 1091339.04 | 0.000 | 97.14% | 98.62% | `{"filetypes/chrome-manifest": 0.7903823256492615}` |
| filetypes/xls | joint_or_at_fp_0 | 39675 | 20762 | 94.30% | 0 | 0.00 | 14427.88 | 0.000 | 97.07% | 96.26% | `{"filegroups/documents": 0.9992794394493103, "filetypes/xls": 0.9000883102416992}` |
| filetypes/elf | joint_or_at_fp_0 | 189551 | 235302 | 89.19% | 0 | 0.00 | 1273.14 | 0.000 | 94.28% | 95.18% | `{"filegroups/native": 0.9774785041809082, "filetypes/elf": 0.9993322491645813, "general": 0.9910392165184021}` |
| filetypes/tar | joint_or_at_fp_0 | 30641 | 48479 | 85.40% | 0 | 0.00 | 6179.25 | 0.000 | 92.13% | 94.35% | `{"filetypes/tar": 0.9949797987937927, "general": 0.9931005835533142}` |
| filetypes/docx | joint_or_at_fp_0 | 4965 | 402 | 82.78% | 0 | 0.00 | 742437.25 | 0.000 | 90.58% | 84.07% | `{"filegroups/documents": 0.5927375555038452, "filetypes/docx": 0.8563660979270935}` |
| filetypes/package.json | joint_or_at_fp_0 | 19381 | 27228 | 82.14% | 0 | 0.00 | 11001.79 | 0.000 | 90.19% | 92.57% | `{"filegroups/config": 0.9999376535415649, "filetypes/package.json": 0.9975766539573669, "general": 0.9966315627098083}` |
| filetypes/msi | joint_or_at_fp_0 | 5646 | 221 | 81.00% | 0 | 0.00 | 1346388.96 | 0.000 | 89.50% | 81.71% | `{"filetypes/msi": 0.5515719056129456, "general": 0.9965694546699524}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6692 | 77.10% | 0 | 0.00 | 44755.86 | 0.000 | 87.07% | 87.98% | `{"filegroups/documents": 0.7193253040313721, "filetypes/ole": 0.9976603984832764, "general": 0.9811504483222961}` |
| filetypes/lnk | joint_or_at_fp_0 | 4614 | 1065 | 74.40% | 0 | 0.00 | 280894.17 | 0.000 | 85.32% | 79.20% | `{"filetypes/lnk": 0.9565479755401611, "general": 0.9990794658660889}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24688 | 73.99% | 0 | 0.00 | 12133.63 | 0.000 | 85.05% | 77.15% | `{"filegroups/documents": 0.9491792321205139, "filetypes/pdf": 0.9200966954231262, "general": 0.9865750670433044}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3417 | 412910 | 73.28% | 0 | 0.00 | 725.51 | 0.000 | 84.58% | 99.78% | `{"filetypes/python-bytecode": 0.9985591769218445}` |
| filetypes/shell | joint_or_at_fp_0 | 15736 | 74257 | 71.31% | 0 | 0.00 | 4034.19 | 0.000 | 83.26% | 94.98% | `{"filegroups/scripts": 0.984512448310852, "filetypes/shell": 0.964005172252655, "general": 0.9549415707588196}` |
| filetypes/macho | joint_or_at_fp_0 | 2694 | 13877 | 69.97% | 0 | 0.00 | 21585.42 | 0.000 | 82.33% | 95.12% | `{"filegroups/native": 0.9462513327598572, "filetypes/macho": 0.9916120767593384, "general": 0.9688243269920349}` |
| filetypes/npm | joint_or_at_fp_0 | 1639 | 826 | 65.53% | 0 | 0.00 | 362022.56 | 0.000 | 79.17% | 77.08% | `{"filetypes/npm": 0.9795939922332764, "general": 0.9821584224700928}` |
| filetypes/whl | joint_or_at_fp_0 | 2440 | 4655 | 61.31% | 0 | 0.00 | 64334.45 | 0.000 | 76.02% | 86.69% | `{"filetypes/whl": 0.9884241223335266, "general": 0.9202864170074463}` |
| filetypes/javascript | joint_or_at_fp_0 | 126572 | 728525 | 58.84% | 0 | 0.00 | 411.20 | 0.000 | 74.09% | 93.91% | `{"filegroups/scripts": 0.9955909252166748, "filetypes/javascript": 0.9904221296310425, "general": 0.998917818069458}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45085 | 58.40% | 0 | 0.00 | 6644.41 | 0.000 | 73.74% | 99.65% | `{"filegroups/scripts": 0.9679048657417297, "filetypes/perl": 0.9751080870628357}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19269 | 57.84% | 0 | 0.00 | 15545.69 | 0.000 | 73.29% | 99.78% | `{"filegroups/scripts": 0.9497441053390503, "filetypes/lua": 0.9422183036804199, "general": 0.9279492497444153}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32504 | 58244 | 53.46% | 0 | 0.00 | 5143.29 | 0.000 | 69.67% | 83.33% | `{"filegroups/source": 0.8607184290885925, "filetypes/kotlin": 0.828954815864563, "general": 0.9909356236457825}` |
| filetypes/php | joint_or_at_fp_0 | 5842 | 173434 | 50.27% | 0 | 0.00 | 1727.29 | 0.000 | 66.91% | 98.38% | `{"filegroups/scripts": 0.9822807908058167, "filetypes/php": 0.9935175180435181, "general": 0.9620183706283569}` |
| filetypes/jar | joint_or_at_fp_0 | 3688 | 7901 | 44.85% | 0 | 0.00 | 37908.68 | 0.000 | 61.92% | 82.45% | `{"filetypes/jar": 0.9735865592956543, "general": 0.972445547580719}` |
| filetypes/pe | joint_or_at_fp_0 | 1370223 | 174255 | 41.86% | 0 | 0.00 | 1719.15 | 0.000 | 59.01% | 48.42% | `{"filegroups/native": 0.9991843104362488, "filetypes/pe": 0.9997188448905945, "general": 0.999767541885376}` |
| filetypes/python | joint_or_at_fp_0 | 20784 | 256351 | 41.68% | 0 | 0.00 | 1168.60 | 0.000 | 58.84% | 95.63% | `{"filegroups/scripts": 0.998991072177887, "filetypes/python": 0.9996987581253052, "general": 0.9939645528793335}` |
| filetypes/ruby | joint_or_at_fp_0 | 259 | 39003 | 37.07% | 0 | 0.00 | 7680.48 | 0.000 | 54.08% | 99.58% | `{"filegroups/scripts": 0.9930518865585327, "filetypes/ruby": 0.9454759955406189}` |
| filetypes/powershell | joint_or_at_fp_0 | 5882 | 2589 | 36.20% | 0 | 0.00 | 115643.10 | 0.000 | 53.15% | 55.70% | `{"filegroups/scripts": 0.9968133568763733, "filetypes/powershell": 0.9954802989959717, "general": 0.9974327683448792}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{"filetypes/html": 0.9971267580986023}` |
| filetypes/crx | learned_blend_at_fp_0 | 802 | 184 | 98.13% | 0 | 0.00 | 1614933.21 | 0.000 | 99.06% | 98.48% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 525 | 97.98% | 0 | 0.00 | 568990.75 | 0.000 | 98.98% | 98.14% | `{"filegroups/documents": 0.07487976551055908, "filetypes/rtf": 0.1712195873260498}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 3243 | 96.76% | 0 | 0.00 | 92332.69 | 0.000 | 98.35% | 97.52% | `{"filetypes/pkg-info": 0.11785441637039185}` |
| filetypes/gem | joint_or_at_fp_0 | 769 | 1099 | 95.58% | 0 | 0.00 | 272215.92 | 0.000 | 97.74% | 98.18% | `{"filetypes/gem": 0.9908872842788696, "general": 0.9284250140190125}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 90 | 273 | 94.44% | 0 | 0.00 | 1091339.04 | 0.000 | 97.14% | 98.62% | `{"filetypes/chrome-manifest": 0.7903823256492615}` |
| filetypes/xls | joint_or_at_fp_0 | 39675 | 20762 | 94.30% | 0 | 0.00 | 14427.88 | 0.000 | 97.07% | 96.26% | `{"filegroups/documents": 0.9992794394493103, "filetypes/xls": 0.9000883102416992}` |
| filetypes/elf | joint_or_at_fp_0 | 189551 | 235302 | 89.19% | 0 | 0.00 | 1273.14 | 0.000 | 94.28% | 95.18% | `{"filegroups/native": 0.9774785041809082, "filetypes/elf": 0.9993322491645813, "general": 0.9910392165184021}` |
| filetypes/tar | joint_or_at_fp_0 | 30641 | 48479 | 85.40% | 0 | 0.00 | 6179.25 | 0.000 | 92.13% | 94.35% | `{"filetypes/tar": 0.9949797987937927, "general": 0.9931005835533142}` |
| filetypes/docx | joint_or_at_fp_0 | 4965 | 402 | 82.78% | 0 | 0.00 | 742437.25 | 0.000 | 90.58% | 84.07% | `{"filegroups/documents": 0.5927375555038452, "filetypes/docx": 0.8563660979270935}` |
| filetypes/package.json | joint_or_at_fp_0 | 19381 | 27228 | 82.14% | 0 | 0.00 | 11001.79 | 0.000 | 90.19% | 92.57% | `{"filegroups/config": 0.9999376535415649, "filetypes/package.json": 0.9975766539573669, "general": 0.9966315627098083}` |
| filetypes/msi | joint_or_at_fp_0 | 5646 | 221 | 81.00% | 0 | 0.00 | 1346388.96 | 0.000 | 89.50% | 81.71% | `{"filetypes/msi": 0.5515719056129456, "general": 0.9965694546699524}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6692 | 77.10% | 0 | 0.00 | 44755.86 | 0.000 | 87.07% | 87.98% | `{"filegroups/documents": 0.7193253040313721, "filetypes/ole": 0.9976603984832764, "general": 0.9811504483222961}` |
| filetypes/lnk | joint_or_at_fp_0 | 4614 | 1065 | 74.40% | 0 | 0.00 | 280894.17 | 0.000 | 85.32% | 79.20% | `{"filetypes/lnk": 0.9565479755401611, "general": 0.9990794658660889}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24688 | 73.99% | 0 | 0.00 | 12133.63 | 0.000 | 85.05% | 77.15% | `{"filegroups/documents": 0.9491792321205139, "filetypes/pdf": 0.9200966954231262, "general": 0.9865750670433044}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3417 | 412910 | 73.28% | 0 | 0.00 | 725.51 | 0.000 | 84.58% | 99.78% | `{"filetypes/python-bytecode": 0.9985591769218445}` |
| filetypes/shell | joint_or_at_fp_0 | 15736 | 74257 | 71.31% | 0 | 0.00 | 4034.19 | 0.000 | 83.26% | 94.98% | `{"filegroups/scripts": 0.984512448310852, "filetypes/shell": 0.964005172252655, "general": 0.9549415707588196}` |
| filetypes/macho | joint_or_at_fp_0 | 2694 | 13877 | 69.97% | 0 | 0.00 | 21585.42 | 0.000 | 82.33% | 95.12% | `{"filegroups/native": 0.9462513327598572, "filetypes/macho": 0.9916120767593384, "general": 0.9688243269920349}` |
| filetypes/npm | joint_or_at_fp_0 | 1639 | 826 | 65.53% | 0 | 0.00 | 362022.56 | 0.000 | 79.17% | 77.08% | `{"filetypes/npm": 0.9795939922332764, "general": 0.9821584224700928}` |
| filetypes/whl | joint_or_at_fp_0 | 2440 | 4655 | 61.31% | 0 | 0.00 | 64334.45 | 0.000 | 76.02% | 86.69% | `{"filetypes/whl": 0.9884241223335266, "general": 0.9202864170074463}` |
| filetypes/javascript | joint_or_at_fp_0 | 126572 | 728525 | 58.84% | 0 | 0.00 | 411.20 | 0.000 | 74.09% | 93.91% | `{"filegroups/scripts": 0.9955909252166748, "filetypes/javascript": 0.9904221296310425, "general": 0.998917818069458}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 45085 | 58.40% | 0 | 0.00 | 6644.41 | 0.000 | 73.74% | 99.65% | `{"filegroups/scripts": 0.9679048657417297, "filetypes/perl": 0.9751080870628357}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19269 | 57.84% | 0 | 0.00 | 15545.69 | 0.000 | 73.29% | 99.78% | `{"filegroups/scripts": 0.9497441053390503, "filetypes/lua": 0.9422183036804199, "general": 0.9279492497444153}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32504 | 58244 | 53.46% | 0 | 0.00 | 5143.29 | 0.000 | 69.67% | 83.33% | `{"filegroups/source": 0.8607184290885925, "filetypes/kotlin": 0.828954815864563, "general": 0.9909356236457825}` |
| filetypes/php | joint_or_at_fp_0 | 5842 | 173434 | 50.27% | 0 | 0.00 | 1727.29 | 0.000 | 66.91% | 98.38% | `{"filegroups/scripts": 0.9822807908058167, "filetypes/php": 0.9935175180435181, "general": 0.9620183706283569}` |
| filetypes/jar | joint_or_at_fp_0 | 3688 | 7901 | 44.85% | 0 | 0.00 | 37908.68 | 0.000 | 61.92% | 82.45% | `{"filetypes/jar": 0.9735865592956543, "general": 0.972445547580719}` |
| filetypes/pe | joint_or_at_fp_0 | 1370223 | 174255 | 41.86% | 0 | 0.00 | 1719.15 | 0.000 | 59.01% | 48.42% | `{"filegroups/native": 0.9991843104362488, "filetypes/pe": 0.9997188448905945, "general": 0.999767541885376}` |
| filetypes/python | joint_or_at_fp_0 | 20784 | 256351 | 41.68% | 0 | 0.00 | 1168.60 | 0.000 | 58.84% | 95.63% | `{"filegroups/scripts": 0.998991072177887, "filetypes/python": 0.9996987581253052, "general": 0.9939645528793335}` |
| filetypes/ruby | joint_or_at_fp_0 | 259 | 39003 | 37.07% | 0 | 0.00 | 7680.48 | 0.000 | 54.08% | 99.58% | `{"filegroups/scripts": 0.9930518865585327, "filetypes/ruby": 0.9454759955406189}` |
| filetypes/powershell | joint_or_at_fp_0 | 5882 | 2589 | 36.20% | 0 | 0.00 | 115643.10 | 0.000 | 53.15% | 55.70% | `{"filegroups/scripts": 0.9968133568763733, "filetypes/powershell": 0.9954802989959717, "general": 0.9974327683448792}` |
