# `filetype/ruby`

LightGBM specialist for `ruby`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=2824 (7 malware / 2817 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9993 [0.9977, 1.0000] | 0.8741 [0.6540, 1.0000] | 0.8333 [0.6000, 1.0000] | - | — |

## Routing

Default-level policy `general_only`. Allowed routes (OR over thresholds): `general`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 20429 rows (65 mal / 20364 ben).
