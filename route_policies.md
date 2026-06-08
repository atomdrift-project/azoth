# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1670971082`
- Rows: 6899010 (2511611 malware, 4387399 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 140 | 11019 | 100.00% | 0 | 0.00 | 27183.28 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | learned_blend_at_fp_0 | 5888 | 507 | 98.18% | 0 | 0.00 | 589131.99 | 0.000 | 99.08% | 98.33% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 37236 | 20747 | 94.72% | 0 | 0.00 | 14438.31 | 0.000 | 97.29% | 96.61% | `{"filegroups/documents": 0.2616017460823059, "filetypes/xls": 0.7707599997520447}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10644 | 1924 | 94.71% | 0 | 0.00 | 155582.19 | 0.000 | 97.28% | 95.52% | `{"filetypes/pkg-info": 0.9867424964904785, "general": 0.9942096471786499}` |
| filetypes/elf | joint_or_at_fp_0 | 179697 | 170249 | 93.94% | 0 | 0.00 | 1759.60 | 0.000 | 96.87% | 96.89% | `{"filegroups/native": 0.9550641775131226, "filetypes/elf": 0.9960418939590454, "general": 0.9921107292175293}` |
| filetypes/tar | joint_or_at_fp_0 | 31218 | 23953 | 87.59% | 0 | 0.00 | 12505.93 | 0.000 | 93.38% | 92.98% | `{"filetypes/tar": 0.9857552647590637, "general": 0.9968264698982239}` |
| filetypes/package.json | joint_or_at_fp_0 | 18438 | 21473 | 86.71% | 0 | 0.00 | 13950.19 | 0.000 | 92.88% | 93.86% | `{"filegroups/config": 0.9997603297233582, "general": 0.9965143203735352}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2887 | 122401 | 85.56% | 0 | 0.00 | 2447.44 | 0.000 | 92.22% | 99.67% | `{"filetypes/python-bytecode": 0.9991198182106018, "general": 0.9913279414176941}` |
| filetypes/ole | joint_or_at_fp_0 | 6930 | 6256 | 81.95% | 0 | 0.00 | 47874.28 | 0.000 | 90.08% | 90.51% | `{"filegroups/documents": 0.23912371695041656, "filetypes/ole": 0.998405396938324}` |
| filetypes/macho | joint_or_at_fp_0 | 2591 | 11727 | 81.28% | 0 | 0.00 | 25542.34 | 0.000 | 89.67% | 96.61% | `{"filegroups/native": 0.6322687268257141, "filetypes/macho": 0.9852601289749146, "general": 0.9906294345855713}` |
| filetypes/docx | joint_or_at_fp_0 | 4775 | 434 | 79.77% | 0 | 0.00 | 687884.06 | 0.000 | 88.75% | 81.46% | `{"filegroups/documents": 0.37744149565696716, "filetypes/docx": 0.9539022445678711, "general": 0.9804851412773132}` |
| filetypes/lnk | joint_or_at_fp_0 | 4362 | 1055 | 73.25% | 0 | 0.00 | 283552.89 | 0.000 | 84.56% | 78.46% | `{"filetypes/lnk": 0.9096791744232178, "general": 0.9994261264801025}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 70 | 448 | 72.86% | 0 | 0.00 | 666459.48 | 0.000 | 84.30% | 96.33% | `{"filetypes/chrome-manifest": 0.9461048245429993}` |
| filetypes/msi | joint_or_at_fp_0 | 5328 | 179 | 72.60% | 0 | 0.00 | 1659666.67 | 0.000 | 84.12% | 73.49% | `{"filetypes/msi": 0.7181465029716492, "general": 0.9974523186683655}` |
| filetypes/clojure | joint_or_at_fp_0 | 125 | 5341 | 70.40% | 0 | 0.00 | 56073.62 | 0.000 | 82.63% | 99.32% | `{"filetypes/clojure": 0.9887803792953491, "general": 0.0453341118991375}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18432 | 69.07% | 0 | 0.00 | 16251.57 | 0.000 | 81.71% | 99.84% | `{"filegroups/scripts": 0.9902631044387817, "filetypes/lua": 0.6899411678314209}` |
| filetypes/shell | joint_or_at_fp_0 | 14519 | 60292 | 68.45% | 0 | 0.00 | 4968.58 | 0.000 | 81.27% | 93.88% | `{"filegroups/scripts": 0.9970836043357849, "filetypes/shell": 0.9518154859542847, "general": 0.9895842671394348}` |
| filetypes/javascript | joint_or_at_fp_0 | 118857 | 605997 | 63.73% | 0 | 0.00 | 494.35 | 0.000 | 77.85% | 94.05% | `{"filegroups/scripts": 0.9990768432617188, "filetypes/javascript": 0.9577401280403137, "general": 0.9987104535102844}` |
| filetypes/java_class | joint_or_at_fp_0 | 1689 | 705477 | 61.93% | 0 | 0.00 | 424.64 | 0.000 | 76.49% | 99.91% | `{"filetypes/java_class": 0.9712562561035156, "general": 0.9961003065109253}` |
| filetypes/pe | joint_or_at_fp_0 | 1329010 | 160061 | 57.17% | 0 | 0.00 | 1871.60 | 0.000 | 72.75% | 61.78% | `{"filegroups/native": 0.9981610774993896, "filetypes/pe": 0.9989663362503052, "general": 0.9999143481254578}` |
| filetypes/vbs | joint_or_at_fp_0 | 11183 | 3306 | 56.24% | 0 | 0.00 | 90573.97 | 0.000 | 71.99% | 66.22% | `{"filetypes/vbs": 0.9980120658874512, "general": 0.996894359588623}` |
| filetypes/jar | joint_or_at_fp_0 | 3442 | 3781 | 55.29% | 0 | 0.00 | 79199.84 | 0.000 | 71.21% | 78.69% | `{"filetypes/jar": 0.8647834658622742, "general": 0.9909077286720276}` |
| filetypes/ruby | joint_or_at_fp_0 | 154 | 25671 | 52.60% | 0 | 0.00 | 11669.03 | 0.000 | 68.94% | 99.72% | `{"filegroups/scripts": 0.9935958981513977, "filetypes/ruby": 0.9971883893013}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32747 | 52001 | 52.56% | 0 | 0.00 | 5760.75 | 0.000 | 68.90% | 81.67% | `{"filegroups/source": 0.9487637877464294, "general": 0.9704094529151917}` |
| filetypes/powershell | joint_or_at_fp_0 | 5372 | 2394 | 51.86% | 0 | 0.00 | 125056.75 | 0.000 | 68.30% | 66.70% | `{"filegroups/scripts": 0.9982317090034485, "filetypes/powershell": 0.9913622140884399, "general": 0.9974666833877563}` |
| filetypes/crx | learned_blend_at_fp_0 | 694 | 79 | 51.15% | 0 | 0.00 | 3721067.61 | 0.000 | 67.68% | 56.14% | `{}` |
| filetypes/perl | joint_or_at_fp_0 | 333 | 39777 | 48.65% | 0 | 0.00 | 7531.03 | 0.000 | 65.45% | 99.57% | `{"filegroups/scripts": 0.9969062209129333, "filetypes/perl": 0.9965039491653442, "general": 0.9910047054290771}` |
| filetypes/python | joint_or_at_fp_0 | 20622 | 197433 | 48.39% | 0 | 0.00 | 1517.33 | 0.000 | 65.22% | 95.12% | `{"filegroups/scripts": 0.9986118078231812, "filetypes/python": 0.9990776181221008, "general": 0.9968701601028442}` |
| filetypes/rar | calibrate_inherited | 20647 | 4 | 48.19% | 0 | 0.00 | 52712919.55 | 0.000 | 65.04% | 48.20% | `{"general": 0.9996287299996618}` |
| filetypes/php | joint_or_at_fp_0 | 5068 | 147446 | 46.49% | 0 | 0.00 | 2031.73 | 0.000 | 63.47% | 98.22% | `{"filegroups/scripts": 0.9989074468612671, "filetypes/php": 0.9980788230895996, "general": 0.9855746030807495}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 140 | 11019 | 100.00% | 0 | 0.00 | 27183.28 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | learned_blend_at_fp_0 | 5888 | 507 | 98.18% | 0 | 0.00 | 589131.99 | 0.000 | 99.08% | 98.33% | `{}` |
| filetypes/xls | joint_or_at_fp_0 | 37236 | 20747 | 94.72% | 0 | 0.00 | 14438.31 | 0.000 | 97.29% | 96.61% | `{"filegroups/documents": 0.2616017460823059, "filetypes/xls": 0.7707599997520447}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10644 | 1924 | 94.71% | 0 | 0.00 | 155582.19 | 0.000 | 97.28% | 95.52% | `{"filetypes/pkg-info": 0.9867424964904785, "general": 0.9942096471786499}` |
| filetypes/elf | joint_or_at_fp_0 | 179697 | 170249 | 93.94% | 0 | 0.00 | 1759.60 | 0.000 | 96.87% | 96.89% | `{"filegroups/native": 0.9550641775131226, "filetypes/elf": 0.9960418939590454, "general": 0.9921107292175293}` |
| filetypes/tar | joint_or_at_fp_0 | 31218 | 23953 | 87.59% | 0 | 0.00 | 12505.93 | 0.000 | 93.38% | 92.98% | `{"filetypes/tar": 0.9857552647590637, "general": 0.9968264698982239}` |
| filetypes/package.json | joint_or_at_fp_0 | 18438 | 21473 | 86.71% | 0 | 0.00 | 13950.19 | 0.000 | 92.88% | 93.86% | `{"filegroups/config": 0.9997603297233582, "general": 0.9965143203735352}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 2887 | 122401 | 85.56% | 0 | 0.00 | 2447.44 | 0.000 | 92.22% | 99.67% | `{"filetypes/python-bytecode": 0.9991198182106018, "general": 0.9913279414176941}` |
| filetypes/ole | joint_or_at_fp_0 | 6930 | 6256 | 81.95% | 0 | 0.00 | 47874.28 | 0.000 | 90.08% | 90.51% | `{"filegroups/documents": 0.23912371695041656, "filetypes/ole": 0.998405396938324}` |
| filetypes/macho | joint_or_at_fp_0 | 2591 | 11727 | 81.28% | 0 | 0.00 | 25542.34 | 0.000 | 89.67% | 96.61% | `{"filegroups/native": 0.6322687268257141, "filetypes/macho": 0.9852601289749146, "general": 0.9906294345855713}` |
| filetypes/docx | joint_or_at_fp_0 | 4775 | 434 | 79.77% | 0 | 0.00 | 687884.06 | 0.000 | 88.75% | 81.46% | `{"filegroups/documents": 0.37744149565696716, "filetypes/docx": 0.9539022445678711, "general": 0.9804851412773132}` |
| filetypes/lnk | joint_or_at_fp_0 | 4362 | 1055 | 73.25% | 0 | 0.00 | 283552.89 | 0.000 | 84.56% | 78.46% | `{"filetypes/lnk": 0.9096791744232178, "general": 0.9994261264801025}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 70 | 448 | 72.86% | 0 | 0.00 | 666459.48 | 0.000 | 84.30% | 96.33% | `{"filetypes/chrome-manifest": 0.9461048245429993}` |
| filetypes/msi | joint_or_at_fp_0 | 5328 | 179 | 72.60% | 0 | 0.00 | 1659666.67 | 0.000 | 84.12% | 73.49% | `{"filetypes/msi": 0.7181465029716492, "general": 0.9974523186683655}` |
| filetypes/clojure | joint_or_at_fp_0 | 125 | 5341 | 70.40% | 0 | 0.00 | 56073.62 | 0.000 | 82.63% | 99.32% | `{"filetypes/clojure": 0.9887803792953491, "general": 0.0453341118991375}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18432 | 69.07% | 0 | 0.00 | 16251.57 | 0.000 | 81.71% | 99.84% | `{"filegroups/scripts": 0.9902631044387817, "filetypes/lua": 0.6899411678314209}` |
| filetypes/shell | joint_or_at_fp_0 | 14519 | 60292 | 68.45% | 0 | 0.00 | 4968.58 | 0.000 | 81.27% | 93.88% | `{"filegroups/scripts": 0.9970836043357849, "filetypes/shell": 0.9518154859542847, "general": 0.9895842671394348}` |
| filetypes/javascript | joint_or_at_fp_0 | 118857 | 605997 | 63.73% | 0 | 0.00 | 494.35 | 0.000 | 77.85% | 94.05% | `{"filegroups/scripts": 0.9990768432617188, "filetypes/javascript": 0.9577401280403137, "general": 0.9987104535102844}` |
| filetypes/java_class | joint_or_at_fp_0 | 1689 | 705477 | 61.93% | 0 | 0.00 | 424.64 | 0.000 | 76.49% | 99.91% | `{"filetypes/java_class": 0.9712562561035156, "general": 0.9961003065109253}` |
| filetypes/pe | joint_or_at_fp_0 | 1329010 | 160061 | 57.17% | 0 | 0.00 | 1871.60 | 0.000 | 72.75% | 61.78% | `{"filegroups/native": 0.9981610774993896, "filetypes/pe": 0.9989663362503052, "general": 0.9999143481254578}` |
| filetypes/vbs | joint_or_at_fp_0 | 11183 | 3306 | 56.24% | 0 | 0.00 | 90573.97 | 0.000 | 71.99% | 66.22% | `{"filetypes/vbs": 0.9980120658874512, "general": 0.996894359588623}` |
| filetypes/jar | joint_or_at_fp_0 | 3442 | 3781 | 55.29% | 0 | 0.00 | 79199.84 | 0.000 | 71.21% | 78.69% | `{"filetypes/jar": 0.8647834658622742, "general": 0.9909077286720276}` |
| filetypes/ruby | joint_or_at_fp_0 | 154 | 25671 | 52.60% | 0 | 0.00 | 11669.03 | 0.000 | 68.94% | 99.72% | `{"filegroups/scripts": 0.9935958981513977, "filetypes/ruby": 0.9971883893013}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32747 | 52001 | 52.56% | 0 | 0.00 | 5760.75 | 0.000 | 68.90% | 81.67% | `{"filegroups/source": 0.9487637877464294, "general": 0.9704094529151917}` |
| filetypes/powershell | joint_or_at_fp_0 | 5372 | 2394 | 51.86% | 0 | 0.00 | 125056.75 | 0.000 | 68.30% | 66.70% | `{"filegroups/scripts": 0.9982317090034485, "filetypes/powershell": 0.9913622140884399, "general": 0.9974666833877563}` |
| filetypes/crx | learned_blend_at_fp_0 | 694 | 79 | 51.15% | 0 | 0.00 | 3721067.61 | 0.000 | 67.68% | 56.14% | `{}` |
| filetypes/perl | joint_or_at_fp_0 | 333 | 39777 | 48.65% | 0 | 0.00 | 7531.03 | 0.000 | 65.45% | 99.57% | `{"filegroups/scripts": 0.9969062209129333, "filetypes/perl": 0.9965039491653442, "general": 0.9910047054290771}` |
| filetypes/python | joint_or_at_fp_0 | 20622 | 197433 | 48.39% | 0 | 0.00 | 1517.33 | 0.000 | 65.22% | 95.12% | `{"filegroups/scripts": 0.9986118078231812, "filetypes/python": 0.9990776181221008, "general": 0.9968701601028442}` |
| filetypes/rar | calibrate_inherited | 20647 | 4 | 48.30% | 0 | 0.00 | 52712919.55 | 0.000 | 65.14% | 48.31% | `{"general": 0.9996271280062199}` |
| filetypes/php | joint_or_at_fp_0 | 5068 | 147446 | 46.49% | 0 | 0.00 | 2031.73 | 0.000 | 63.47% | 98.22% | `{"filegroups/scripts": 0.9989074468612671, "filetypes/php": 0.9980788230895996, "general": 0.9855746030807495}` |
