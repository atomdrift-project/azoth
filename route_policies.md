# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1685037226`
- Rows: 7416064 (2543560 malware, 4872504 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.70% | 0 | 0.00 | 577769.77 | 0.000 | 99.35% | 98.81% | `{"filegroups/documents": 0.03179101273417473, "filetypes/rtf": 0.016215085983276367}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 95.77% | 0 | 0.00 | 133232.58 | 0.000 | 97.84% | 96.51% | `{"filetypes/pkg-info": 0.9865292310714722, "general": 0.9824052453041077}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 94.37% | 0 | 0.00 | 14428.57 | 0.000 | 97.10% | 96.37% | `{"filegroups/documents": 0.49092817306518555, "filetypes/xls": 0.9387679696083069}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 92.56% | 0 | 0.00 | 1671.88 | 0.000 | 96.13% | 96.25% | `{"filegroups/native": 0.9655287265777588, "filetypes/elf": 0.9970917701721191, "general": 0.9778026342391968}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 88.76% | 0 | 0.00 | 13046.76 | 0.000 | 94.04% | 94.97% | `{"filegroups/config": 0.9992030262947083, "filetypes/package.json": 0.9969614148139954, "general": 0.9921825528144836}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 79 | 450 | 86.08% | 0 | 0.00 | 663507.29 | 0.000 | 92.52% | 97.92% | `{"filetypes/chrome-manifest": 0.9099287986755371}` |
| filetypes/ole | joint_or_at_fp_0 | 7042 | 6381 | 82.16% | 0 | 0.00 | 46936.67 | 0.000 | 90.21% | 90.64% | `{"filegroups/documents": 0.7653979063034058, "filetypes/ole": 0.3788658380508423, "general": 0.9955987334251404}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3159 | 194703 | 80.09% | 0 | 0.00 | 1538.60 | 0.000 | 88.94% | 99.68% | `{"filetypes/python-bytecode": 0.9992477893829346, "general": 0.9766547679901123}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 79.07% | 0 | 0.00 | 24332.80 | 0.000 | 88.31% | 96.34% | `{"filegroups/native": 0.732079803943634, "filetypes/macho": 0.9881566762924194, "general": 0.9629740715026855}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 74.41% | 0 | 0.00 | 664980.11 | 0.000 | 85.32% | 76.58% | `{"filegroups/documents": 0.583914041519165, "filetypes/docx": 0.9784104228019714}` |
| filetypes/tar | joint_or_at_fp_0 | 31109 | 26895 | 74.29% | 0 | 0.00 | 11138.00 | 0.000 | 85.25% | 86.21% | `{"filetypes/tar": 0.9993809461593628, "general": 0.9971179962158203}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 73.54% | 0 | 0.00 | 281157.79 | 0.000 | 84.75% | 78.67% | `{"filetypes/lnk": 0.9540192484855652, "general": 0.9983258247375488}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.965197741985321}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 68.65% | 0 | 0.00 | 1540208.46 | 0.000 | 81.41% | 69.74% | `{"filetypes/msi": 0.8788959383964539, "general": 0.9746996760368347}` |
| filetypes/shell | joint_or_at_fp_0 | 14965 | 65207 | 66.71% | 0 | 0.00 | 4594.08 | 0.000 | 80.03% | 93.79% | `{"filegroups/scripts": 0.9913555979728699, "filetypes/shell": 0.9599254131317139, "general": 0.9966090321540833}` |
| filetypes/vbs | joint_or_at_fp_0 | 11375 | 3331 | 65.11% | 0 | 0.00 | 89894.49 | 0.000 | 78.87% | 73.01% | `{"filetypes/vbs": 0.9855564832687378, "general": 0.9903786778450012}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 64.08% | 0 | 0.00 | 73469.86 | 0.000 | 78.11% | 83.36% | `{"filetypes/jar": 0.8195528388023376}` |
| filetypes/javascript | joint_or_at_fp_0 | 121134 | 643321 | 60.97% | 0 | 0.00 | 465.67 | 0.000 | 75.75% | 93.82% | `{"filegroups/scripts": 0.9974320530891418, "filetypes/javascript": 0.9656803607940674, "general": 0.9988300800323486}` |
| filetypes/java_class | joint_or_at_fp_0 | 1785 | 786063 | 59.66% | 0 | 0.00 | 381.11 | 0.000 | 74.74% | 99.91% | `{"filegroups/portable": 0.9999638795852661, "filetypes/java_class": 0.9740312099456787, "general": 0.9582540988922119}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/pe | joint_or_at_fp_0 | 1337376 | 162465 | 57.36% | 0 | 0.00 | 1843.91 | 0.000 | 72.90% | 61.98% | `{"filegroups/native": 0.9985658526420593, "filetypes/pe": 0.9986572265625, "general": 0.9997826814651489}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32985 | 55207 | 51.44% | 0 | 0.00 | 5426.22 | 0.000 | 67.93% | 81.84% | `{"filetypes/kotlin": 0.7201052904129028, "general": 0.8662064671516418}` |
| filetypes/perl | learned_blend_at_fp_0 | 358 | 42499 | 51.40% | 0 | 0.00 | 7048.70 | 0.000 | 67.90% | 99.59% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 51.02% | 0 | 0.00 | 15932.63 | 0.000 | 67.57% | 99.75% | `{"filetypes/lua": 0.693849503993988, "general": 0.9245051145553589}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 49.65% | 0 | 0.00 | 121951.33 | 0.000 | 66.36% | 65.03% | `{"filegroups/scripts": 0.9946820139884949, "filetypes/powershell": 0.9949887990951538, "general": 0.9945769309997559}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 49.17% | 0 | 0.00 | 1918.69 | 0.000 | 65.92% | 98.30% | `{"filegroups/scripts": 0.9913409352302551, "filetypes/php": 0.964704155921936, "general": 0.9004867076873779}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 47.58% | 0 | 0.00 | 1372.10 | 0.000 | 64.48% | 95.10% | `{"filegroups/scripts": 0.9965590834617615, "filetypes/python": 0.9978185892105103, "general": 0.9917882680892944}` |
| filetypes/ruby | joint_or_at_fp_0 | 220 | 28744 | 45.00% | 0 | 0.00 | 10421.57 | 0.000 | 62.07% | 99.58% | `{"filegroups/scripts": 0.9586553573608398, "filetypes/ruby": 0.9951184988021851, "general": 0.9575048089027405}` |
| filetypes/whl | filetype_only_at_fp_0 | 384 | 758 | 34.90% | 0 | 0.00 | 394435.39 | 0.000 | 51.74% | 78.11% | `{"filetypes/whl": 0.8879406452178955}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | learned_blend_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.70% | 0 | 0.00 | 577769.77 | 0.000 | 99.35% | 98.81% | `{"filegroups/documents": 0.03179101273417473, "filetypes/rtf": 0.016215085983276367}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 95.77% | 0 | 0.00 | 133232.58 | 0.000 | 97.84% | 96.51% | `{"filetypes/pkg-info": 0.9865292310714722, "general": 0.9824052453041077}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 94.37% | 0 | 0.00 | 14428.57 | 0.000 | 97.10% | 96.37% | `{"filegroups/documents": 0.49092817306518555, "filetypes/xls": 0.9387679696083069}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 92.56% | 0 | 0.00 | 1671.88 | 0.000 | 96.13% | 96.25% | `{"filegroups/native": 0.9655287265777588, "filetypes/elf": 0.9970917701721191, "general": 0.9778026342391968}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 88.76% | 0 | 0.00 | 13046.76 | 0.000 | 94.04% | 94.97% | `{"filegroups/config": 0.9992030262947083, "filetypes/package.json": 0.9969614148139954, "general": 0.9921825528144836}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 79 | 450 | 86.08% | 0 | 0.00 | 663507.29 | 0.000 | 92.52% | 97.92% | `{"filetypes/chrome-manifest": 0.9099287986755371}` |
| filetypes/ole | joint_or_at_fp_0 | 7042 | 6381 | 82.16% | 0 | 0.00 | 46936.67 | 0.000 | 90.21% | 90.64% | `{"filegroups/documents": 0.7653979063034058, "filetypes/ole": 0.3788658380508423, "general": 0.9955987334251404}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3159 | 194703 | 80.09% | 0 | 0.00 | 1538.60 | 0.000 | 88.94% | 99.68% | `{"filetypes/python-bytecode": 0.9992477893829346, "general": 0.9766547679901123}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 79.07% | 0 | 0.00 | 24332.80 | 0.000 | 88.31% | 96.34% | `{"filegroups/native": 0.732079803943634, "filetypes/macho": 0.9881566762924194, "general": 0.9629740715026855}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 74.41% | 0 | 0.00 | 664980.11 | 0.000 | 85.32% | 76.58% | `{"filegroups/documents": 0.583914041519165, "filetypes/docx": 0.9784104228019714}` |
| filetypes/tar | joint_or_at_fp_0 | 31109 | 26895 | 74.29% | 0 | 0.00 | 11138.00 | 0.000 | 85.25% | 86.21% | `{"filetypes/tar": 0.9993809461593628, "general": 0.9971179962158203}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 73.54% | 0 | 0.00 | 281157.79 | 0.000 | 84.75% | 78.67% | `{"filetypes/lnk": 0.9540192484855652, "general": 0.9983258247375488}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.965197741985321}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 68.65% | 0 | 0.00 | 1540208.46 | 0.000 | 81.41% | 69.74% | `{"filetypes/msi": 0.8788959383964539, "general": 0.9746996760368347}` |
| filetypes/shell | joint_or_at_fp_0 | 14965 | 65207 | 66.71% | 0 | 0.00 | 4594.08 | 0.000 | 80.03% | 93.79% | `{"filegroups/scripts": 0.9913555979728699, "filetypes/shell": 0.9599254131317139, "general": 0.9966090321540833}` |
| filetypes/vbs | joint_or_at_fp_0 | 11375 | 3331 | 65.11% | 0 | 0.00 | 89894.49 | 0.000 | 78.87% | 73.01% | `{"filetypes/vbs": 0.9855564832687378, "general": 0.9903786778450012}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 64.08% | 0 | 0.00 | 73469.86 | 0.000 | 78.11% | 83.36% | `{"filetypes/jar": 0.8195528388023376}` |
| filetypes/javascript | joint_or_at_fp_0 | 121134 | 643321 | 60.97% | 0 | 0.00 | 465.67 | 0.000 | 75.75% | 93.82% | `{"filegroups/scripts": 0.9974320530891418, "filetypes/javascript": 0.9656803607940674, "general": 0.9988300800323486}` |
| filetypes/java_class | joint_or_at_fp_0 | 1785 | 786063 | 59.66% | 0 | 0.00 | 381.11 | 0.000 | 74.74% | 99.91% | `{"filegroups/portable": 0.9999638795852661, "filetypes/java_class": 0.9740312099456787, "general": 0.9582540988922119}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/pe | joint_or_at_fp_0 | 1337376 | 162465 | 57.36% | 0 | 0.00 | 1843.91 | 0.000 | 72.90% | 61.98% | `{"filegroups/native": 0.9985658526420593, "filetypes/pe": 0.9986572265625, "general": 0.9997826814651489}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32985 | 55207 | 51.44% | 0 | 0.00 | 5426.22 | 0.000 | 67.93% | 81.84% | `{"filetypes/kotlin": 0.7201052904129028, "general": 0.8662064671516418}` |
| filetypes/perl | learned_blend_at_fp_0 | 358 | 42499 | 51.40% | 0 | 0.00 | 7048.70 | 0.000 | 67.90% | 99.59% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 51.02% | 0 | 0.00 | 15932.63 | 0.000 | 67.57% | 99.75% | `{"filetypes/lua": 0.693849503993988, "general": 0.9245051145553589}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 49.65% | 0 | 0.00 | 121951.33 | 0.000 | 66.36% | 65.03% | `{"filegroups/scripts": 0.9946820139884949, "filetypes/powershell": 0.9949887990951538, "general": 0.9945769309997559}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 49.17% | 0 | 0.00 | 1918.69 | 0.000 | 65.92% | 98.30% | `{"filegroups/scripts": 0.9913409352302551, "filetypes/php": 0.964704155921936, "general": 0.9004867076873779}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 47.58% | 0 | 0.00 | 1372.10 | 0.000 | 64.48% | 95.10% | `{"filegroups/scripts": 0.9965590834617615, "filetypes/python": 0.9978185892105103, "general": 0.9917882680892944}` |
| filetypes/ruby | joint_or_at_fp_0 | 220 | 28744 | 45.00% | 0 | 0.00 | 10421.57 | 0.000 | 62.07% | 99.58% | `{"filegroups/scripts": 0.9586553573608398, "filetypes/ruby": 0.9951184988021851, "general": 0.9575048089027405}` |
| filetypes/whl | filetype_only_at_fp_0 | 384 | 758 | 34.90% | 0 | 0.00 | 394435.39 | 0.000 | 51.74% | 78.11% | `{"filetypes/whl": 0.8879406452178955}` |
