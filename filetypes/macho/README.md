# `filetype/macho`

LightGBM specialist for `macho`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `macho` slice of the locked test partition: 262 malware / 1,383 benign (1,645 rows). The OR-rule fires across `filetypes/macho` via the `learned_blend_at_fp_1` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 67.18% | 176 | 0 | 0.0 | `learned_blend_at_fp_1` |

## Specialist Performance

`filetypes/macho` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9990 | 0.9947 | 0.9638 | 84.35% | 0.0098 | — |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_1` over `general`, `filegroups/native`, `filetypes/macho`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 11,115 (1,805 mal / 9,310 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
