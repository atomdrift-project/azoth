# `filetype/data`

LightGBM specialist for `data`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1215 (58 malware / 1157 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9705 [0.9438, 0.9899] | 0.8811 [0.7978, 0.9407] | 0.8762 [0.8190, 0.9358] | - | — |

## Routing

Default-level policy `filetype_only_at_fp_0`. Allowed routes (OR over thresholds): `filetypes/data`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=300, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 8214 rows (347 mal / 7867 ben).
