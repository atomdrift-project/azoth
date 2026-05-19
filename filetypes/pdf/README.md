# `filetype/pdf`

LightGBM specialist for `pdf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `pdf` slice of the locked test partition: 21,777 malware / 1,734 benign (23,511 rows). The OR-rule fires across `general`, `filegroups/documents`, `filetypes/pdf` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 5.87% | 1,278 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/pdf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9438 | 0.9935 | 0.9889 | 6.13% | 0.8291 | ROC -0.0474 / PR +0.0002 |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `general`, `filegroups/documents`, `filetypes/pdf`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 162,814 (150,685 mal / 12,129 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 120 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 40 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
