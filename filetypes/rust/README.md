# `filetype/rust`

LightGBM specialist for `rust`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=9702 (163 malware / 9539 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7397 [0.6989, 0.7831] | 0.1193 [0.0777, 0.1740] | 0.1826 [0.1361, 0.2613] | - | — |

## Routing

Default-level policy `general_only`. Allowed routes (OR over thresholds): `general`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=200, num_leaves=128, max_depth=14, min_child_samples=50, learning_rate=0.04, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 67947 rows (1116 mal / 66831 ben).
