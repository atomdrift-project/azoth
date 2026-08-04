# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `2609513337`
- Rows: 15612661 (2667318 malware, 12945343 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | calibrate_inherited | 6256 | 838 | 97.44% | 0 | 0.00 | 356847.73 | 0.000 | 98.70% | 97.74% | `{"filegroups/documents": 0.41988725586472936, "general": 0.9992432083545102}` |
| filetypes/html | calibrate_inherited | 256 | 58805 | 96.09% | 0 | 0.00 | 5094.22 | 0.000 | 98.01% | 99.98% | `{"filegroups/documents": 0.41988725586472936, "general": 0.9992432083545102}` |
| filetypes/asar | learned_blend_at_fp_0 | 184 | 142 | 95.65% | 0 | 0.00 | 2087572.73 | 0.000 | 97.78% | 97.55% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 59 | 519 | 93.22% | 0 | 0.00 | 575549.71 | 0.000 | 96.49% | 99.31% | `{"filetypes/applescript": 0.7472195625305176}` |
| filetypes/elf | joint_or_at_fp_0 | 194022 | 697546 | 90.70% | 0 | 0.00 | 429.47 | 0.000 | 95.12% | 97.98% | `{"filegroups/native": 0.9596691131591797, "filetypes/elf": 0.9995152950286865, "general": 0.9913403391838074}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87638 | 31109 | 82.08% | 0 | 0.00 | 9629.33 | 0.000 | 90.16% | 86.78% | `{"filetypes/ole_doc": 0.9942498207092285}` |
| filetypes/macho | joint_or_at_fp_0 | 2832 | 26328 | 78.67% | 0 | 0.00 | 11377.86 | 0.000 | 88.06% | 97.93% | `{"filegroups/native": 0.6859586238861084, "filetypes/macho": 0.9565427303314209}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 4723 | 68.87% | 0 | 0.00 | 63408.48 | 0.000 | 81.57% | 82.52% | `{"filegroups/scripts": 0.993938684463501, "filetypes/powershell": 0.9411367774009705, "general": 0.9924433827400208}` |
| filetypes/scala | calibrate_inherited | 3 | 47791 | 66.67% | 0 | 0.00 | 6268.21 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9967483628882767, "general": 0.9992432083545102}` |
| filetypes/perl | joint_or_at_fp_0 | 399 | 74969 | 65.16% | 0 | 0.00 | 3995.88 | 0.000 | 78.91% | 99.82% | `{"filetypes/perl": 0.9951916933059692, "general": 0.9805285334587097}` |
| filetypes/nupkg | joint_or_at_fp_0 | 87 | 3091 | 63.22% | 0 | 0.00 | 96870.95 | 0.000 | 77.46% | 98.99% | `{"filetypes/nupkg": 0.9734525680541992, "general": 0.9764500856399536}` |
| filetypes/shell | joint_or_at_fp_0 | 18430 | 151968 | 56.47% | 0 | 0.00 | 1971.27 | 0.000 | 72.18% | 95.29% | `{"filegroups/scripts": 0.9968389272689819, "filetypes/shell": 0.9912537932395935, "general": 0.9921882152557373}` |
| filetypes/pe | joint_or_at_fp_0 | 1375216 | 207179 | 52.46% | 0 | 0.00 | 1445.95 | 0.000 | 68.82% | 58.68% | `{"filegroups/native": 0.9980703592300415, "filetypes/pe": 0.9985036849975586, "general": 0.999842643737793}` |
| filetypes/python | joint_or_at_fp_0 | 23263 | 602051 | 50.07% | 0 | 0.00 | 497.59 | 0.000 | 66.73% | 98.14% | `{"filegroups/scripts": 0.9958101511001587, "filetypes/python": 0.9944425225257874, "general": 0.9941239356994629}` |
| filetypes/vbs | joint_or_at_fp_0 | 12355 | 3635 | 49.43% | 0 | 0.00 | 82379.59 | 0.000 | 66.16% | 60.93% | `{"filetypes/vbs": 0.996155321598053, "general": 0.9955137968063354}` |
| filetypes/javascript | learned_blend_at_fp_0 | 140798 | 1385508 | 47.18% | 0 | 0.00 | 216.22 | 0.000 | 64.11% | 95.13% | `{}` |
| filetypes/zst | calibrate_inherited | 10472 | 286116 | 44.61% | 0 | 0.00 | 1047.03 | 0.000 | 61.70% | 98.04% | `{"general": 0.9992432083545102}` |
| filetypes/php | joint_or_at_fp_0 | 6459 | 596953 | 42.03% | 0 | 0.00 | 501.84 | 0.000 | 59.19% | 99.38% | `{"filegroups/scripts": 0.9949984550476074, "filetypes/php": 0.985375702381134, "general": 0.9985631704330444}` |
| filetypes/7z | calibrate_inherited | 9000 | 224 | 37.03% | 0 | 0.00 | 1328477.28 | 0.000 | 54.05% | 38.56% | `{"general": 0.9992432083545102}` |
| filetypes/rar | calibrate_inherited | 22184 | 13 | 36.26% | 0 | 0.00 | 20581666.52 | 0.000 | 53.22% | 36.30% | `{"general": 0.9992432083545102}` |
| filetypes/rpm | joint_or_at_fp_0 | 87 | 43010 | 34.48% | 0 | 0.00 | 6964.96 | 0.000 | 51.28% | 99.87% | `{"filetypes/rpm": 0.9999833106994629}` |
| filetypes/kotlin | calibrate_inherited | 32374 | 82843 | 33.89% | 0 | 0.00 | 3616.09 | 0.000 | 50.62% | 81.42% | `{"filegroups/source": 0.9967483628882767, "general": 0.9992432083545102}` |
| filetypes/whl | joint_or_at_fp_0 | 3817 | 8031 | 33.30% | 0 | 0.00 | 37295.15 | 0.000 | 49.96% | 78.51% | `{"filetypes/whl": 0.9987744688987732, "general": 0.9911831021308899}` |
| filetypes/groovy | joint_or_at_fp_0 | 153 | 10540 | 32.68% | 0 | 0.00 | 28418.47 | 0.000 | 49.26% | 99.04% | `{"filetypes/groovy": 0.9903106689453125}` |
| filetypes/zip | joint_or_at_fp_0 | 107393 | 29609 | 30.29% | 0 | 0.00 | 10117.13 | 0.000 | 46.50% | 45.36% | `{"filetypes/zip": 0.9990334510803223, "general": 0.9979831576347351}` |
| filetypes/ooxml | calibrate_inherited | 67975 | 3086 | 26.25% | 0 | 0.00 | 97027.83 | 0.000 | 41.59% | 29.45% | `{"general": 0.9992432083545102}` |
| filetypes/dockerfile | joint_or_at_fp_0 | 190 | 4514 | 24.74% | 0 | 0.00 | 66343.34 | 0.000 | 39.66% | 96.96% | `{"filetypes/dockerfile": 0.9821121692657471, "general": 0.9978517293930054}` |
| filetypes/swift | calibrate_inherited | 69 | 43183 | 24.64% | 0 | 0.00 | 6937.05 | 0.000 | 39.53% | 99.88% | `{"filegroups/source": 0.9967483628882767, "general": 0.9992432083545102}` |
| filetypes/pkg_info | calibrate_inherited | 10623 | 15544 | 24.16% | 0 | 0.00 | 19270.74 | 0.000 | 38.91% | 69.21% | `{"general": 0.9992432083545102}` |
| filetypes/cargo.toml | joint_or_at_fp_0 | 418 | 7904 | 19.14% | 0 | 0.00 | 37894.29 | 0.000 | 32.13% | 95.94% | `{"filetypes/cargo.toml": 0.9910498857498169, "general": 0.9573752880096436}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/rtf | calibrate_inherited | 6256 | 838 | 97.44% | 0 | 0.00 | 356847.73 | 0.000 | 98.70% | 97.74% | `{"filegroups/documents": 0.4195871127034577, "general": 0.9991578399470851}` |
| filetypes/html | calibrate_inherited | 256 | 58805 | 96.09% | 0 | 0.00 | 5094.22 | 0.000 | 98.01% | 99.98% | `{"filegroups/documents": 0.4195871127034577, "general": 0.9991578399470851}` |
| filetypes/asar | learned_blend_at_fp_0 | 184 | 142 | 95.65% | 0 | 0.00 | 2087572.73 | 0.000 | 97.78% | 97.55% | `{}` |
| filetypes/applescript | joint_or_at_fp_0 | 59 | 519 | 93.22% | 0 | 0.00 | 575549.71 | 0.000 | 96.49% | 99.31% | `{"filetypes/applescript": 0.7472195625305176}` |
| filetypes/elf | joint_or_at_fp_0 | 194022 | 697546 | 90.70% | 0 | 0.00 | 429.47 | 0.000 | 95.12% | 97.98% | `{"filegroups/native": 0.9596691131591797, "filetypes/elf": 0.9995152950286865, "general": 0.9913403391838074}` |
| filetypes/ole_doc | filetype_only_at_fp_0 | 87638 | 31109 | 82.08% | 0 | 0.00 | 9629.33 | 0.000 | 90.16% | 86.78% | `{"filetypes/ole_doc": 0.9942498207092285}` |
| filetypes/macho | joint_or_at_fp_0 | 2832 | 26328 | 78.67% | 0 | 0.00 | 11377.86 | 0.000 | 88.06% | 97.93% | `{"filegroups/native": 0.6859586238861084, "filetypes/macho": 0.9565427303314209}` |
| filetypes/powershell | joint_or_at_fp_0 | 6049 | 4723 | 68.87% | 0 | 0.00 | 63408.48 | 0.000 | 81.57% | 82.52% | `{"filegroups/scripts": 0.993938684463501, "filetypes/powershell": 0.9411367774009705, "general": 0.9924433827400208}` |
| filetypes/scala | calibrate_inherited | 3 | 47791 | 66.67% | 0 | 0.00 | 6268.21 | 0.000 | 80.00% | 100.00% | `{"filegroups/source": 0.9965800028010258, "general": 0.9991578399470851}` |
| filetypes/perl | joint_or_at_fp_0 | 399 | 74969 | 65.16% | 0 | 0.00 | 3995.88 | 0.000 | 78.91% | 99.82% | `{"filetypes/perl": 0.9951916933059692, "general": 0.9805285334587097}` |
| filetypes/nupkg | joint_or_at_fp_0 | 87 | 3091 | 63.22% | 0 | 0.00 | 96870.95 | 0.000 | 77.46% | 98.99% | `{"filetypes/nupkg": 0.9734525680541992, "general": 0.9764500856399536}` |
| filetypes/shell | joint_or_at_fp_0 | 18430 | 151968 | 56.47% | 0 | 0.00 | 1971.27 | 0.000 | 72.18% | 95.29% | `{"filegroups/scripts": 0.9968389272689819, "filetypes/shell": 0.9912537932395935, "general": 0.9921882152557373}` |
| filetypes/pe | joint_or_at_fp_0 | 1375216 | 207179 | 52.46% | 0 | 0.00 | 1445.95 | 0.000 | 68.82% | 58.68% | `{"filegroups/native": 0.9980703592300415, "filetypes/pe": 0.9985036849975586, "general": 0.999842643737793}` |
| filetypes/python | joint_or_at_fp_0 | 23263 | 602051 | 50.07% | 0 | 0.00 | 497.59 | 0.000 | 66.73% | 98.14% | `{"filegroups/scripts": 0.9958101511001587, "filetypes/python": 0.9944425225257874, "general": 0.9941239356994629}` |
| filetypes/vbs | joint_or_at_fp_0 | 12355 | 3635 | 49.43% | 0 | 0.00 | 82379.59 | 0.000 | 66.16% | 60.93% | `{"filetypes/vbs": 0.996155321598053, "general": 0.9955137968063354}` |
| filetypes/zst | calibrate_inherited | 10472 | 286116 | 47.63% | 0 | 0.00 | 1047.03 | 0.000 | 64.53% | 98.15% | `{"general": 0.9991578399470851}` |
| filetypes/javascript | learned_blend_at_fp_0 | 140798 | 1385508 | 47.18% | 0 | 0.00 | 216.22 | 0.000 | 64.11% | 95.13% | `{}` |
| filetypes/php | joint_or_at_fp_0 | 6459 | 596953 | 42.03% | 0 | 0.00 | 501.84 | 0.000 | 59.19% | 99.38% | `{"filegroups/scripts": 0.9949984550476074, "filetypes/php": 0.985375702381134, "general": 0.9985631704330444}` |
| filetypes/7z | calibrate_inherited | 9000 | 224 | 39.03% | 0 | 0.00 | 1328477.28 | 0.000 | 56.15% | 40.51% | `{"general": 0.9991578399470851}` |
| filetypes/rar | calibrate_inherited | 22184 | 13 | 37.72% | 0 | 0.00 | 20581666.52 | 0.000 | 54.78% | 37.76% | `{"general": 0.9991578399470851}` |
| filetypes/rpm | joint_or_at_fp_0 | 87 | 43010 | 34.48% | 0 | 0.00 | 6964.96 | 0.000 | 51.28% | 99.87% | `{"filetypes/rpm": 0.9999833106994629}` |
| filetypes/kotlin | calibrate_inherited | 32374 | 82843 | 34.03% | 0 | 0.00 | 3616.09 | 0.000 | 50.78% | 81.46% | `{"filegroups/source": 0.9965800028010258, "general": 0.9991578399470851}` |
| filetypes/whl | joint_or_at_fp_0 | 3817 | 8031 | 33.30% | 0 | 0.00 | 37295.15 | 0.000 | 49.96% | 78.51% | `{"filetypes/whl": 0.9987744688987732, "general": 0.9911831021308899}` |
| filetypes/groovy | joint_or_at_fp_0 | 153 | 10540 | 32.68% | 0 | 0.00 | 28418.47 | 0.000 | 49.26% | 99.04% | `{"filetypes/groovy": 0.9903106689453125}` |
| filetypes/zip | joint_or_at_fp_0 | 107393 | 29609 | 30.29% | 0 | 0.00 | 10117.13 | 0.000 | 46.50% | 45.36% | `{"filetypes/zip": 0.9990334510803223, "general": 0.9979831576347351}` |
| filetypes/ooxml | calibrate_inherited | 67975 | 3086 | 26.43% | 0 | 0.00 | 97027.83 | 0.000 | 41.81% | 29.63% | `{"general": 0.9991578399470851}` |
| filetypes/swift | calibrate_inherited | 69 | 43183 | 26.09% | 0 | 0.00 | 6937.05 | 0.000 | 41.38% | 99.88% | `{"filegroups/source": 0.9965800028010258, "general": 0.9991578399470851}` |
| filetypes/pkg_info | calibrate_inherited | 10623 | 15544 | 25.54% | 0 | 0.00 | 19270.74 | 0.000 | 40.69% | 69.77% | `{"general": 0.9991578399470851}` |
| filetypes/dockerfile | joint_or_at_fp_0 | 190 | 4514 | 24.74% | 0 | 0.00 | 66343.34 | 0.000 | 39.66% | 96.96% | `{"filetypes/dockerfile": 0.9821121692657471, "general": 0.9978517293930054}` |
| filetypes/cargo.toml | joint_or_at_fp_0 | 418 | 7904 | 19.14% | 0 | 0.00 | 37894.29 | 0.000 | 32.13% | 95.94% | `{"filetypes/cargo.toml": 0.9910498857498169, "general": 0.9573752880096436}` |
