# `filetype/text`

LightGBM specialist for `text`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `text` slice of the test partition: 159 malware / 7979 benign (8138 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.7609 | 0.2044 | 11.95% | 0.2581 | 0.0372 |

## Specialist Performance

`filetypes/text` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.7602 | 0.1877 | 0.2353 | 0.00% | 0.0179 | — |

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
