# `filetype/python-bytecode`

LightGBM specialist for `python-bytecode`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=1659 (113 malware / 1546 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9983 [0.9965, 0.9998] | 0.9855 [0.9717, 0.9976] | 0.9774 [0.9537, 0.9956] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filetypes/python-bytecode`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=120, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 11686 rows (846 mal / 10840 ben).
