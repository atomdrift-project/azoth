# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `199337321`
- Rows: 2293938 (472475 malware, 1821463 benign)

## L5 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | general_only | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | general_only | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | general_only | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/doc | general_only | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/lnk | general_only | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/elf | filetype_only | 15610 | 95323 | 98.99% | 1 | 10.49 | 0.549 | 99.49% | 99.86% | `{"filetypes/elf": 0.9951940178871155}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.20% | 0 | 0.00 | 0.000 | 99.09% | 99.78% | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| filetypes/package.json | group_primary_with_escape | 15355 | 6451 | 97.73% | 1 | 155.01 | 0.549 | 98.85% | 98.39% | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| filetypes/rar | general_only | 745 | 3 | 96.11% | 0 | 0.00 | 0.000 | 98.02% | 96.12% | `{"general": 0.2747366726398468}` |
| filetypes/rtf | general_only | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 93.91% | 1 | 108.04 | 0.549 | 96.86% | 96.17% | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| filetypes/javascript | specialist_primary_with_escape | 56552 | 333111 | 92.99% | 1 | 3.00 | 0.549 | 96.37% | 98.98% | `{"filetypes/javascript": 0.9995086789131165, "general": 0.997726321220398}` |
| filetypes/python-bytecode | filetype_only | 84 | 8406 | 91.67% | 0 | 0.00 | 0.000 | 95.65% | 99.92% | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| filetypes/pkg-info | filetype_only | 3671 | 702 | 91.04% | 1 | 1424.50 | 0.549 | 95.30% | 92.45% | `{"filetypes/pkg-info": 0.07038185745477676}` |
| filetypes/tar | filetype_only | 1041 | 338 | 90.87% | 0 | 0.00 | 0.000 | 95.22% | 93.11% | `{"filetypes/tar": 0.5931394696235657}` |
| filetypes/python | or_general_primary | 11667 | 97779 | 89.81% | 1 | 10.23 | 0.549 | 94.63% | 98.91% | `{"filegroups/scripts": 0.9916728734970093, "filetypes/python": 0.9997654557228088, "general": 0.9818487763404846}` |
| filetypes/ruby | group_only | 69 | 11944 | 86.96% | 0 | 0.00 | 0.000 | 93.02% | 99.93% | `{"filegroups/scripts": 0.9507483839988708}` |
| filetypes/data | or_general_primary | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | filetype_only | 1247 | 16375 | 82.36% | 0 | 0.00 | 0.000 | 90.33% | 98.75% | `{"filetypes/php": 0.9792458415031433}` |
| filetypes/java_class | group_only | 364 | 7262 | 79.67% | 0 | 0.00 | 0.000 | 88.69% | 99.03% | `{"filegroups/portable": 0.8742847442626953}` |
| filetypes/zip | specialist_primary_with_escape | 31411 | 2835 | 74.70% | 1 | 352.73 | 0.549 | 85.52% | 76.79% | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| filetypes/xls | general_only | 170 | 33 | 70.59% | 0 | 0.00 | 0.000 | 82.76% | 75.37% | `{"general": 0.9652759432792664}` |
| filetypes/batch | filetype_only | 308 | 1483 | 68.18% | 0 | 0.00 | 0.000 | 81.08% | 94.53% | `{"filetypes/batch": 0.9842783212661743}` |
| filetypes/7z | or_general_primary | 3115 | 22 | 67.87% | 1 | 45454.55 | 0.549 | 80.84% | 68.06% | `{"filegroups/archive": 0.9847283959388733, "general": 0.9607616662979126}` |
| filetypes/tar.bz2 | general_only | 3 | 176 | 66.67% | 0 | 0.00 | 0.000 | 80.00% | 99.44% | `{"general": 0.9954475164413452}` |
| filetypes/xz | group_only | 41 | 23312 | 65.85% | 0 | 0.00 | 0.000 | 79.41% | 99.94% | `{"filegroups/archive": 0.2578180432319641}` |
| filetypes/objc | general_only | 5 | 4231 | 60.00% | 0 | 0.00 | 0.000 | 75.00% | 99.95% | `{"general": 0.9881909489631653}` |
| filetypes/kotlin | group_primary_with_escape | 626 | 28870 | 57.83% | 0 | 0.00 | 0.000 | 73.28% | 99.10% | `{"filegroups/source": 0.5903330445289612, "filetypes/kotlin": 0.06616190075874329}` |
| filetypes/java | or_general_primary | 18 | 21029 | 50.00% | 0 | 0.00 | 0.000 | 66.67% | 99.96% | `{"filegroups/source": 0.9824634790420532, "general": 0.19315451383590698}` |
| filetypes/github-actions | general_only | 2 | 3153 | 50.00% | 0 | 0.00 | 0.000 | 66.67% | 99.97% | `{"general": 0.8459287881851196}` |

## L9 Hostile

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | general_only | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | general_only | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | general_only | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/doc | general_only | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/lnk | general_only | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/elf | filetype_only | 15610 | 95323 | 98.99% | 1 | 10.49 | 0.549 | 99.49% | 99.86% | `{"filetypes/elf": 0.9951940178871155}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.20% | 0 | 0.00 | 0.000 | 99.09% | 99.78% | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| filetypes/package.json | group_primary_with_escape | 15355 | 6451 | 97.73% | 1 | 155.01 | 0.549 | 98.85% | 98.39% | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| filetypes/rar | general_only | 745 | 3 | 96.11% | 0 | 0.00 | 0.000 | 98.02% | 96.12% | `{"general": 0.2747366726398468}` |
| filetypes/rtf | general_only | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/javascript | filetype_only | 56552 | 333111 | 94.04% | 2 | 6.00 | 1.098 | 96.93% | 99.13% | `{"filetypes/javascript": 0.998388409614563}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 93.91% | 1 | 108.04 | 0.549 | 96.86% | 96.17% | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| filetypes/python-bytecode | filetype_only | 84 | 8406 | 91.67% | 0 | 0.00 | 0.000 | 95.65% | 99.92% | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| filetypes/pkg-info | filetype_only | 3671 | 702 | 91.04% | 1 | 1424.50 | 0.549 | 95.30% | 92.45% | `{"filetypes/pkg-info": 0.07038185745477676}` |
| filetypes/tar | filetype_only | 1041 | 338 | 90.87% | 0 | 0.00 | 0.000 | 95.22% | 93.11% | `{"filetypes/tar": 0.5931394696235657}` |
| filetypes/python | or_general_primary | 11667 | 97779 | 89.81% | 1 | 10.23 | 0.549 | 94.63% | 98.91% | `{"filegroups/scripts": 0.9916728734970093, "filetypes/python": 0.9997654557228088, "general": 0.9818487763404846}` |
| filetypes/jar | or_general_primary | 569 | 1061 | 88.22% | 1 | 942.51 | 0.549 | 93.66% | 95.83% | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
| filetypes/ruby | group_only | 69 | 11944 | 86.96% | 0 | 0.00 | 0.000 | 93.02% | 99.93% | `{"filegroups/scripts": 0.9507483839988708}` |
| filetypes/data | or_general_primary | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | filetype_only | 1247 | 16375 | 82.36% | 0 | 0.00 | 0.000 | 90.33% | 98.75% | `{"filetypes/php": 0.9792458415031433}` |
| filetypes/java_class | group_only | 364 | 7262 | 79.67% | 0 | 0.00 | 0.000 | 88.69% | 99.03% | `{"filegroups/portable": 0.8742847442626953}` |
| filetypes/zip | specialist_primary_with_escape | 31411 | 2835 | 74.70% | 1 | 352.73 | 0.549 | 85.52% | 76.79% | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| filetypes/xls | general_only | 170 | 33 | 70.59% | 0 | 0.00 | 0.000 | 82.76% | 75.37% | `{"general": 0.9652759432792664}` |
| filetypes/batch | filetype_only | 308 | 1483 | 68.18% | 0 | 0.00 | 0.000 | 81.08% | 94.53% | `{"filetypes/batch": 0.9842783212661743}` |
| filetypes/7z | or_general_primary | 3115 | 22 | 67.87% | 1 | 45454.55 | 0.549 | 80.84% | 68.06% | `{"filegroups/archive": 0.9847283959388733, "general": 0.9607616662979126}` |
| filetypes/shell | group_primary_with_escape | 1756 | 35576 | 67.37% | 1 | 28.11 | 0.549 | 80.48% | 98.46% | `{"filegroups/scripts": 0.9686398506164551, "filetypes/shell": 0.9585855007171631, "general": 0.9515489339828491}` |
| filetypes/tar.bz2 | general_only | 3 | 176 | 66.67% | 0 | 0.00 | 0.000 | 80.00% | 99.44% | `{"general": 0.9954475164413452}` |
| filetypes/xz | group_only | 41 | 23312 | 65.85% | 0 | 0.00 | 0.000 | 79.41% | 99.94% | `{"filegroups/archive": 0.2578180432319641}` |
| filetypes/objc | general_only | 5 | 4231 | 60.00% | 0 | 0.00 | 0.000 | 75.00% | 99.95% | `{"general": 0.9881909489631653}` |
| filetypes/kotlin | group_primary_with_escape | 626 | 28870 | 57.83% | 0 | 0.00 | 0.000 | 73.28% | 99.10% | `{"filegroups/source": 0.5903330445289612, "filetypes/kotlin": 0.06616190075874329}` |

## L5 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | general_only | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | general_only | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | general_only | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | general_only | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/doc | general_only | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/elf | filetype_only | 15610 | 95323 | 99.41% | 4 | 41.96 | 2.196 | 99.69% | 99.91% | `{"filetypes/elf": 0.973215639591217}` |
| filetypes/lnk | general_only | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/ruby | group_primary_with_escape | 69 | 11944 | 98.55% | 1 | 83.72 | 0.549 | 98.55% | 99.98% | `{"filegroups/scripts": 0.9507483839988708, "filetypes/ruby": 0.995830237865448, "general": 0.8743661046028137}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.20% | 0 | 0.00 | 0.000 | 99.09% | 99.78% | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| filetypes/package.json | group_primary_with_escape | 15355 | 6451 | 97.73% | 1 | 155.01 | 0.549 | 98.85% | 98.39% | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| filetypes/rar | or_general_primary | 745 | 3 | 97.32% | 1 | 333333.33 | 0.549 | 98.57% | 97.19% | `{"filegroups/archive": 0.07848110049962997, "general": 0.2747366726398468}` |
| filetypes/tar | or_general_primary | 1041 | 338 | 97.12% | 1 | 2958.58 | 0.549 | 98.49% | 97.75% | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5931394696235657, "general": 0.8572259545326233}` |
| filetypes/rtf | general_only | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/python | specialist_primary_with_escape | 11667 | 97779 | 95.41% | 4 | 40.91 | 2.196 | 97.63% | 99.51% | `{"filetypes/python": 0.9160045981407166, "general": 0.9818487763404846}` |
| filetypes/javascript | filetype_only | 56552 | 333111 | 95.27% | 15 | 45.03 | 8.235 | 97.57% | 99.31% | `{"filetypes/javascript": 0.8397032618522644}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 93.91% | 1 | 108.04 | 0.549 | 96.86% | 96.17% | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| filetypes/python-bytecode | filetype_only | 84 | 8406 | 91.67% | 0 | 0.00 | 0.000 | 95.65% | 99.92% | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| filetypes/ole | group_primary_with_escape | 380 | 5317 | 91.32% | 1 | 188.08 | 0.549 | 95.33% | 99.40% | `{"filetypes/ole": 0.9899150729179382, "general": 0.9884464740753174}` |
| filetypes/pkg-info | filetype_only | 3671 | 702 | 91.04% | 1 | 1424.50 | 0.549 | 95.30% | 92.45% | `{"filetypes/pkg-info": 0.07038185745477676}` |
| filetypes/jar | or_general_primary | 569 | 1061 | 88.22% | 1 | 942.51 | 0.549 | 93.66% | 95.83% | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
| filetypes/data | or_general_primary | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | group_primary_with_escape | 1247 | 16375 | 85.08% | 1 | 61.07 | 0.549 | 91.90% | 98.94% | `{"filegroups/scripts": 0.960743248462677, "filetypes/php": 0.9792458415031433, "general": 0.92668616771698}` |
| filetypes/java_class | or_general_primary | 364 | 7262 | 82.42% | 1 | 137.70 | 0.549 | 90.23% | 99.15% | `{"filetypes/java_class": 0.9461427927017212, "general": 0.8206426501274109}` |
| filetypes/perl | or_general_primary | 149 | 21917 | 81.88% | 1 | 45.63 | 0.549 | 89.71% | 99.87% | `{"filegroups/scripts": 0.6773157119750977, "filetypes/perl": 0.9500136375427246, "general": 0.5572389364242554}` |
| filetypes/batch | or_general_primary | 308 | 1483 | 79.87% | 1 | 674.31 | 0.549 | 88.65% | 96.48% | `{"filegroups/scripts": 0.7781511545181274, "filetypes/batch": 0.9842783212661743, "general": 0.8541349172592163}` |
| filetypes/docx | general_only | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | general_only | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/zip | specialist_primary_with_escape | 31411 | 2835 | 74.70% | 1 | 352.73 | 0.549 | 85.52% | 76.79% | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| filetypes/xz | or_general_primary | 41 | 23312 | 73.17% | 1 | 42.90 | 0.549 | 83.33% | 99.95% | `{"filegroups/archive": 0.2578180432319641, "general": 0.7811363339424133}` |
| filetypes/xls | general_only | 170 | 33 | 70.59% | 0 | 0.00 | 0.000 | 82.76% | 75.37% | `{"general": 0.9652759432792664}` |

## L9 Suspicious

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/tar.xz | general_only | 5 | 227 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.8479825854301453}` |
| filetypes/cab | general_only | 3 | 1 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9575597047805786}` |
| filetypes/desktop-entry | general_only | 2 | 212 | 100.00% | 0 | 0.00 | 0.000 | 100.00% | 100.00% | `{"general": 0.9924401044845581}` |
| filetypes/pkg | general_only | 1 | 10 | 100.00% | 1 | 100000.00 | 0.549 | 66.67% | 90.91% | `{"general": 0.03306693211197853}` |
| filetypes/doc | general_only | 1550 | 15 | 99.68% | 0 | 0.00 | 0.000 | 99.84% | 99.68% | `{"general": 0.9489932060241699}` |
| filetypes/elf | filetype_only | 15610 | 95323 | 99.58% | 7 | 73.43 | 3.843 | 99.77% | 99.94% | `{"filetypes/elf": 0.9218172430992126}` |
| filetypes/lnk | general_only | 203 | 16 | 99.01% | 0 | 0.00 | 0.000 | 99.50% | 99.09% | `{"general": 0.05043259263038635}` |
| filetypes/ruby | group_primary_with_escape | 69 | 11944 | 98.55% | 1 | 83.72 | 0.549 | 98.55% | 99.98% | `{"filegroups/scripts": 0.9507483839988708, "filetypes/ruby": 0.995830237865448, "general": 0.8743661046028137}` |
| filetypes/zst | or_general_primary | 2282 | 16133 | 98.20% | 0 | 0.00 | 0.000 | 99.09% | 99.78% | `{"filetypes/zst": 0.9954463839530945, "general": 0.8635274171829224}` |
| filetypes/package.json | group_primary_with_escape | 15355 | 6451 | 97.73% | 1 | 155.01 | 0.549 | 98.85% | 98.39% | `{"filegroups/config": 0.9598770141601562, "general": 0.9896659851074219}` |
| filetypes/rar | or_general_primary | 745 | 3 | 97.32% | 1 | 333333.33 | 0.549 | 98.57% | 97.19% | `{"filegroups/archive": 0.07848110049962997, "general": 0.2747366726398468}` |
| filetypes/tar | or_general_primary | 1041 | 338 | 97.12% | 1 | 2958.58 | 0.549 | 98.49% | 97.75% | `{"filegroups/archive": 0.8024291396141052, "filetypes/tar": 0.5931394696235657, "general": 0.8572259545326233}` |
| filetypes/python | specialist_primary_with_escape | 11667 | 97779 | 96.46% | 7 | 71.59 | 3.843 | 98.17% | 99.62% | `{"filetypes/python": 0.7431784272193909, "general": 0.9818487763404846}` |
| filetypes/rtf | general_only | 69 | 408 | 95.65% | 0 | 0.00 | 0.000 | 97.78% | 99.37% | `{"general": 0.826679527759552}` |
| filetypes/javascript | filetype_only | 56552 | 333111 | 95.32% | 26 | 78.05 | 14.274 | 97.58% | 99.31% | `{"filetypes/javascript": 0.22858473658561707}` |
| filetypes/tar.gz | or_general_primary | 15692 | 9256 | 93.91% | 1 | 108.04 | 0.549 | 96.86% | 96.17% | `{"filegroups/archive": 0.9820064306259155, "filetypes/tar.gz": 0.9383400082588196, "general": 0.9858265519142151}` |
| filetypes/python-bytecode | filetype_only | 84 | 8406 | 91.67% | 0 | 0.00 | 0.000 | 95.65% | 99.92% | `{"filetypes/python-bytecode": 0.7946628332138062}` |
| filetypes/ole | group_primary_with_escape | 380 | 5317 | 91.32% | 1 | 188.08 | 0.549 | 95.33% | 99.40% | `{"filetypes/ole": 0.9899150729179382, "general": 0.9884464740753174}` |
| filetypes/pkg-info | filetype_only | 3671 | 702 | 91.04% | 1 | 1424.50 | 0.549 | 95.30% | 92.45% | `{"filetypes/pkg-info": 0.07038185745477676}` |
| filetypes/jar | or_general_primary | 569 | 1061 | 88.22% | 1 | 942.51 | 0.549 | 93.66% | 95.83% | `{"filegroups/portable": 0.8732023239135742, "filetypes/jar": 0.9174808859825134, "general": 0.8665791749954224}` |
| filetypes/data | or_general_primary | 299 | 8570 | 85.95% | 0 | 0.00 | 0.000 | 92.45% | 99.53% | `{"filetypes/data": 0.7614107131958008, "general": 0.9008088707923889}` |
| filetypes/php | group_primary_with_escape | 1247 | 16375 | 85.08% | 1 | 61.07 | 0.549 | 91.90% | 98.94% | `{"filegroups/scripts": 0.960743248462677, "filetypes/php": 0.9792458415031433, "general": 0.92668616771698}` |
| filetypes/java_class | or_general_primary | 364 | 7262 | 82.42% | 1 | 137.70 | 0.549 | 90.23% | 99.15% | `{"filetypes/java_class": 0.9461427927017212, "general": 0.8206426501274109}` |
| filetypes/perl | or_general_primary | 149 | 21917 | 81.88% | 1 | 45.63 | 0.549 | 89.71% | 99.87% | `{"filegroups/scripts": 0.6773157119750977, "filetypes/perl": 0.9500136375427246, "general": 0.5572389364242554}` |
| filetypes/batch | or_general_primary | 308 | 1483 | 79.87% | 1 | 674.31 | 0.549 | 88.65% | 96.48% | `{"filegroups/scripts": 0.7781511545181274, "filetypes/batch": 0.9842783212661743, "general": 0.8541349172592163}` |
| filetypes/docx | general_only | 160 | 199 | 78.12% | 1 | 5025.13 | 0.549 | 87.41% | 89.97% | `{"general": 0.8694261312484741}` |
| filetypes/applescript | general_only | 22 | 51 | 77.27% | 1 | 19607.84 | 0.549 | 85.00% | 91.78% | `{"general": 0.04313071444630623}` |
| filetypes/zip | specialist_primary_with_escape | 31411 | 2835 | 74.70% | 1 | 352.73 | 0.549 | 85.52% | 76.79% | `{"filegroups/archive": 0.9977139830589294, "filetypes/zip": 0.9837130308151245, "general": 0.9974381327629089}` |
| filetypes/xz | or_general_primary | 41 | 23312 | 73.17% | 1 | 42.90 | 0.549 | 83.33% | 99.95% | `{"filegroups/archive": 0.2578180432319641, "general": 0.7811363339424133}` |
| filetypes/xls | general_only | 170 | 33 | 70.59% | 0 | 0.00 | 0.000 | 82.76% | 75.37% | `{"general": 0.9652759432792664}` |
