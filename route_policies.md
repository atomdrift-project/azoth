# Azoth Route Policy Search

Best calibrated decision policy per filetype route. `*_with_escape` policies start from the specialist/group model, then allow general/group/type escape thresholds only when they add detections inside the route FP budget.

- Calibration snapshot: `5548950182`
- Rows: 19922689 (2963955 malware, 16958734 benign)

## L50 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 133 | 261 | 96.24% | 0 | 0.00 | 1141228.16 | 0.000 | 98.08% | 98.73% | `{"filetypes/bmp": 0.864970862865448}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 551 | 92.86% | 0 | 0.00 | 542214.75 | 0.000 | 96.30% | 99.34% | `{"filetypes/applescript": 0.3741610050201416}` |
| filetypes/mp3 | learned_blend_at_fp_0 | 196 | 329 | 91.84% | 0 | 0.00 | 906423.91 | 0.000 | 95.74% | 96.95% | `{}` |
| filetypes/asar | joint_or_at_fp_0 | 198 | 364 | 84.85% | 0 | 0.00 | 819625.97 | 0.000 | 91.80% | 94.66% | `{"filetypes/asar": 0.9176011681556702, "general": 0.863434374332428}` |
| filetypes/elf | joint_or_at_fp_0 | 197673 | 896861 | 82.71% | 0 | 0.00 | 334.02 | 0.000 | 90.54% | 96.88% | `{"filegroups/native": 0.9983146786689758, "filetypes/elf": 0.9998401403427124, "general": 0.9987873435020447}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 96 | 82.47% | 0 | 0.00 | 3072367.68 | 0.000 | 90.39% | 84.22% | `{"filetypes/cab": 0.9307347536087036, "general": 0.843382716178894}` |
| filetypes/html | joint_or_at_fp_0 | 342 | 276388 | 73.10% | 0 | 0.00 | 1083.88 | 0.000 | 84.46% | 99.97% | `{"filegroups/documents": 0.9166281819343567, "general": 0.9891511797904968}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 392 | 70.74% | 0 | 0.00 | 761304.70 | 0.000 | 82.87% | 72.00% | `{"filetypes/7z": 0.9947372674942017, "general": 0.9953701496124268}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 2969 | 8252 | 69.01% | 0 | 0.00 | 36296.52 | 0.000 | 81.67% | 91.80% | `{"filetypes/python_sdist": 0.9994314908981323, "general": 0.9643476009368896}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 193890 | 66.54% | 0 | 0.00 | 1545.06 | 0.000 | 79.91% | 99.96% | `{"filegroups/scripts": 0.9798375964164734, "filetypes/ruby": 0.9991861581802368, "general": 0.9350982904434204}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 602 | 64.02% | 0 | 0.00 | 496393.82 | 0.000 | 78.06% | 89.03% | `{}` |
| filetypes/shell | joint_or_at_fp_0 | 18947 | 164246 | 59.12% | 0 | 0.00 | 1823.91 | 0.000 | 74.31% | 95.77% | `{"filegroups/scripts": 0.9965369701385498, "filetypes/shell": 0.9964820146560669, "general": 0.9924511313438416}` |
| filetypes/dex | joint_or_at_fp_0 | 86 | 267 | 56.98% | 0 | 0.00 | 1115726.19 | 0.000 | 72.59% | 89.52% | `{"filetypes/dex": 0.8050459027290344, "general": 0.962040901184082}` |
| filetypes/tar | joint_or_at_fp_0 | 25334 | 89349 | 56.41% | 0 | 0.00 | 3352.79 | 0.000 | 72.13% | 90.37% | `{"filetypes/tar": 0.9992161989212036, "general": 0.9953067898750305}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 55.46% | 0 | 0.00 | 2980667.38 | 0.000 | 71.35% | 68.90% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9904627203941345}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44771 | 54.24% | 0 | 0.00 | 6691.01 | 0.000 | 70.33% | 99.94% | `{"general": 0.15437142550945282}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27346 | 84135 | 48.77% | 0 | 0.00 | 3560.56 | 0.000 | 65.57% | 87.43% | `{"filegroups/source": 0.9786453247070312, "filetypes/kotlin": 0.932830810546875, "general": 0.9933233857154846}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 46.30% | 0 | 0.00 | 255936.45 | 0.000 | 63.30% | 56.94% | `{"filetypes/lnk": 0.9949637651443481, "general": 0.9975140690803528}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28628 | 45.98% | 0 | 0.00 | 10463.80 | 0.000 | 62.99% | 99.84% | `{"filegroups/scripts": 0.9912540912628174, "filetypes/lua": 0.9913892149925232}` |
| filetypes/xpi | joint_or_at_fp_0 | 60 | 3177 | 45.00% | 0 | 0.00 | 94249.93 | 0.000 | 62.07% | 98.98% | `{"general": 0.9267789721488953}` |
| filetypes/npm | joint_or_at_fp_0 | 23735 | 198779 | 44.44% | 0 | 0.00 | 1507.06 | 0.000 | 61.53% | 94.07% | `{"filetypes/npm": 0.9999206066131592, "general": 0.9992729425430298}` |
| filetypes/perl | joint_or_at_fp_0 | 435 | 80331 | 43.91% | 0 | 0.00 | 3729.17 | 0.000 | 61.02% | 99.70% | `{"filegroups/scripts": 0.9894083142280579, "filetypes/perl": 0.9978692531585693, "general": 0.9975235462188721}` |
| filetypes/jar | joint_or_at_fp_0 | 3789 | 41075 | 43.57% | 0 | 0.00 | 7293.06 | 0.000 | 60.70% | 95.23% | `{"filetypes/jar": 0.9959813952445984, "general": 0.998820424079895}` |
| filetypes/python | joint_or_at_fp_0 | 23537 | 676233 | 43.55% | 0 | 0.00 | 443.00 | 0.000 | 60.68% | 98.10% | `{"filegroups/scripts": 0.9983296990394592, "filetypes/python": 0.9976376891136169, "general": 0.9938123822212219}` |
| filetypes/powershell | joint_or_at_fp_0 | 5949 | 6139 | 42.66% | 0 | 0.00 | 48786.47 | 0.000 | 59.81% | 71.78% | `{"filegroups/scripts": 0.9983533620834351, "filetypes/powershell": 0.9963827133178711, "general": 0.9988251328468323}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 91505 | 32042 | 36.91% | 0 | 0.00 | 9348.96 | 0.000 | 53.92% | 53.27% | `{"filetypes/ole_doc": 0.9992323517799377, "general": 0.9995884299278259}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 36.39% | 0 | 0.00 | 292981.55 | 0.000 | 53.36% | 45.49% | `{"filegroups/documents": 0.9999420046806335, "filetypes/rtf": 0.9931700229644775, "general": 0.9988256692886353}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 35.93% | 0 | 0.00 | 5495548.85 | 0.000 | 52.87% | 36.09% | `{"general": 0.9995707679368523}` |
| filetypes/zip | joint_or_at_fp_0 | 107307 | 92186 | 32.52% | 0 | 0.00 | 3249.61 | 0.000 | 49.08% | 63.70% | `{"filetypes/zip": 0.9996384978294373, "general": 0.998327910900116}` |
| filetypes/package.json | joint_or_at_fp_0 | 22318 | 76616 | 32.07% | 0 | 0.00 | 3909.98 | 0.000 | 48.57% | 84.68% | `{"filegroups/config": 0.9999938011169434, "filetypes/package.json": 0.9999186396598816, "general": 0.9994248747825623}` |

## L100 Hostile

Rows marked † are below data resolution: the per-filetype calibration sample is too small to credibly assert FP/100M ≤ target at this level (95% CI). The threshold shown is the loosest empirical 0-FP threshold; FP/100M is what the test partition actually observed under that threshold. *95% CI upper* is the Clopper-Pearson upper bound on deployment FP/100M given the observed FP count in this filetype's benigns.

| Route | Policy | Malware | Benign | Recall | FP | FP/100M | 95% CI upper (FP/100M) | Global FP/100M | F1 | Accuracy | Thresholds |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| filetypes/bmp | joint_or_at_fp_0 | 133 | 261 | 96.24% | 0 | 0.00 | 1141228.16 | 0.000 | 98.08% | 98.73% | `{"filetypes/bmp": 0.864970862865448}` |
| filetypes/applescript | joint_or_at_fp_0 | 56 | 551 | 92.86% | 0 | 0.00 | 542214.75 | 0.000 | 96.30% | 99.34% | `{"filetypes/applescript": 0.3741610050201416}` |
| filetypes/mp3 | learned_blend_at_fp_0 | 196 | 329 | 91.84% | 0 | 0.00 | 906423.91 | 0.000 | 95.74% | 96.95% | `{}` |
| filetypes/asar | joint_or_at_fp_0 | 198 | 364 | 84.85% | 0 | 0.00 | 819625.97 | 0.000 | 91.80% | 94.66% | `{"filetypes/asar": 0.9176011681556702, "general": 0.863434374332428}` |
| filetypes/elf | joint_or_at_fp_0 | 197673 | 896861 | 82.71% | 0 | 0.00 | 334.02 | 0.000 | 90.54% | 96.88% | `{"filegroups/native": 0.9983146786689758, "filetypes/elf": 0.9998401403427124, "general": 0.9987873435020447}` |
| filetypes/cab | joint_or_at_fp_0 | 867 | 96 | 82.47% | 0 | 0.00 | 3072367.68 | 0.000 | 90.39% | 84.22% | `{"filetypes/cab": 0.9307347536087036, "general": 0.843382716178894}` |
| filetypes/html | joint_or_at_fp_0 | 342 | 276388 | 73.10% | 0 | 0.00 | 1083.88 | 0.000 | 84.46% | 99.97% | `{"filegroups/documents": 0.9166281819343567, "general": 0.9891511797904968}` |
| filetypes/7z | joint_or_at_fp_0 | 8764 | 392 | 70.74% | 0 | 0.00 | 761304.70 | 0.000 | 82.87% | 72.00% | `{"filetypes/7z": 0.9947372674942017, "general": 0.9953701496124268}` |
| filetypes/python_sdist | joint_or_at_fp_0 | 2969 | 8252 | 69.01% | 0 | 0.00 | 36296.52 | 0.000 | 81.67% | 91.80% | `{"filetypes/python_sdist": 0.9994314908981323, "general": 0.9643476009368896}` |
| filetypes/ruby | joint_or_at_fp_0 | 257 | 193890 | 66.54% | 0 | 0.00 | 1545.06 | 0.000 | 79.91% | 99.96% | `{"filegroups/scripts": 0.9798375964164734, "filetypes/ruby": 0.9991861581802368, "general": 0.9350982904434204}` |
| filetypes/ico | learned_blend_at_fp_0 | 264 | 602 | 64.02% | 0 | 0.00 | 496393.82 | 0.000 | 78.06% | 89.03% | `{}` |
| filetypes/shell | joint_or_at_fp_0 | 18947 | 164246 | 59.12% | 0 | 0.00 | 1823.91 | 0.000 | 74.31% | 95.77% | `{"filegroups/scripts": 0.9965369701385498, "filetypes/shell": 0.9964820146560669, "general": 0.9924511313438416}` |
| filetypes/dex | joint_or_at_fp_0 | 86 | 267 | 56.98% | 0 | 0.00 | 1115726.19 | 0.000 | 72.59% | 89.52% | `{"filetypes/dex": 0.8050459027290344, "general": 0.962040901184082}` |
| filetypes/tar | joint_or_at_fp_0 | 25334 | 89349 | 56.41% | 0 | 0.00 | 3352.79 | 0.000 | 72.13% | 90.37% | `{"filetypes/tar": 0.9992161989212036, "general": 0.9953067898750305}` |
| filetypes/chm | joint_or_at_fp_0 | 229 | 99 | 55.46% | 0 | 0.00 | 2980667.38 | 0.000 | 71.35% | 68.90% | `{"filetypes/chm": 0.8947448134422302, "general": 0.9904627203941345}` |
| filetypes/swift | joint_or_at_fp_0 | 59 | 44771 | 54.24% | 0 | 0.00 | 6691.01 | 0.000 | 70.33% | 99.94% | `{"general": 0.15437142550945282}` |
| filetypes/kotlin | joint_or_at_fp_0 | 27346 | 84135 | 48.77% | 0 | 0.00 | 3560.56 | 0.000 | 65.57% | 87.43% | `{"filegroups/source": 0.9786453247070312, "filetypes/kotlin": 0.932830810546875, "general": 0.9933233857154846}` |
| filetypes/lnk | joint_or_at_fp_0 | 4732 | 1169 | 46.30% | 0 | 0.00 | 255936.45 | 0.000 | 63.30% | 56.94% | `{"filetypes/lnk": 0.9949637651443481, "general": 0.9975140690803528}` |
| filetypes/lua | joint_or_at_fp_0 | 87 | 28628 | 45.98% | 0 | 0.00 | 10463.80 | 0.000 | 62.99% | 99.84% | `{"filegroups/scripts": 0.9912540912628174, "filetypes/lua": 0.9913892149925232}` |
| filetypes/xpi | joint_or_at_fp_0 | 60 | 3177 | 45.00% | 0 | 0.00 | 94249.93 | 0.000 | 62.07% | 98.98% | `{"general": 0.9267789721488953}` |
| filetypes/npm | joint_or_at_fp_0 | 23735 | 198779 | 44.44% | 0 | 0.00 | 1507.06 | 0.000 | 61.53% | 94.07% | `{"filetypes/npm": 0.9999206066131592, "general": 0.9992729425430298}` |
| filetypes/perl | joint_or_at_fp_0 | 435 | 80331 | 43.91% | 0 | 0.00 | 3729.17 | 0.000 | 61.02% | 99.70% | `{"filegroups/scripts": 0.9894083142280579, "filetypes/perl": 0.9978692531585693, "general": 0.9975235462188721}` |
| filetypes/jar | joint_or_at_fp_0 | 3789 | 41075 | 43.57% | 0 | 0.00 | 7293.06 | 0.000 | 60.70% | 95.23% | `{"filetypes/jar": 0.9959813952445984, "general": 0.998820424079895}` |
| filetypes/python | joint_or_at_fp_0 | 23537 | 676233 | 43.55% | 0 | 0.00 | 443.00 | 0.000 | 60.68% | 98.10% | `{"filegroups/scripts": 0.9983296990394592, "filetypes/python": 0.9976376891136169, "general": 0.9938123822212219}` |
| filetypes/powershell | joint_or_at_fp_0 | 5949 | 6139 | 42.66% | 0 | 0.00 | 48786.47 | 0.000 | 59.81% | 71.78% | `{"filegroups/scripts": 0.9983533620834351, "filetypes/powershell": 0.9963827133178711, "general": 0.9988251328468323}` |
| filetypes/rar | calibrate_inherited | 22193 | 53 | 41.80% | 0 | 0.00 | 5495548.85 | 0.000 | 58.95% | 41.94% | `{"general": 0.9994034133049241}` |
| filetypes/ole_doc | joint_or_at_fp_0 | 91505 | 32042 | 36.91% | 0 | 0.00 | 9348.96 | 0.000 | 53.92% | 53.27% | `{"filetypes/ole_doc": 0.9992323517799377, "general": 0.9995884299278259}` |
| filetypes/rtf | joint_or_at_fp_0 | 6112 | 1021 | 36.39% | 0 | 0.00 | 292981.55 | 0.000 | 53.36% | 45.49% | `{"filegroups/documents": 0.9999420046806335, "filetypes/rtf": 0.9931700229644775, "general": 0.9988256692886353}` |
| filetypes/zip | joint_or_at_fp_0 | 107307 | 92186 | 32.52% | 0 | 0.00 | 3249.61 | 0.000 | 49.08% | 63.70% | `{"filetypes/zip": 0.9996384978294373, "general": 0.998327910900116}` |
| filetypes/package.json | joint_or_at_fp_0 | 22318 | 76616 | 32.07% | 0 | 0.00 | 3909.98 | 0.000 | 48.57% | 84.68% | `{"filegroups/config": 0.9999938011169434, "filetypes/package.json": 0.9999186396598816, "general": 0.9994248747825623}` |
