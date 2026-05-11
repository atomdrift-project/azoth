# `filetype/text`

LightGBM specialist for `text`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=7632 (133 malware / 7499 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.6790 [0.6144, 0.7367] | 0.2477 [0.1850, 0.3245] | 0.3101 [0.2507, 0.3863] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filetypes/text`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 53535 rows (877 mal / 52658 ben).
