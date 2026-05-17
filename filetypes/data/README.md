# `filetype/data`

LightGBM specialist for `data`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1210 (58 malware / 1152 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9729 [0.9459, 0.9932] | 0.8949 [0.8160, 0.9509] | 0.8738 [0.8160, 0.9275] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filetypes/data`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=300, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 8174 rows (347 mal / 7827 ben).
