# `filetype/perl`

LightGBM specialist for `perl`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=3791 (25 malware / 3766 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9961 [0.9882, 1.0000] | 0.9565 [0.8793, 1.0000] | 0.9388 [0.8889, 1.0000] | - | — |

## Routing

Default-level policy `or_general_primary`. Allowed routes (OR over thresholds): `general`, `filegroups/scripts`, `filetypes/perl`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 26329 rows (169 mal / 26160 ben).
