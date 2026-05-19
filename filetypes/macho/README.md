# `filetype/macho`

LightGBM specialist for `macho`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

`filetypes/macho` specialist scored *alone* on its test-partition slice: 258 malware / 1382 benign (1640 rows). The bundle README reports the deployed ensemble's metrics on this same slice; numbers there will differ.

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9988 | 0.9936 | 95.94% | 0.0108 | — |

## Routing

Default level `learned_blend_at_fp_0` over `general`, `filegroups/native`, `filetypes/macho`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 11059 (1783 mal / 9276 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
