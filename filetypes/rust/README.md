# `filetype/rust`

LightGBM specialist for `rust`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

`filetypes/rust` specialist scored *alone* on its test-partition slice: 164 malware / 9604 benign (9768 rows). The bundle README reports the deployed ensemble's metrics on this same slice; numbers there will differ.

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7708 | 0.1057 | 18.05% | 0.0165 | — |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filetypes/rust`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 68339 (1117 mal / 67222 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 200 |
| num_leaves | 128 |
| max_depth | 14 |
| min_child_samples | 50 |
| learning_rate | 0.04 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
