# `filetype/package.json`

LightGBM specialist for `package.json`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `package.json` slice of the locked test partition: 2,162 malware / 1,361 benign (3,523 rows). The OR-rule fires across `general`, `filegroups/config`, `filetypes/package.json` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 92.74% | 2,006 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/package.json` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9992 | 0.9996 | 0.9972 | 90.69% | 0.0034 | — |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `general`, `filegroups/config`, `filetypes/package.json`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 25,259 (15,617 mal / 9,642 ben) |
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
