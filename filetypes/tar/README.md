# `filetype/tar`

LightGBM specialist for `tar`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=157 (111 malware / 46 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9845 [0.9702, 0.9982] | 0.9935 [0.9872, 0.9993] | 0.9817 [0.9626, 0.9955] | - | — |

## Routing

Default-level policy `group_only`. Allowed routes (OR over thresholds): `filegroups/archive`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 1245 rows (928 mal / 317 ben).
