# `filetype/ruby`

LightGBM specialist for `ruby`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `ruby` slice of the test partition: 7 malware / 2943 benign (2950 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.9991 | 0.6428 | 57.14% | 0.8000 | 0.0103 |

## Specialist Performance

`filetypes/ruby` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9989 | 0.8599 | 0.8333 | 71.43% | 0.0068 | — |

## Routing

Default level `joint_or_at_fp_0` over `general`, `filegroups/scripts`, `filetypes/ruby`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 20606 (66 mal / 20540 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.03 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
