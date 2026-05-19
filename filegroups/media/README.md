# `filegroup/media`

LightGBM specialist for `bmp`, `gif`, `jpeg`, `jpg`, `mp3`, `mp4`, `png`, `svg`, `webp`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `media`). ROC 0.9871, PR 0.8759, F1 0.8048 on 16364 rows (782 mal / 15582 ben).

## Routing

Default-level policy `—`. Allowed routes (OR over thresholds): none. Per-level severity thresholds in `route_policies.md` at the bundle root.

## Training

LightGBM binary classifier: estimators=400, num_leaves=96, max_depth=12, min_child_samples=50, learning_rate=0.05, subsample=0.8, colsample=0.8, reg_alpha=0.0, reg_lambda=1.0, early_stop=25, device=auto. Feature spec: general-shared, 60358 features, policy `general_shared`. Trained on 113181 rows (5437 mal / 107744 ben).
