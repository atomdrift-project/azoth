# `filetype/elf`

LightGBM specialist for `elf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `elf` slice of the locked test partition: 8,826 malware / 16,927 benign (25,753 rows). The OR-rule fires across `general`, `filegroups/native`, `filetypes/elf` via the `learned_blend_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 93.07% | 8,150 | 0 | 0.0 | `learned_blend_at_fp_0` |

## Specialist Performance

`filetypes/elf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9999 | 0.9999 | 0.9947 | 93.65% | 0.0038 | ROC +0.0066 / PR +0.0066 |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_0` over `general`, `filegroups/native`, `filetypes/elf`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 178,232 (61,224 mal / 117,008 ben) |
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
