# `filetype/xml`

LightGBM specialist for `xml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `xml` slice of the locked test partition: 291 malware / 18,378 benign (18,669 rows). The OR-rule fires across `general`, `filegroups/config`, `filetypes/xml` via the `learned_blend_at_fp_3` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 2.74% | 8 | 0 | 0.0 | `learned_blend_at_fp_3` |

## Specialist Performance

`filetypes/xml` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.5068 | 0.0245 | 0.0307 | 0.00% | 0.0153 | — |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_3` over `general`, `filegroups/config`, `filetypes/xml`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 129,881 (1,965 mal / 127,916 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 128 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
