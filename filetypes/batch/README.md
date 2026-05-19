# `filetype/batch`

LightGBM specialist for `batch`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

`filetypes/batch` specialist scored *alone* on its test-partition slice: 21095 malware / 425 benign (21520 rows). The bundle README reports the deployed ensemble's metrics on this same slice; numbers there will differ.

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9996 | 1.0000 | 99.88% | 0.0020 | — |

## Routing

Default level `learned_blend_at_fp_3` over `general`, `filegroups/scripts`, `filetypes/batch`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 150148 (146980 mal / 3168 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
