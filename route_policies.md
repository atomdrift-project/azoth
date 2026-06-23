# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `1831375006`
- Rows: 8312102 (2614009 malware, 5698093 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{"filetypes/html": 0.9971267580986023}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 525 | 97.98% | 0 | 0.00 | 568990.75 | 0.000 | 98.98% | 98.14% | `{"filegroups/documents": 0.04553401470184326, "filetypes/rtf": 0.1712195873260498}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 2947 | 96.75% | 0 | 0.00 | 101601.97 | 0.000 | 98.35% | 97.46% | `{"filetypes/pkg-info": 0.12018036842346191}` |
| filetypes/crx | joint_or_at_fp_0 | 893 | 182 | 96.30% | 0 | 0.00 | 1632534.07 | 0.000 | 98.12% | 96.93% | `{"filetypes/crx": 0.43714338541030884, "general": 0.9354020953178406}` |
| filetypes/doc | calibrate_inherited | 34688 | 85 | 96.19% | 0 | 0.00 | 3463007.50 | 0.000 | 98.06% | 96.20% | `{"filegroups/documents": 0.18407809734344482, "general": 0.9995627097348578}` |
| filetypes/gem | joint_or_at_fp_0 | 854 | 1083 | 96.02% | 0 | 0.00 | 276232.02 | 0.000 | 97.97% | 98.24% | `{"filetypes/gem": 0.9645111560821533, "general": 0.9265512228012085}` |
| filetypes/xls | joint_or_at_fp_0 | 39675 | 20762 | 94.31% | 0 | 0.00 | 14427.88 | 0.000 | 97.07% | 96.27% | `{"filegroups/documents": 0.9931027889251709, "filetypes/xls": 0.9000883102416992, "general": 0.9979779720306396}` |
| filetypes/applescript | learned_blend_at_fp_0 | 57 | 229 | 92.98% | 0 | 0.00 | 1299660.55 | 0.000 | 96.36% | 98.60% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 189608 | 205020 | 90.99% | 0 | 0.00 | 1461.18 | 0.000 | 95.28% | 95.67% | `{"filegroups/native": 0.9847175478935242, "filetypes/elf": 0.9972903728485107, "general": 0.9921343326568604}` |
| filetypes/package.json | joint_or_at_fp_0 | 19179 | 26858 | 85.72% | 0 | 0.00 | 11153.34 | 0.000 | 92.31% | 94.05% | `{"filegroups/config": 0.9995417594909668, "filetypes/package.json": 0.9991888403892517, "general": 0.9960484504699707}` |
| filetypes/tar | joint_or_at_fp_0 | 30579 | 48299 | 82.65% | 0 | 0.00 | 6202.28 | 0.000 | 90.50% | 93.27% | `{"filetypes/tar": 0.998319685459137, "general": 0.9939501285552979}` |
| filetypes/docx | joint_or_at_fp_0 | 5065 | 402 | 81.15% | 0 | 0.00 | 742437.25 | 0.000 | 89.59% | 82.53% | `{"filegroups/documents": 0.5677497982978821, "filetypes/docx": 0.8922969698905945}` |
| filetypes/msi | joint_or_at_fp_0 | 5644 | 218 | 80.90% | 0 | 0.00 | 1364790.24 | 0.000 | 89.44% | 81.61% | `{"filetypes/msi": 0.555561363697052, "general": 0.9854252934455872}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6674 | 76.20% | 0 | 0.00 | 44876.54 | 0.000 | 86.50% | 87.49% | `{"filegroups/documents": 0.7310907244682312, "filetypes/ole": 0.9971190690994263}` |
| filetypes/lnk | joint_or_at_fp_0 | 4614 | 1065 | 74.40% | 0 | 0.00 | 280894.17 | 0.000 | 85.32% | 79.20% | `{"filetypes/lnk": 0.9565479755401611, "general": 0.9992970824241638}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 97 | 304 | 74.23% | 0 | 0.00 | 980598.72 | 0.000 | 85.21% | 93.77% | `{"filetypes/chrome-manifest": 0.9263573884963989}` |
| filetypes/macho | joint_or_at_fp_0 | 2693 | 13832 | 74.19% | 0 | 0.00 | 21655.64 | 0.000 | 85.18% | 95.79% | `{"filegroups/native": 0.9292101263999939, "filetypes/macho": 0.9887740612030029, "general": 0.9761720895767212}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24682 | 73.53% | 0 | 0.00 | 12136.58 | 0.000 | 84.74% | 76.74% | `{"filegroups/documents": 0.9932157397270203, "filetypes/pdf": 0.9362694025039673, "general": 0.9835054278373718}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3417 | 393848 | 69.65% | 0 | 0.00 | 760.63 | 0.000 | 82.11% | 99.74% | `{"filetypes/python-bytecode": 0.9996863603591919, "general": 0.9460391402244568}` |
| filetypes/whl | joint_or_at_fp_0 | 2425 | 4645 | 69.20% | 0 | 0.00 | 64472.91 | 0.000 | 81.79% | 89.43% | `{"filetypes/whl": 0.987389326095581, "general": 0.9601284265518188}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 7002 | 66.41% | 0 | 0.00 | 42774.80 | 0.000 | 79.82% | 99.38% | `{"filetypes/clojure": 0.9773902297019958}` |
| filetypes/shell | joint_or_at_fp_0 | 15722 | 72548 | 63.78% | 0 | 0.00 | 4129.23 | 0.000 | 77.89% | 93.55% | `{"filegroups/scripts": 0.9930756092071533, "filetypes/shell": 0.9718871712684631, "general": 0.9496476054191589}` |
| filetypes/pe | joint_or_at_fp_0 | 1370153 | 172762 | 57.36% | 0 | 0.00 | 1734.01 | 0.000 | 72.90% | 62.13% | `{"filegroups/native": 0.9994462132453918, "filetypes/pe": 0.9969835877418518, "general": 0.9997603297233582}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 44914 | 57.11% | 0 | 0.00 | 6669.71 | 0.000 | 72.70% | 99.63% | `{"filetypes/perl": 0.9909163117408752}` |
| filetypes/javascript | joint_or_at_fp_0 | 126491 | 714570 | 54.35% | 0 | 0.00 | 419.23 | 0.000 | 70.42% | 93.13% | `{"filegroups/scripts": 0.9965267777442932, "filetypes/javascript": 0.9934003353118896, "general": 0.998794674873352}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32506 | 58157 | 53.56% | 0 | 0.00 | 5150.98 | 0.000 | 69.76% | 83.35% | `{"filegroups/source": 0.8865004181861877, "filetypes/kotlin": 0.7523986101150513, "general": 0.8847092986106873}` |
| filetypes/npm | joint_or_at_fp_0 | 1488 | 637 | 52.08% | 0 | 0.00 | 469183.52 | 0.000 | 68.49% | 66.45% | `{"filetypes/npm": 0.9936395287513733, "general": 0.9821503162384033}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19247 | 49.02% | 0 | 0.00 | 15563.46 | 0.000 | 65.79% | 99.73% | `{"filegroups/scripts": 0.974675714969635, "filetypes/lua": 0.9751942157745361, "general": 0.922386646270752}` |
| filetypes/php | joint_or_at_fp_0 | 5839 | 172350 | 47.70% | 0 | 0.00 | 1738.15 | 0.000 | 64.59% | 98.29% | `{"filegroups/scripts": 0.9932729005813599, "filetypes/php": 0.9984034895896912, "general": 0.9296882748603821}` |
| filetypes/java_class | joint_or_at_fp_0 | 1959 | 826178 | 46.15% | 0 | 0.00 | 362.60 | 0.000 | 63.15% | 99.87% | `{"filetypes/java_class": 0.9999011754989624, "general": 0.9828046560287476}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/html | joint_or_at_fp_0 | 255 | 15802 | 99.61% | 0 | 0.00 | 18956.13 | 0.000 | 99.80% | 99.99% | `{"filetypes/html": 0.9971267580986023}` |
| filetypes/rtf | joint_or_at_fp_0 | 6251 | 525 | 97.98% | 0 | 0.00 | 568990.75 | 0.000 | 98.98% | 98.14% | `{"filegroups/documents": 0.04553401470184326, "filetypes/rtf": 0.1712195873260498}` |
| filetypes/pkg-info | joint_or_at_fp_0 | 10566 | 2947 | 96.75% | 0 | 0.00 | 101601.97 | 0.000 | 98.35% | 97.46% | `{"filetypes/pkg-info": 0.12018036842346191}` |
| filetypes/crx | joint_or_at_fp_0 | 893 | 182 | 96.30% | 0 | 0.00 | 1632534.07 | 0.000 | 98.12% | 96.93% | `{"filetypes/crx": 0.43714338541030884, "general": 0.9354020953178406}` |
| filetypes/gem | joint_or_at_fp_0 | 854 | 1083 | 96.02% | 0 | 0.00 | 276232.02 | 0.000 | 97.97% | 98.24% | `{"filetypes/gem": 0.9645111560821533, "general": 0.9265512228012085}` |
| filetypes/xls | joint_or_at_fp_0 | 39675 | 20762 | 94.31% | 0 | 0.00 | 14427.88 | 0.000 | 97.07% | 96.27% | `{"filegroups/documents": 0.9931027889251709, "filetypes/xls": 0.9000883102416992, "general": 0.9979779720306396}` |
| filetypes/applescript | learned_blend_at_fp_0 | 57 | 229 | 92.98% | 0 | 0.00 | 1299660.55 | 0.000 | 96.36% | 98.60% | `{}` |
| filetypes/elf | joint_or_at_fp_0 | 189608 | 205020 | 90.99% | 0 | 0.00 | 1461.18 | 0.000 | 95.28% | 95.67% | `{"filegroups/native": 0.9847175478935242, "filetypes/elf": 0.9972903728485107, "general": 0.9921343326568604}` |
| filetypes/package.json | joint_or_at_fp_0 | 19179 | 26858 | 85.72% | 0 | 0.00 | 11153.34 | 0.000 | 92.31% | 94.05% | `{"filegroups/config": 0.9995417594909668, "filetypes/package.json": 0.9991888403892517, "general": 0.9960484504699707}` |
| filetypes/tar | joint_or_at_fp_0 | 30579 | 48299 | 82.65% | 0 | 0.00 | 6202.28 | 0.000 | 90.50% | 93.27% | `{"filetypes/tar": 0.998319685459137, "general": 0.9939501285552979}` |
| filetypes/docx | joint_or_at_fp_0 | 5065 | 402 | 81.15% | 0 | 0.00 | 742437.25 | 0.000 | 89.59% | 82.53% | `{"filegroups/documents": 0.5677497982978821, "filetypes/docx": 0.8922969698905945}` |
| filetypes/msi | joint_or_at_fp_0 | 5644 | 218 | 80.90% | 0 | 0.00 | 1364790.24 | 0.000 | 89.44% | 81.61% | `{"filetypes/msi": 0.555561363697052, "general": 0.9854252934455872}` |
| filetypes/ole | joint_or_at_fp_0 | 7392 | 6674 | 76.20% | 0 | 0.00 | 44876.54 | 0.000 | 86.50% | 87.49% | `{"filegroups/documents": 0.7310907244682312, "filetypes/ole": 0.9971190690994263}` |
| filetypes/lnk | joint_or_at_fp_0 | 4614 | 1065 | 74.40% | 0 | 0.00 | 280894.17 | 0.000 | 85.32% | 79.20% | `{"filetypes/lnk": 0.9565479755401611, "general": 0.9992970824241638}` |
| filetypes/chrome-manifest | joint_or_at_fp_0 | 97 | 304 | 74.23% | 0 | 0.00 | 980598.72 | 0.000 | 85.21% | 93.77% | `{"filetypes/chrome-manifest": 0.9263573884963989}` |
| filetypes/macho | joint_or_at_fp_0 | 2693 | 13832 | 74.19% | 0 | 0.00 | 21655.64 | 0.000 | 85.18% | 95.79% | `{"filegroups/native": 0.9292101263999939, "filetypes/macho": 0.9887740612030029, "general": 0.9761720895767212}` |
| filetypes/pdf | joint_or_at_fp_0 | 178639 | 24682 | 73.53% | 0 | 0.00 | 12136.58 | 0.000 | 84.74% | 76.74% | `{"filegroups/documents": 0.9932157397270203, "filetypes/pdf": 0.9362694025039673, "general": 0.9835054278373718}` |
| filetypes/python-bytecode | joint_or_at_fp_0 | 3417 | 393848 | 69.65% | 0 | 0.00 | 760.63 | 0.000 | 82.11% | 99.74% | `{"filetypes/python-bytecode": 0.9996863603591919, "general": 0.9460391402244568}` |
| filetypes/whl | joint_or_at_fp_0 | 2425 | 4645 | 69.20% | 0 | 0.00 | 64472.91 | 0.000 | 81.79% | 89.43% | `{"filetypes/whl": 0.987389326095581, "general": 0.9601284265518188}` |
| filetypes/clojure | joint_or_at_fp_0 | 131 | 7002 | 66.41% | 0 | 0.00 | 42774.80 | 0.000 | 79.82% | 99.38% | `{"filetypes/clojure": 0.9773902297019958}` |
| filetypes/shell | joint_or_at_fp_0 | 15722 | 72548 | 63.78% | 0 | 0.00 | 4129.23 | 0.000 | 77.89% | 93.55% | `{"filegroups/scripts": 0.9930756092071533, "filetypes/shell": 0.9718871712684631, "general": 0.9496476054191589}` |
| filetypes/pe | joint_or_at_fp_0 | 1370153 | 172762 | 57.36% | 0 | 0.00 | 1734.01 | 0.000 | 72.90% | 62.13% | `{"filegroups/native": 0.9994462132453918, "filetypes/pe": 0.9969835877418518, "general": 0.9997603297233582}` |
| filetypes/perl | joint_or_at_fp_0 | 387 | 44914 | 57.11% | 0 | 0.00 | 6669.71 | 0.000 | 72.70% | 99.63% | `{"filetypes/perl": 0.9909163117408752}` |
| filetypes/javascript | joint_or_at_fp_0 | 126491 | 714570 | 54.35% | 0 | 0.00 | 419.23 | 0.000 | 70.42% | 93.13% | `{"filegroups/scripts": 0.9965267777442932, "filetypes/javascript": 0.9934003353118896, "general": 0.998794674873352}` |
| filetypes/kotlin | joint_or_at_fp_0 | 32506 | 58157 | 53.56% | 0 | 0.00 | 5150.98 | 0.000 | 69.76% | 83.35% | `{"filegroups/source": 0.8865004181861877, "filetypes/kotlin": 0.7523986101150513, "general": 0.8847092986106873}` |
| filetypes/npm | joint_or_at_fp_0 | 1488 | 637 | 52.08% | 0 | 0.00 | 469183.52 | 0.000 | 68.49% | 66.45% | `{"filetypes/npm": 0.9936395287513733, "general": 0.9821503162384033}` |
| filetypes/lua | joint_or_at_fp_0 | 102 | 19247 | 49.02% | 0 | 0.00 | 15563.46 | 0.000 | 65.79% | 99.73% | `{"filegroups/scripts": 0.974675714969635, "filetypes/lua": 0.9751942157745361, "general": 0.922386646270752}` |
| filetypes/php | joint_or_at_fp_0 | 5839 | 172350 | 47.70% | 0 | 0.00 | 1738.15 | 0.000 | 64.59% | 98.29% | `{"filegroups/scripts": 0.9932729005813599, "filetypes/php": 0.9984034895896912, "general": 0.9296882748603821}` |
| filetypes/java_class | joint_or_at_fp_0 | 1959 | 826178 | 46.15% | 0 | 0.00 | 362.60 | 0.000 | 63.15% | 99.87% | `{"filetypes/java_class": 0.9999011754989624, "general": 0.9828046560287476}` |
| filetypes/powershell | joint_or_at_fp_0 | 5877 | 2588 | 44.84% | 0 | 0.00 | 115687.75 | 0.000 | 61.91% | 61.70% | `{"filegroups/scripts": 0.9967621564865112, "filetypes/powershell": 0.9924114942550659, "general": 0.9963623285293579}` |
