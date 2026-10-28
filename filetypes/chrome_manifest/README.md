# `filetype/chrome_manifest`

LightGBM specialist for `chrome-manifest`, `chrome_manifest`, `chromemanifest`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `chrome_manifest` slice of the locked test partition: 12 malware / 152 benign (164 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.716204 | 0.962171 | 0.555556 | 41.67% | - |

## Specialist Performance

`filetypes/chrome_manifest` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.723074 | 0.964364 | 0.555556 | 41.67% | 0.0467 | — |

## Recall by FP level (per 100M benigns)

<img src="recall_curve.svg" alt="chrome_manifest: recall by FP level (per 100M benigns)" height="300" />

Each curve plots recall at the per-100M-benign FP target for the route. The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `chrome_manifest` are scored by `filetypes/chrome_manifest`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 974 (76 mal / 898 ben) |
| Feature spec | 1573 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 50 |
| device | auto |
