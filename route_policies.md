# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1745508752`
- Rows: 8028377 (2619304 malware, 5409073 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6240 | 524 | 97.88% | 0 | 0.00 | 570073.51 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.6954308152198792, "filetypes/rtf": 0.7239898443222046}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10656 | 2662 | 96.86% | 0 | 0.00 | 112473.60 | 0.000 | 98.40% | 97.48% | `{"filetypes/pkg-info": 0.4651772975921631}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.20% | 0 | 0.00 | 14427.88 | 0.000 | 97.01% | 96.20% | `{"filetypes/xls": 0.9140002131462097, "general": 0.9988190531730652}` |
| filetypes/gem | joint_or_at_fp_0 | 232 | 876 | 93.10% | 0 | 0.00 | 341394.49 | 0.000 | 96.43% | 98.56% | `{"filetypes/gem": 0.6840130090713501}` |
| filetypes/elf | joint_or_at_fp_0 | 189106 | 193999 | 93.00% | 0 | 0.00 | 1544.19 | 0.000 | 96.37% | 96.54% | `{"filegroups/native": 0.991166889667511, "filetypes/elf": 0.9943563342094421, "general": 0.9917684197425842}` |
| filetypes/package.json | joint_or_at_fp_0 | 19114 | 24775 | 90.32% | 0 | 0.00 | 12091.02 | 0.000 | 94.91% | 95.78% | `{"filegroups/config": 0.999531626701355, "filetypes/package.json": 0.99933260679245, "general": 0.9964730143547058}` |
| filetypes/tar | joint_or_at_fp_0 | 31245 | 41664 | 88.25% | 0 | 0.00 | 7189.96 | 0.000 | 93.76% | 94.96% | `{"filetypes/tar": 0.9804834127426147, "general": 0.996971070766449}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 460 | 85.71% | 0 | 0.00 | 649130.13 | 0.000 | 92.31% | 97.64% | `{"filetypes/chrome-manifest": 0.8841935992240906}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 462 | 80.71% | 0 | 0.00 | 646329.15 | 0.000 | 89.33% | 82.33% | `{"filegroups/documents": 0.5756855010986328, "filetypes/docx": 0.9677990078926086}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 211 | 79.22% | 0 | 0.00 | 1409747.01 | 0.000 | 88.40% | 79.97% | `{"filetypes/msi": 0.6352884769439697, "general": 0.9888006448745728}` |
| filetypes/macho | joint_or_at_fp_0 | 2647 | 12992 | 78.92% | 0 | 0.00 | 23055.63 | 0.000 | 88.22% | 96.43% | `{"filegroups/native": 0.8965191841125488, "filetypes/macho": 0.9906078577041626}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 300920 | 77.65% | 0 | 0.00 | 995.52 | 0.000 | 87.42% | 99.75% | `{"filetypes/python-bytecode": 0.9994853734970093, "general": 0.9836860299110413}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24567 | 74.69% | 0 | 0.00 | 12193.39 | 0.000 | 85.51% | 77.75% | `{"filegroups/documents": 0.8556629419326782, "filetypes/pdf": 0.902738094329834, "general": 0.9776129722595215}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.57% | 0 | 0.00 | 280894.17 | 0.000 | 84.77% | 78.53% | `{"filetypes/lnk": 0.9742423892021179, "general": 0.9985592365264893}` |
| filetypes/shell | joint_or_at_fp_0 | 15655 | 69835 | 70.55% | 0 | 0.00 | 4289.64 | 0.000 | 82.73% | 94.61% | `{"filegroups/scripts": 0.9927046895027161, "filetypes/shell": 0.899219274520874, "general": 0.9779383540153503}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 6051 | 67.18% | 0 | 0.00 | 49495.80 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.9649064540863037}` |
| filetypes/npm | joint_or_at_fp_0 | 1281 | 214 | 63.54% | 0 | 0.00 | 1390122.21 | 0.000 | 77.71% | 68.76% | `{"filetypes/npm": 0.8397960066795349, "general": 0.9554066061973572}` |
| filetypes/whl | joint_or_at_fp_0 | 835 | 4498 | 57.37% | 0 | 0.00 | 66579.26 | 0.000 | 72.91% | 93.32% | `{"filetypes/whl": 0.981730580329895}` |
| filetypes/crx | joint_or_at_fp_0 | 882 | 176 | 56.46% | 0 | 0.00 | 1687716.38 | 0.000 | 72.17% | 63.71% | `{"filetypes/crx": 0.9767345786094666, "general": 0.9219282865524292}` |
| filetypes/pe | joint_or_at_fp_0 | 1368564 | 167298 | 55.09% | 0 | 0.00 | 1790.64 | 0.000 | 71.04% | 59.98% | `{"filegroups/native": 0.9992542862892151, "filetypes/pe": 0.9973049163818359, "general": 0.9998183846473694}` |
| filetypes/powershell | joint_or_at_fp_0 | 5848 | 2570 | 53.13% | 0 | 0.00 | 116497.55 | 0.000 | 69.39% | 67.44% | `{"filegroups/scripts": 0.9945532083511353, "filetypes/powershell": 0.9870693683624268, "general": 0.9921095371246338}` |
| filetypes/javascript | joint_or_at_fp_0 | 126983 | 683050 | 51.84% | 0 | 0.00 | 438.58 | 0.000 | 68.28% | 92.45% | `{"filegroups/scripts": 0.9986749291419983, "filetypes/javascript": 0.9937307834625244, "general": 0.998189389705658}` |
| filetypes/perl | joint_or_at_fp_0 | 381 | 44293 | 51.18% | 0 | 0.00 | 6763.22 | 0.000 | 67.71% | 99.58% | `{"filegroups/scripts": 0.9694051742553711, "filetypes/perl": 0.9970625042915344}` |
| filetypes/php | joint_or_at_fp_0 | 5654 | 166868 | 49.73% | 0 | 0.00 | 1795.25 | 0.000 | 66.43% | 98.35% | `{"filegroups/scripts": 0.9898805618286133, "filetypes/php": 0.9939479827880859, "general": 0.8907710909843445}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32521 | 58538 | 48.71% | 0 | 0.00 | 5117.45 | 0.000 | 65.51% | 81.68% | `{"filegroups/source": 0.9380845427513123, "filetypes/kotlin": 0.9812876582145691, "general": 0.9345684051513672}` |
| filetypes/lua | joint_or_at_fp_0 | 99 | 19013 | 48.48% | 0 | 0.00 | 15754.99 | 0.000 | 65.31% | 99.73% | `{"filegroups/scripts": 0.9707030653953552, "filetypes/lua": 0.8253804445266724}` |
| filetypes/jar | joint_or_at_fp_0 | 3681 | 5473 | 46.37% | 0 | 0.00 | 54721.59 | 0.000 | 63.36% | 78.44% | `{"filetypes/jar": 0.9655675888061523, "general": 0.9621884226799011}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6594 | 42.41% | 0 | 0.00 | 45420.87 | 0.000 | 59.56% | 69.57% | `{"filegroups/documents": 0.9641605019569397, "general": 0.991355299949646}` |
| filetypes/ruby | joint_or_at_fp_0 | 249 | 29177 | 40.96% | 0 | 0.00 | 10266.92 | 0.000 | 58.12% | 99.50% | `{"filegroups/scripts": 0.9537885785102844, "filetypes/ruby": 0.9646695256233215}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 147 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 6240 | 524 | 97.88% | 0 | 0.00 | 570073.51 | 0.000 | 98.93% | 98.05% | `{"filegroups/documents": 0.6954308152198792, "filetypes/rtf": 0.7239898443222046}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10656 | 2662 | 96.86% | 0 | 0.00 | 112473.60 | 0.000 | 98.40% | 97.48% | `{"filetypes/pkg-info": 0.4651772975921631}` |
| filetypes/xls | joint_or_at_fp_0 | 39585 | 20762 | 94.20% | 0 | 0.00 | 14427.88 | 0.000 | 97.01% | 96.20% | `{"filetypes/xls": 0.9140002131462097, "general": 0.9988190531730652}` |
| filetypes/gem | joint_or_at_fp_0 | 232 | 876 | 93.10% | 0 | 0.00 | 341394.49 | 0.000 | 96.43% | 98.56% | `{"filetypes/gem": 0.6840130090713501}` |
| filetypes/elf | joint_or_at_fp_0 | 189106 | 193999 | 93.00% | 0 | 0.00 | 1544.19 | 0.000 | 96.37% | 96.54% | `{"filegroups/native": 0.991166889667511, "filetypes/elf": 0.9943563342094421, "general": 0.9917684197425842}` |
| filetypes/package.json | joint_or_at_fp_0 | 19114 | 24775 | 90.32% | 0 | 0.00 | 12091.02 | 0.000 | 94.91% | 95.78% | `{"filegroups/config": 0.999531626701355, "filetypes/package.json": 0.99933260679245, "general": 0.9964730143547058}` |
| filetypes/tar | joint_or_at_fp_0 | 31245 | 41664 | 88.25% | 0 | 0.00 | 7189.96 | 0.000 | 93.76% | 94.96% | `{"filetypes/tar": 0.9804834127426147, "general": 0.996971070766449}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 91 | 460 | 85.71% | 0 | 0.00 | 649130.13 | 0.000 | 92.31% | 97.64% | `{"filetypes/chrome-manifest": 0.8841935992240906}` |
| filetypes/docx | joint_or_at_fp_0 | 5055 | 462 | 80.71% | 0 | 0.00 | 646329.15 | 0.000 | 89.33% | 82.33% | `{"filegroups/documents": 0.5756855010986328, "filetypes/docx": 0.9677990078926086}` |
| filetypes/msi | joint_or_at_fp_0 | 5625 | 211 | 79.22% | 0 | 0.00 | 1409747.01 | 0.000 | 88.40% | 79.97% | `{"filetypes/msi": 0.6352884769439697, "general": 0.9888006448745728}` |
| filetypes/macho | joint_or_at_fp_0 | 2647 | 12992 | 78.92% | 0 | 0.00 | 23055.63 | 0.000 | 88.22% | 96.43% | `{"filegroups/native": 0.8965191841125488, "filetypes/macho": 0.9906078577041626}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3392 | 300920 | 77.65% | 0 | 0.00 | 995.52 | 0.000 | 87.42% | 99.75% | `{"filetypes/python-bytecode": 0.9994853734970093, "general": 0.9836860299110413}` |
| filetypes/pdf | joint_or_at_fp_0 | 178633 | 24567 | 74.69% | 0 | 0.00 | 12193.39 | 0.000 | 85.51% | 77.75% | `{"filegroups/documents": 0.8556629419326782, "filetypes/pdf": 0.902738094329834, "general": 0.9776129722595215}` |
| filetypes/lnk | joint_or_at_fp_0 | 4600 | 1065 | 73.57% | 0 | 0.00 | 280894.17 | 0.000 | 84.77% | 78.53% | `{"filetypes/lnk": 0.9742423892021179, "general": 0.9985592365264893}` |
| filetypes/shell | joint_or_at_fp_0 | 15655 | 69835 | 70.55% | 0 | 0.00 | 4289.64 | 0.000 | 82.73% | 94.61% | `{"filegroups/scripts": 0.9927046895027161, "filetypes/shell": 0.899219274520874, "general": 0.9779383540153503}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 6051 | 67.18% | 0 | 0.00 | 49495.80 | 0.000 | 80.37% | 99.30% | `{"filetypes/clojure": 0.9649064540863037}` |
| filetypes/npm | joint_or_at_fp_0 | 1281 | 214 | 63.54% | 0 | 0.00 | 1390122.21 | 0.000 | 77.71% | 68.76% | `{"filetypes/npm": 0.8397960066795349, "general": 0.9554066061973572}` |
| filetypes/whl | joint_or_at_fp_0 | 835 | 4498 | 57.37% | 0 | 0.00 | 66579.26 | 0.000 | 72.91% | 93.32% | `{"filetypes/whl": 0.981730580329895}` |
| filetypes/crx | joint_or_at_fp_0 | 882 | 176 | 56.46% | 0 | 0.00 | 1687716.38 | 0.000 | 72.17% | 63.71% | `{"filetypes/crx": 0.9767345786094666, "general": 0.9219282865524292}` |
| filetypes/pe | joint_or_at_fp_0 | 1368564 | 167298 | 55.09% | 0 | 0.00 | 1790.64 | 0.000 | 71.04% | 59.98% | `{"filegroups/native": 0.9992542862892151, "filetypes/pe": 0.9973049163818359, "general": 0.9998183846473694}` |
| filetypes/powershell | joint_or_at_fp_0 | 5848 | 2570 | 53.13% | 0 | 0.00 | 116497.55 | 0.000 | 69.39% | 67.44% | `{"filegroups/scripts": 0.9945532083511353, "filetypes/powershell": 0.9870693683624268, "general": 0.9921095371246338}` |
| filetypes/javascript | joint_or_at_fp_0 | 126983 | 683050 | 51.84% | 0 | 0.00 | 438.58 | 0.000 | 68.28% | 92.45% | `{"filegroups/scripts": 0.9986749291419983, "filetypes/javascript": 0.9937307834625244, "general": 0.998189389705658}` |
| filetypes/perl | joint_or_at_fp_0 | 381 | 44293 | 51.18% | 0 | 0.00 | 6763.22 | 0.000 | 67.71% | 99.58% | `{"filegroups/scripts": 0.9694051742553711, "filetypes/perl": 0.9970625042915344}` |
| filetypes/php | joint_or_at_fp_0 | 5654 | 166868 | 49.73% | 0 | 0.00 | 1795.25 | 0.000 | 66.43% | 98.35% | `{"filegroups/scripts": 0.9898805618286133, "filetypes/php": 0.9939479827880859, "general": 0.8907710909843445}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32521 | 58538 | 48.71% | 0 | 0.00 | 5117.45 | 0.000 | 65.51% | 81.68% | `{"filegroups/source": 0.9380845427513123, "filetypes/kotlin": 0.9812876582145691, "general": 0.9345684051513672}` |
| filetypes/lua | joint_or_at_fp_0 | 99 | 19013 | 48.48% | 0 | 0.00 | 15754.99 | 0.000 | 65.31% | 99.73% | `{"filegroups/scripts": 0.9707030653953552, "filetypes/lua": 0.8253804445266724}` |
| filetypes/jar | joint_or_at_fp_0 | 3681 | 5473 | 46.37% | 0 | 0.00 | 54721.59 | 0.000 | 63.36% | 78.44% | `{"filetypes/jar": 0.9655675888061523, "general": 0.9621884226799011}` |
| filetypes/ole | joint_or_at_fp_0 | 7390 | 6594 | 42.41% | 0 | 0.00 | 45420.87 | 0.000 | 59.56% | 69.57% | `{"filegroups/documents": 0.9641605019569397, "general": 0.991355299949646}` |
| filetypes/ruby | joint_or_at_fp_0 | 249 | 29177 | 40.96% | 0 | 0.00 | 10266.92 | 0.000 | 58.12% | 99.50% | `{"filegroups/scripts": 0.9537885785102844, "filetypes/ruby": 0.9646695256233215}` |
