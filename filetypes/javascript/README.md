# `filetype/javascript`

LightGBM specialist for `javascript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `javascript` slice of the locked test partition: 10,529 malware / 59,665 benign (70,194 rows). The OR-rule fires across `general`, `filegroups/scripts`, `filetypes/javascript` via the `filetype_only` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 88.33% | 9,382 | 2 | 33.5 | `filetype_only` |

## Specialist Performance

`filetypes/javascript` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9996 | 0.9981 | 0.9817 | 74.43% | 0.0052 | — |

## Routing

At the L3 deploy level the policy is `filetype_only` over `filetypes/javascript`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 486,647 (73,852 mal / 412,795 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
