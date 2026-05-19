# `filetype/xml`

LightGBM specialist for `xml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=18209 (288 malware / 17921 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.7451 [0.7178, 0.7715] | 0.1445 [0.1096, 0.1819] | 0.3306 [0.2813, 0.3815] | - | — |

## Routing

Default-level policy `joint_or_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/config`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 125937 rows (1948 mal / 123989 ben).
