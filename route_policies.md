# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1685037226`
- Rows: 7416064 (2543560 malware, 4872504 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9976853132247925}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.57% | 0 | 0.00 | 577769.77 | 0.000 | 99.28% | 98.68% | `{"filegroups/documents": 0.6970841288566589, "filetypes/rtf": 0.016215085983276367}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 95.77% | 0 | 0.00 | 133232.58 | 0.000 | 97.84% | 96.51% | `{"filetypes/pkg-info": 0.9865292310714722, "general": 0.9824052453041077}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 94.32% | 0 | 0.00 | 1671.88 | 0.000 | 97.08% | 97.14% | `{"filegroups/native": 0.9655287265777588, "filetypes/elf": 0.9927176237106323, "general": 0.9778323769569397}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 94.16% | 0 | 0.00 | 14428.57 | 0.000 | 96.99% | 96.23% | `{"filetypes/xls": 0.938723623752594}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 88.28% | 0 | 0.00 | 13046.76 | 0.000 | 93.78% | 94.76% | `{"filegroups/config": 0.9994091987609863, "filetypes/package.json": 0.9969614148139954, "general": 0.9921825528144836}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 79 | 450 | 86.08% | 0 | 0.00 | 663507.29 | 0.000 | 92.52% | 97.92% | `{"filetypes/chrome-manifest": 0.9099287986755371}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 84.09% | 0 | 0.00 | 24332.80 | 0.000 | 91.36% | 97.22% | `{"filegroups/native": 0.732079803943634, "filetypes/macho": 0.9798775315284729, "general": 0.9629740715026855}` |
| filetypes/ole | joint_or_at_fp_0 | 7042 | 6381 | 82.18% | 0 | 0.00 | 46936.67 | 0.000 | 90.22% | 90.65% | `{"filegroups/documents": 0.9597269892692566, "filetypes/ole": 0.3788658380508423}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3159 | 194703 | 80.09% | 0 | 0.00 | 1538.60 | 0.000 | 88.94% | 99.68% | `{"filetypes/python-bytecode": 0.9992477893829346, "general": 0.9766547679901123}` |
| filetypes/tar | joint_or_at_fp_0 | 31332 | 26900 | 73.76% | 0 | 0.00 | 11135.93 | 0.000 | 84.90% | 85.88% | `{"filetypes/tar": 0.9993809461593628, "general": 0.9971179962158203}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 73.54% | 0 | 0.00 | 281157.79 | 0.000 | 84.75% | 78.67% | `{"filetypes/lnk": 0.9540192484855652, "general": 0.9983258247375488}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 72.98% | 0 | 0.00 | 664980.11 | 0.000 | 84.38% | 75.27% | `{"filegroups/documents": 0.9805161952972412, "filetypes/docx": 0.9784104228019714, "general": 0.9840129017829895}` |
| filetypes/shell | joint_or_at_fp_0 | 14965 | 65207 | 70.06% | 0 | 0.00 | 4594.08 | 0.000 | 82.39% | 94.41% | `{"filegroups/scripts": 0.9914060831069946, "filetypes/shell": 0.9432698488235474, "general": 0.9966090321540833}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.965197741985321}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 68.65% | 0 | 0.00 | 1540208.46 | 0.000 | 81.41% | 69.74% | `{"filetypes/msi": 0.8788959383964539, "general": 0.9746996760368347}` |
| filetypes/whl | joint_or_at_fp_0 | 202 | 758 | 66.34% | 0 | 0.00 | 394435.39 | 0.000 | 79.76% | 92.92% | `{"filetypes/whl": 0.8879406452178955}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 58.70% | 0 | 0.00 | 73469.86 | 0.000 | 73.98% | 80.87% | `{"filetypes/jar": 0.7942995429039001}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32997 | 55207 | 52.35% | 0 | 0.00 | 5426.22 | 0.000 | 68.72% | 82.17% | `{"filegroups/source": 0.9605473875999451, "filetypes/kotlin": 0.7279399037361145, "general": 0.8662064671516418}` |
| filetypes/pe | joint_or_at_fp_0 | 1337376 | 162465 | 51.61% | 0 | 0.00 | 1843.91 | 0.000 | 68.08% | 56.85% | `{"filegroups/native": 0.9985658526420593, "filetypes/pe": 0.9995201826095581, "general": 0.9997823238372803}` |
| filetypes/perl | learned_blend_at_fp_0 | 358 | 42499 | 51.40% | 0 | 0.00 | 7048.70 | 0.000 | 67.90% | 99.59% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 51.02% | 0 | 0.00 | 15932.63 | 0.000 | 67.57% | 99.75% | `{"filetypes/lua": 0.693849503993988, "general": 0.9245051145553589}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 49.78% | 0 | 0.00 | 1918.69 | 0.000 | 66.47% | 98.32% | `{"filegroups/scripts": 0.9913409352302551, "filetypes/php": 0.9915758967399597, "general": 0.9004867076873779}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 49.70% | 0 | 0.00 | 121951.33 | 0.000 | 66.40% | 65.07% | `{"filegroups/scripts": 0.9946820139884949, "filetypes/powershell": 0.9970746040344238, "general": 0.9945769309997559}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 48.09% | 0 | 0.00 | 1372.10 | 0.000 | 64.95% | 95.15% | `{"filegroups/scripts": 0.9965571165084839, "filetypes/python": 0.9992274045944214, "general": 0.9917882680892944}` |
| filetypes/javascript | joint_or_at_fp_0 | 121123 | 643321 | 45.19% | 0 | 0.00 | 465.67 | 0.000 | 62.25% | 91.32% | `{"filegroups/scripts": 0.9974133372306824, "filetypes/javascript": 0.9979830980300903, "general": 0.9988300800323486}` |
| filetypes/ruby | joint_or_at_fp_0 | 220 | 28744 | 45.00% | 0 | 0.00 | 10421.57 | 0.000 | 62.07% | 99.58% | `{"filegroups/scripts": 0.9586553573608398, "filetypes/ruby": 0.9951184988021851, "general": 0.9575048089027405}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1785 | 786063 | 43.47% | 0 | 0.00 | 381.11 | 0.000 | 60.60% | 99.87% | `{}` |
| filetypes/zip | joint_or_at_fp_0 | 102558 | 13076 | 36.77% | 0 | 0.00 | 22907.53 | 0.000 | 53.77% | 43.92% | `{"filetypes/zip": 0.9965572357177734, "general": 0.998996913433075}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 140 | 15792 | 100.00% | 0 | 0.00 | 18968.14 | 0.000 | 100.00% | 100.00% | `{"filetypes/html": 0.9976853132247925}` |
| filetypes/rtf | joint_or_at_fp_0 | 5945 | 517 | 98.57% | 0 | 0.00 | 577769.77 | 0.000 | 99.28% | 98.68% | `{"filegroups/documents": 0.6970841288566589, "filetypes/rtf": 0.016215085983276367}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10647 | 2247 | 95.77% | 0 | 0.00 | 133232.58 | 0.000 | 97.84% | 96.51% | `{"filetypes/pkg-info": 0.9865292310714722, "general": 0.9824052453041077}` |
| filetypes/elf | joint_or_at_fp_0 | 181628 | 179182 | 94.32% | 0 | 0.00 | 1671.88 | 0.000 | 97.08% | 97.14% | `{"filegroups/native": 0.9655287265777588, "filetypes/elf": 0.9927176237106323, "general": 0.9778323769569397}` |
| filetypes/xls | joint_or_at_fp_0 | 37679 | 20761 | 94.16% | 0 | 0.00 | 14428.57 | 0.000 | 96.99% | 96.23% | `{"filetypes/xls": 0.938723623752594}` |
| filetypes/package.json | joint_or_at_fp_0 | 18597 | 22960 | 88.28% | 0 | 0.00 | 13046.76 | 0.000 | 93.78% | 94.76% | `{"filegroups/config": 0.9994091987609863, "filetypes/package.json": 0.9969614148139954, "general": 0.9921825528144836}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 79 | 450 | 86.08% | 0 | 0.00 | 663507.29 | 0.000 | 92.52% | 97.92% | `{"filetypes/chrome-manifest": 0.9099287986755371}` |
| filetypes/macho | joint_or_at_fp_0 | 2609 | 12310 | 84.09% | 0 | 0.00 | 24332.80 | 0.000 | 91.36% | 97.22% | `{"filegroups/native": 0.732079803943634, "filetypes/macho": 0.9798775315284729, "general": 0.9629740715026855}` |
| filetypes/ole | joint_or_at_fp_0 | 7042 | 6381 | 82.18% | 0 | 0.00 | 46936.67 | 0.000 | 90.22% | 90.65% | `{"filegroups/documents": 0.9597269892692566, "filetypes/ole": 0.3788658380508423}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3159 | 194703 | 80.09% | 0 | 0.00 | 1538.60 | 0.000 | 88.94% | 99.68% | `{"filetypes/python-bytecode": 0.9992477893829346, "general": 0.9766547679901123}` |
| filetypes/tar | joint_or_at_fp_0 | 31332 | 26900 | 73.76% | 0 | 0.00 | 11135.93 | 0.000 | 84.90% | 85.88% | `{"filetypes/tar": 0.9993809461593628, "general": 0.9971179962158203}` |
| filetypes/lnk | joint_or_at_fp_0 | 4425 | 1064 | 73.54% | 0 | 0.00 | 281157.79 | 0.000 | 84.75% | 78.67% | `{"filetypes/lnk": 0.9540192484855652, "general": 0.9983258247375488}` |
| filetypes/docx | joint_or_at_fp_0 | 4833 | 449 | 72.98% | 0 | 0.00 | 664980.11 | 0.000 | 84.38% | 75.27% | `{"filegroups/documents": 0.9805161952972412, "filetypes/docx": 0.9784104228019714, "general": 0.9840129017829895}` |
| filetypes/shell | joint_or_at_fp_0 | 14965 | 65207 | 70.06% | 0 | 0.00 | 4594.08 | 0.000 | 82.39% | 94.41% | `{"filegroups/scripts": 0.9914060831069946, "filetypes/shell": 0.9432698488235474, "general": 0.9966090321540833}` |
| filetypes/clojure | joint_or_at_fp_0 | 128 | 5580 | 68.75% | 0 | 0.00 | 53672.55 | 0.000 | 81.48% | 99.30% | `{"filetypes/clojure": 0.965197741985321}` |
| filetypes/msi | joint_or_at_fp_0 | 5385 | 193 | 68.65% | 0 | 0.00 | 1540208.46 | 0.000 | 81.41% | 69.74% | `{"filetypes/msi": 0.8788959383964539, "general": 0.9746996760368347}` |
| filetypes/whl | joint_or_at_fp_0 | 202 | 758 | 66.34% | 0 | 0.00 | 394435.39 | 0.000 | 79.76% | 92.92% | `{"filetypes/whl": 0.8879406452178955}` |
| filetypes/crx | joint_or_at_fp_0 | 786 | 79 | 59.29% | 0 | 0.00 | 3721067.61 | 0.000 | 74.44% | 63.01% | `{"filetypes/crx": 0.9103931188583374, "general": 0.9465426802635193}` |
| filetypes/jar | joint_or_at_fp_0 | 3516 | 4076 | 58.70% | 0 | 0.00 | 73469.86 | 0.000 | 73.98% | 80.87% | `{"filetypes/jar": 0.7942995429039001}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32997 | 55207 | 52.35% | 0 | 0.00 | 5426.22 | 0.000 | 68.72% | 82.17% | `{"filegroups/source": 0.9605473875999451, "filetypes/kotlin": 0.7279399037361145, "general": 0.8662064671516418}` |
| filetypes/pe | joint_or_at_fp_0 | 1337376 | 162465 | 51.61% | 0 | 0.00 | 1843.91 | 0.000 | 68.08% | 56.85% | `{"filegroups/native": 0.9985658526420593, "filetypes/pe": 0.9995201826095581, "general": 0.9997823238372803}` |
| filetypes/perl | learned_blend_at_fp_0 | 358 | 42499 | 51.40% | 0 | 0.00 | 7048.70 | 0.000 | 67.90% | 99.59% | `{}` |
| filetypes/lua | joint_or_at_fp_0 | 98 | 18801 | 51.02% | 0 | 0.00 | 15932.63 | 0.000 | 67.57% | 99.75% | `{"filetypes/lua": 0.693849503993988, "general": 0.9245051145553589}` |
| filetypes/php | joint_or_at_fp_0 | 5416 | 156133 | 49.78% | 0 | 0.00 | 1918.69 | 0.000 | 66.47% | 98.32% | `{"filegroups/scripts": 0.9913409352302551, "filetypes/php": 0.9915758967399597, "general": 0.9004867076873779}` |
| filetypes/powershell | joint_or_at_fp_0 | 5583 | 2455 | 49.70% | 0 | 0.00 | 121951.33 | 0.000 | 66.40% | 65.07% | `{"filegroups/scripts": 0.9946820139884949, "filetypes/powershell": 0.9970746040344238, "general": 0.9945769309997559}` |
| filetypes/python | joint_or_at_fp_0 | 22518 | 218331 | 48.09% | 0 | 0.00 | 1372.10 | 0.000 | 64.95% | 95.15% | `{"filegroups/scripts": 0.9965571165084839, "filetypes/python": 0.9992274045944214, "general": 0.9917882680892944}` |
| filetypes/javascript | joint_or_at_fp_0 | 121123 | 643321 | 45.19% | 0 | 0.00 | 465.67 | 0.000 | 62.25% | 91.32% | `{"filegroups/scripts": 0.9974133372306824, "filetypes/javascript": 0.9979830980300903, "general": 0.9988300800323486}` |
| filetypes/ruby | joint_or_at_fp_0 | 220 | 28744 | 45.00% | 0 | 0.00 | 10421.57 | 0.000 | 62.07% | 99.58% | `{"filegroups/scripts": 0.9586553573608398, "filetypes/ruby": 0.9951184988021851, "general": 0.9575048089027405}` |
| filetypes/java_class | learned_blend_at_fp_0 | 1785 | 786063 | 43.47% | 0 | 0.00 | 381.11 | 0.000 | 60.60% | 99.87% | `{}` |
| filetypes/zip | joint_or_at_fp_0 | 102558 | 13076 | 36.77% | 0 | 0.00 | 22907.53 | 0.000 | 53.77% | 43.92% | `{"filetypes/zip": 0.9965572357177734, "general": 0.998996913433075}` |
