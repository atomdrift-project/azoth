# `filetype/rust`

LightGBM specialist for `rust`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `rust` slice of the locked test partition: 164 malware / 9,604 benign (9,768 rows). The OR-rule fires across `general`, `filetypes/rust` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 1.22% | 2 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/rust` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.7708 | 0.1057 | 0.1805 | 1.22% | 0.0165 | — |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `general`, `filetypes/rust`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 68,339 (1,117 mal / 67,222 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 200 |
| num_leaves | 128 |
| max_depth | 14 |
| min_child_samples | 50 |
| learning_rate | 0.04 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
