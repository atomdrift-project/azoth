# `filetype/macho`

LightGBM specialist for `macho`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `macho` slice of the test partition: 258 malware / 1382 benign (1640 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.9988 | 0.9936 | 80.62% | 0.9594 | 0.0107 |

## Specialist Performance

`filetypes/macho` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9988 | 0.9936 | 0.9594 | 80.62% | 0.0108 | — |

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
