# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `4674529089`
- Rows: 19413768 (2958322 malware, 16455446 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 534 | 92.73% | 0 | 0.00 | 559427.89 | 0.000 | 96.23% | 99.32% | `{"filetypes/applescript": 0.7845582962036133, "general": 0.9737351536750793}` |
| filetypes/asar | learned_blend_at_fp_0 | 192 | 359 | 89.58% | 0 | 0.00 | 830993.81 | 0.000 | 94.51% | 96.37% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 197636 | 891732 | 87.51% | 0 | 0.00 | 335.94 | 0.000 | 93.34% | 97.73% | `{"filegroups/native": 0.993800163269043, "filetypes/elf": 0.9999209046363831, "general": 0.9960137605667114}` |
| filetypes/chm | joint_or_at_fp_0 | 305 | 72 | 84.59% | 0 | 0.00 | 4075368.62 | 0.000 | 91.65% | 87.53% | `{"filetypes/chm": 0.7755849957466125, "general": 0.05870908871293068}` |
| filetypes/7z | joint_or_at_fp_0 | 9053 | 375 | 79.62% | 0 | 0.00 | 795679.52 | 0.000 | 88.65% | 80.43% | `{"filetypes/7z": 0.9845231175422668, "general": 0.9634636044502258}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 386 | 69.84% | 0 | 0.00 | 773092.59 | 0.000 | 82.24% | 95.77% | `{"filetypes/dmg": 0.9743145704269409, "general": 0.9773210287094116}` |
| filetypes/shell | joint_or_at_fp_0 | 18907 | 167322 | 65.23% | 0 | 0.00 | 1790.38 | 0.000 | 78.96% | 96.47% | `{"filegroups/scripts": 0.9987349510192871, "filetypes/shell": 0.9968612790107727, "general": 0.9893345236778259}` |
| filetypes/html | joint_or_at_fp_0 | 320 | 262156 | 60.62% | 0 | 0.00 | 1142.72 | 0.000 | 75.49% | 99.95% | `{"filegroups/documents": 0.9950773119926453, "general": 0.9583646059036255}` |
| filetypes/tar | joint_or_at_fp_0 | 33624 | 87553 | 58.61% | 0 | 0.00 | 3421.56 | 0.000 | 73.90% | 88.51% | `{"filetypes/tar": 0.9995971918106079, "general": 0.998708188533783}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 1186978 | 58.14% | 0 | 0.00 | 252.38 | 0.000 | 73.53% | 99.88% | `{"filetypes/python_bytecode": 0.9998993873596191, "general": 0.9867785573005676}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 91480 | 31900 | 56.93% | 0 | 0.00 | 9390.57 | 0.000 | 72.56% | 68.07% | `{"filetypes/ole_doc": 0.9994955062866211, "general": 0.9978461265563965}` |
| filetypes/cab | learned_blend_at_fp_0 | 883 | 86 | 55.27% | 0 | 0.00 | 3423437.28 | 0.000 | 71.19% | 59.24% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 2862 | 36986 | 54.72% | 0 | 0.00 | 8099.31 | 0.000 | 70.73% | 96.75% | `{"filegroups/native": 0.9862859845161438, "filetypes/macho": 0.995182991027832, "general": 0.987189769744873}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 1013 | 7541 | 51.63% | 0 | 0.00 | 39718.04 | 0.000 | 68.10% | 94.27% | `{"filetypes/python_sdist": 0.9968740940093994, "general": 0.9806063771247864}` |
| filetypes/kotlin | joint_or_at_fp_0 | 31716 | 84143 | 51.20% | 0 | 0.00 | 3560.22 | 0.000 | 67.73% | 86.64% | `{"filegroups/source": 0.9889034032821655, "filetypes/kotlin": 0.9667292833328247, "general": 0.9961152672767639}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44669 | 50.72% | 0 | 0.00 | 6706.29 | 0.000 | 67.31% | 99.92% | `{"general": 0.9638645052909851}` |
| filetypes/package.json | joint_or_at_fp_0 | 22370 | 75941 | 50.51% | 0 | 0.00 | 3944.74 | 0.000 | 67.11% | 88.74% | `{"filegroups/config": 0.9999874830245972, "filetypes/package.json": 0.9998137950897217, "general": 0.9989531636238098}` |
| filetypes/lua | joint_or_at_fp_0 | 115 | 28011 | 49.57% | 0 | 0.00 | 10694.27 | 0.000 | 66.28% | 99.79% | `{"filegroups/scripts": 0.9970859885215759, "filetypes/lua": 0.9567145109176636, "general": 0.9676010608673096}` |
| filetypes/powershell | joint_or_at_fp_0 | 6056 | 5844 | 47.14% | 0 | 0.00 | 51248.54 | 0.000 | 64.08% | 73.10% | `{"filegroups/scripts": 0.9988722205162048, "filetypes/powershell": 0.9927161335945129, "general": 0.9981876015663147}` |
| filetypes/npm | joint_or_at_fp_0 | 17999 | 162401 | 46.75% | 0 | 0.00 | 1844.63 | 0.000 | 63.72% | 94.69% | `{"filetypes/npm": 0.9994276165962219, "general": 0.9993807077407837}` |
| filetypes/gem | joint_or_at_fp_0 | 2109 | 112758 | 44.90% | 0 | 0.00 | 2656.74 | 0.000 | 61.98% | 98.99% | `{"filetypes/gem": 0.9972406029701233, "general": 0.9419142007827759}` |
| filetypes/rtf | joint_or_at_fp_0 | 6257 | 973 | 42.56% | 0 | 0.00 | 307412.67 | 0.000 | 59.71% | 50.29% | `{"filegroups/documents": 0.9999147057533264, "filetypes/rtf": 0.9938548803329468, "general": 0.9987455010414124}` |
| filetypes/javascript | joint_or_at_fp_0 | 146889 | 1780737 | 40.85% | 0 | 0.00 | 168.23 | 0.000 | 58.00% | 95.49% | `{"filegroups/scripts": 0.999054491519928, "filetypes/javascript": 0.9987862706184387, "general": 0.9958264827728271}` |
| filetypes/lnk | joint_or_at_fp_0 | 4733 | 1156 | 38.58% | 0 | 0.00 | 258810.90 | 0.000 | 55.68% | 50.64% | `{"filetypes/lnk": 0.9930663108825684, "general": 0.9970788955688477}` |
| filetypes/python | joint_or_at_fp_0 | 23709 | 673495 | 37.36% | 0 | 0.00 | 444.80 | 0.000 | 54.39% | 97.87% | `{"filegroups/scripts": 0.9987145066261292, "filetypes/python": 0.9990981221199036, "general": 0.9953400492668152}` |
| filetypes/ruby | joint_or_at_fp_0 | 406 | 186668 | 36.70% | 0 | 0.00 | 1604.83 | 0.000 | 53.69% | 99.86% | `{"filegroups/scripts": 0.9908872246742249, "filetypes/ruby": 0.9898930788040161}` |
| filetypes/jar | joint_or_at_fp_0 | 3943 | 40358 | 32.08% | 0 | 0.00 | 7422.62 | 0.000 | 48.58% | 93.95% | `{"filetypes/jar": 0.9981085658073425, "general": 0.9728924036026001}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67993 | 5854 | 29.50% | 0 | 0.00 | 51161.02 | 0.000 | 45.56% | 35.09% | `{"filetypes/ooxml": 0.9963874220848083, "general": 0.9972153306007385}` |
| filetypes/zip | joint_or_at_fp_0 | 109230 | 64699 | 29.37% | 0 | 0.00 | 4630.15 | 0.000 | 45.41% | 55.65% | `{"filetypes/zip": 0.9993611574172974, "general": 0.9966455698013306}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2941 | 275 | 26.73% | 0 | 0.00 | 1083445.18 | 0.000 | 42.18% | 32.99% | `{"filetypes/apk_android": 0.9451460242271423, "general": 0.5373435020446777}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/applescript | joint_or_at_fp_0 | 55 | 534 | 92.73% | 0 | 0.00 | 559427.89 | 0.000 | 96.23% | 99.32% | `{"filetypes/applescript": 0.7845582962036133, "general": 0.9737351536750793}` |
| filetypes/asar | learned_blend_at_fp_0 | 192 | 359 | 89.58% | 0 | 0.00 | 830993.81 | 0.000 | 94.51% | 96.37% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 197636 | 891732 | 87.51% | 0 | 0.00 | 335.94 | 0.000 | 93.34% | 97.73% | `{"filegroups/native": 0.993800163269043, "filetypes/elf": 0.9999209046363831, "general": 0.9960137605667114}` |
| filetypes/chm | joint_or_at_fp_0 | 305 | 72 | 84.59% | 0 | 0.00 | 4075368.62 | 0.000 | 91.65% | 87.53% | `{"filetypes/chm": 0.7755849957466125, "general": 0.05870908871293068}` |
| filetypes/7z | joint_or_at_fp_0 | 9053 | 375 | 79.62% | 0 | 0.00 | 795679.52 | 0.000 | 88.65% | 80.43% | `{"filetypes/7z": 0.9845231175422668, "general": 0.9634636044502258}` |
| filetypes/dmg | joint_or_at_fp_0 | 63 | 386 | 69.84% | 0 | 0.00 | 773092.59 | 0.000 | 82.24% | 95.77% | `{"filetypes/dmg": 0.9743145704269409, "general": 0.9773210287094116}` |
| filetypes/shell | joint_or_at_fp_0 | 18907 | 167322 | 65.23% | 0 | 0.00 | 1790.38 | 0.000 | 78.96% | 96.47% | `{"filegroups/scripts": 0.9987349510192871, "filetypes/shell": 0.9968612790107727, "general": 0.9893345236778259}` |
| filetypes/html | joint_or_at_fp_0 | 320 | 262156 | 60.62% | 0 | 0.00 | 1142.72 | 0.000 | 75.49% | 99.95% | `{"filegroups/documents": 0.9950773119926453, "general": 0.9583646059036255}` |
| filetypes/tar | joint_or_at_fp_0 | 33624 | 87553 | 58.61% | 0 | 0.00 | 3421.56 | 0.000 | 73.90% | 88.51% | `{"filetypes/tar": 0.9995971918106079, "general": 0.998708188533783}` |
| filetypes/python_bytecode | joint_or_at_fp_0 | 3507 | 1186978 | 58.14% | 0 | 0.00 | 252.38 | 0.000 | 73.53% | 99.88% | `{"filetypes/python_bytecode": 0.9998993873596191, "general": 0.9867785573005676}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 91480 | 31900 | 56.93% | 0 | 0.00 | 9390.57 | 0.000 | 72.56% | 68.07% | `{"filetypes/ole_doc": 0.9994955062866211, "general": 0.9978461265563965}` |
| filetypes/cab | learned_blend_at_fp_0 | 883 | 86 | 55.27% | 0 | 0.00 | 3423437.28 | 0.000 | 71.19% | 59.24% | `{}` |
| filetypes/macho | joint_or_at_fp_0 | 2862 | 36986 | 54.72% | 0 | 0.00 | 8099.31 | 0.000 | 70.73% | 96.75% | `{"filegroups/native": 0.9862859845161438, "filetypes/macho": 0.995182991027832, "general": 0.987189769744873}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 1013 | 7541 | 51.63% | 0 | 0.00 | 39718.04 | 0.000 | 68.10% | 94.27% | `{"filetypes/python_sdist": 0.9968740940093994, "general": 0.9806063771247864}` |
| filetypes/kotlin | joint_or_at_fp_0 | 31716 | 84143 | 51.20% | 0 | 0.00 | 3560.22 | 0.000 | 67.73% | 86.64% | `{"filegroups/source": 0.9889034032821655, "filetypes/kotlin": 0.9667292833328247, "general": 0.9961152672767639}` |
| filetypes/swift | joint_or_at_fp_0 | 69 | 44669 | 50.72% | 0 | 0.00 | 6706.29 | 0.000 | 67.31% | 99.92% | `{"general": 0.9638645052909851}` |
| filetypes/package.json | joint_or_at_fp_0 | 22370 | 75941 | 50.51% | 0 | 0.00 | 3944.74 | 0.000 | 67.11% | 88.74% | `{"filegroups/config": 0.9999874830245972, "filetypes/package.json": 0.9998137950897217, "general": 0.9989531636238098}` |
| filetypes/lua | joint_or_at_fp_0 | 115 | 28011 | 49.57% | 0 | 0.00 | 10694.27 | 0.000 | 66.28% | 99.79% | `{"filegroups/scripts": 0.9970859885215759, "filetypes/lua": 0.9567145109176636, "general": 0.9676010608673096}` |
| filetypes/powershell | joint_or_at_fp_0 | 6056 | 5844 | 47.14% | 0 | 0.00 | 51248.54 | 0.000 | 64.08% | 73.10% | `{"filegroups/scripts": 0.9988722205162048, "filetypes/powershell": 0.9927161335945129, "general": 0.9981876015663147}` |
| filetypes/npm | joint_or_at_fp_0 | 17999 | 162401 | 46.75% | 0 | 0.00 | 1844.63 | 0.000 | 63.72% | 94.69% | `{"filetypes/npm": 0.9994276165962219, "general": 0.9993807077407837}` |
| filetypes/gem | joint_or_at_fp_0 | 2109 | 112758 | 44.90% | 0 | 0.00 | 2656.74 | 0.000 | 61.98% | 98.99% | `{"filetypes/gem": 0.9972406029701233, "general": 0.9419142007827759}` |
| filetypes/rtf | joint_or_at_fp_0 | 6257 | 973 | 42.56% | 0 | 0.00 | 307412.67 | 0.000 | 59.71% | 50.29% | `{"filegroups/documents": 0.9999147057533264, "filetypes/rtf": 0.9938548803329468, "general": 0.9987455010414124}` |
| filetypes/javascript | joint_or_at_fp_0 | 146889 | 1780737 | 40.85% | 0 | 0.00 | 168.23 | 0.000 | 58.00% | 95.49% | `{"filegroups/scripts": 0.999054491519928, "filetypes/javascript": 0.9987862706184387, "general": 0.9958264827728271}` |
| filetypes/lnk | joint_or_at_fp_0 | 4733 | 1156 | 38.58% | 0 | 0.00 | 258810.90 | 0.000 | 55.68% | 50.64% | `{"filetypes/lnk": 0.9930663108825684, "general": 0.9970788955688477}` |
| filetypes/python | joint_or_at_fp_0 | 23709 | 673495 | 37.36% | 0 | 0.00 | 444.80 | 0.000 | 54.39% | 97.87% | `{"filegroups/scripts": 0.9987145066261292, "filetypes/python": 0.9990981221199036, "general": 0.9953400492668152}` |
| filetypes/ruby | joint_or_at_fp_0 | 406 | 186668 | 36.70% | 0 | 0.00 | 1604.83 | 0.000 | 53.69% | 99.86% | `{"filegroups/scripts": 0.9908872246742249, "filetypes/ruby": 0.9898930788040161}` |
| filetypes/jar | joint_or_at_fp_0 | 3943 | 40358 | 32.08% | 0 | 0.00 | 7422.62 | 0.000 | 48.58% | 93.95% | `{"filetypes/jar": 0.9981085658073425, "general": 0.9728924036026001}` |
| filetypes/ooxml | joint_or_at_fp_0 | 67993 | 5854 | 29.50% | 0 | 0.00 | 51161.02 | 0.000 | 45.56% | 35.09% | `{"filetypes/ooxml": 0.9963874220848083, "general": 0.9972153306007385}` |
| filetypes/zip | joint_or_at_fp_0 | 109230 | 64699 | 29.37% | 0 | 0.00 | 4630.15 | 0.000 | 45.41% | 55.65% | `{"filetypes/zip": 0.9993611574172974, "general": 0.9966455698013306}` |
| filetypes/apk_android | joint_or_at_fp_0 | 2941 | 275 | 26.73% | 0 | 0.00 | 1083445.18 | 0.000 | 42.18% | 32.99% | `{"filetypes/apk_android": 0.9451460242271423, "general": 0.5373435020446777}` |
