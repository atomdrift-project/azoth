# `filetype/msi`

LightGBM specialist for `msi`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Deployed at L3 hostile on the `msi` slice of the locked test partition: 218 malware / 8 benign (226 rows). The OR-rule fires across `filetypes/msi` via the `filetype_only` policy.

| Recall | TP | FP | FP / M | Policy |
|---:|---:|---:|---:|---|
| 61.11% | 143 | 0 | 0.0 | `filetype_only` |

## Specialist Performance

`filetypes/msi` specialist scored *alone* on the same slice (the ensemble usually does better — that's the point of the routing).

| ROC AUC | PR AUC | F1 | Recall @ 3FP/M | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.9828 | 0.9994 | 0.9887 | — | 0.1586 | — |

## Routing

At the L3 deploy level the policy is `filetype_only` over `filetypes/msi`. Full per-level thresholds: [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 1,713 (1,588 mal / 125 ben) |
| Feature spec | 60778 features (`general_shared`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
