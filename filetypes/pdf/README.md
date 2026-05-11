# `filetype/pdf`

LightGBM specialist for `pdf`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=358 (9 malware / 349 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9335 [0.8939, 0.9698] | 0.2365 [0.1568, 0.4079] | 0.4375 [0.3028, 0.6429] | - | ROC -0.0577 / PR -0.7568 |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=40, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 2434 rows (85 mal / 2349 ben).
