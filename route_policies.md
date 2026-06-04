# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1658031131`
- Rows: 6710141 (2491517 malware, 4218624 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 10847 | 100.00% | 0 | 0.00 | 27614.26 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9956511855125427}` |
| filetypes/rtf | joint_or_at_fp_0 | 5865 | 502 | 98.81% | 0 | 0.00 | 594982.34 | 0.000 | 99.40% | 98.90% | `{"filegroups/documents": 0.46621882915496826, "filetypes/rtf": 0.14464563131332397}` |
| filetypes/batch | joint_or_at_fp_0 | 176358 | 4798 | 97.53% | 0 | 0.00 | 62417.62 | 0.000 | 98.75% | 97.60% | `{"filegroups/scripts": 0.9979010820388794, "filetypes/batch": 0.9972212314605713, "general": 0.9972652792930603}` |
| filetypes/elf | learned_blend_at_fp_0 | 178960 | 163743 | 95.91% | 0 | 0.00 | 1829.52 | 0.000 | 97.91% | 97.86% | `{}` |
| filetypes/xls | learned_blend_at_fp_0 | 37051 | 20747 | 93.61% | 0 | 0.00 | 14438.31 | 0.000 | 96.70% | 95.90% | `{}` |
| filetypes/python-bytecode | learned_blend_at_fp_0 | 2722 | 86146 | 93.53% | 0 | 0.00 | 3477.45 | 0.000 | 96.66% | 99.80% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 18353 | 20467 | 90.00% | 0 | 0.00 | 14635.82 | 0.000 | 94.74% | 95.27% | `{"filegroups/config": 0.9999018907546997, "filetypes/package.json": 0.9982081651687622, "general": 0.9970642328262329}` |
| filetypes/tar | learned_blend_at_fp_0 | 31043 | 22349 | 89.64% | 0 | 0.00 | 13403.43 | 0.000 | 94.54% | 93.98% | `{}` |
| filetypes/macho | learned_blend_at_fp_0 | 2583 | 11579 | 84.44% | 0 | 0.00 | 25868.77 | 0.000 | 91.56% | 97.16% | `{}` |
| filetypes/lnk | learned_blend_at_fp_0 | 4344 | 1055 | 83.63% | 0 | 0.00 | 283552.89 | 0.000 | 91.09% | 86.83% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 6887 | 6214 | 82.00% | 0 | 0.00 | 48197.78 | 0.000 | 90.11% | 90.54% | `{"filegroups/documents": 0.7249563336372375, "filetypes/ole": 0.9786415696144104}` |
| filetypes/docx | joint_or_at_fp_0 | 4756 | 433 | 81.94% | 0 | 0.00 | 689467.22 | 0.000 | 90.07% | 83.45% | `{"filegroups/documents": 0.9727789163589478, "filetypes/docx": 0.6076767444610596, "general": 0.9669691324234009}` |
| filetypes/clojure | learned_blend_at_fp_0 | 121 | 5183 | 81.82% | 0 | 0.00 | 57782.49 | 0.000 | 90.00% | 99.59% | `{}` |
| filetypes/pkg-info | learned_blend_at_fp_0 | 10636 | 1782 | 80.10% | 0 | 0.00 | 167969.45 | 0.000 | 88.95% | 82.95% | `{}` |
| filetypes/shell | learned_blend_at_fp_0 | 14262 | 58885 | 79.46% | 0 | 0.00 | 5087.30 | 0.000 | 88.55% | 95.99% | `{}` |
| filetypes/jar | joint_or_at_fp_0 | 3397 | 3737 | 71.21% | 0 | 0.00 | 80131.97 | 0.000 | 83.18% | 86.29% | `{"filetypes/jar": 0.6623266935348511, "general": 0.9993686079978943}` |
| filetypes/crx | joint_or_at_fp_0 | 622 | 79 | 65.11% | 0 | 0.00 | 3721067.61 | 0.000 | 78.87% | 69.04% | `{"filetypes/crx": 0.9098513126373291, "general": 0.9899091124534607}` |
| filetypes/perl | learned_blend_at_fp_0 | 316 | 39244 | 62.97% | 0 | 0.00 | 7633.31 | 0.000 | 77.28% | 99.70% | `{}` |
| filetypes/javascript | learned_blend_at_fp_0 | 116755 | 582359 | 59.36% | 0 | 0.00 | 514.41 | 0.000 | 74.50% | 93.21% | `{}` |
| filetypes/ruby | joint_or_at_fp_0 | 118 | 24970 | 57.63% | 0 | 0.00 | 11996.61 | 0.000 | 73.12% | 99.80% | `{"filegroups/scripts": 0.9891042709350586, "filetypes/ruby": 0.9992208480834961, "general": 0.9624097943305969}` |
| filetypes/php | joint_or_at_fp_0 | 4271 | 145907 | 52.49% | 0 | 0.00 | 2053.16 | 0.000 | 68.85% | 98.65% | `{"filegroups/scripts": 0.9969192743301392, "filetypes/php": 0.9988455772399902, "general": 0.9762199521064758}` |
| filetypes/pe | joint_or_at_fp_0 | 1325391 | 159706 | 52.35% | 0 | 0.00 | 1875.76 | 0.000 | 68.73% | 57.48% | `{"filegroups/native": 0.999677300453186, "filetypes/pe": 0.9993385672569275}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32560 | 51362 | 51.58% | 0 | 0.00 | 5832.41 | 0.000 | 68.06% | 81.21% | `{"filegroups/source": 0.9750577211380005, "filetypes/kotlin": 0.5626204609870911, "general": 0.9768744111061096}` |
| filetypes/powershell | joint_or_at_fp_0 | 5220 | 2370 | 51.15% | 0 | 0.00 | 126322.35 | 0.000 | 67.68% | 66.40% | `{"filegroups/scripts": 0.9969203472137451, "filetypes/powershell": 0.9927195310592651, "general": 0.9965300559997559}` |
| filetypes/chrome-manifest | learned_blend_at_fp_0 | 63 | 447 | 50.79% | 0 | 0.00 | 667945.45 | 0.000 | 67.37% | 93.92% | `{}` |
| filetypes/python | joint_or_at_fp_0 | 18793 | 181115 | 47.01% | 0 | 0.00 | 1654.04 | 0.000 | 63.96% | 95.02% | `{"filegroups/scripts": 0.9981874823570251, "filetypes/python": 0.9999244213104248, "general": 0.9976562261581421}` |
| filetypes/vbs | learned_blend_at_fp_0 | 11083 | 3294 | 41.25% | 0 | 0.00 | 90903.78 | 0.000 | 58.41% | 54.71% | `{}` |
| filetypes/doc | calibrate_inherited | 32603 | 78 | 39.11% | 0 | 0.00 | 3767863.42 | 0.000 | 56.23% | 39.25% | `{"filegroups/documents": 0.9938012957572937, "general": 0.9997240304946899}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18299 | 37.11% | 0 | 0.00 | 16369.68 | 0.000 | 54.14% | 99.67% | `{"filegroups/scripts": 0.9784010648727417, "filetypes/lua": 0.8241344094276428}` |
| filetypes/zip | joint_or_at_fp_0 | 101434 | 11880 | 34.57% | 0 | 0.00 | 25213.42 | 0.000 | 51.38% | 41.43% | `{"filetypes/zip": 0.9976928234100342, "general": 0.9978596568107605}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 10847 | 100.00% | 0 | 0.00 | 27614.26 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9956511855125427}` |
| filetypes/rtf | joint_or_at_fp_0 | 5865 | 502 | 98.81% | 0 | 0.00 | 594982.34 | 0.000 | 99.40% | 98.90% | `{"filegroups/documents": 0.46621882915496826, "filetypes/rtf": 0.14464563131332397}` |
| filetypes/batch | joint_or_at_fp_0 | 176358 | 4798 | 97.53% | 0 | 0.00 | 62417.62 | 0.000 | 98.75% | 97.60% | `{"filegroups/scripts": 0.9979010820388794, "filetypes/batch": 0.9972212314605713, "general": 0.9972652792930603}` |
| filetypes/elf | learned_blend_at_fp_0 | 178960 | 163743 | 95.91% | 0 | 0.00 | 1829.52 | 0.000 | 97.91% | 97.86% | `{}` |
| filetypes/xls | learned_blend_at_fp_0 | 37051 | 20747 | 93.61% | 0 | 0.00 | 14438.31 | 0.000 | 96.70% | 95.90% | `{}` |
| filetypes/python-bytecode | learned_blend_at_fp_0 | 2722 | 86146 | 93.53% | 0 | 0.00 | 3477.45 | 0.000 | 96.66% | 99.80% | `{}` |
| filetypes/package.json | joint_or_at_fp_0 | 18353 | 20467 | 90.00% | 0 | 0.00 | 14635.82 | 0.000 | 94.74% | 95.27% | `{"filegroups/config": 0.9999018907546997, "filetypes/package.json": 0.9982081651687622, "general": 0.9970642328262329}` |
| filetypes/tar | learned_blend_at_fp_0 | 31043 | 22349 | 89.64% | 0 | 0.00 | 13403.43 | 0.000 | 94.54% | 93.98% | `{}` |
| filetypes/macho | learned_blend_at_fp_0 | 2583 | 11579 | 84.44% | 0 | 0.00 | 25868.77 | 0.000 | 91.56% | 97.16% | `{}` |
| filetypes/lnk | learned_blend_at_fp_0 | 4344 | 1055 | 83.63% | 0 | 0.00 | 283552.89 | 0.000 | 91.09% | 86.83% | `{}` |
| filetypes/ole | joint_or_at_fp_0 | 6887 | 6214 | 82.00% | 0 | 0.00 | 48197.78 | 0.000 | 90.11% | 90.54% | `{"filegroups/documents": 0.7249563336372375, "filetypes/ole": 0.9786415696144104}` |
| filetypes/docx | joint_or_at_fp_0 | 4756 | 433 | 81.94% | 0 | 0.00 | 689467.22 | 0.000 | 90.07% | 83.45% | `{"filegroups/documents": 0.9727789163589478, "filetypes/docx": 0.6076767444610596, "general": 0.9669691324234009}` |
| filetypes/clojure | learned_blend_at_fp_0 | 121 | 5183 | 81.82% | 0 | 0.00 | 57782.49 | 0.000 | 90.00% | 99.59% | `{}` |
| filetypes/pkg-info | learned_blend_at_fp_0 | 10636 | 1782 | 80.10% | 0 | 0.00 | 167969.45 | 0.000 | 88.95% | 82.95% | `{}` |
| filetypes/shell | learned_blend_at_fp_0 | 14262 | 58885 | 79.46% | 0 | 0.00 | 5087.30 | 0.000 | 88.55% | 95.99% | `{}` |
| filetypes/jar | joint_or_at_fp_0 | 3397 | 3737 | 71.21% | 0 | 0.00 | 80131.97 | 0.000 | 83.18% | 86.29% | `{"filetypes/jar": 0.6623266935348511, "general": 0.9993686079978943}` |
| filetypes/crx | joint_or_at_fp_0 | 622 | 79 | 65.11% | 0 | 0.00 | 3721067.61 | 0.000 | 78.87% | 69.04% | `{"filetypes/crx": 0.9098513126373291, "general": 0.9899091124534607}` |
| filetypes/perl | learned_blend_at_fp_0 | 316 | 39244 | 62.97% | 0 | 0.00 | 7633.31 | 0.000 | 77.28% | 99.70% | `{}` |
| filetypes/javascript | learned_blend_at_fp_0 | 116755 | 582359 | 59.36% | 0 | 0.00 | 514.41 | 0.000 | 74.50% | 93.21% | `{}` |
| filetypes/ruby | joint_or_at_fp_0 | 118 | 24970 | 57.63% | 0 | 0.00 | 11996.61 | 0.000 | 73.12% | 99.80% | `{"filegroups/scripts": 0.9891042709350586, "filetypes/ruby": 0.9992208480834961, "general": 0.9624097943305969}` |
| filetypes/php | joint_or_at_fp_0 | 4271 | 145907 | 52.49% | 0 | 0.00 | 2053.16 | 0.000 | 68.85% | 98.65% | `{"filegroups/scripts": 0.9969192743301392, "filetypes/php": 0.9988455772399902, "general": 0.9762199521064758}` |
| filetypes/pe | joint_or_at_fp_0 | 1325391 | 159706 | 52.35% | 0 | 0.00 | 1875.76 | 0.000 | 68.73% | 57.48% | `{"filegroups/native": 0.999677300453186, "filetypes/pe": 0.9993385672569275}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32560 | 51362 | 51.58% | 0 | 0.00 | 5832.41 | 0.000 | 68.06% | 81.21% | `{"filegroups/source": 0.9750577211380005, "filetypes/kotlin": 0.5626204609870911, "general": 0.9768744111061096}` |
| filetypes/powershell | joint_or_at_fp_0 | 5220 | 2370 | 51.15% | 0 | 0.00 | 126322.35 | 0.000 | 67.68% | 66.40% | `{"filegroups/scripts": 0.9969203472137451, "filetypes/powershell": 0.9927195310592651, "general": 0.9965300559997559}` |
| filetypes/chrome-manifest | learned_blend_at_fp_0 | 63 | 447 | 50.79% | 0 | 0.00 | 667945.45 | 0.000 | 67.37% | 93.92% | `{}` |
| filetypes/python | joint_or_at_fp_0 | 18793 | 181115 | 47.01% | 0 | 0.00 | 1654.04 | 0.000 | 63.96% | 95.02% | `{"filegroups/scripts": 0.9981874823570251, "filetypes/python": 0.9999244213104248, "general": 0.9976562261581421}` |
| filetypes/vbs | learned_blend_at_fp_0 | 11083 | 3294 | 41.25% | 0 | 0.00 | 90903.78 | 0.000 | 58.41% | 54.71% | `{}` |
| filetypes/doc | calibrate_inherited | 32603 | 78 | 39.17% | 0 | 0.00 | 3767863.42 | 0.000 | 56.29% | 39.31% | `{"filegroups/documents": 0.9938012957572937, "general": 0.9995547533035278}` |
| filetypes/lua | joint_or_at_fp_0 | 97 | 18299 | 37.11% | 0 | 0.00 | 16369.68 | 0.000 | 54.14% | 99.67% | `{"filegroups/scripts": 0.9784010648727417, "filetypes/lua": 0.8241344094276428}` |
| filetypes/zip | joint_or_at_fp_0 | 101434 | 11880 | 34.57% | 0 | 0.00 | 25213.42 | 0.000 | 51.38% | 41.43% | `{"filetypes/zip": 0.9976928234100342, "general": 0.9978596568107605}` |
