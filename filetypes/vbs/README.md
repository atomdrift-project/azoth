# `filetype/vbs`

LightGBM specialist for `vbs`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=506 (89 malware / 417 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9969 [0.9943, 0.9991] | 0.9854 [0.9733, 0.9958] | 0.9392 [0.9186, 0.9775] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 3483 rows (670 mal / 2813 ben).
