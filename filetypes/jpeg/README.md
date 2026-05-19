# `filetype/jpeg`

LightGBM specialist for `jpeg`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `jpeg` slice of the test partition: 125 malware / 1319 benign (1444 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.7716 | 0.3336 | 0.80% | 0.3212 | 0.0744 |

## Specialist Performance

`filetypes/jpeg` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.7714 | 0.3336 | 0.3212 | 0.80% | 0.0745 | — |

## Routing

Default level `learned_blend_at_fp_1` over `general`, `filegroups/media`, `filetypes/jpeg`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 10467 (844 mal / 9623 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
