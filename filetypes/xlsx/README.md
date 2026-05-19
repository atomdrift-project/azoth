# `filetype/xlsx`

LightGBM specialist for `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Ensemble Performance

Deployed at L3 hostile on the `xlsx` slice of the locked test partition: 2,232 malware / 12 benign (2,244 rows). The OR-rule fires across `general`, `filegroups/documents`, `filetypes/xlsx` via the `learned_blend_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 28.23% | 630 | 0 | 0.0 | `learned_blend_at_fp_0` |

## Specialist Performance

`filetypes/xlsx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.5000 | 0.9947 | 0.9973 | — | 0.0053 | — |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_0` over `general`, `filegroups/documents`, `filetypes/xlsx`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 15,655 (15,523 mal / 132 ben) |
| Feature spec | 60358 features (`general_shared`) |
| n_estimators | 100 |
| num_leaves | 48 |
| max_depth | 12 |
| min_child_samples | 20 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
