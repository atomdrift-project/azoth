# `filetype/shell`

LightGBM specialist for `shell`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `shell` slice of the locked test partition: 920 malware / 5,682 benign (6,602 rows). The OR-rule fires across `filetypes/shell` via the `filetype_only` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 46.21% | 366 | 0 | 0.0 | `filetype_only` |

## Specialist Performance

`filetypes/shell` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9969 | 0.9855 | 0.9470 | 81.09% | 0.0137 | — |

## Routing

At the L3 deploy level the policy is `filetype_only` over `filetypes/shell`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 44,922 (5,513 mal / 39,409 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 150 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
