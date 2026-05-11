# `filetype/batch`

LightGBM specialist for `batch`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=307 (63 malware / 244 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9908 [0.9810, 0.9967] | 0.9680 [0.9380, 0.9884] | 0.9134 [0.8615, 0.9613] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 2301 rows (376 mal / 1925 ben).
