# `filetype/pptx`

LightGBM specialist for `pptx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `pptx` slice of the locked test partition: 22 malware / 21 benign (43 rows). The OR-rule fires across `general`, `filegroups/documents`, `filetypes/pptx` via the `learned_blend_at_fp_0` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 27.27% | 6 | 0 | 0.0 | `learned_blend_at_fp_0` |

## Specialist Performance

`filetypes/pptx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.6071 | 0.6534 | 0.6769 | 0.00% | 0.4821 | — |

## Routing

At the L3 deploy level the policy is `learned_blend_at_fp_0` over `general`, `filegroups/documents`, `filetypes/pptx`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 276 (106 mal / 170 ben) |
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
