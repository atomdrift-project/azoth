# `filetype/png`

LightGBM specialist for `png`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=13001 (623 malware / 12378 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.5642 [0.5410, 0.5890] | 0.1497 [0.1254, 0.1746] | 0.1780 [0.1407, 0.2149] | - | — |

## Routing

Default-level policy `filetype_only`. Allowed routes (OR over thresholds): `filetypes/png`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=150, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 89183 rows (4377 mal / 84806 ben).
