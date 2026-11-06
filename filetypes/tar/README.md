# `filetype/tar`

LightGBM specialist for `tar`, `tar.bz2`, `tar.gz`, `tar.xz`, `tar.zst`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `tar` slice of the locked test partition: 1,908 malware / 13,561 benign (15,469 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.978276 | 0.995454 | 0.820370 | 69.65% | - |

## Specialist Performance

`filetypes/tar` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.979415 | 0.995712 | 0.793811 | 65.88% | 0.0132 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="tar: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `tar` are scored by `filegroups/archive`, `filegroups/filegroups_archive_oct26`, `filegroups/filetypes_tar_oct26`, `filegroups/tar_benign_weight_recovery`, `filegroups/tar_general_layout_recovery`, `filegroups/tar_retained_hnm_recovery`, `filetypes/tar`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 105,388 (20,203 mal / 85,185 ben) |
| Feature spec | 2144 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
