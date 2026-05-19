# `filetype/unknown`

LightGBM specialist for `unknown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `unknown` slice of the locked test partition: 1,342 malware / 2,020 benign (3,362 rows). The OR-rule fires across `filetypes/unknown` via the `filetype_only_at_fp_3` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 0.00% | 0 | 0 | 0.0 | `filetype_only_at_fp_3` |

## Specialist Performance

`filetypes/unknown` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.8312 | 0.8045 | 0.7651 | 0.00% | 0.3915 | — |

## Routing

At the L3 deploy level the policy is `filetype_only_at_fp_3` over `filetypes/unknown`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 23,626 (9,702 mal / 13,924 ben) |
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
