# `filetype/pptx`

LightGBM specialist for `pptx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Test partition, n=43 (22 malware / 21 benign).

| ROC AUC [95% CI] | PR AUC [95% CI] | F1 [95% CI] | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|
| 0.6071 | 0.6534 | 0.6769 | - | — |

## Routing

Default-level policy `learned_blend_at_fp_0`. Allowed routes (OR over thresholds): `general`, `filegroups/documents`, `filetypes/pptx`. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=100, num_leaves=48, max_depth=12, min_child_samples=20, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 276 rows (106 mal / 170 ben).
