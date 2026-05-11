# `filetype/php`

LightGBM specialist for `php`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=6572 (453 malware / 6119 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9937 [0.9914, 0.9955] | 0.9499 [0.9358, 0.9614] | 0.8964 [0.8744, 0.9171] | - | — |

## Routing

Default-level policy `general_only`. Allowed routes (OR over thresholds): `general`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 45971 rows (2921 mal / 43050 ben).
