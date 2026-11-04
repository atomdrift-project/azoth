# `filegroup/filegroups_archive_oct26`

LightGBM specialist for `7z`, `apk`, `apk_alpine`, `apk_android`, `cab`, `chm`, `conda`, `cpio`, `crate`, `crx`, `deb`, `dmg`, `ear`, `egg`, `gem`, `ipa`, `iso`, `jar`, `msix`, `npm`, `nupkg`, `oci_image`, `ociimage`, `pkg`, `pkg_arch`, `pkg_freebsd`, `pkg_macos`, `python_sdist`, `pythonsdist`, `rar`, `rpa`, `rpm`, `snap`, `squashfs`, `tar`, `tar.bz2`, `tar.gz`, `tar.xz`, `tar.zst`, `tgz`, `vsix`, `war`, `whl`, `xbps`, `xpi`, `zip`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `filegroups_archive_oct26`). ROC 0.898411, PR 0.870927, F1 0.8800 on 169,840 rows (25,696 mal / 144,144 ben).

## Routing

Files matching `filegroups_archive_oct26` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,014,114 (134,013 mal / 880,101 ben) |
| Feature spec | 43075 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
