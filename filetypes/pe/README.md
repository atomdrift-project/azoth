# `filetype/pe`

LightGBM specialist for `pe`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `pe` slice of the locked test partition: 110,233 malware / 18,952 benign (129,185 rows). The OR-rule fires across `general`, `filegroups/native`, `filetypes/pe` via the `learned_blend_at_fp_4` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 91.11% | 102,961 | 3 | 158.3 | `learned_blend_at_fp_4` |

## Specialist Performance

`filetypes/pe` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9999 | 1.0000 | 0.9988 | 84.76% | 0.0022 | ROC +0.0017 / PR +0.0017 |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_4` over `general`, `filegroups/native`, `filetypes/pe`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 924,481 (791,466 mal / 133,015 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
