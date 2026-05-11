# `filetype/gz`

LightGBM specialist for `gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=5398 (23 malware / 5375 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8412 [0.7881, 0.8869] | 0.3963 [0.1808, 0.5688] | 0.5625 [0.2963, 0.7222] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/archive`, `filetypes/gz`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 37764 rows (193 mal / 37571 ben).
