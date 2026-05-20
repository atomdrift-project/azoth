# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `1349983353`
- Rows: 4727335 (1702977 malware, 3024358 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727335 | 1702977 | 3024358 | 78.86% | 0.02% | 150.11 | 99.97% | 88.17% | 92.38% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208678 | 73107 | 135571 | 96.87% | 0.00% | 44.257 | 99.99% | 98.40% | 98.90% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053636 | 901669 | 151967 | 94.25% | 0.01% | 111.87 | 100.00% | 97.04% | 95.08% | general,filegroups/native,filetypes/pe |
| filetype/python | 148142 | 17917 | 130225 | 71.81% | 0.00% | 38.395 | 99.96% | 83.58% | 96.59% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556832 | 84374 | 472458 | 94.40% | 0.01% | 57.148 | 99.97% | 97.10% | 99.15% | general,filegroups/scripts,filetypes/javascript |
| filetype/batch | 172618 | 168939 | 3679 | 99.37% | 0.05% | 543.63 | 100.00% | 99.68% | 99.39% | general,filegroups/scripts,filetypes/batch |
| filetype/pkg-info | 11667 | 10634 | 1033 | 98.66% | 0.00% | 0 | 100.00% | 99.33% | 98.78% | general,filetypes/pkg-info |
| filetype/rtf | 1945 | 1465 | 480 | 98.02% | 0.83% | 8333.3 | 99.72% | 98.86% | 98.30% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 29418 | 17793 | 11625 | 97.54% | 0.04% | 430.11 | 99.97% | 98.74% | 98.50% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7285 | 1928 | 5357 | 96.32% | 0.13% | 1306.7 | 99.62% | 97.94% | 98.93% | general,filegroups/documents,filetypes/ole |
| filetype/kotlin | 66007 | 23477 | 42530 | 95.81% | 0.01% | 70.538 | 99.99% | 97.86% | 98.51% | general,filegroups/source,filetypes/kotlin |
| filetype/php | 90446 | 3856 | 86590 | 94.45% | 0.01% | 57.743 | 99.86% | 97.08% | 99.76% | general,filegroups/scripts,filetypes/php |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727335 | 1702977 | 3024358 | 79.18% | 0.01% | 148.13 | 99.97% | 88.37% | 92.49% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208678 | 73107 | 135571 | 96.87% | 0.00% | 44.257 | 99.99% | 98.40% | 98.90% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053636 | 901669 | 151967 | 94.33% | 0.01% | 138.19 | 100.00% | 97.08% | 95.15% | general,filegroups/native,filetypes/pe |
| filetype/python | 148142 | 17917 | 130225 | 71.82% | 0.00% | 38.395 | 99.96% | 83.59% | 96.59% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556832 | 84374 | 472458 | 94.40% | 0.01% | 57.148 | 99.97% | 97.10% | 99.15% | general,filegroups/scripts,filetypes/javascript |
| filetype/batch | 172618 | 168939 | 3679 | 99.37% | 0.05% | 543.63 | 100.00% | 99.68% | 99.39% | general,filegroups/scripts,filetypes/batch |
| filetype/pkg-info | 11667 | 10634 | 1033 | 98.67% | 0.00% | 0 | 100.00% | 99.33% | 98.79% | general,filetypes/pkg-info |
| filetype/rtf | 1945 | 1465 | 480 | 98.02% | 0.83% | 8333.3 | 99.72% | 98.86% | 98.30% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 29418 | 17793 | 11625 | 97.54% | 0.04% | 430.11 | 99.97% | 98.74% | 98.50% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7285 | 1928 | 5357 | 96.32% | 0.13% | 1306.7 | 99.62% | 97.94% | 98.93% | general,filegroups/documents,filetypes/ole |
| filetype/kotlin | 66007 | 23477 | 42530 | 95.81% | 0.01% | 70.538 | 99.99% | 97.85% | 98.50% | general,filegroups/source,filetypes/kotlin |
| filetype/php | 90446 | 3856 | 86590 | 94.45% | 0.01% | 57.743 | 99.86% | 97.08% | 99.76% | general,filegroups/scripts,filetypes/php |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727335 | 1702977 | 3024358 | 80.87% | 0.03% | 259.89 | 99.94% | 89.40% | 93.09% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208678 | 73107 | 135571 | 96.90% | 0.01% | 51.633 | 99.99% | 98.42% | 98.91% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053636 | 901669 | 151967 | 94.96% | 0.08% | 750.16 | 99.99% | 97.41% | 95.68% | general,filegroups/native,filetypes/pe |
| filetype/python | 148142 | 17917 | 130225 | 84.42% | 0.02% | 184.3 | 99.84% | 91.49% | 98.10% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556832 | 84374 | 472458 | 95.66% | 0.01% | 135.46 | 99.92% | 97.74% | 99.33% | general,filegroups/scripts,filetypes/javascript |
| filetype/batch | 172618 | 168939 | 3679 | 99.74% | 0.22% | 2174.5 | 100.00% | 99.87% | 99.74% | general,filegroups/scripts,filetypes/batch |
| filetype/package.json | 29418 | 17793 | 11625 | 99.40% | 0.14% | 1376.3 | 99.91% | 99.65% | 99.58% | general,filegroups/config,filetypes/package.json |
| filetype/pkg-info | 11667 | 10634 | 1033 | 98.99% | 0.68% | 6776.4 | 99.93% | 99.46% | 99.02% | general,filetypes/pkg-info |
| filetype/rtf | 1945 | 1465 | 480 | 98.02% | 0.83% | 8333.3 | 99.72% | 98.86% | 98.30% | general,filegroups/documents,filetypes/rtf |
| filetype/ole | 7285 | 1928 | 5357 | 96.32% | 0.13% | 1306.7 | 99.62% | 97.94% | 98.93% | general,filegroups/documents,filetypes/ole |
| filetype/kotlin | 66007 | 23477 | 42530 | 95.89% | 0.07% | 681.87 | 99.87% | 97.84% | 98.49% | general,filegroups/source,filetypes/kotlin |
| filetype/php | 90446 | 3856 | 86590 | 94.50% | 0.01% | 69.292 | 99.84% | 97.10% | 99.76% | general,filegroups/scripts,filetypes/php |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4727335 | 1702977 | 3024358 | 82.42% | 0.04% | 350.16 | 99.92% | 90.33% | 93.65% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/javascript,filetypes/c,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/xml,filetypes/python,filetypes/png,filetypes/go,filetypes/php,filetypes/rust,filetypes/kotlin,filetypes/text,filetypes/csharp,filetypes/shell,filetypes/python-bytecode,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/plist,filetypes/macho,filetypes/jpeg,filetypes/pkg-info,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/powershell,filetypes/jar,filetypes/lnk,filetypes/rtf |
| filetype/elf | 208678 | 73107 | 135571 | 97.97% | 0.02% | 154.9 | 99.97% | 98.96% | 99.28% | general,filegroups/native,filetypes/elf |
| filetype/pe | 1053636 | 901669 | 151967 | 97.21% | 0.13% | 1309.5 | 99.98% | 98.58% | 97.59% | general,filegroups/native,filetypes/pe |
| filetype/python | 148142 | 17917 | 130225 | 87.22% | 0.03% | 322.52 | 99.73% | 93.06% | 98.43% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 556832 | 84374 | 472458 | 96.21% | 0.02% | 201.08 | 99.88% | 98.01% | 99.41% | general,filegroups/scripts,filetypes/javascript |
| filetype/batch | 172618 | 168939 | 3679 | 99.81% | 0.33% | 3261.8 | 99.99% | 99.90% | 99.80% | general,filegroups/scripts,filetypes/batch |
| filetype/package.json | 29418 | 17793 | 11625 | 99.40% | 0.14% | 1376.3 | 99.91% | 99.65% | 99.58% | general,filegroups/config,filetypes/package.json |
| filetype/pkg-info | 11667 | 10634 | 1033 | 98.99% | 0.68% | 6776.4 | 99.93% | 99.46% | 99.02% | general,filetypes/pkg-info |
| filetype/rtf | 1945 | 1465 | 480 | 98.02% | 0.83% | 8333.3 | 99.72% | 98.86% | 98.30% | general,filegroups/documents,filetypes/rtf |
| filetype/ole | 7285 | 1928 | 5357 | 96.32% | 0.13% | 1306.7 | 99.62% | 97.94% | 98.93% | general,filegroups/documents,filetypes/ole |
| filetype/kotlin | 66007 | 23477 | 42530 | 95.92% | 0.09% | 917 | 99.83% | 97.83% | 98.49% | general,filegroups/source,filetypes/kotlin |
| filetype/php | 90446 | 3856 | 86590 | 94.58% | 0.01% | 115.49 | 99.73% | 97.09% | 99.76% | general,filegroups/scripts,filetypes/php |
