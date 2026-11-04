# `filetype/yaml`

LightGBM specialist for `yaml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `yaml` slice of the locked test partition: 4 malware / 7,234 benign (7,238 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.500807 | 0.756998 | 0.444444 | 50.00% | - |

## Specialist Performance

`filetypes/yaml` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.501000 | 0.766571 | 0.666667 | 50.00% | 0.0003 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="yaml: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `yaml` are scored by `filegroups/config`, `filetypes/yaml`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 42,863 (6 mal / 42,857 ben) |
| Feature spec | 3040 features (`accepted_pinned`) |
| n_estimators | 250 |
| num_leaves | 32 |
| max_depth | 8 |
| min_child_samples | 10 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 5.0 |
| early_stopping_rounds | 25 |
| device | cpu |
