# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `1234486188`
- Rows: 4231044 (1486369 malware, 2744675 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4231044 | 1486369 | 2744675 | 69.05% | 0.01% | 124.24 | 99.97% | 81.68% | 89.12% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/php,filetypes/text,filetypes/csharp,filetypes/zip,filetypes/kotlin,filetypes/shell,filetypes/gz,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/xz,filetypes/ruby,filetypes/python-bytecode,filetypes/makefile,filetypes/plist,filetypes/pkg-info,filetypes/jpeg,filetypes/macho,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/jar,filetypes/powershell,filetypes/lnk,filetypes/rtf |
| filetype/elf | 159208 | 36386 | 122822 | 95.83% | 0.01% | 73.277 | 99.97% | 97.86% | 99.04% | general,filegroups/native,filetypes/elf |
| filetype/pe | 961480 | 812716 | 148764 | 79.30% | 0.01% | 100.83 | 100.00% | 88.45% | 82.50% | general,filegroups/native,filetypes/pe |
| filetype/python | 141020 | 17651 | 123369 | 70.02% | 0.02% | 170.22 | 99.83% | 82.31% | 96.23% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 512705 | 76882 | 435823 | 60.81% | 0.00% | 16.062 | 99.99% | 75.63% | 94.12% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 26530 | 10380 | 16150 | 100.00% | 0.13% | 1300.3 | 99.80% | 99.90% | 99.92% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 11559 | 10633 | 926 | 98.42% | 0.97% | 9719.2 | 99.91% | 99.16% | 98.47% | general,filetypes/pkg-info |
| filetype/rtf | 1815 | 1340 | 475 | 98.06% | 0.21% | 2105.3 | 99.92% | 98.98% | 98.51% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 27307 | 17700 | 9607 | 97.99% | 0.05% | 520.45 | 99.97% | 98.97% | 98.68% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7169 | 1844 | 5325 | 97.07% | 0.11% | 1126.8 | 99.67% | 98.35% | 99.16% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 140645 | 138295 | 2350 | 94.03% | 0.13% | 1276.6 | 100.00% | 96.92% | 94.12% | general,filegroups/scripts,filetypes/batch |
| filetype/tar | 1487 | 1110 | 377 | 90.90% | 0.00% | 0 | 100.00% | 95.23% | 93.21% | general,filegroups/archive |
| filetype/python-bytecode | 22902 | 1576 | 21326 | 89.72% | 0.02% | 234.46 | 99.65% | 94.42% | 99.27% | general,filetypes/python-bytecode |
| filetype/tar.gz | 40137 | 27692 | 12445 | 89.50% | 0.15% | 1526.7 | 99.92% | 94.42% | 92.71% | general,filegroups/archive,filetypes/tar.gz |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4231044 | 1486369 | 2744675 | 71.33% | 0.01% | 138.09 | 99.96% | 83.25% | 89.92% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/php,filetypes/text,filetypes/csharp,filetypes/zip,filetypes/kotlin,filetypes/shell,filetypes/gz,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/xz,filetypes/ruby,filetypes/python-bytecode,filetypes/makefile,filetypes/plist,filetypes/pkg-info,filetypes/jpeg,filetypes/macho,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/jar,filetypes/powershell,filetypes/lnk,filetypes/rtf |
| filetype/elf | 159208 | 36386 | 122822 | 95.93% | 0.01% | 81.419 | 99.97% | 97.91% | 99.06% | general,filegroups/native,filetypes/elf |
| filetype/pe | 961480 | 812716 | 148764 | 82.54% | 0.02% | 248.72 | 99.99% | 90.43% | 85.24% | general,filegroups/native,filetypes/pe |
| filetype/python | 141020 | 17651 | 123369 | 70.03% | 0.02% | 170.22 | 99.83% | 82.32% | 96.23% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 512705 | 76882 | 435823 | 60.94% | 0.00% | 16.062 | 99.99% | 75.73% | 94.14% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 26530 | 10380 | 16150 | 100.00% | 0.13% | 1300.3 | 99.80% | 99.90% | 99.92% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 11559 | 10633 | 926 | 98.42% | 0.97% | 9719.2 | 99.91% | 99.16% | 98.47% | general,filetypes/pkg-info |
| filetype/rtf | 1815 | 1340 | 475 | 98.06% | 0.21% | 2105.3 | 99.92% | 98.98% | 98.51% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 27307 | 17700 | 9607 | 97.99% | 0.05% | 520.45 | 99.97% | 98.97% | 98.68% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7169 | 1844 | 5325 | 97.07% | 0.11% | 1126.8 | 99.67% | 98.35% | 99.16% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 140645 | 138295 | 2350 | 94.03% | 0.13% | 1276.6 | 100.00% | 96.92% | 94.12% | general,filegroups/scripts,filetypes/batch |
| filetype/tar | 1487 | 1110 | 377 | 91.35% | 0.00% | 0 | 100.00% | 95.48% | 93.54% | general,filegroups/archive |
| filetype/python-bytecode | 22902 | 1576 | 21326 | 89.72% | 0.02% | 234.46 | 99.65% | 94.42% | 99.27% | general,filetypes/python-bytecode |
| filetype/tar.gz | 40137 | 27692 | 12445 | 89.53% | 0.16% | 1607.1 | 99.92% | 94.44% | 92.72% | general,filegroups/archive,filetypes/tar.gz |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4231044 | 1486369 | 2744675 | 76.23% | 0.02% | 230.26 | 99.94% | 86.49% | 91.64% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/php,filetypes/text,filetypes/csharp,filetypes/zip,filetypes/kotlin,filetypes/shell,filetypes/gz,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/xz,filetypes/ruby,filetypes/python-bytecode,filetypes/makefile,filetypes/plist,filetypes/pkg-info,filetypes/jpeg,filetypes/macho,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/jar,filetypes/powershell,filetypes/lnk,filetypes/rtf |
| filetype/elf | 159208 | 36386 | 122822 | 96.78% | 0.01% | 113.99 | 99.96% | 98.35% | 99.26% | general,filegroups/native,filetypes/elf |
| filetype/pe | 961480 | 812716 | 148764 | 87.70% | 0.07% | 739.43 | 99.98% | 93.44% | 89.59% | general,filegroups/native,filetypes/pe |
| filetype/python | 141020 | 17651 | 123369 | 71.06% | 0.03% | 283.7 | 99.72% | 82.98% | 96.35% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 512705 | 76882 | 435823 | 79.65% | 0.01% | 121.61 | 99.91% | 88.64% | 96.94% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 26530 | 10380 | 16150 | 100.00% | 0.13% | 1300.3 | 99.80% | 99.90% | 99.92% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 11559 | 10633 | 926 | 98.42% | 0.97% | 9719.2 | 99.91% | 99.16% | 98.47% | general,filetypes/pkg-info |
| filetype/rtf | 1815 | 1340 | 475 | 98.06% | 0.21% | 2105.3 | 99.92% | 98.98% | 98.51% | general,filegroups/documents,filetypes/rtf |
| filetype/package.json | 27307 | 17700 | 9607 | 97.99% | 0.05% | 520.45 | 99.97% | 98.97% | 98.68% | general,filegroups/config,filetypes/package.json |
| filetype/ole | 7169 | 1844 | 5325 | 97.07% | 0.11% | 1126.8 | 99.67% | 98.35% | 99.16% | general,filegroups/documents,filetypes/ole |
| filetype/batch | 140645 | 138295 | 2350 | 94.10% | 0.17% | 1702.1 | 100.00% | 96.96% | 94.20% | general,filegroups/scripts,filetypes/batch |
| filetype/xls | 10232 | 10183 | 49 | 92.22% | 0.00% | 0 | 100.00% | 95.95% | 92.26% | general,filegroups/documents |
| filetype/tar | 1487 | 1110 | 377 | 91.98% | 0.00% | 0 | 100.00% | 95.82% | 94.01% | general,filegroups/archive |
| filetype/tar.gz | 40137 | 27692 | 12445 | 90.08% | 0.17% | 1687.4 | 99.92% | 94.75% | 93.11% | general,filegroups/archive,filetypes/tar.gz |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 4231044 | 1486369 | 2744675 | 77.32% | 0.03% | 306.78 | 99.93% | 87.18% | 92.01% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/pdf,filetypes/batch,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/php,filetypes/text,filetypes/csharp,filetypes/zip,filetypes/kotlin,filetypes/shell,filetypes/gz,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/xz,filetypes/ruby,filetypes/python-bytecode,filetypes/makefile,filetypes/plist,filetypes/pkg-info,filetypes/jpeg,filetypes/macho,filetypes/data,filetypes/ole,filetypes/vbs,filetypes/groovy,filetypes/jar,filetypes/powershell,filetypes/lnk,filetypes/rtf |
| filetype/elf | 159208 | 36386 | 122822 | 97.67% | 0.02% | 219.83 | 99.92% | 98.78% | 99.45% | general,filegroups/native,filetypes/elf |
| filetype/pe | 961480 | 812716 | 148764 | 88.48% | 0.09% | 927.64 | 99.98% | 93.88% | 90.25% | general,filegroups/native,filetypes/pe |
| filetype/python | 141020 | 17651 | 123369 | 71.54% | 0.03% | 348.55 | 99.66% | 83.29% | 96.41% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 512705 | 76882 | 435823 | 81.27% | 0.02% | 213.39 | 99.85% | 89.61% | 97.17% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 26530 | 10380 | 16150 | 100.00% | 0.13% | 1300.3 | 99.80% | 99.90% | 99.92% | general,filegroups/archive,filetypes/zst |
| filetype/package.json | 27307 | 17700 | 9607 | 99.39% | 0.16% | 1561.4 | 99.91% | 99.65% | 99.55% | general,filegroups/config,filetypes/package.json |
| filetype/batch | 140645 | 138295 | 2350 | 99.05% | 0.21% | 2127.7 | 100.00% | 99.52% | 99.06% | general,filegroups/scripts,filetypes/batch |
| filetype/pkg-info | 11559 | 10633 | 926 | 98.42% | 0.97% | 9719.2 | 99.91% | 99.16% | 98.47% | general,filetypes/pkg-info |
| filetype/rtf | 1815 | 1340 | 475 | 98.06% | 0.21% | 2105.3 | 99.92% | 98.98% | 98.51% | general,filegroups/documents,filetypes/rtf |
| filetype/ole | 7169 | 1844 | 5325 | 97.07% | 0.11% | 1126.8 | 99.67% | 98.35% | 99.16% | general,filegroups/documents,filetypes/ole |
| filetype/xls | 10232 | 10183 | 49 | 92.48% | 0.00% | 0 | 100.00% | 96.09% | 92.51% | general,filegroups/documents |
| filetype/tar | 1487 | 1110 | 377 | 92.16% | 0.00% | 0 | 100.00% | 95.92% | 94.15% | general,filegroups/archive |
| filetype/tar.gz | 40137 | 27692 | 12445 | 90.20% | 0.18% | 1767.8 | 99.91% | 94.81% | 93.18% | general,filegroups/archive,filetypes/tar.gz |
