# `filetype/npm`

LightGBM specialist for `npm`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `npm` slice of the locked test partition: 3,675 malware / 44,281 benign (47,956 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.973833 | 0.993752 | 0.849546 | 73.90% | - |

## Specialist Performance

`filetypes/npm` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.975260 | 0.994305 | 0.815280 | 68.82% | 0.0083 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="npm: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `npm` are scored by `filegroups/archive`, `filegroups/archive_oct31`, `filegroups/filegroups_archive_oct26`, `filegroups/filetypes_npm_oct26`, `filegroups/npm_benign_weight_recovery`, `filegroups/npm_general_layout_recovery`, `filegroups/npm_new_training_recovery`, `filegroups/npm_retained_hnm_recovery`, `filegroups/npm_six_seed_complement`, `filetypes/npm`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 292,711 (20,750 mal / 271,961 ben) |
| Feature spec | 31846 features (`accepted_pinned`) |
| n_estimators | 800 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.025 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 2.0 |
| early_stopping_rounds | 60 |
| device | cpu |
