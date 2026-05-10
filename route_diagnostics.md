# Azoth Route Diagnostics

Marginal-value report for the routed ensemble. `after general` measures the best single-route addition to the general model under the level budget. `final marginal` measures whether a route can still add anything after the final selected ensemble.

- Calibration snapshot: `762136079`
- Rows: 2990924 (618271 malware, 2372653 benign)
- Search: `coordinate_descent_v1`

## Selected Routes

| L | Severity | Selected routes |
| ---: | --- | --- |
| 0 | hostile | general, filegroups/source, filetypes/go |
| 0 | suspicious | general, filegroups/source, filetypes/go |
| 1 | hostile | general, filegroups/source, filetypes/go |
| 1 | suspicious | general, filegroups/source, filetypes/go |
| 2 | hostile | general, filegroups/source, filetypes/go |
| 2 | suspicious | general, filegroups/source, filetypes/go |
| 3 | hostile | general, filegroups/source, filetypes/go |
| 3 | suspicious | general, filegroups/source, filetypes/go |
| 4 | hostile | general, filegroups/source, filetypes/go |
| 4 | suspicious | general, filegroups/source, filetypes/go |
| 5 | hostile | general, filegroups/source, filetypes/go |
| 5 | suspicious | general, filegroups/source, filetypes/go |
| 6 | hostile | general, filegroups/source, filetypes/go |
| 6 | suspicious | general, filegroups/source, filetypes/go |
| 7 | hostile | general, filegroups/source, filetypes/go |
| 7 | suspicious | general, filegroups/source, filetypes/go |
| 8 | hostile | general, filegroups/source, filetypes/go |
| 8 | suspicious | general, filegroups/source, filetypes/go |
| 9 | hostile | general, filegroups/source, filetypes/go |
| 9 | suspicious | general, filegroups/source, filetypes/go |

## L5 Hostile

| Route | Sel | Rows | Alone TP/FP | After general +TP/+FP | Final +TP/+FP | Threshold |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| filetypes/go | Y | 11556 | 7/0 | 0/0 | 0/0 | 0.69269 |
| filegroups/source | Y | 104116 | 2/0 | 0/0 | 0/0 | 0.81546 |
| filetypes/powershell | - | 235 | 1/0 | 0/0 | 0/0 | - |
| filetypes/shell | - | 5339 | 1/0 | 0/0 | 0/0 | - |
| filegroups/archive | - | 19236 | 0/0 | 0/0 | 0/0 | - |
| filegroups/config | - | 18911 | 0/0 | 0/0 | 0/0 | - |
| filegroups/documents | - | 1663 | 0/0 | 0/0 | 0/0 | - |
| filegroups/media | - | 12734 | 0/0 | 0/0 | 0/0 | - |
| filegroups/native | - | 86334 | 0/0 | 0/0 | 0/0 | - |
| filegroups/portable | - | 23526 | 0/0 | 0/0 | 0/0 | - |
| filegroups/scripts | - | 89404 | 0/0 | 0/0 | 0/0 | - |
| filetypes/batch | - | 305 | 0/0 | 0/0 | 0/0 | - |
| filetypes/c | - | 61998 | 0/0 | 0/0 | 0/0 | - |
| filetypes/csharp | - | 5664 | 0/0 | 0/0 | 0/0 | - |
| filetypes/data | - | 1107 | 0/0 | 0/0 | 0/0 | - |
| filetypes/docx | - | 94 | 0/0 | 0/0 | 0/0 | - |
| filetypes/elf | - | 16563 | 0/0 | 0/0 | 0/0 | - |
| filetypes/gz | - | 3813 | 0/0 | 0/0 | 0/0 | - |
| filetypes/jar | - | 268 | 0/0 | 0/0 | 0/0 | - |
| filetypes/java_class | - | 23258 | 0/0 | 0/0 | 0/0 | - |
| filetypes/javascript | - | 54258 | 0/0 | 0/0 | 0/0 | - |
| filetypes/jpeg | - | 1009 | 0/0 | 0/0 | 0/0 | - |
| filetypes/kotlin | - | 4528 | 0/0 | 0/0 | 0/0 | - |
| filetypes/macho | - | 884 | 0/0 | 0/0 | 0/0 | - |
| filetypes/makefile | - | 2423 | 0/0 | 0/0 | 0/0 | - |

## L5 Suspicious

| Route | Sel | Rows | Alone TP/FP | After general +TP/+FP | Final +TP/+FP | Threshold |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| filetypes/go | Y | 11556 | 7/0 | 0/0 | 0/0 | 0.69269 |
| filegroups/source | Y | 104116 | 3/7 | 0/0 | 0/0 | 0.81546 |
| filegroups/archive | - | 19236 | 2/3 | 0/0 | 0/0 | - |
| filetypes/c | - | 61998 | 2/7 | 0/0 | 0/0 | - |
| filetypes/plist | - | 1507 | 2/3 | 0/0 | 0/0 | - |
| filetypes/shell | - | 5339 | 2/6 | 0/0 | 0/0 | - |
| filetypes/batch | - | 305 | 1/4 | 0/0 | 0/0 | - |
| filetypes/docx | - | 94 | 1/1 | 0/0 | 0/0 | - |
| filetypes/ole | - | 681 | 1/4 | 0/0 | 0/0 | - |
| filetypes/pe | - | 68887 | 1/5 | 0/0 | 0/0 | - |
| filetypes/perl | - | 3671 | 1/2 | 0/0 | 0/0 | - |
| filetypes/php | - | 5428 | 1/7 | 0/0 | 0/0 | - |
| filetypes/powershell | - | 235 | 1/0 | 0/0 | 0/0 | - |
| filetypes/python | - | 15913 | 1/4 | 0/0 | 0/0 | - |
| filetypes/python-bytecode | - | 1376 | 1/6 | 0/0 | 0/0 | - |
| filetypes/rtf | - | 68 | 1/1 | 0/0 | 0/0 | - |
| filetypes/rust | - | 8792 | 1/5 | 0/0 | 0/0 | - |
| filetypes/tar | - | 192 | 1/4 | 0/0 | 0/0 | - |
| filetypes/zip | - | 4761 | 1/4 | 0/0 | 0/0 | - |
| filegroups/config | - | 18911 | 0/0 | 0/0 | 0/0 | - |
| filegroups/documents | - | 1663 | 0/0 | 0/0 | 0/0 | - |
| filegroups/media | - | 12734 | 0/0 | 0/0 | 0/0 | - |
| filegroups/native | - | 86334 | 0/0 | 0/0 | 0/0 | - |
| filegroups/portable | - | 23526 | 0/0 | 0/0 | 0/0 | - |
| filegroups/scripts | - | 89404 | 0/0 | 0/0 | 0/0 | - |

## L9 Hostile

| Route | Sel | Rows | Alone TP/FP | After general +TP/+FP | Final +TP/+FP | Threshold |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| filetypes/go | Y | 11556 | 7/0 | 0/0 | 0/0 | 0.69269 |
| filegroups/source | Y | 104116 | 2/0 | 0/0 | 0/0 | 0.81546 |
| filetypes/powershell | - | 235 | 1/0 | 0/0 | 0/0 | - |
| filetypes/shell | - | 5339 | 1/0 | 0/0 | 0/0 | - |
| filegroups/archive | - | 19236 | 0/0 | 0/0 | 0/0 | - |
| filegroups/config | - | 18911 | 0/0 | 0/0 | 0/0 | - |
| filegroups/documents | - | 1663 | 0/0 | 0/0 | 0/0 | - |
| filegroups/media | - | 12734 | 0/0 | 0/0 | 0/0 | - |
| filegroups/native | - | 86334 | 0/0 | 0/0 | 0/0 | - |
| filegroups/portable | - | 23526 | 0/0 | 0/0 | 0/0 | - |
| filegroups/scripts | - | 89404 | 0/0 | 0/0 | 0/0 | - |
| filetypes/batch | - | 305 | 0/0 | 0/0 | 0/0 | - |
| filetypes/c | - | 61998 | 0/0 | 0/0 | 0/0 | - |
| filetypes/csharp | - | 5664 | 0/0 | 0/0 | 0/0 | - |
| filetypes/data | - | 1107 | 0/0 | 0/0 | 0/0 | - |
| filetypes/docx | - | 94 | 0/0 | 0/0 | 0/0 | - |
| filetypes/elf | - | 16563 | 0/0 | 0/0 | 0/0 | - |
| filetypes/gz | - | 3813 | 0/0 | 0/0 | 0/0 | - |
| filetypes/jar | - | 268 | 0/0 | 0/0 | 0/0 | - |
| filetypes/java_class | - | 23258 | 0/0 | 0/0 | 0/0 | - |
| filetypes/javascript | - | 54258 | 0/0 | 0/0 | 0/0 | - |
| filetypes/jpeg | - | 1009 | 0/0 | 0/0 | 0/0 | - |
| filetypes/kotlin | - | 4528 | 0/0 | 0/0 | 0/0 | - |
| filetypes/macho | - | 884 | 0/0 | 0/0 | 0/0 | - |
| filetypes/makefile | - | 2423 | 0/0 | 0/0 | 0/0 | - |

## L9 Suspicious

| Route | Sel | Rows | Alone TP/FP | After general +TP/+FP | Final +TP/+FP | Threshold |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| filetypes/go | Y | 11556 | 7/0 | 0/0 | 0/0 | 0.69269 |
| filegroups/source | Y | 104116 | 3/7 | 0/0 | 0/0 | 0.81546 |
| filegroups/native | - | 86334 | 5/15 | 0/0 | 0/0 | - |
| filegroups/archive | - | 19236 | 4/13 | 0/0 | 0/0 | - |
| filetypes/png | - | 11725 | 4/14 | 0/0 | 0/0 | - |
| filetypes/batch | - | 305 | 2/8 | 0/0 | 0/0 | - |
| filetypes/c | - | 61998 | 2/7 | 0/0 | 0/0 | - |
| filetypes/csharp | - | 5664 | 2/10 | 0/0 | 0/0 | - |
| filetypes/jar | - | 268 | 2/14 | 0/0 | 0/0 | - |
| filetypes/makefile | - | 2423 | 2/15 | 0/0 | 0/0 | - |
| filetypes/perl | - | 3671 | 2/14 | 0/0 | 0/0 | - |
| filetypes/php | - | 5428 | 2/11 | 0/0 | 0/0 | - |
| filetypes/plist | - | 1507 | 2/3 | 0/0 | 0/0 | - |
| filetypes/shell | - | 5339 | 2/6 | 0/0 | 0/0 | - |
| filetypes/zip | - | 4761 | 2/15 | 0/0 | 0/0 | - |
| filegroups/config | - | 18911 | 1/14 | 0/0 | 0/0 | - |
| filegroups/documents | - | 1663 | 1/8 | 0/0 | 0/0 | - |
| filetypes/docx | - | 94 | 1/1 | 0/0 | 0/0 | - |
| filetypes/java_class | - | 23258 | 1/12 | 0/0 | 0/0 | - |
| filetypes/ole | - | 681 | 1/4 | 0/0 | 0/0 | - |
| filetypes/pe | - | 68887 | 1/5 | 0/0 | 0/0 | - |
| filetypes/powershell | - | 235 | 1/0 | 0/0 | 0/0 | - |
| filetypes/python | - | 15913 | 1/4 | 0/0 | 0/0 | - |
| filetypes/python-bytecode | - | 1376 | 1/6 | 0/0 | 0/0 | - |
| filetypes/rtf | - | 68 | 1/1 | 0/0 | 0/0 | - |
