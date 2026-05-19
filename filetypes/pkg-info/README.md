# `filetype/pkg-info`

LightGBM specialist for `pkg-info`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1390 (1276 malware / 114 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9994 [0.9987, 0.9999] | 0.9999 [0.9999, 1.0000] | 0.9973 [0.9953, 0.9992] | - | — |

## Routing

Default-level policy `filetype_only_at_fp_0`. Allowed routes (OR over thresholds): `filetypes/pkg-info`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 10264 rows (9358 mal / 906 ben).
