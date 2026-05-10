# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `762136079`
- Rows: 2990924 (618271 malware, 2372653 benign)

## L5 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | general_only | 9 | 1384 | 100.00% | 0 | 0.00 | 2162.21 | 0.000 | 100.00% | 100.00% | `{"general": 0.8594487309455872}` |
| filetypes/desktop-entry† | general_only | 2 | 231 | 100.00% | 0 | 0.00 | 12884.81 | 0.000 | 100.00% | 100.00% | `{"general": 0.9922379851341248}` |
| filetypes/pkg† | general_only | 1 | 13 | 100.00% | 0 | 0.00 | 205816.67 | 0.000 | 100.00% | 100.00% | `{"general": 0.0017194385873153806}` |
| filetypes/doc† | general_only | 1899 | 23 | 99.79% | 0 | 0.00 | 122123.39 | 0.000 | 99.89% | 99.79% | `{"general": 0.002071269089356065}` |
| filetypes/lnk† | general_only | 285 | 17 | 99.30% | 0 | 0.00 | 161566.11 | 0.000 | 99.65% | 99.34% | `{"general": 0.0039053931832313538}` |
| filetypes/tar† | or_general_primary | 1042 | 355 | 97.02% | 0 | 0.00 | 8403.18 | 0.000 | 98.49% | 97.78% | `{"filegroups/archive": 1.0, "general": 0.7734574675559998}` |
| filetypes/zst† | general_only | 2282 | 16150 | 96.93% | 0 | 0.00 | 185.48 | 0.000 | 98.44% | 99.62% | `{"general": 0.8446625471115112}` |
| filetypes/rar† | general_only | 952 | 4 | 95.69% | 0 | 0.00 | 527129.20 | 0.000 | 97.80% | 95.71% | `{"general": 0.0008109572809189558}` |
| filetypes/rtf† | general_only | 89 | 437 | 95.51% | 0 | 0.00 | 6831.78 | 0.000 | 97.70% | 99.24% | `{"general": 0.9508298635482788}` |
| filetypes/pkg-info† | general_only | 3681 | 807 | 91.69% | 0 | 0.00 | 3705.30 | 0.000 | 95.66% | 93.18% | `{"general": 0.7194933891296387}` |
| filetypes/chm† | general_only | 17 | 5 | 88.24% | 0 | 0.00 | 450719.73 | 0.000 | 93.75% | 90.91% | `{"general": 0.5562927722930908}` |
| filetypes/elf† | or_general_primary | 21965 | 111877 | 87.03% | 0 | 0.00 | 26.78 | 0.000 | 93.07% | 97.87% | `{"filegroups/native": 1.0, "filetypes/elf": 1.0, "general": 0.989948570728302}` |
| filetypes/package.json† | or_general_primary | 15658 | 7205 | 86.72% | 0 | 0.00 | 415.70 | 0.000 | 92.89% | 90.90% | `{"filegroups/config": 1.0, "filetypes/package.json": 1.0, "general": 0.9915000796318054}` |
| filetypes/tar.gz† | or_general_primary | 19387 | 11894 | 85.12% | 0 | 0.00 | 251.84 | 0.000 | 91.96% | 90.78% | `{"filegroups/archive": 1.0, "filetypes/tar.gz": 1.0, "general": 0.9977129101753235}` |
| filetypes/cab† | general_only | 5 | 23 | 80.00% | 0 | 0.00 | 122123.39 | 0.000 | 88.89% | 96.43% | `{"general": 0.9920740127563477}` |
| filetypes/zip† | or_general_primary | 32962 | 5584 | 77.44% | 0 | 0.00 | 536.34 | 0.000 | 87.28% | 80.71% | `{"filegroups/archive": 0.006320903543382883, "filetypes/zip": 1.0, "general": 0.9965186715126038}` |
| filetypes/xz† | general_only | 42 | 23367 | 76.19% | 0 | 0.00 | 128.20 | 0.000 | 86.49% | 99.96% | `{"general": 0.8812193274497986}` |
| filetypes/7z† | general_only | 3780 | 34 | 75.16% | 0 | 0.00 | 84339.64 | 0.000 | 85.82% | 75.38% | `{"general": 0.9988694190979004}` |
| filetypes/jar† | general_only | 606 | 1566 | 74.26% | 0 | 0.00 | 1911.15 | 0.000 | 85.23% | 92.82% | `{"general": 0.9402996897697449}` |
| filetypes/applescript† | general_only | 22 | 100 | 72.73% | 0 | 0.00 | 29513.05 | 0.000 | 84.21% | 95.08% | `{"general": 0.9594946503639221}` |
| filetypes/xls† | general_only | 229 | 42 | 69.00% | 0 | 0.00 | 68842.61 | 0.000 | 81.65% | 73.80% | `{"general": 0.29995617270469666}` |
| filetypes/tar.bz2† | general_only | 3 | 186 | 66.67% | 0 | 0.00 | 15977.08 | 0.000 | 80.00% | 99.47% | `{"general": 0.9955074191093445}` |
| filetypes/perl† | or_general_primary | 157 | 29368 | 65.61% | 0 | 0.00 | 102.00 | 0.000 | 79.23% | 99.82% | `{"filegroups/scripts": 1.0, "filetypes/perl": 1.0, "general": 0.9737693071365356}` |
| filetypes/javascript† | or_general_primary | 57629 | 375582 | 65.08% | 0 | 0.00 | 7.98 | 0.000 | 78.85% | 95.35% | `{"filegroups/scripts": 1.0, "filetypes/javascript": 1.0, "general": 0.9950519800186157}` |
| filetypes/docx† | general_only | 372 | 219 | 61.83% | 0 | 0.00 | 13586.01 | 0.000 | 76.41% | 75.97% | `{"general": 0.860793948173523}` |
| filetypes/kotlin† | or_general_primary | 928 | 34931 | 60.88% | 0 | 0.00 | 85.76 | 0.000 | 75.69% | 98.99% | `{"filegroups/source": 1.0, "filetypes/kotlin": 1.0, "general": 0.7555142045021057}` |
| filetypes/ruby† | or_general_primary | 70 | 23108 | 60.00% | 0 | 0.00 | 129.63 | 0.000 | 75.00% | 99.88% | `{"filegroups/scripts": 1.0, "filetypes/ruby": 1.0, "general": 0.9729308485984802}` |
| filetypes/objc† | general_only | 5 | 17944 | 60.00% | 0 | 0.00 | 166.94 | 0.000 | 75.00% | 99.99% | `{"general": 0.9903209805488586}` |
| filetypes/crx† | general_only | 37 | 13 | 56.76% | 0 | 0.00 | 205816.67 | 0.000 | 72.41% | 68.00% | `{"general": 0.9494370818138123}` |
| filetypes/data† | or_general_primary | 361 | 8705 | 55.96% | 0 | 0.00 | 344.08 | 0.000 | 71.76% | 98.25% | `{"filetypes/data": 1.0, "general": 0.9315239191055298}` |

## L9 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | general_only | 9 | 1384 | 100.00% | 0 | 0.00 | 2162.21 | 0.000 | 100.00% | 100.00% | `{"general": 0.8594487309455872}` |
| filetypes/desktop-entry† | general_only | 2 | 231 | 100.00% | 0 | 0.00 | 12884.81 | 0.000 | 100.00% | 100.00% | `{"general": 0.9922379851341248}` |
| filetypes/pkg† | general_only | 1 | 13 | 100.00% | 0 | 0.00 | 205816.67 | 0.000 | 100.00% | 100.00% | `{"general": 0.0017194385873153806}` |
| filetypes/doc† | general_only | 1899 | 23 | 99.79% | 0 | 0.00 | 122123.39 | 0.000 | 99.89% | 99.79% | `{"general": 0.002071269089356065}` |
| filetypes/lnk† | general_only | 285 | 17 | 99.30% | 0 | 0.00 | 161566.11 | 0.000 | 99.65% | 99.34% | `{"general": 0.0039053931832313538}` |
| filetypes/tar† | or_general_primary | 1042 | 355 | 97.02% | 0 | 0.00 | 8403.18 | 0.000 | 98.49% | 97.78% | `{"filegroups/archive": 1.0, "general": 0.7734574675559998}` |
| filetypes/zst† | general_only | 2282 | 16150 | 96.93% | 0 | 0.00 | 185.48 | 0.000 | 98.44% | 99.62% | `{"general": 0.8446625471115112}` |
| filetypes/rar† | general_only | 952 | 4 | 95.69% | 0 | 0.00 | 527129.20 | 0.000 | 97.80% | 95.71% | `{"general": 0.0008109572809189558}` |
| filetypes/rtf† | general_only | 89 | 437 | 95.51% | 0 | 0.00 | 6831.78 | 0.000 | 97.70% | 99.24% | `{"general": 0.9508298635482788}` |
| filetypes/pkg-info† | general_only | 3681 | 807 | 91.69% | 0 | 0.00 | 3705.30 | 0.000 | 95.66% | 93.18% | `{"general": 0.7194933891296387}` |
| filetypes/chm† | general_only | 17 | 5 | 88.24% | 0 | 0.00 | 450719.73 | 0.000 | 93.75% | 90.91% | `{"general": 0.5562927722930908}` |
| filetypes/elf† | or_general_primary | 21965 | 111877 | 87.03% | 0 | 0.00 | 26.78 | 0.000 | 93.07% | 97.87% | `{"filegroups/native": 1.0, "filetypes/elf": 1.0, "general": 0.989948570728302}` |
| filetypes/package.json† | or_general_primary | 15658 | 7205 | 86.72% | 0 | 0.00 | 415.70 | 0.000 | 92.89% | 90.90% | `{"filegroups/config": 1.0, "filetypes/package.json": 1.0, "general": 0.9915000796318054}` |
| filetypes/tar.gz† | or_general_primary | 19387 | 11894 | 85.12% | 0 | 0.00 | 251.84 | 0.000 | 91.96% | 90.78% | `{"filegroups/archive": 1.0, "filetypes/tar.gz": 1.0, "general": 0.9977129101753235}` |
| filetypes/cab† | general_only | 5 | 23 | 80.00% | 0 | 0.00 | 122123.39 | 0.000 | 88.89% | 96.43% | `{"general": 0.9920740127563477}` |
| filetypes/zip† | or_general_primary | 32962 | 5584 | 77.44% | 0 | 0.00 | 536.34 | 0.000 | 87.28% | 80.71% | `{"filegroups/archive": 0.006320903543382883, "filetypes/zip": 1.0, "general": 0.9965186715126038}` |
| filetypes/xz† | general_only | 42 | 23367 | 76.19% | 0 | 0.00 | 128.20 | 0.000 | 86.49% | 99.96% | `{"general": 0.8812193274497986}` |
| filetypes/7z† | general_only | 3780 | 34 | 75.16% | 0 | 0.00 | 84339.64 | 0.000 | 85.82% | 75.38% | `{"general": 0.9988694190979004}` |
| filetypes/jar† | general_only | 606 | 1566 | 74.26% | 0 | 0.00 | 1911.15 | 0.000 | 85.23% | 92.82% | `{"general": 0.9402996897697449}` |
| filetypes/applescript† | general_only | 22 | 100 | 72.73% | 0 | 0.00 | 29513.05 | 0.000 | 84.21% | 95.08% | `{"general": 0.9594946503639221}` |
| filetypes/xls† | general_only | 229 | 42 | 69.00% | 0 | 0.00 | 68842.61 | 0.000 | 81.65% | 73.80% | `{"general": 0.29995617270469666}` |
| filetypes/tar.bz2† | general_only | 3 | 186 | 66.67% | 0 | 0.00 | 15977.08 | 0.000 | 80.00% | 99.47% | `{"general": 0.9955074191093445}` |
| filetypes/perl† | or_general_primary | 157 | 29368 | 65.61% | 0 | 0.00 | 102.00 | 0.000 | 79.23% | 99.82% | `{"filegroups/scripts": 1.0, "filetypes/perl": 1.0, "general": 0.9737693071365356}` |
| filetypes/javascript | or_general_primary | 57629 | 375582 | 65.08% | 0 | 0.00 | 7.98 | 0.000 | 78.85% | 95.35% | `{"filegroups/scripts": 1.0, "filetypes/javascript": 1.0, "general": 0.9950519800186157}` |
| filetypes/docx† | general_only | 372 | 219 | 61.83% | 0 | 0.00 | 13586.01 | 0.000 | 76.41% | 75.97% | `{"general": 0.860793948173523}` |
| filetypes/kotlin† | or_general_primary | 928 | 34931 | 60.88% | 0 | 0.00 | 85.76 | 0.000 | 75.69% | 98.99% | `{"filegroups/source": 1.0, "filetypes/kotlin": 1.0, "general": 0.7555142045021057}` |
| filetypes/ruby† | or_general_primary | 70 | 23108 | 60.00% | 0 | 0.00 | 129.63 | 0.000 | 75.00% | 99.88% | `{"filegroups/scripts": 1.0, "filetypes/ruby": 1.0, "general": 0.9729308485984802}` |
| filetypes/objc† | general_only | 5 | 17944 | 60.00% | 0 | 0.00 | 166.94 | 0.000 | 75.00% | 99.99% | `{"general": 0.9903209805488586}` |
| filetypes/crx† | general_only | 37 | 13 | 56.76% | 0 | 0.00 | 205816.67 | 0.000 | 72.41% | 68.00% | `{"general": 0.9494370818138123}` |
| filetypes/data† | or_general_primary | 361 | 8705 | 55.96% | 0 | 0.00 | 344.08 | 0.000 | 71.76% | 98.25% | `{"filetypes/data": 1.0, "general": 0.9315239191055298}` |

## L5 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | general_only | 9 | 1384 | 100.00% | 0 | 0.00 | 2162.21 | 0.000 | 100.00% | 100.00% | `{"general": 0.8594487309455872}` |
| filetypes/desktop-entry† | general_only | 2 | 231 | 100.00% | 0 | 0.00 | 12884.81 | 0.000 | 100.00% | 100.00% | `{"general": 0.9922379851341248}` |
| filetypes/pkg† | general_only | 1 | 13 | 100.00% | 0 | 0.00 | 205816.67 | 0.000 | 100.00% | 100.00% | `{"general": 0.0017194385873153806}` |
| filetypes/doc† | general_only | 1899 | 23 | 99.79% | 0 | 0.00 | 122123.39 | 0.000 | 99.89% | 99.79% | `{"general": 0.002071269089356065}` |
| filetypes/lnk† | general_only | 285 | 17 | 99.30% | 0 | 0.00 | 161566.11 | 0.000 | 99.65% | 99.34% | `{"general": 0.0039053931832313538}` |
| filetypes/tar† | or_general_primary | 1042 | 355 | 97.02% | 0 | 0.00 | 8403.18 | 0.000 | 98.49% | 97.78% | `{"filegroups/archive": 1.0, "general": 0.7734574675559998}` |
| filetypes/zst† | general_only | 2282 | 16150 | 96.93% | 0 | 0.00 | 185.48 | 0.000 | 98.44% | 99.62% | `{"general": 0.8446625471115112}` |
| filetypes/rar† | general_only | 952 | 4 | 95.69% | 0 | 0.00 | 527129.20 | 0.000 | 97.80% | 95.71% | `{"general": 0.0008109572809189558}` |
| filetypes/rtf† | general_only | 89 | 437 | 95.51% | 0 | 0.00 | 6831.78 | 0.000 | 97.70% | 99.24% | `{"general": 0.9508298635482788}` |
| filetypes/pkg-info† | general_only | 3681 | 807 | 91.69% | 0 | 0.00 | 3705.30 | 0.000 | 95.66% | 93.18% | `{"general": 0.7194933891296387}` |
| filetypes/chm† | general_only | 17 | 5 | 88.24% | 0 | 0.00 | 450719.73 | 0.000 | 93.75% | 90.91% | `{"general": 0.5562927722930908}` |
| filetypes/elf | or_general_primary | 21965 | 111877 | 87.17% | 1 | 8.94 | 42.40 | 0.421 | 93.14% | 97.89% | `{"filegroups/native": 1.0, "filetypes/elf": 1.0, "general": 0.9891113042831421}` |
| filetypes/package.json† | or_general_primary | 15658 | 7205 | 86.72% | 0 | 0.00 | 415.70 | 0.000 | 92.89% | 90.90% | `{"filegroups/config": 1.0, "filetypes/package.json": 1.0, "general": 0.9915000796318054}` |
| filetypes/tar.gz† | or_general_primary | 19387 | 11894 | 85.12% | 0 | 0.00 | 251.84 | 0.000 | 91.96% | 90.78% | `{"filegroups/archive": 1.0, "filetypes/tar.gz": 1.0, "general": 0.9977129101753235}` |
| filetypes/cab† | general_only | 5 | 23 | 80.00% | 0 | 0.00 | 122123.39 | 0.000 | 88.89% | 96.43% | `{"general": 0.9920740127563477}` |
| filetypes/zip† | or_general_primary | 32962 | 5584 | 77.44% | 0 | 0.00 | 536.34 | 0.000 | 87.28% | 80.71% | `{"filegroups/archive": 0.006320903543382883, "filetypes/zip": 1.0, "general": 0.9965186715126038}` |
| filetypes/xz† | general_only | 42 | 23367 | 76.19% | 0 | 0.00 | 128.20 | 0.000 | 86.49% | 99.96% | `{"general": 0.8812193274497986}` |
| filetypes/7z† | general_only | 3780 | 34 | 75.16% | 0 | 0.00 | 84339.64 | 0.000 | 85.82% | 75.38% | `{"general": 0.9988694190979004}` |
| filetypes/jar† | general_only | 606 | 1566 | 74.26% | 0 | 0.00 | 1911.15 | 0.000 | 85.23% | 92.82% | `{"general": 0.9402996897697449}` |
| filetypes/applescript† | general_only | 22 | 100 | 72.73% | 0 | 0.00 | 29513.05 | 0.000 | 84.21% | 95.08% | `{"general": 0.9594946503639221}` |
| filetypes/javascript | or_general_primary | 57629 | 375582 | 72.68% | 10 | 26.63 | 45.16 | 4.215 | 84.17% | 96.36% | `{"filegroups/scripts": 1.0, "filetypes/javascript": 1.0, "general": 0.9919425249099731}` |
| filetypes/xls† | general_only | 229 | 42 | 69.00% | 0 | 0.00 | 68842.61 | 0.000 | 81.65% | 73.80% | `{"general": 0.29995617270469666}` |
| filetypes/tar.bz2† | general_only | 3 | 186 | 66.67% | 0 | 0.00 | 15977.08 | 0.000 | 80.00% | 99.47% | `{"general": 0.9955074191093445}` |
| filetypes/perl† | or_general_primary | 157 | 29368 | 65.61% | 0 | 0.00 | 102.00 | 0.000 | 79.23% | 99.82% | `{"filegroups/scripts": 1.0, "filetypes/perl": 1.0, "general": 0.9737693071365356}` |
| filetypes/pe | or_general_primary | 410851 | 140808 | 63.20% | 2 | 14.20 | 44.71 | 0.843 | 77.45% | 72.59% | `{"filegroups/native": 1.0, "filetypes/pe": 0.9999626874923706, "general": 0.9979832172393799}` |
| filetypes/docx† | general_only | 372 | 219 | 61.83% | 0 | 0.00 | 13586.01 | 0.000 | 76.41% | 75.97% | `{"general": 0.860793948173523}` |
| filetypes/kotlin† | or_general_primary | 928 | 34931 | 60.88% | 0 | 0.00 | 85.76 | 0.000 | 75.69% | 98.99% | `{"filegroups/source": 1.0, "filetypes/kotlin": 1.0, "general": 0.7555142045021057}` |
| filetypes/ruby† | or_general_primary | 70 | 23108 | 60.00% | 0 | 0.00 | 129.63 | 0.000 | 75.00% | 99.88% | `{"filegroups/scripts": 1.0, "filetypes/ruby": 1.0, "general": 0.9729308485984802}` |
| filetypes/objc† | general_only | 5 | 17944 | 60.00% | 0 | 0.00 | 166.94 | 0.000 | 75.00% | 99.99% | `{"general": 0.9903209805488586}` |
| filetypes/python | or_general_primary | 13423 | 112372 | 57.42% | 1 | 8.90 | 42.22 | 0.421 | 72.95% | 95.46% | `{"filegroups/scripts": 1.0, "filetypes/python": 1.0, "general": 0.9963129758834839}` |

## L9 Suspicious

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/1M | 95% CI upper | Global FP/1M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html† | general_only | 9 | 1384 | 100.00% | 0 | 0.00 | 2162.21 | 0.000 | 100.00% | 100.00% | `{"general": 0.8594487309455872}` |
| filetypes/desktop-entry† | general_only | 2 | 231 | 100.00% | 0 | 0.00 | 12884.81 | 0.000 | 100.00% | 100.00% | `{"general": 0.9922379851341248}` |
| filetypes/pkg† | general_only | 1 | 13 | 100.00% | 0 | 0.00 | 205816.67 | 0.000 | 100.00% | 100.00% | `{"general": 0.0017194385873153806}` |
| filetypes/doc† | general_only | 1899 | 23 | 99.79% | 0 | 0.00 | 122123.39 | 0.000 | 99.89% | 99.79% | `{"general": 0.002071269089356065}` |
| filetypes/lnk† | general_only | 285 | 17 | 99.30% | 0 | 0.00 | 161566.11 | 0.000 | 99.65% | 99.34% | `{"general": 0.0039053931832313538}` |
| filetypes/tar† | or_general_primary | 1042 | 355 | 97.02% | 0 | 0.00 | 8403.18 | 0.000 | 98.49% | 97.78% | `{"filegroups/archive": 1.0, "general": 0.7734574675559998}` |
| filetypes/zst† | general_only | 2282 | 16150 | 96.93% | 0 | 0.00 | 185.48 | 0.000 | 98.44% | 99.62% | `{"general": 0.8446625471115112}` |
| filetypes/rar† | general_only | 952 | 4 | 95.69% | 0 | 0.00 | 527129.20 | 0.000 | 97.80% | 95.71% | `{"general": 0.0008109572809189558}` |
| filetypes/rtf† | general_only | 89 | 437 | 95.51% | 0 | 0.00 | 6831.78 | 0.000 | 97.70% | 99.24% | `{"general": 0.9508298635482788}` |
| filetypes/pkg-info† | general_only | 3681 | 807 | 91.69% | 0 | 0.00 | 3705.30 | 0.000 | 95.66% | 93.18% | `{"general": 0.7194933891296387}` |
| filetypes/chm† | general_only | 17 | 5 | 88.24% | 0 | 0.00 | 450719.73 | 0.000 | 93.75% | 90.91% | `{"general": 0.5562927722930908}` |
| filetypes/elf | or_general_primary | 21965 | 111877 | 87.18% | 3 | 26.82 | 69.30 | 1.264 | 93.14% | 97.89% | `{"filegroups/native": 1.0, "filetypes/elf": 1.0, "general": 0.9890598058700562}` |
| filetypes/package.json† | or_general_primary | 15658 | 7205 | 86.72% | 0 | 0.00 | 415.70 | 0.000 | 92.89% | 90.90% | `{"filegroups/config": 1.0, "filetypes/package.json": 1.0, "general": 0.9915000796318054}` |
| filetypes/tar.gz† | or_general_primary | 19387 | 11894 | 85.12% | 0 | 0.00 | 251.84 | 0.000 | 91.96% | 90.78% | `{"filegroups/archive": 1.0, "filetypes/tar.gz": 1.0, "general": 0.9977129101753235}` |
| filetypes/cab† | general_only | 5 | 23 | 80.00% | 0 | 0.00 | 122123.39 | 0.000 | 88.89% | 96.43% | `{"general": 0.9920740127563477}` |
| filetypes/javascript | or_general_primary | 57629 | 375582 | 79.78% | 20 | 53.25 | 77.38 | 8.429 | 88.74% | 97.31% | `{"filegroups/scripts": 1.0, "filetypes/javascript": 1.0, "general": 0.9867922067642212}` |
| filetypes/zip† | or_general_primary | 32962 | 5584 | 77.44% | 0 | 0.00 | 536.34 | 0.000 | 87.28% | 80.71% | `{"filegroups/archive": 0.006320903543382883, "filetypes/zip": 1.0, "general": 0.9965186715126038}` |
| filetypes/xz† | general_only | 42 | 23367 | 76.19% | 0 | 0.00 | 128.20 | 0.000 | 86.49% | 99.96% | `{"general": 0.8812193274497986}` |
| filetypes/7z† | general_only | 3780 | 34 | 75.16% | 0 | 0.00 | 84339.64 | 0.000 | 85.82% | 75.38% | `{"general": 0.9988694190979004}` |
| filetypes/jar† | general_only | 606 | 1566 | 74.26% | 0 | 0.00 | 1911.15 | 0.000 | 85.23% | 92.82% | `{"general": 0.9402996897697449}` |
| filetypes/applescript† | general_only | 22 | 100 | 72.73% | 0 | 0.00 | 29513.05 | 0.000 | 84.21% | 95.08% | `{"general": 0.9594946503639221}` |
| filetypes/python | or_general_primary | 13423 | 112372 | 71.68% | 3 | 26.70 | 69.00 | 1.264 | 83.50% | 96.98% | `{"filegroups/scripts": 1.0, "filetypes/python": 1.0, "general": 0.9934084415435791}` |
| filetypes/xls† | general_only | 229 | 42 | 69.00% | 0 | 0.00 | 68842.61 | 0.000 | 81.65% | 73.80% | `{"general": 0.29995617270469666}` |
| filetypes/pe | or_general_primary | 410851 | 140808 | 66.84% | 5 | 35.51 | 74.66 | 2.107 | 80.12% | 75.30% | `{"filegroups/native": 1.0, "filetypes/pe": 0.9999626874923706, "general": 0.9975352883338928}` |
| filetypes/tar.bz2† | general_only | 3 | 186 | 66.67% | 0 | 0.00 | 15977.08 | 0.000 | 80.00% | 99.47% | `{"general": 0.9955074191093445}` |
| filetypes/perl† | or_general_primary | 157 | 29368 | 65.61% | 0 | 0.00 | 102.00 | 0.000 | 79.23% | 99.82% | `{"filegroups/scripts": 1.0, "filetypes/perl": 1.0, "general": 0.9737693071365356}` |
| filetypes/java_class | general_only | 603 | 184472 | 62.02% | 8 | 43.37 | 78.25 | 3.372 | 75.94% | 99.87% | `{"general": 0.9439346790313721}` |
| filetypes/docx† | general_only | 372 | 219 | 61.83% | 0 | 0.00 | 13586.01 | 0.000 | 76.41% | 75.97% | `{"general": 0.860793948173523}` |
| filetypes/kotlin† | or_general_primary | 928 | 34931 | 60.88% | 0 | 0.00 | 85.76 | 0.000 | 75.69% | 98.99% | `{"filegroups/source": 1.0, "filetypes/kotlin": 1.0, "general": 0.7555142045021057}` |
| filetypes/ruby† | or_general_primary | 70 | 23108 | 60.00% | 0 | 0.00 | 129.63 | 0.000 | 75.00% | 99.88% | `{"filegroups/scripts": 1.0, "filetypes/ruby": 1.0, "general": 0.9729308485984802}` |
