# `filetype/jpeg`

LightGBM specialist for `jpeg`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1444 (125 malware / 1319 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7714 [0.7329, 0.8047] | 0.3336 [0.2623, 0.4101] | 0.3212 [0.2666, 0.4159] | - | — |

## Routing

Default-level policy `learned_blend_at_fp_1`. Allowed routes (OR over thresholds): `general`, `filegroups/media`, `filetypes/jpeg`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 10467 rows (844 mal / 9623 ben).
