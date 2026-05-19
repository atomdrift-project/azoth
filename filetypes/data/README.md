# `filetype/data`

LightGBM specialist for `data`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `data` slice of the locked test partition: 58 malware / 1,157 benign (1,215 rows). The OR-rule fires across `filetypes/data` via the `filetype_only_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 77.59% | 45 | 0 | 0.0 | `filetype_only_at_fp_0` |

## Specialist Performance

`filetypes/data` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9705 | 0.8811 | 0.8762 | 72.41% | 0.0118 | — |

## Routing

At the L3 deploy level the policy is `filetype_only_at_fp_0` over `filetypes/data`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 8,214 (347 mal / 7,867 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.03 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
