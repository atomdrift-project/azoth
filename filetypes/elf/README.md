# `filetype/elf`

LightGBM specialist for `elf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `elf` slice of the locked test partition: 9,019 malware / 17,064 benign (26,083 rows). The OR-rule fires across `general`, `filegroups/native`, `filetypes/elf` via the `learned_blend_at_fp_3` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 93.14% | 8,352 | 0 | 0.0 | `learned_blend_at_fp_3` |

## Specialist Performance

`filetypes/elf` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9999 | 0.9999 | 0.9954 | 81.43% | 0.0025 | ROC +0.0066 / PR +0.0066 |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_3` over `general`, `filegroups/native`, `filetypes/elf`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 182,595 (64,088 mal / 118,507 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
