# `filetype/pptx`

LightGBM specialist for `pptx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed routed ensemble on the `pptx` slice of the test partition: 22 malware / 21 benign (43 rows). These are the headline numbers from the bundle [README](../../README.md).

| ROC AUC | PR AUC | Recall @ 3FP/M | F1 | Brier |
|---:|---:|---:|---:|---:|
| 0.6071 | 0.6534 | 0.00% | 67.69% | 0.4821 |

## Specialist Performance

`filetypes/pptx` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.6071 | 0.6534 | 67.69% | 0.4821 | — |

## Routing

Default level `learned_blend_at_fp_0` over `general`, `filegroups/documents`, `filetypes/pptx`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

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
