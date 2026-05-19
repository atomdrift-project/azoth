# `filetype/makefile`

LightGBM specialist for `makefile`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `makefile` slice of the test partition: 17 malware / 2740 benign (2757 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.7597 | 0.0184 | 0.00% | 5.83% | 0.0062 |

## Specialist Performance

`filetypes/makefile` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7599 | 0.0184 | 5.83% | 0.0062 | — |

## Routing

Default level `joint_or_at_fp_0` over `filegroups/source`, `filetypes/makefile`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 18940 (146 mal / 18794 ben) |
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
