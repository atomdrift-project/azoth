# `filetype/unknown`

LightGBM specialist for `unknown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `unknown` slice of the test partition: 1342 malware / 2020 benign (3362 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.8331 | 0.8282 | 12.37% | 0.7641 | 0.1208 |

## Specialist Performance

`filetypes/unknown` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.8312 | 0.8045 | 0.7651 | 0.00% | 0.3915 | — |

## Routing

Default level `filetype_only_at_fp_3` over `filetypes/unknown`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 23626 (9702 mal / 13924 ben) |
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
