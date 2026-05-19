# `filetype/javascript`

LightGBM specialist for `javascript`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `javascript` slice of the locked test partition: 10,488 malware / 59,418 benign (69,906 rows). The OR-rule fires across `general`, `filegroups/scripts`, `filetypes/javascript` via the `filetype_only` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 64.25% | 6,798 | 0 | 0.0 | `filetype_only` |

## Specialist Performance

`filetypes/javascript` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9960 | 0.9825 | 0.9320 | 68.86% | 0.0186 | — |

## Routing

At the L3 deploy level the policy is `filetype_only` over `filetypes/javascript`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 481,289 (72,891 mal / 408,398 ben) |
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
