# `filetype/apk_android`

LightGBM specialist for `apk_android`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `apk_android` slice of the locked test partition: 517 malware / 121 benign (638 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.944361 | 0.845101 | 0.948454 | 97.87% | - |

## Specialist Performance

`filetypes/apk_android` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.932235 | 0.809006 | 0.789766 | 68.67% | 0.2576 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="apk_android: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `apk_android` are scored by `filegroups/apk_android_retained_hnm_recovery`, `filegroups/archive`, `filetypes/apk_android`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 3,502 (3,246 mal / 256 ben) |
| Feature spec | 23080 features (`route_specific`) |
| n_estimators | 250 |
| num_leaves | 16 |
| max_depth | 6 |
| min_child_samples | 10 |
| learning_rate | 0.02 |
| subsample / colsample | 0.6 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 10 |
| device | auto |
