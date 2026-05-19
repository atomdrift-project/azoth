# `filetype/batch`

LightGBM specialist for `batch`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=21520 (21095 malware / 425 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9996 [0.9994, 0.9997] | 1.0000 [1.0000, 1.0000] | 0.9988 [0.9986, 0.9991] | - | — |

## Routing

Default-level policy `learned_blend_at_fp_3`. Allowed routes (OR over thresholds): `general`, `filegroups/scripts`, `filetypes/batch`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=300, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 150148 rows (146980 mal / 3168 ben).
