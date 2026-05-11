# `filetype/unknown`

LightGBM specialist for `unknown`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=2040 (65 malware / 1975 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.2903 [0.2368, 0.3485] | 0.0399 [0.0203, 0.0762] | 0.0642 [0.0631, 0.1306] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filetypes/unknown`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 14053 rows (443 mal / 13610 ben).
