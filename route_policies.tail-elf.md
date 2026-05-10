# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `199337321`
- Rows: 2293938 (472475 malware, 1821463 benign)

## L5 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | or_general_primary | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | or_general_primary | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | or_general_primary | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | or_general_primary | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/doc | or_general_primary | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/elf | specialist_primary_with_escape | 15610 | 95323 | 99.26% | 1 | 10.49 | 0.549 | 99.62% | 99.89% | `{"filetypes/elf": 0.9951940178871155}` |
| filetypes/lnk | or_general_primary | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.29% | 1 | 61.98 | 0.549 | 99.12% | 99.78% | `{"filegroups/archive": 0.9976335763931274, "general": 0.8635274171829224}` |
| filetypes/rar | or_general_primary | 745 | 3 | 96.24% | 0 | 0.00 | 0.000 | 98.08% | 96.26% | `{"filegroups/archive": 0.0023353532887995243, "general": 0.2747366726398468}` |
| filetypes/rtf | specialist_primary_with_escape | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/tar | specialist_primary_with_escape | 1041 | 338 | 94.81% | 1 | 2958.58 | 0.549 | 97.29% | 96.01% | `{"filegroups/archive": 0.9996289610862732, "filetypes/tar": 0.7380364537239075, "general": 0.8572259545326233}` |
| filetypes/package.json | specialist_primary_with_escape | 15355 | 6451 | 92.75% | 1 | 155.01 | 0.549 | 96.23% | 94.89% | `{"general": 0.9824850559234619}` |
| filetypes/pkg-info | specialist_primary_with_escape | 3671 | 702 | 90.06% | 1 | 1424.50 | 0.549 | 94.75% | 91.63% | `{"general": 0.5379334688186646}` |
| filetypes/ruby | specialist_primary_with_escape | 69 | 11944 | 89.86% | 1 | 83.72 | 0.549 | 93.94% | 99.93% | `{"general": 0.7836131453514099}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 87.96% | 1 | 108.04 | 0.549 | 93.59% | 92.42% | `{"filegroups/archive": 0.9999964833259583, "filetypes/tar.gz": 0.9999642372131348, "general": 0.9858265519142151}` |
| filetypes/data | specialist_primary_with_escape | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/python | specialist_primary_with_escape | 11674 | 97779 | 84.70% | 1 | 10.23 | 0.549 | 91.71% | 98.37% | `{"filetypes/python": 0.9919191002845764, "general": 0.9818487763404846}` |
| filetypes/php | or_general_primary | 1246 | 16375 | 83.55% | 1 | 61.07 | 0.549 | 91.00% | 98.83% | `{"filetypes/php": 0.9491043090820312, "general": 0.9131830334663391}` |
| filetypes/java_class | specialist_primary_with_escape | 364 | 7262 | 80.77% | 1 | 137.70 | 0.549 | 89.23% | 99.07% | `{"general": 0.8206426501274109}` |
| filetypes/javascript | or_general_primary | 56548 | 333110 | 79.05% | 1 | 3.00 | 0.549 | 88.30% | 96.96% | `{"filegroups/scripts": 0.9999687075614929, "filetypes/javascript": 0.9999224543571472, "general": 0.9862461090087891}` |
| filetypes/python-bytecode | specialist_primary_with_escape | 84 | 8406 | 78.57% | 1 | 118.96 | 0.549 | 87.42% | 99.78% | `{"filetypes/python-bytecode": 0.8959823250770569, "general": 0.7202142477035522}` |
| filetypes/docx | specialist_primary_with_escape | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | or_general_primary | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/jar | specialist_primary_with_escape | 581 | 1061 | 76.76% | 1 | 942.51 | 0.549 | 86.77% | 91.72% | `{"filetypes/jar": 0.5095304250717163, "general": 0.8665791749954224}` |
| filetypes/perl | specialist_primary_with_escape | 149 | 21761 | 75.17% | 1 | 45.95 | 0.549 | 85.50% | 99.83% | `{"filetypes/perl": 0.9907156229019165, "general": 0.5572389364242554}` |
| filetypes/7z | group_primary_with_escape | 3115 | 22 | 73.58% | 1 | 45454.55 | 0.549 | 84.76% | 73.73% | `{"filegroups/archive": 0.0014036035863682628, "general": 0.9892896413803101}` |
| filetypes/xls | or_general_primary | 170 | 33 | 71.76% | 1 | 30303.03 | 0.549 | 83.28% | 75.86% | `{"filegroups/documents": 0.9375917911529541, "general": 0.9652759432792664}` |
| filetypes/zip | specialist_primary_with_escape | 31399 | 2835 | 70.93% | 1 | 352.73 | 0.549 | 82.99% | 73.33% | `{"filegroups/archive": 0.9999703764915466, "filetypes/zip": 0.9996939897537231, "general": 0.9974381327629089}` |
| filetypes/batch | specialist_primary_with_escape | 308 | 1483 | 68.83% | 1 | 674.31 | 0.549 | 81.38% | 94.58% | `{"filetypes/batch": 0.9624754190444946, "general": 0.8541349172592163}` |
| filetypes/pptx | or_general_primary | 3 | 167 | 66.67% | 1 | 5988.02 | 0.549 | 66.67% | 98.82% | `{"general": 0.8834270238876343}` |

## L9 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | or_general_primary | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | or_general_primary | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | or_general_primary | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | or_general_primary | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/doc | or_general_primary | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/elf | specialist_primary_with_escape | 15610 | 95323 | 99.26% | 1 | 10.49 | 0.549 | 99.62% | 99.89% | `{"filetypes/elf": 0.9951940178871155}` |
| filetypes/lnk | or_general_primary | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.29% | 1 | 61.98 | 0.549 | 99.12% | 99.78% | `{"filegroups/archive": 0.9976335763931274, "general": 0.8635274171829224}` |
| filetypes/rar | or_general_primary | 745 | 3 | 96.24% | 0 | 0.00 | 0.000 | 98.08% | 96.26% | `{"filegroups/archive": 0.0023353532887995243, "general": 0.2747366726398468}` |
| filetypes/rtf | specialist_primary_with_escape | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/tar | specialist_primary_with_escape | 1041 | 338 | 94.81% | 1 | 2958.58 | 0.549 | 97.29% | 96.01% | `{"filegroups/archive": 0.9996289610862732, "filetypes/tar": 0.7380364537239075, "general": 0.8572259545326233}` |
| filetypes/package.json | specialist_primary_with_escape | 15355 | 6451 | 92.75% | 1 | 155.01 | 0.549 | 96.23% | 94.89% | `{"general": 0.9824850559234619}` |
| filetypes/pkg-info | specialist_primary_with_escape | 3671 | 702 | 90.06% | 1 | 1424.50 | 0.549 | 94.75% | 91.63% | `{"general": 0.5379334688186646}` |
| filetypes/ruby | specialist_primary_with_escape | 69 | 11944 | 89.86% | 1 | 83.72 | 0.549 | 93.94% | 99.93% | `{"general": 0.7836131453514099}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 87.96% | 1 | 108.04 | 0.549 | 93.59% | 92.42% | `{"filegroups/archive": 0.9999964833259583, "filetypes/tar.gz": 0.9999642372131348, "general": 0.9858265519142151}` |
| filetypes/data | specialist_primary_with_escape | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/python | specialist_primary_with_escape | 11674 | 97779 | 84.70% | 1 | 10.23 | 0.549 | 91.71% | 98.37% | `{"filetypes/python": 0.9919191002845764, "general": 0.9818487763404846}` |
| filetypes/php | or_general_primary | 1246 | 16375 | 83.55% | 1 | 61.07 | 0.549 | 91.00% | 98.83% | `{"filetypes/php": 0.9491043090820312, "general": 0.9131830334663391}` |
| filetypes/javascript | or_general_primary | 56548 | 333110 | 81.18% | 2 | 6.00 | 1.098 | 89.61% | 97.27% | `{"filegroups/scripts": 0.9999687075614929, "filetypes/javascript": 0.9999224543571472, "general": 0.9840287566184998}` |
| filetypes/java_class | specialist_primary_with_escape | 364 | 7262 | 80.77% | 1 | 137.70 | 0.549 | 89.23% | 99.07% | `{"general": 0.8206426501274109}` |
| filetypes/python-bytecode | specialist_primary_with_escape | 84 | 8406 | 78.57% | 1 | 118.96 | 0.549 | 87.42% | 99.78% | `{"filetypes/python-bytecode": 0.8959823250770569, "general": 0.7202142477035522}` |
| filetypes/docx | specialist_primary_with_escape | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | or_general_primary | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/jar | specialist_primary_with_escape | 581 | 1061 | 76.76% | 1 | 942.51 | 0.549 | 86.77% | 91.72% | `{"filetypes/jar": 0.5095304250717163, "general": 0.8665791749954224}` |
| filetypes/perl | specialist_primary_with_escape | 149 | 21761 | 75.17% | 1 | 45.95 | 0.549 | 85.50% | 99.83% | `{"filetypes/perl": 0.9907156229019165, "general": 0.5572389364242554}` |
| filetypes/7z | group_primary_with_escape | 3115 | 22 | 73.58% | 1 | 45454.55 | 0.549 | 84.76% | 73.73% | `{"filegroups/archive": 0.0014036035863682628, "general": 0.9892896413803101}` |
| filetypes/xls | or_general_primary | 170 | 33 | 71.76% | 1 | 30303.03 | 0.549 | 83.28% | 75.86% | `{"filegroups/documents": 0.9375917911529541, "general": 0.9652759432792664}` |
| filetypes/zip | specialist_primary_with_escape | 31399 | 2835 | 70.93% | 1 | 352.73 | 0.549 | 82.99% | 73.33% | `{"filegroups/archive": 0.9999703764915466, "filetypes/zip": 0.9996939897537231, "general": 0.9974381327629089}` |
| filetypes/batch | specialist_primary_with_escape | 308 | 1483 | 68.83% | 1 | 674.31 | 0.549 | 81.38% | 94.58% | `{"filetypes/batch": 0.9624754190444946, "general": 0.8541349172592163}` |
| filetypes/pptx | or_general_primary | 3 | 167 | 66.67% | 1 | 5988.02 | 0.549 | 66.67% | 98.82% | `{"general": 0.8834270238876343}` |

## L5 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | or_general_primary | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | or_general_primary | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | or_general_primary | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | or_general_primary | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/doc | or_general_primary | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/elf | specialist_primary_with_escape | 15610 | 95323 | 99.57% | 3 | 31.47 | 1.647 | 99.78% | 99.94% | `{"filetypes/elf": 0.9804892539978027}` |
| filetypes/lnk | or_general_primary | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.29% | 1 | 61.98 | 0.549 | 99.12% | 99.78% | `{"filegroups/archive": 0.9976335763931274, "general": 0.8635274171829224}` |
| filetypes/rar | or_general_primary | 745 | 3 | 96.24% | 0 | 0.00 | 0.000 | 98.08% | 96.26% | `{"filegroups/archive": 0.0023353532887995243, "general": 0.2747366726398468}` |
| filetypes/rtf | specialist_primary_with_escape | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/tar | specialist_primary_with_escape | 1041 | 338 | 94.81% | 1 | 2958.58 | 0.549 | 97.29% | 96.01% | `{"filegroups/archive": 0.9996289610862732, "filetypes/tar": 0.7380364537239075, "general": 0.8572259545326233}` |
| filetypes/package.json | specialist_primary_with_escape | 15355 | 6451 | 92.75% | 1 | 155.01 | 0.549 | 96.23% | 94.89% | `{"general": 0.9824850559234619}` |
| filetypes/pkg-info | specialist_primary_with_escape | 3671 | 702 | 90.06% | 1 | 1424.50 | 0.549 | 94.75% | 91.63% | `{"general": 0.5379334688186646}` |
| filetypes/ruby | specialist_primary_with_escape | 69 | 11944 | 89.86% | 1 | 83.72 | 0.549 | 93.94% | 99.93% | `{"general": 0.7836131453514099}` |
| filetypes/python | specialist_primary_with_escape | 11674 | 97779 | 89.82% | 4 | 40.91 | 2.196 | 94.62% | 98.91% | `{"filetypes/python": 0.9919191002845764, "general": 0.9685817956924438}` |
| filetypes/javascript | or_general_primary | 56548 | 333110 | 88.56% | 15 | 45.03 | 8.235 | 93.92% | 98.34% | `{"filetypes/javascript": 0.9999224543571472, "general": 0.9419882297515869}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 87.96% | 1 | 108.04 | 0.549 | 93.59% | 92.42% | `{"filegroups/archive": 0.9999964833259583, "filetypes/tar.gz": 0.9999642372131348, "general": 0.9858265519142151}` |
| filetypes/data | specialist_primary_with_escape | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | or_general_primary | 1246 | 16375 | 83.55% | 1 | 61.07 | 0.549 | 91.00% | 98.83% | `{"filetypes/php": 0.9491043090820312, "general": 0.9131830334663391}` |
| filetypes/java_class | specialist_primary_with_escape | 364 | 7262 | 80.77% | 1 | 137.70 | 0.549 | 89.23% | 99.07% | `{"general": 0.8206426501274109}` |
| filetypes/python-bytecode | specialist_primary_with_escape | 84 | 8406 | 78.57% | 1 | 118.96 | 0.549 | 87.42% | 99.78% | `{"filetypes/python-bytecode": 0.8959823250770569, "general": 0.7202142477035522}` |
| filetypes/docx | specialist_primary_with_escape | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | or_general_primary | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/jar | specialist_primary_with_escape | 581 | 1061 | 76.76% | 1 | 942.51 | 0.549 | 86.77% | 91.72% | `{"filetypes/jar": 0.5095304250717163, "general": 0.8665791749954224}` |
| filetypes/perl | specialist_primary_with_escape | 149 | 21761 | 75.17% | 1 | 45.95 | 0.549 | 85.50% | 99.83% | `{"filetypes/perl": 0.9907156229019165, "general": 0.5572389364242554}` |
| filetypes/7z | group_primary_with_escape | 3115 | 22 | 73.58% | 1 | 45454.55 | 0.549 | 84.76% | 73.73% | `{"filegroups/archive": 0.0014036035863682628, "general": 0.9892896413803101}` |
| filetypes/xls | or_general_primary | 170 | 33 | 71.76% | 1 | 30303.03 | 0.549 | 83.28% | 75.86% | `{"filegroups/documents": 0.9375917911529541, "general": 0.9652759432792664}` |
| filetypes/zip | specialist_primary_with_escape | 31399 | 2835 | 70.93% | 1 | 352.73 | 0.549 | 82.99% | 73.33% | `{"filegroups/archive": 0.9999703764915466, "filetypes/zip": 0.9996939897537231, "general": 0.9974381327629089}` |
| filetypes/batch | specialist_primary_with_escape | 308 | 1483 | 68.83% | 1 | 674.31 | 0.549 | 81.38% | 94.58% | `{"filetypes/batch": 0.9624754190444946, "general": 0.8541349172592163}` |
| filetypes/pptx | or_general_primary | 3 | 167 | 66.67% | 1 | 5988.02 | 0.549 | 66.67% | 98.82% | `{"general": 0.8834270238876343}` |

## L9 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | or_general_primary | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | or_general_primary | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | or_general_primary | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | or_general_primary | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/elf | specialist_primary_with_escape | 15610 | 95323 | 99.69% | 7 | 73.43 | 3.843 | 99.82% | 99.95% | `{"filetypes/elf": 0.9218172430992126}` |
| filetypes/doc | or_general_primary | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/lnk | or_general_primary | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.29% | 1 | 61.98 | 0.549 | 99.12% | 99.78% | `{"filegroups/archive": 0.9976335763931274, "general": 0.8635274171829224}` |
| filetypes/rar | or_general_primary | 745 | 3 | 96.24% | 0 | 0.00 | 0.000 | 98.08% | 96.26% | `{"filegroups/archive": 0.0023353532887995243, "general": 0.2747366726398468}` |
| filetypes/rtf | specialist_primary_with_escape | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/tar | specialist_primary_with_escape | 1041 | 338 | 94.81% | 1 | 2958.58 | 0.549 | 97.29% | 96.01% | `{"filegroups/archive": 0.9996289610862732, "filetypes/tar": 0.7380364537239075, "general": 0.8572259545326233}` |
| filetypes/package.json | specialist_primary_with_escape | 15355 | 6451 | 92.75% | 1 | 155.01 | 0.549 | 96.23% | 94.89% | `{"general": 0.9824850559234619}` |
| filetypes/python | specialist_primary_with_escape | 11674 | 97779 | 90.81% | 7 | 71.59 | 3.843 | 95.15% | 99.01% | `{"filetypes/python": 0.9919191002845764, "general": 0.9583919048309326}` |
| filetypes/pkg-info | specialist_primary_with_escape | 3671 | 702 | 90.06% | 1 | 1424.50 | 0.549 | 94.75% | 91.63% | `{"general": 0.5379334688186646}` |
| filetypes/ruby | specialist_primary_with_escape | 69 | 11944 | 89.86% | 1 | 83.72 | 0.549 | 93.94% | 99.93% | `{"general": 0.7836131453514099}` |
| filetypes/javascript | or_general_primary | 56548 | 333110 | 89.21% | 26 | 78.05 | 14.274 | 94.28% | 98.43% | `{"filetypes/javascript": 0.9999224543571472, "general": 0.9267908930778503}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 87.96% | 1 | 108.04 | 0.549 | 93.59% | 92.42% | `{"filegroups/archive": 0.9999964833259583, "filetypes/tar.gz": 0.9999642372131348, "general": 0.9858265519142151}` |
| filetypes/data | specialist_primary_with_escape | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | or_general_primary | 1246 | 16375 | 83.55% | 1 | 61.07 | 0.549 | 91.00% | 98.83% | `{"filetypes/php": 0.9491043090820312, "general": 0.9131830334663391}` |
| filetypes/java_class | specialist_primary_with_escape | 364 | 7262 | 80.77% | 1 | 137.70 | 0.549 | 89.23% | 99.07% | `{"general": 0.8206426501274109}` |
| filetypes/python-bytecode | specialist_primary_with_escape | 84 | 8406 | 78.57% | 1 | 118.96 | 0.549 | 87.42% | 99.78% | `{"filetypes/python-bytecode": 0.8959823250770569, "general": 0.7202142477035522}` |
| filetypes/docx | specialist_primary_with_escape | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | or_general_primary | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/jar | specialist_primary_with_escape | 581 | 1061 | 76.76% | 1 | 942.51 | 0.549 | 86.77% | 91.72% | `{"filetypes/jar": 0.5095304250717163, "general": 0.8665791749954224}` |
| filetypes/perl | specialist_primary_with_escape | 149 | 21761 | 75.17% | 1 | 45.95 | 0.549 | 85.50% | 99.83% | `{"filetypes/perl": 0.9907156229019165, "general": 0.5572389364242554}` |
| filetypes/7z | group_primary_with_escape | 3115 | 22 | 73.58% | 1 | 45454.55 | 0.549 | 84.76% | 73.73% | `{"filegroups/archive": 0.0014036035863682628, "general": 0.9892896413803101}` |
| filetypes/xls | or_general_primary | 170 | 33 | 71.76% | 1 | 30303.03 | 0.549 | 83.28% | 75.86% | `{"filegroups/documents": 0.9375917911529541, "general": 0.9652759432792664}` |
| filetypes/zip | specialist_primary_with_escape | 31399 | 2835 | 70.93% | 1 | 352.73 | 0.549 | 82.99% | 73.33% | `{"filegroups/archive": 0.9999703764915466, "filetypes/zip": 0.9996939897537231, "general": 0.9974381327629089}` |
| filetypes/batch | specialist_primary_with_escape | 308 | 1483 | 68.83% | 1 | 674.31 | 0.549 | 81.38% | 94.58% | `{"filetypes/batch": 0.9624754190444946, "general": 0.8541349172592163}` |
| filetypes/pptx | or_general_primary | 3 | 167 | 66.67% | 1 | 5988.02 | 0.549 | 66.67% | 98.82% | `{"general": 0.8834270238876343}` |
