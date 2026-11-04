# `filetype/cab`

LightGBM specialist for `cab`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `cab` slice of the locked test partition: 106 malware / 13 benign (119 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.999912 | 0.999274 | 0.995261 | 99.06% | - |

## Specialist Performance

`filetypes/cab` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 1.000000 | 1.000000 | 0.000000 | 0.00% | 0.0159 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="cab: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `cab` are scored by `filegroups/archive`, `filegroups/rare_archive_recovery`, `filetypes/cab`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 744 (665 mal / 79 ben) |
| Feature spec | 19201 features (`accepted_pinned`) |
| n_estimators | 400 |
| num_leaves | 15 |
| max_depth | 6 |
| min_child_samples | 5 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 5.0 |
| early_stopping_rounds | 50 |
| device | cpu |
