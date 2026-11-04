# `filegroup/general_previous`

LightGBM specialist for `7z`, `aiff`, `ani`, `apk_alpine`, `apk_android`, `applescript`, `asar`, `asp`, `avif`, `batch`, `beam`, `bmp`, `bz2`, `c`, `cab`, `cargo.lock`, `cargo.toml`, `cfml`, `chm`, `chrome_manifest`, `clojure`, `cmake`, `composer`, `composer.json`, `composer.lock`, `conda`, `cpan`, `cpio`, `cran`, `crate`, `crx`, `csharp`, `data`, `deb`, `desktop_entry`, `dex`, `dmg`, `dockerfile`, `dos_com`, `egg`, `elf`, `elixir`, `flatpak`, `font`, `gem`, `gemfile.lock`, `gentoo_binpkg`, `gif`, `github_actions`, `go`, `go.mod`, `go.sum`, `go_module`, `groovy`, `gyp`, `gz`, `html`, `ico`, `ipa`, `ircii`, `iso`, `jar`, `java`, `java_class`, `javascript`, `jpeg`, `json`, `jsp`, `kotlin`, `lnk`, `lua`, `lzma`, `macho`, `makefile`, `markdown`, `mirc`, `mp3`, `mp4`, `ne`, `nib`, `npm`, `nrbf`, `nupkg`, `objective_c`, `oci_image`, `odf`, `ole_doc`, `ooxml`, `package-lock.json`, `package.json`, `pbxproj`, `pdf`, `pe`, `perl`, `pgp_signature`, `phar`, `php`, `pickle`, `pipfile.lock`, `pkg_arch`, `pkg_freebsd`, `pkg_info`, `pkg_macos`, `plist`, `png`, `pnpm-lock.yaml`, `poetry.lock`, `postscript`, `powershell`, `ppsx`, `pyproject.toml`, `python`, `python_bytecode`, `python_sdist`, `rar`, `reg`, `registry`, `requirements.txt`, `rpa`, `rpm`, `rtf`, `ruby`, `rust`, `scala`, `shell`, `snap`, `squashfs`, `src_info`, `static-lib`, `svg`, `swift`, `systemd_service`, `tar`, `tex`, `text`, `tiff`, `unknown`, `vbs`, `vhd`, `vsix`, `vsix_manifest`, `wasm`, `wav`, `webp`, `whl`, `xml`, `xpi`, `xz`, `yaml`, `yara`, `yarn.lock`, `zig`, `zip`, `zst`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `general_previous`). ROC -, PR -, F1 - on - rows (- mal / - ben).

## Routing

Files matching `general_previous` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 14,854,553 (- mal / - ben) |
| Feature spec | 128071 features (`?`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
