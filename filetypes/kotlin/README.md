# `filetype/kotlin`

LightGBM specialist for `kotlin`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=5000 (131 malware / 4869 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9602 [0.9345, 0.9833] | 0.8736 [0.8217, 0.9200] | 0.8559 [0.8063, 0.9009] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/kotlin`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 34823 rows (878 mal / 33945 ben).
