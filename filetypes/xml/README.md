# `filetype/xml`

LightGBM specialist for `xml`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=16007 (177 malware / 15830 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.5885 [0.5460, 0.6309] | 0.0221 [0.0163, 0.0342] | 0.0783 [0.0427, 0.1278] | - | — |

## Routing

Default-level policy `no_policy`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=250, num_leaves=96, max_depth=12, min_child_samples=100, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 47621 features, policy `general_shared`. Trained on 111425 rows (1211 mal / 110214 ben).
