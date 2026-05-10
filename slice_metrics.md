# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `762136079`
- Rows: 374918 (77361 malware, 297557 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 374918 | 77361 | 297557 | 84.93% | 0.00% | 3.3607 | 100.00% | 91.85% | 96.89% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/config,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/elf,filetypes/python,filetypes/png,filetypes/go,filetypes/rust,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/zip,filetypes/kotlin,filetypes/tar.gz,filetypes/perl,filetypes/ruby,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/plist,filetypes/python-bytecode,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/batch,filetypes/jar,filetypes/powershell,filetypes/vbs,filetypes/tar,filetypes/docx,filetypes/rtf,filetypes/msi |
| filetype/elf | 16563 | 2764 | 13799 | 97.40% | 0.00% | 0 | 100.00% | 98.68% | 99.57% | general,filegroups/native,filetypes/elf |
| filetype/pe | 68887 | 51401 | 17486 | 86.30% | 0.01% | 57.189 | 100.00% | 92.64% | 89.77% | general,filegroups/native,filetypes/pe |
| filetype/python | 15913 | 1715 | 14198 | 86.01% | 0.00% | 0 | 100.00% | 92.48% | 98.49% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 54258 | 7213 | 47045 | 87.02% | 0.00% | 0 | 100.00% | 93.06% | 98.27% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 2335 | 273 | 2062 | 100.00% | 0.00% | 0 | 100.00% | 100.00% | 100.00% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 581 | 485 | 96 | 99.79% | 0.00% | 0 | 100.00% | 99.90% | 99.83% | general,filetypes/pkg-info |
| filetype/doc | 212 | 206 | 6 | 99.51% | 0.00% | 0 | 100.00% | 99.76% | 99.53% | general,filegroups/documents |
| filetype/package.json | 2831 | 1963 | 868 | 97.96% | 0.00% | 0 | 100.00% | 98.97% | 98.59% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 192 | 146 | 46 | 96.58% | 0.00% | 0 | 100.00% | 98.26% | 97.40% | general,filegroups/archive,filetypes/tar |
| filetype/7z | 472 | 469 | 3 | 95.52% | 0.00% | 0 | 100.00% | 97.71% | 95.55% | general,filegroups/archive |
| filetype/tar.gz | 3995 | 2470 | 1525 | 95.43% | 0.00% | 0 | 100.00% | 97.66% | 97.17% | general,filegroups/archive,filetypes/tar.gz |
| filetype/python-bytecode | 1376 | 109 | 1267 | 94.50% | 0.00% | 0 | 100.00% | 97.17% | 99.56% | general,filetypes/python-bytecode |
| filetype/docx | 94 | 67 | 27 | 89.55% | 0.00% | 0 | 100.00% | 94.49% | 92.55% | general,filegroups/documents,filetypes/docx |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 374918 | 77361 | 297557 | 85.20% | 0.00% | 6.7214 | 100.00% | 92.01% | 96.95% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/config,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/elf,filetypes/python,filetypes/png,filetypes/go,filetypes/rust,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/zip,filetypes/kotlin,filetypes/tar.gz,filetypes/perl,filetypes/ruby,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/plist,filetypes/python-bytecode,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/batch,filetypes/jar,filetypes/powershell,filetypes/vbs,filetypes/tar,filetypes/docx,filetypes/rtf,filetypes/msi |
| filetype/elf | 16563 | 2764 | 13799 | 97.40% | 0.00% | 0 | 100.00% | 98.68% | 99.57% | general,filegroups/native,filetypes/elf |
| filetype/pe | 68887 | 51401 | 17486 | 86.69% | 0.01% | 114.38 | 100.00% | 92.87% | 90.06% | general,filegroups/native,filetypes/pe |
| filetype/python | 15913 | 1715 | 14198 | 86.01% | 0.00% | 0 | 100.00% | 92.48% | 98.49% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 54258 | 7213 | 47045 | 87.08% | 0.00% | 0 | 100.00% | 93.09% | 98.28% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 2335 | 273 | 2062 | 100.00% | 0.00% | 0 | 100.00% | 100.00% | 100.00% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 581 | 485 | 96 | 99.79% | 0.00% | 0 | 100.00% | 99.90% | 99.83% | general,filetypes/pkg-info |
| filetype/doc | 212 | 206 | 6 | 99.51% | 0.00% | 0 | 100.00% | 99.76% | 99.53% | general,filegroups/documents |
| filetype/package.json | 2831 | 1963 | 868 | 97.96% | 0.00% | 0 | 100.00% | 98.97% | 98.59% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 192 | 146 | 46 | 96.58% | 0.00% | 0 | 100.00% | 98.26% | 97.40% | general,filegroups/archive,filetypes/tar |
| filetype/7z | 472 | 469 | 3 | 95.74% | 0.00% | 0 | 100.00% | 97.82% | 95.76% | general,filegroups/archive |
| filetype/tar.gz | 3995 | 2470 | 1525 | 95.43% | 0.00% | 0 | 100.00% | 97.66% | 97.17% | general,filegroups/archive,filetypes/tar.gz |
| filetype/python-bytecode | 1376 | 109 | 1267 | 94.50% | 0.00% | 0 | 100.00% | 97.17% | 99.56% | general,filetypes/python-bytecode |
| filetype/docx | 94 | 67 | 27 | 89.55% | 0.00% | 0 | 100.00% | 94.49% | 92.55% | general,filegroups/documents,filetypes/docx |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 374918 | 77361 | 297557 | 86.29% | 0.00% | 47.05 | 99.98% | 92.63% | 97.17% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/config,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/elf,filetypes/python,filetypes/png,filetypes/go,filetypes/rust,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/zip,filetypes/kotlin,filetypes/tar.gz,filetypes/perl,filetypes/ruby,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/plist,filetypes/python-bytecode,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/batch,filetypes/jar,filetypes/powershell,filetypes/vbs,filetypes/tar,filetypes/docx,filetypes/rtf,filetypes/msi |
| filetype/elf | 16563 | 2764 | 13799 | 97.40% | 0.00% | 0 | 100.00% | 98.68% | 99.57% | general,filegroups/native,filetypes/elf |
| filetype/pe | 68887 | 51401 | 17486 | 88.26% | 0.06% | 629.07 | 99.98% | 93.76% | 91.23% | general,filegroups/native,filetypes/pe |
| filetype/python | 15913 | 1715 | 14198 | 86.06% | 0.00% | 0 | 100.00% | 92.51% | 98.50% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 54258 | 7213 | 47045 | 87.25% | 0.01% | 63.769 | 99.95% | 93.17% | 98.30% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 2335 | 273 | 2062 | 100.00% | 0.00% | 0 | 100.00% | 100.00% | 100.00% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 581 | 485 | 96 | 99.79% | 0.00% | 0 | 100.00% | 99.90% | 99.83% | general,filetypes/pkg-info |
| filetype/doc | 212 | 206 | 6 | 99.51% | 0.00% | 0 | 100.00% | 99.76% | 99.53% | general,filegroups/documents |
| filetype/package.json | 2831 | 1963 | 868 | 97.96% | 0.00% | 0 | 100.00% | 98.97% | 98.59% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 192 | 146 | 46 | 96.58% | 0.00% | 0 | 100.00% | 98.26% | 97.40% | general,filegroups/archive,filetypes/tar |
| filetype/7z | 472 | 469 | 3 | 95.74% | 0.00% | 0 | 100.00% | 97.82% | 95.76% | general,filegroups/archive |
| filetype/tar.gz | 3995 | 2470 | 1525 | 95.43% | 0.00% | 0 | 100.00% | 97.66% | 97.17% | general,filegroups/archive,filetypes/tar.gz |
| filetype/python-bytecode | 1376 | 109 | 1267 | 94.50% | 0.00% | 0 | 100.00% | 97.17% | 99.56% | general,filetypes/python-bytecode |
| filetype/docx | 94 | 67 | 27 | 89.55% | 0.00% | 0 | 100.00% | 94.49% | 92.55% | general,filegroups/documents,filetypes/docx |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 374918 | 77361 | 297557 | 88.61% | 0.01% | 77.296 | 99.97% | 93.95% | 97.64% | general,filegroups/scripts,filegroups/native,filegroups/portable,filegroups/archive,filegroups/documents,filegroups/config,filetypes/pe,filetypes/c,filetypes/javascript,filetypes/elf,filetypes/python,filetypes/png,filetypes/go,filetypes/rust,filetypes/csharp,filetypes/php,filetypes/shell,filetypes/zip,filetypes/kotlin,filetypes/tar.gz,filetypes/perl,filetypes/ruby,filetypes/package.json,filetypes/zst,filetypes/unknown,filetypes/plist,filetypes/python-bytecode,filetypes/data,filetypes/jpeg,filetypes/macho,filetypes/ole,filetypes/pkg-info,filetypes/batch,filetypes/jar,filetypes/powershell,filetypes/vbs,filetypes/tar,filetypes/docx,filetypes/rtf,filetypes/msi |
| filetype/elf | 16563 | 2764 | 13799 | 97.40% | 0.00% | 0 | 100.00% | 98.68% | 99.57% | general,filegroups/native,filetypes/elf |
| filetype/pe | 68887 | 51401 | 17486 | 91.57% | 0.10% | 972.21 | 99.96% | 95.58% | 93.69% | general,filegroups/native,filetypes/pe |
| filetype/python | 15913 | 1715 | 14198 | 87.17% | 0.01% | 70.432 | 99.93% | 93.12% | 98.61% | general,filegroups/scripts,filetypes/python |
| filetype/javascript | 54258 | 7213 | 47045 | 87.73% | 0.01% | 63.769 | 99.95% | 93.44% | 98.36% | general,filegroups/scripts,filetypes/javascript |
| filetype/zst | 2335 | 273 | 2062 | 100.00% | 0.00% | 0 | 100.00% | 100.00% | 100.00% | general,filegroups/archive,filetypes/zst |
| filetype/pkg-info | 581 | 485 | 96 | 99.79% | 0.00% | 0 | 100.00% | 99.90% | 99.83% | general,filetypes/pkg-info |
| filetype/doc | 212 | 206 | 6 | 99.51% | 0.00% | 0 | 100.00% | 99.76% | 99.53% | general,filegroups/documents |
| filetype/package.json | 2831 | 1963 | 868 | 98.12% | 0.00% | 0 | 100.00% | 99.05% | 98.69% | general,filegroups/config,filetypes/package.json |
| filetype/tar | 192 | 146 | 46 | 96.58% | 0.00% | 0 | 100.00% | 98.26% | 97.40% | general,filegroups/archive,filetypes/tar |
| filetype/7z | 472 | 469 | 3 | 95.74% | 0.00% | 0 | 100.00% | 97.82% | 95.76% | general,filegroups/archive |
| filetype/tar.gz | 3995 | 2470 | 1525 | 95.51% | 0.00% | 0 | 100.00% | 97.70% | 97.22% | general,filegroups/archive,filetypes/tar.gz |
| filetype/python-bytecode | 1376 | 109 | 1267 | 94.50% | 0.00% | 0 | 100.00% | 97.17% | 99.56% | general,filetypes/python-bytecode |
