# `filetype/plist`

LightGBM specialist for `plist`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `plist` slice of the locked test partition: 68 malware / 1,544 benign (1,612 rows). The OR-rule fires across `filegroups/config`, `filetypes/plist` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 1.47% | 1 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/plist` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.6257 | 0.1043 | 0.1600 | 1.47% | 0.0410 | — |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `filegroups/config`, `filetypes/plist`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 11,288 (541 mal / 10,747 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 64 |
| max_depth | 12 |
| min_child_samples | 120 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
