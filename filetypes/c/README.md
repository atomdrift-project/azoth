# `filetype/c`

LightGBM specialist for `c`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=63941 (1756 malware / 62185 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8913 [0.8837, 0.8995] | 0.4354 [0.4174, 0.4535] | 0.4319 [0.4168, 0.4491] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=130, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 445407 rows (12470 mal / 432937 ben).
