# `filetype/java_class`

LightGBM specialist for `java_class`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=31694 (77 malware / 31617 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9996 [0.9986, 1.0000] | 0.9722 [0.9378, 0.9946] | 0.9682 [0.9383, 0.9935] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 223800 rows (542 mal / 223258 ben).
