# `filetype/batch`

LightGBM specialist for `batch`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `batch` slice of the locked test partition: 21,095 malware / 425 benign (21,520 rows). The OR-rule fires across `general`, `filegroups/scripts`, `filetypes/batch` via the `learned_blend_at_fp_3` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 98.85% | 20,852 | 0 | 0.0 | `learned_blend_at_fp_3` |

## Specialist Performance

`filetypes/batch` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9996 | 1.0000 | 0.9988 | 98.84% | 0.0020 | — |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_3` over `general`, `filegroups/scripts`, `filetypes/batch`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 150,148 (146,980 mal / 3,168 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
