# Azoth Slice Metrics

Effective routed ensemble metrics by corpus slice. A filetype row uses the route litmus would use for that filetype: `az`, calibrated `az/<filegroup>`, and calibrated `az/<filetype>` when available.

- Calibration snapshot: `762136079`
- Rows: 2990924 (618271 malware, 2372653 benign)

## L5 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 2990924 | 618271 | 2372653 | 71.18% | 0.00% | 13.487 | 99.99% | 83.16% | 94.04% | general,filegroups/source,filetypes/go |
| filetype/elf | 133842 | 21965 | 111877 | 83.52% | 0.00% | 0 | 100.00% | 91.02% | 97.30% | general |
| filetype/pe | 551659 | 410851 | 140808 | 75.96% | 0.01% | 106.53 | 100.00% | 86.34% | 82.09% | general |
| filetype/python | 125795 | 13423 | 112372 | 64.00% | 0.00% | 17.798 | 99.98% | 78.04% | 96.16% | general |
| filetype/javascript | 433211 | 57629 | 375582 | 59.38% | 0.00% | 0 | 100.00% | 74.51% | 94.60% | general |
| filetype/zst | 18432 | 2282 | 16150 | 91.41% | 0.00% | 0 | 100.00% | 95.51% | 98.94% | general |
| filetype/tar.gz | 31281 | 19387 | 11894 | 89.00% | 0.01% | 84.076 | 99.99% | 94.18% | 93.18% | general |
| filetype/7z | 3814 | 3780 | 34 | 86.85% | 2.94% | 29412 | 99.97% | 92.95% | 86.94% | general |
| filetype/tar | 1397 | 1042 | 355 | 81.77% | 0.00% | 0 | 100.00% | 89.97% | 86.40% | general |
| filetype/zip | 38546 | 32962 | 5584 | 78.44% | 0.05% | 537.25 | 99.99% | 87.91% | 81.55% | general |
| filetype/package.json | 22863 | 15658 | 7205 | 75.43% | 0.00% | 0 | 100.00% | 86.00% | 83.17% | general |
| filetype/pkg-info | 4488 | 3681 | 807 | 65.42% | 0.00% | 0 | 100.00% | 79.09% | 71.64% | general |

## L9 Hostile

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 2990924 | 618271 | 2372653 | 71.18% | 0.00% | 13.487 | 99.99% | 83.16% | 94.04% | general,filegroups/source,filetypes/go |
| filetype/elf | 133842 | 21965 | 111877 | 83.52% | 0.00% | 0 | 100.00% | 91.02% | 97.30% | general |
| filetype/pe | 551659 | 410851 | 140808 | 75.96% | 0.01% | 106.53 | 100.00% | 86.34% | 82.09% | general |
| filetype/python | 125795 | 13423 | 112372 | 64.00% | 0.00% | 17.798 | 99.98% | 78.04% | 96.16% | general |
| filetype/javascript | 433211 | 57629 | 375582 | 59.38% | 0.00% | 0 | 100.00% | 74.51% | 94.60% | general |
| filetype/zst | 18432 | 2282 | 16150 | 91.41% | 0.00% | 0 | 100.00% | 95.51% | 98.94% | general |
| filetype/tar.gz | 31281 | 19387 | 11894 | 89.00% | 0.01% | 84.076 | 99.99% | 94.18% | 93.18% | general |
| filetype/7z | 3814 | 3780 | 34 | 86.85% | 2.94% | 29412 | 99.97% | 92.95% | 86.94% | general |
| filetype/tar | 1397 | 1042 | 355 | 81.77% | 0.00% | 0 | 100.00% | 89.97% | 86.40% | general |
| filetype/zip | 38546 | 32962 | 5584 | 78.44% | 0.05% | 537.25 | 99.99% | 87.91% | 81.55% | general |
| filetype/package.json | 22863 | 15658 | 7205 | 75.43% | 0.00% | 0 | 100.00% | 86.00% | 83.17% | general |
| filetype/pkg-info | 4488 | 3681 | 807 | 65.42% | 0.00% | 0 | 100.00% | 79.09% | 71.64% | general |

## L5 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 2990924 | 618271 | 2372653 | 76.16% | 0.00% | 29.081 | 99.99% | 86.46% | 95.07% | general,filegroups/source,filetypes/go |
| filetype/elf | 133842 | 21965 | 111877 | 85.28% | 0.00% | 0 | 100.00% | 92.06% | 97.58% | general |
| filetype/pe | 551659 | 410851 | 140808 | 81.00% | 0.03% | 319.58 | 99.99% | 89.50% | 85.84% | general |
| filetype/python | 125795 | 13423 | 112372 | 70.28% | 0.00% | 17.798 | 99.98% | 82.54% | 96.83% | general |
| filetype/javascript | 433211 | 57629 | 375582 | 68.63% | 0.00% | 5.3251 | 99.99% | 81.40% | 95.83% | general |
| filetype/zst | 18432 | 2282 | 16150 | 93.56% | 0.00% | 0 | 100.00% | 96.67% | 99.20% | general |
| filetype/tar.gz | 31281 | 19387 | 11894 | 90.46% | 0.02% | 168.15 | 99.99% | 94.99% | 94.08% | general |
| filetype/7z | 3814 | 3780 | 34 | 88.28% | 2.94% | 29412 | 99.97% | 93.76% | 88.36% | general |
| filetype/tar | 1397 | 1042 | 355 | 84.64% | 0.00% | 0 | 100.00% | 91.68% | 88.55% | general |
| filetype/package.json | 22863 | 15658 | 7205 | 82.51% | 0.00% | 0 | 100.00% | 90.42% | 88.02% | general |
| filetype/zip | 38546 | 32962 | 5584 | 80.58% | 0.11% | 1074.5 | 99.98% | 89.24% | 83.38% | general |
| filetype/pkg-info | 4488 | 3681 | 807 | 77.86% | 0.00% | 0 | 100.00% | 87.55% | 81.84% | general |

## L9 Suspicious

| Scope | Rows | Malware | Benign | Recall | FPR | FP/1M | Precision | F1 | Accuracy | Routes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| all | 2990924 | 618271 | 2372653 | 76.93% | 0.00% | 37.932 | 99.98% | 86.95% | 95.23% | general,filegroups/source,filetypes/go |
| filetype/elf | 133842 | 21965 | 111877 | 85.48% | 0.00% | 0 | 100.00% | 92.17% | 97.62% | general |
| filetype/pe | 551659 | 410851 | 140808 | 81.87% | 0.04% | 390.6 | 99.98% | 90.03% | 86.49% | general |
| filetype/python | 125795 | 13423 | 112372 | 71.57% | 0.00% | 26.697 | 99.97% | 83.42% | 96.96% | general |
| filetype/javascript | 433211 | 57629 | 375582 | 69.53% | 0.00% | 23.963 | 99.98% | 82.02% | 95.94% | general |
| filetype/zst | 18432 | 2282 | 16150 | 93.78% | 0.00% | 0 | 100.00% | 96.79% | 99.23% | general |
| filetype/tar.gz | 31281 | 19387 | 11894 | 90.69% | 0.02% | 168.15 | 99.99% | 95.12% | 94.23% | general |
| filetype/7z | 3814 | 3780 | 34 | 88.54% | 2.94% | 29412 | 99.97% | 93.91% | 88.62% | general |
| filetype/tar | 1397 | 1042 | 355 | 85.32% | 0.00% | 0 | 100.00% | 92.08% | 89.05% | general |
| filetype/package.json | 22863 | 15658 | 7205 | 83.32% | 0.00% | 0 | 100.00% | 90.90% | 88.58% | general |
| filetype/zip | 38546 | 32962 | 5584 | 80.90% | 0.14% | 1432.7 | 99.97% | 89.43% | 83.65% | general |
| filetype/pkg-info | 4488 | 3681 | 807 | 78.51% | 0.00% | 0 | 100.00% | 87.96% | 82.38% | general |
