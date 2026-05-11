# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `1123787257`
- Rows: 3285920 (699360 malware, 2586560 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 3285920 | 699360 | 2586560 | 80.46% | 0.01% | 131.84 | 99.94% | 89.15% | 95.83% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/text,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/gz,filetypes/kotlin,filetypes/zip,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/zst,filetypes/unknown,filetypes/python-bytecode,filetypes/plist,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/vbs,filetypes/pdf,filetypes/batch,filetypes/powershell,filetypes/jar,filetypes/rtf |
| filetype/elf | 140212 | 22261 | 117951 | 87.88% | 0.00% | 16.956 | 99.99% | 93.54% | 98.07% | general,filegroups/native,filetypes/elf |
| filetype/pe | 614797 | 470591 | 144206 | 88.32% | 0.04% | 353.66 | 99.99% | 93.79% | 91.05% | general,filegroups/native,filetypes/pe |
| filetype/python | 131829 | 14625 | 117204 | 79.54% | 0.01% | 76.789 | 99.92% | 88.58% | 97.72% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 455588 | 58630 | 396958 | 56.71% | 0.00% | 0 | 100.00% | 72.37% | 94.43% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 18433 | 2283 | 16150 | 100.00% | 0.24% | 2352.9 | 98.36% | 99.17% | 99.79% | general,filegroups/archive,filetypes/zst |
| filetype/doc | 1925 | 1899 | 26 | 99.58% | 0.00% | 0 | 100.00% | 99.79% | 99.58% | general,filegroups/documents |
| filetype/rtf | 561 | 89 | 472 | 98.88% | 0.21% | 2118.6 | 98.88% | 98.88% | 99.64% | general,filegroups/documents,filetypes/rtf |
| filetype/macho | 7533 | 1354 | 6179 | 97.49% | 0.26% | 2589.4 | 98.80% | 98.14% | 99.34% | general,filegroups/native,filetypes/macho |
| filetype/ole | 5579 | 259 | 5320 | 96.53% | 0.11% | 1127.8 | 97.66% | 97.09% | 99.73% | general,filegroups/documents,filetypes/ole |
| filetype/tar.gz | 31608 | 19546 | 12062 | 94.48% | 0.05% | 497.43 | 99.97% | 97.15% | 96.57% | general,filegroups/archive,filetypes/tar.gz |
| filetype/pkg-info | 4560 | 3683 | 877 | 94.22% | 1.37% | 13683 | 99.66% | 96.86% | 95.07% | general,filetypes/pkg-info |
| filetype/package.json | 24738 | 15739 | 8999 | 94.19% | 0.06% | 555.62 | 99.97% | 96.99% | 96.29% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 1406 | 1043 | 363 | 91.66% | 0.00% | 0 | 100.00% | 95.65% | 93.81% | general,filegroups/archive |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 3285920 | 699360 | 2586560 | 80.74% | 0.01% | 133 | 99.94% | 89.32% | 95.89% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/text,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/gz,filetypes/kotlin,filetypes/zip,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/zst,filetypes/unknown,filetypes/python-bytecode,filetypes/plist,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/vbs,filetypes/pdf,filetypes/batch,filetypes/powershell,filetypes/jar,filetypes/rtf |
| filetype/elf | 140212 | 22261 | 117951 | 88.05% | 0.00% | 16.956 | 99.99% | 93.64% | 98.10% | general,filegroups/native,filetypes/elf |
| filetype/pe | 614797 | 470591 | 144206 | 88.53% | 0.04% | 374.46 | 99.99% | 93.91% | 91.21% | general,filegroups/native,filetypes/pe |
| filetype/python | 131829 | 14625 | 117204 | 79.54% | 0.01% | 76.789 | 99.92% | 88.58% | 97.72% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 455588 | 58630 | 396958 | 57.24% | 0.00% | 0 | 100.00% | 72.80% | 94.50% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 18433 | 2283 | 16150 | 100.00% | 0.24% | 2352.9 | 98.36% | 99.17% | 99.79% | general,filegroups/archive,filetypes/zst |
| filetype/doc | 1925 | 1899 | 26 | 99.58% | 0.00% | 0 | 100.00% | 99.79% | 99.58% | general,filegroups/documents |
| filetype/rtf | 561 | 89 | 472 | 98.88% | 0.21% | 2118.6 | 98.88% | 98.88% | 99.64% | general,filegroups/documents,filetypes/rtf |
| filetype/macho | 7533 | 1354 | 6179 | 97.49% | 0.26% | 2589.4 | 98.80% | 98.14% | 99.34% | general,filegroups/native,filetypes/macho |
| filetype/ole | 5579 | 259 | 5320 | 96.53% | 0.11% | 1127.8 | 97.66% | 97.09% | 99.73% | general,filegroups/documents,filetypes/ole |
| filetype/tar.gz | 31608 | 19546 | 12062 | 94.49% | 0.05% | 497.43 | 99.97% | 97.15% | 96.57% | general,filegroups/archive,filetypes/tar.gz |
| filetype/pkg-info | 4560 | 3683 | 877 | 94.22% | 1.37% | 13683 | 99.66% | 96.86% | 95.07% | general,filetypes/pkg-info |
| filetype/package.json | 24738 | 15739 | 8999 | 94.20% | 0.06% | 555.62 | 99.97% | 97.00% | 96.29% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 1406 | 1043 | 363 | 91.75% | 0.00% | 0 | 100.00% | 95.70% | 93.88% | general,filegroups/archive |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 3285920 | 699360 | 2586560 | 85.46% | 0.02% | 233.9 | 99.90% | 92.12% | 96.89% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/text,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/gz,filetypes/kotlin,filetypes/zip,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/zst,filetypes/unknown,filetypes/python-bytecode,filetypes/plist,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/vbs,filetypes/pdf,filetypes/batch,filetypes/powershell,filetypes/jar,filetypes/rtf |
| filetype/elf | 140212 | 22261 | 117951 | 95.31% | 0.02% | 178.04 | 99.90% | 97.55% | 99.24% | general,filegroups/native,filetypes/elf |
| filetype/pe | 614797 | 470591 | 144206 | 90.25% | 0.08% | 804.4 | 99.97% | 94.86% | 92.52% | general,filegroups/native,filetypes/pe |
| filetype/python | 131829 | 14625 | 117204 | 81.09% | 0.03% | 273.03 | 99.73% | 89.45% | 97.88% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 455588 | 58630 | 396958 | 89.79% | 0.01% | 113.36 | 99.91% | 94.58% | 98.68% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 18433 | 2283 | 16150 | 100.00% | 0.24% | 2352.9 | 98.36% | 99.17% | 99.79% | general,filegroups/archive,filetypes/zst |
| filetype/doc | 1925 | 1899 | 26 | 99.58% | 0.00% | 0 | 100.00% | 99.79% | 99.58% | general,filegroups/documents |
| filetype/rtf | 561 | 89 | 472 | 98.88% | 0.21% | 2118.6 | 98.88% | 98.88% | 99.64% | general,filegroups/documents,filetypes/rtf |
| filetype/macho | 7533 | 1354 | 6179 | 97.49% | 0.26% | 2589.4 | 98.80% | 98.14% | 99.34% | general,filegroups/native,filetypes/macho |
| filetype/ole | 5579 | 259 | 5320 | 96.53% | 0.11% | 1127.8 | 97.66% | 97.09% | 99.73% | general,filegroups/documents,filetypes/ole |
| filetype/tar.gz | 31608 | 19546 | 12062 | 94.65% | 0.06% | 580.33 | 99.96% | 97.24% | 96.67% | general,filegroups/archive,filetypes/tar.gz |
| filetype/package.json | 24738 | 15739 | 8999 | 94.43% | 0.06% | 555.62 | 99.97% | 97.12% | 96.44% | general,filegroups/config,filetypes/package.json |
| filetype/pkg-info | 4560 | 3683 | 877 | 94.22% | 1.37% | 13683 | 99.66% | 96.86% | 95.07% | general,filetypes/pkg-info |
| filetype/tar | 1406 | 1043 | 363 | 93.38% | 0.00% | 0 | 100.00% | 96.58% | 95.09% | general,filegroups/archive |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 3285920 | 699360 | 2586560 | 87.81% | 0.03% | 326.3 | 99.86% | 93.45% | 97.38% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/source,filegroups/config,filegroups/media,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/java_class,filetypes/elf,filetypes/python,filetypes/xml,filetypes/png,filetypes/go,filetypes/rust,filetypes/text,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/gz,filetypes/kotlin,filetypes/zip,filetypes/tar.gz,filetypes/perl,filetypes/package.json,filetypes/ruby,filetypes/makefile,filetypes/zst,filetypes/unknown,filetypes/python-bytecode,filetypes/plist,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/vbs,filetypes/pdf,filetypes/batch,filetypes/powershell,filetypes/jar,filetypes/rtf |
| filetype/elf | 140212 | 22261 | 117951 | 96.91% | 0.03% | 347.6 | 99.81% | 98.34% | 99.48% | general,filegroups/native,filetypes/elf |
| filetype/pe | 614797 | 470591 | 144206 | 92.98% | 0.14% | 1414.6 | 99.95% | 96.34% | 94.59% | general,filegroups/native,filetypes/pe |
| filetype/python | 131829 | 14625 | 117204 | 81.75% | 0.03% | 315.69 | 99.69% | 89.83% | 97.95% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 455588 | 58630 | 396958 | 90.28% | 0.02% | 158.71 | 99.88% | 94.84% | 98.74% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 18433 | 2283 | 16150 | 100.00% | 0.24% | 2352.9 | 98.36% | 99.17% | 99.79% | general,filegroups/archive,filetypes/zst |
| filetype/doc | 1925 | 1899 | 26 | 99.58% | 0.00% | 0 | 100.00% | 99.79% | 99.58% | general,filegroups/documents |
| filetype/package.json | 24738 | 15739 | 8999 | 99.39% | 0.14% | 1444.6 | 99.92% | 99.65% | 99.56% | general,filegroups/config,filetypes/package.json |
| filetype/rtf | 561 | 89 | 472 | 98.88% | 0.21% | 2118.6 | 98.88% | 98.88% | 99.64% | general,filegroups/documents,filetypes/rtf |
| filetype/macho | 7533 | 1354 | 6179 | 97.49% | 0.26% | 2589.4 | 98.80% | 98.14% | 99.34% | general,filegroups/native,filetypes/macho |
| filetype/ole | 5579 | 259 | 5320 | 96.53% | 0.11% | 1127.8 | 97.66% | 97.09% | 99.73% | general,filegroups/documents,filetypes/ole |
| filetype/tar.gz | 31608 | 19546 | 12062 | 95.22% | 0.07% | 663.24 | 99.96% | 97.53% | 97.02% | general,filegroups/archive,filetypes/tar.gz |
| filetype/java_class | 255494 | 619 | 254875 | 94.67% | 0.01% | 149.09 | 93.91% | 94.29% | 99.97% | general,filegroups/portable,filetypes/java_class |
| filetype/tar | 1406 | 1043 | 363 | 94.44% | 0.00% | 0 | 100.00% | 97.14% | 95.87% | general,filegroups/archive |
