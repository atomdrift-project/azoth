# `filetype/xlsx`

LightGBM specialist for `xlsx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

> Benchmark AUC degenerate on this split. Routed full-corpus calibration governs deployment.

## Ensemble Performance

Deployed at L3 hostile on the `xlsx` slice of the locked test partition: 2,237 malware / 12 benign (2,249 rows). The OR-rule fires across `filegroups/documents` via the `joint_or_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 29.32% | 656 | 0 | 0.0 | `joint_or_at_fp_0` |

## Specialist Performance

`filetypes/xlsx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.5000 | 0.9947 | 0.9973 | — | 0.0053 | — |

## Routing

At the L3 deploy level the policy is `joint_or_at_fp_0` over `filegroups/documents`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 15,678 (15,546 mal / 132 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 100 |
| num_leaves | 48 |
| max_depth | 12 |
| min_child_samples | 20 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
