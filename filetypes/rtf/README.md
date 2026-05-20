# `filetype/rtf`

LightGBM specialist for `rtf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `rtf` slice of the locked test partition: 215 malware / 51 benign (266 rows). The OR-rule fires across `general`, `filegroups/documents`, `filetypes/rtf` via the `max_rule` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 97.67% | 210 | 0 | 0.0 | `max_rule` |

## Specialist Performance

`filetypes/rtf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9983 | 0.9996 | 0.9885 | 95.35% | 0.0299 | — |

## Routing

At the L3 deploy level the policy is `max_rule` over `general`, `filegroups/documents`, `filetypes/rtf`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,679 (1,250 mal / 429 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 40 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
