# `filetype/java_class`

LightGBM specialist for `java_class`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=47243 (173 malware / 47070 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.9849 [0.9679, 0.9959] | 0.9254 [0.8819, 0.9622] | 0.9181 [0.8889, 0.9419] | - | — |

## Routing

Default-level policy `joint_or_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/portable`, `filetypes/java_class`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=128, max_depth=12, min_child_samples=100, learning_rate=0.03, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=2.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 319282 rows (1120 mal / 318162 ben).
