# `filetype/jpeg`

LightGBM specialist for `jpeg`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1398 (116 malware / 1282 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7571 [0.7210, 0.7925] | 0.2647 [0.2055, 0.3289] | 0.2686 [0.2355, 0.3355] | - | — |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/media`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 10133 rows (765 mal / 9368 ben).
