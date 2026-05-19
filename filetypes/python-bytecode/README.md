# `filetype/python-bytecode`

LightGBM specialist for `python-bytecode`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `python-bytecode` slice of the locked test partition: 233 malware / 3,841 benign (4,074 rows). The OR-rule fires across `general` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 29.61% | 69 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/python-bytecode` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9992 | 0.9929 | 0.9892 | 97.85% | 0.0016 | — |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `general`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 26,312 (1,621 mal / 24,691 ben) |
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
