# `filetype/tar`

LightGBM specialist for `tar`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=170 (125 malware / 45 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9812 [0.9618, 0.9986] | 0.9936 [0.9870, 0.9995] | 0.9796 [0.9583, 0.9960] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 1322 rows (986 mal / 336 ben).
