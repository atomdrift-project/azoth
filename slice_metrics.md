# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `1310931333`
- Rows: 4682982 (1692465 malware, 2990517 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4682982 | 1692465 | 2990517 | 69.91% | 0.01% | 135.76 | 99.97% | 82.28% | 89.12% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/perl,filetypes/python-bytecode,filetypes/package.json,filetypes/unknown,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 204813 | 70572 | 134241 | 95.11% | 0.00% | 37.246 | 99.99% | 97.49% | 98.31% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1049319 | 897596 | 151723 | 81.44% | 0.02% | 164.77 | 100.00% | 89.77% | 84.12% | general,filegroups/native,filetypes/pe |
| filetype/python | 147386 | 17903 | 129483 | 66.49% | 0.01% | 61.784 | 99.93% | 79.85% | 95.92% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 552073 | 83592 | 468481 | 69.62% | 0.00% | 32.018 | 99.97% | 82.08% | 95.40% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11656 | 10634 | 1022 | 98.99% | 1.17% | 11742 | 99.89% | 99.44% | 98.98% | general,filetypes/pkg-info |
| filetype/rtf | 1935 | 1455 | 480 | 98.08% | 0.83% | 8333.3 | 99.72% | 98.89% | 98.35% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 28802 | 17780 | 11022 | 97.72% | 0.06% | 635.09 | 99.96% | 98.83% | 98.57% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7281 | 1924 | 5357 | 96.57% | 0.13% | 1306.7 | 99.62% | 98.07% | 99.00% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 171892 | 168290 | 3602 | 93.77% | 0.11% | 1110.5 | 100.00% | 96.78% | 93.90% | general,filegroups/scripts,filetypes/batch |
| filetype/xls | 10526 | 10475 | 51 | 92.99% | 0.00% | 0 | 100.00% | 96.37% | 93.03% | general,filegroups/documents |
| filetype/python-bytecode | 31357 | 1856 | 29501 | 90.03% | 0.03% | 271.18 | 99.52% | 94.54% | 99.38% | general,filetypes/python-bytecode |
| filetype/perl | 31739 | 224 | 31515 | 83.04% | 0.06% | 634.62 | 90.29% | 86.51% | 99.82% | general,filegroups/scripts,filetypes/perl |
| filetype/shell | 51768 | 6515 | 45253 | 82.49% | 0.02% | 198.88 | 99.83% | 90.33% | 97.78% | general,filegroups/scripts,filetypes/shell |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4682982 | 1692465 | 2990517 | 70.87% | 0.01% | 147.13 | 99.96% | 82.94% | 89.46% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/perl,filetypes/python-bytecode,filetypes/package.json,filetypes/unknown,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 204813 | 70572 | 134241 | 95.20% | 0.00% | 44.696 | 99.99% | 97.54% | 98.34% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1049319 | 897596 | 151723 | 82.56% | 0.02% | 237.27 | 100.00% | 90.45% | 85.08% | general,filegroups/native,filetypes/pe |
| filetype/python | 147386 | 17903 | 129483 | 66.51% | 0.01% | 61.784 | 99.93% | 79.86% | 95.93% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 552073 | 83592 | 468481 | 70.86% | 0.00% | 38.422 | 99.97% | 82.93% | 95.58% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11656 | 10634 | 1022 | 98.99% | 1.17% | 11742 | 99.89% | 99.44% | 98.98% | general,filetypes/pkg-info |
| filetype/rtf | 1935 | 1455 | 480 | 98.08% | 0.83% | 8333.3 | 99.72% | 98.89% | 98.35% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 28802 | 17780 | 11022 | 97.72% | 0.06% | 635.09 | 99.96% | 98.83% | 98.57% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7281 | 1924 | 5357 | 96.57% | 0.13% | 1306.7 | 99.62% | 98.07% | 99.00% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 171892 | 168290 | 3602 | 93.77% | 0.11% | 1110.5 | 100.00% | 96.78% | 93.90% | general,filegroups/scripts,filetypes/batch |
| filetype/xls | 10526 | 10475 | 51 | 92.99% | 0.00% | 0 | 100.00% | 96.37% | 93.03% | general,filegroups/documents |
| filetype/python-bytecode | 31357 | 1856 | 29501 | 90.03% | 0.03% | 271.18 | 99.52% | 94.54% | 99.38% | general,filetypes/python-bytecode |
| filetype/perl | 31739 | 224 | 31515 | 83.04% | 0.06% | 634.62 | 90.29% | 86.51% | 99.82% | general,filegroups/scripts,filetypes/perl |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4682982 | 1692465 | 2990517 | 73.64% | 0.02% | 239.76 | 99.94% | 84.80% | 90.46% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/perl,filetypes/python-bytecode,filetypes/package.json,filetypes/unknown,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 204813 | 70572 | 134241 | 95.47% | 0.01% | 74.493 | 99.99% | 97.68% | 98.43% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1049319 | 897596 | 151723 | 85.68% | 0.06% | 632.73 | 99.99% | 92.28% | 87.74% | general,filegroups/native,filetypes/pe |
| filetype/python | 147386 | 17903 | 129483 | 68.58% | 0.02% | 208.52 | 99.78% | 81.29% | 96.17% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 552073 | 83592 | 468481 | 78.26% | 0.02% | 217.72 | 99.84% | 87.74% | 96.69% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11656 | 10634 | 1022 | 98.99% | 1.17% | 11742 | 99.89% | 99.44% | 98.98% | general,filetypes/pkg-info |
| filetype/rtf | 1935 | 1455 | 480 | 98.08% | 0.83% | 8333.3 | 99.72% | 98.89% | 98.35% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 28802 | 17780 | 11022 | 97.72% | 0.06% | 635.09 | 99.96% | 98.83% | 98.57% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7281 | 1924 | 5357 | 96.57% | 0.13% | 1306.7 | 99.62% | 98.07% | 99.00% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 171892 | 168290 | 3602 | 93.95% | 0.25% | 2498.6 | 99.99% | 96.88% | 94.07% | general,filegroups/scripts,filetypes/batch |
| filetype/xls | 10526 | 10475 | 51 | 92.99% | 0.00% | 0 | 100.00% | 96.37% | 93.03% | general,filegroups/documents |
| filetype/python-bytecode | 31357 | 1856 | 29501 | 90.03% | 0.03% | 271.18 | 99.52% | 94.54% | 99.38% | general,filetypes/python-bytecode |
| filetype/perl | 31739 | 224 | 31515 | 83.04% | 0.06% | 634.62 | 90.29% | 86.51% | 99.82% | general,filegroups/scripts,filetypes/perl |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4682982 | 1692465 | 2990517 | 77.68% | 0.03% | 314.66 | 99.93% | 87.41% | 91.91% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/perl,filetypes/python-bytecode,filetypes/package.json,filetypes/unknown,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 204813 | 70572 | 134241 | 96.11% | 0.01% | 119.19 | 99.98% | 98.01% | 98.65% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1049319 | 897596 | 151723 | 92.51% | 0.13% | 1285.2 | 99.98% | 96.10% | 93.57% | general,filegroups/native,filetypes/pe |
| filetype/python | 147386 | 17903 | 129483 | 68.65% | 0.02% | 223.97 | 99.76% | 81.33% | 96.17% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 552073 | 83592 | 468481 | 78.53% | 0.02% | 228.4 | 99.84% | 87.91% | 96.73% | general,filegroups/scripts,filetypes/javascript |
| filetype/package.json | 28802 | 17780 | 11022 | 99.38% | 0.14% | 1360.9 | 99.92% | 99.65% | 99.57% | general,filegroups/config,filetypes/package.json |
| filetype/pkg-info | 11656 | 10634 | 1022 | 98.99% | 1.17% | 11742 | 99.89% | 99.44% | 98.98% | general,filetypes/pkg-info |
| filetype/rtf | 1935 | 1455 | 480 | 98.08% | 0.83% | 8333.3 | 99.72% | 98.89% | 98.35% | general,filegroups/documents,filetypes/rtf |
| filetype/ole | 7281 | 1924 | 5357 | 96.57% | 0.13% | 1306.7 | 99.62% | 98.07% | 99.00% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 171892 | 168290 | 3602 | 93.96% | 0.25% | 2498.6 | 99.99% | 96.89% | 94.08% | general,filegroups/scripts,filetypes/batch |
| filetype/xls | 10526 | 10475 | 51 | 92.99% | 0.00% | 0 | 100.00% | 96.37% | 93.03% | general,filegroups/documents |
| filetype/python-bytecode | 31357 | 1856 | 29501 | 90.03% | 0.03% | 271.18 | 99.52% | 94.54% | 99.38% | general,filetypes/python-bytecode |
| filetype/java_class | 368768 | 1297 | 367471 | 84.58% | 0.01% | 127.9 | 95.89% | 89.88% | 99.93% | general,filegroups/portable,filetypes/java_class |
