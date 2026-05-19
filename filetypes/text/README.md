# `filetype/text`

LightGBM specialist for `text`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

`filetypes/text` specialist scored *alone* on its test-partition slice: 159 malware / 7979 benign (8138 rows). The bundle README reports the deployed ensemble's metrics on this same slice; numbers there will differ.

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7602 | 0.1877 | 23.53% | 0.0179 | — |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filetypes/text`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 56781 (1029 mal / 55752 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 50 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
