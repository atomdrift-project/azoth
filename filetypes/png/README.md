# `filetype/png`

LightGBM specialist for `png`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=14995 (657 malware / 14338 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.5981 [0.5787, 0.6153] | 0.1043 [0.0846, 0.1220] | 0.1261 [0.1161, 0.1529] | - | — |

## Routing

Default-level policy `learned_blend_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/media`, `filetypes/png`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 102714 rows (4593 mal / 98121 ben).
