# `filetype/gz`

LightGBM specialist for `gz`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=5745 (156 malware / 5589 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.8117 [0.7717, 0.8528] | 0.6895 [0.6154, 0.7521] | 0.8030 [0.7519, 0.8529] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/archive`, `filetypes/gz`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 56209 features, policy `general_shared`. Trained on 40425 rows (1093 mal / 39332 ben).
