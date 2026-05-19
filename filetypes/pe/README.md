# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `pe` slice of the locked test partition: 109,970 malware / 18,938 benign (128,908 rows). The OR-rule fires across `general`, `filegroups/native`, `filetypes/pe` via the `learned_blend_at_fp_3` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 78.71% | 88,731 | 3 | 158.4 | `learned_blend_at_fp_3` |

## Specialist Performance

`filetypes/pe` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9983 | 0.9997 | 0.9942 | 46.79% | 0.0163 | ROC +0.0001 / PR +0.0014 |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_3` over `general`, `filegroups/native`, `filetypes/pe`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 919,254 (786,579 mal / 132,675 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
