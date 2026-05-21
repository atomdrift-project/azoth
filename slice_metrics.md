# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `1384435807`
- Rows: 4727598 (1703195 malware, 3024403 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727598 | 1703195 | 3024403 | 89.81% | 0.10% | 984.33 | 99.81% | 94.54% | 96.27% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208758 | 73175 | 135583 | 99.98% | 0.03% | 287.65 | 99.95% | 99.96% | 99.97% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053716 | 901748 | 151968 | 93.40% | 0.01% | 118.45 | 100.00% | 96.59% | 94.35% | general,filegroups/native,filetypes/pe |
| filetype/python | 148143 | 17917 | 130226 | 93.40% | 0.02% | 153.58 | 99.88% | 96.53% | 99.19% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556861 | 84394 | 472467 | 94.25% | 0.00% | 48.681 | 99.97% | 97.03% | 99.13% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11667 | 10634 | 1033 | 99.94% | 1.45% | 14521 | 99.86% | 99.90% | 99.82% | general,filetypes/pkg-info |
| filetype/batch | 172620 | 168941 | 3679 | 99.72% | 0.19% | 1902.7 | 100.00% | 99.86% | 99.72% | general,filegroups/scripts,filetypes/batch |
| filetype/python-bytecode | 32792 | 1868 | 30924 | 99.52% | 0.02% | 161.69 | 99.73% | 99.62% | 99.96% | general,filetypes/python-bytecode |
| filetype/package.json | 29419 | 17793 | 11626 | 99.33% | 0.03% | 344.06 | 99.98% | 99.65% | 99.58% | general,filegroups/config,filetypes/package.json |
| filetype/perl | 31768 | 224 | 31544 | 99.11% | 0.05% | 538.93 | 92.89% | 95.90% | 99.94% | general,filegroups/scripts,filetypes/perl |
| filetype/macho | 12760 | 2067 | 10693 | 98.89% | 0.05% | 467.6 | 99.76% | 99.32% | 99.78% | general,filegroups/native,filetypes/macho |
| filetype/doc | 11066 | 11032 | 34 | 98.77% | 0.00% | 0 | 100.00% | 99.38% | 98.77% | general,filegroups/documents |
| filetype/pdf | 187078 | 173215 | 13863 | 98.44% | 0.03% | 288.54 | 100.00% | 99.21% | 98.55% | general,filegroups/documents,filetypes/pdf |
| filetype/ole | 7285 | 1928 | 5357 | 98.18% | 0.19% | 1866.7 | 99.47% | 98.83% | 99.38% | general,filegroups/documents,filetypes/ole |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727598 | 1703195 | 3024403 | 90.38% | 0.10% | 995.9 | 99.80% | 94.86% | 96.47% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208758 | 73175 | 135583 | 99.98% | 0.03% | 287.65 | 99.95% | 99.96% | 99.97% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053716 | 901748 | 151968 | 93.56% | 0.02% | 223.73 | 100.00% | 96.67% | 94.49% | general,filegroups/native,filetypes/pe |
| filetype/python | 148143 | 17917 | 130226 | 95.36% | 0.02% | 199.65 | 99.85% | 97.55% | 99.42% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556861 | 84394 | 472467 | 94.25% | 0.00% | 48.681 | 99.97% | 97.03% | 99.13% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11667 | 10634 | 1033 | 99.94% | 1.45% | 14521 | 99.86% | 99.90% | 99.82% | general,filetypes/pkg-info |
| filetype/batch | 172620 | 168941 | 3679 | 99.72% | 0.19% | 1902.7 | 100.00% | 99.86% | 99.72% | general,filegroups/scripts,filetypes/batch |
| filetype/python-bytecode | 32792 | 1868 | 30924 | 99.52% | 0.02% | 161.69 | 99.73% | 99.62% | 99.96% | general,filetypes/python-bytecode |
| filetype/package.json | 29419 | 17793 | 11626 | 99.33% | 0.03% | 344.06 | 99.98% | 99.65% | 99.58% | general,filegroups/config,filetypes/package.json |
| filetype/perl | 31768 | 224 | 31544 | 99.11% | 0.05% | 538.93 | 92.89% | 95.90% | 99.94% | general,filegroups/scripts,filetypes/perl |
| filetype/macho | 12760 | 2067 | 10693 | 98.89% | 0.05% | 467.6 | 99.76% | 99.32% | 99.78% | general,filegroups/native,filetypes/macho |
| filetype/doc | 11066 | 11032 | 34 | 98.77% | 0.00% | 0 | 100.00% | 99.38% | 98.77% | general,filegroups/documents |
| filetype/pdf | 187078 | 173215 | 13863 | 98.44% | 0.03% | 288.54 | 100.00% | 99.21% | 98.55% | general,filegroups/documents,filetypes/pdf |
| filetype/ole | 7285 | 1928 | 5357 | 98.18% | 0.19% | 1866.7 | 99.47% | 98.83% | 99.38% | general,filegroups/documents,filetypes/ole |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727598 | 1703195 | 3024403 | 91.56% | 0.11% | 1075.6 | 99.79% | 95.50% | 96.89% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208758 | 73175 | 135583 | 99.98% | 0.03% | 287.65 | 99.95% | 99.96% | 99.97% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053716 | 901748 | 151968 | 94.47% | 0.07% | 671.19 | 99.99% | 97.15% | 95.26% | general,filegroups/native,filetypes/pe |
| filetype/python | 148143 | 17917 | 130226 | 97.81% | 0.05% | 537.53 | 99.60% | 98.70% | 99.69% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556861 | 84394 | 472467 | 95.81% | 0.01% | 137.58 | 99.92% | 97.82% | 99.35% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11667 | 10634 | 1033 | 99.94% | 1.45% | 14521 | 99.86% | 99.90% | 99.82% | general,filetypes/pkg-info |
| filetype/batch | 172620 | 168941 | 3679 | 99.80% | 0.27% | 2718.1 | 99.99% | 99.90% | 99.80% | general,filegroups/scripts,filetypes/batch |
| filetype/package.json | 29419 | 17793 | 11626 | 99.53% | 0.10% | 1032.2 | 99.93% | 99.73% | 99.67% | general,filegroups/config,filetypes/package.json |
| filetype/python-bytecode | 32792 | 1868 | 30924 | 99.52% | 0.02% | 161.69 | 99.73% | 99.62% | 99.96% | general,filetypes/python-bytecode |
| filetype/perl | 31768 | 224 | 31544 | 99.11% | 0.05% | 538.93 | 92.89% | 95.90% | 99.94% | general,filegroups/scripts,filetypes/perl |
| filetype/macho | 12760 | 2067 | 10693 | 98.89% | 0.05% | 467.6 | 99.76% | 99.32% | 99.78% | general,filegroups/native,filetypes/macho |
| filetype/doc | 11066 | 11032 | 34 | 98.77% | 0.00% | 0 | 100.00% | 99.38% | 98.77% | general,filegroups/documents |
| filetype/pdf | 187078 | 173215 | 13863 | 98.44% | 0.03% | 288.54 | 100.00% | 99.21% | 98.56% | general,filegroups/documents,filetypes/pdf |
| filetype/ole | 7285 | 1928 | 5357 | 98.18% | 0.19% | 1866.7 | 99.47% | 98.83% | 99.38% | general,filegroups/documents,filetypes/ole |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727598 | 1703195 | 3024403 | 92.59% | 0.12% | 1241.2 | 99.76% | 96.04% | 97.25% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208758 | 73175 | 135583 | 99.98% | 0.03% | 302.4 | 99.94% | 99.96% | 99.97% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053716 | 901748 | 151968 | 95.89% | 0.11% | 1072.6 | 99.98% | 97.89% | 96.47% | general,filegroups/native,filetypes/pe |
| filetype/python | 148143 | 17917 | 130226 | 98.25% | 0.08% | 752.54 | 99.45% | 98.84% | 99.72% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556861 | 84394 | 472467 | 96.60% | 0.02% | 243.4 | 99.86% | 98.20% | 99.46% | general,filegroups/scripts,filetypes/javascript |
| filetype/pkg-info | 11667 | 10634 | 1033 | 99.94% | 1.45% | 14521 | 99.86% | 99.90% | 99.82% | general,filetypes/pkg-info |
| filetype/batch | 172620 | 168941 | 3679 | 99.84% | 0.38% | 3805.4 | 99.99% | 99.91% | 99.83% | general,filegroups/scripts,filetypes/batch |
| filetype/package.json | 29419 | 17793 | 11626 | 99.53% | 0.10% | 1032.2 | 99.93% | 99.73% | 99.67% | general,filegroups/config,filetypes/package.json |
| filetype/python-bytecode | 32792 | 1868 | 30924 | 99.52% | 0.02% | 161.69 | 99.73% | 99.62% | 99.96% | general,filetypes/python-bytecode |
| filetype/perl | 31768 | 224 | 31544 | 99.11% | 0.05% | 538.93 | 92.89% | 95.90% | 99.94% | general,filegroups/scripts,filetypes/perl |
| filetype/macho | 12760 | 2067 | 10693 | 98.89% | 0.05% | 467.6 | 99.76% | 99.32% | 99.78% | general,filegroups/native,filetypes/macho |
| filetype/doc | 11066 | 11032 | 34 | 98.77% | 0.00% | 0 | 100.00% | 99.38% | 98.77% | general,filegroups/documents |
| filetype/pdf | 187078 | 173215 | 13863 | 98.45% | 0.03% | 288.54 | 100.00% | 99.22% | 98.56% | general,filegroups/documents,filetypes/pdf |
