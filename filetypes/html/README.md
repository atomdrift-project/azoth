# `filetype/html`

LightGBM specialist for `hta`, `html`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Ensemble Performance

Routed ensemble (general + filegroup + filetype where applicable) on the `html` slice of the locked test partition: 11,512 malware / 54,350 benign (65,862 rows).

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier |
|---:|---:|---:|---:|---:|
| 0.999718 | 0.999930 | 0.988234 | 97.77% | - |

## Specialist Performance

`filetypes/html` specialist scored alone on the same held-out slice, using its saved thresholds.

| PR AUC | ROC AUC | F1 | Recall @ L25 | Brier | Δ vs EMBER 2024 |
|---:|---:|---:|---:|---:|---:|
| 0.988108 | 0.995254 | 0.930449 | 87.04% | 0.0088 | — |

## Recall by FP level (pool-adjusted)

<img src="recall_curve.svg" alt="html: recall by FP level (pool-adjusted)" height="300" />

Each curve plots recall at the route's pool-adjusted FP level. L0 allows zero observed calibration FPs; positive L allows `1 + (L - 1) * N / 100_000_000` for N benigns. See the [shared level definition](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md). The vertical dashed line marks the L25 deploy operating point.

## Routing

Files matching `html` are scored by `filegroups/documents`, `filegroups/historical_filegroups_documents_frozen`, `filegroups/historical_filetypes_html_frozen`, `filegroups/html_benign_weight_recovery`, `filegroups/html_general_layout_recovery`, `filegroups/html_hnm_recovery`, `filegroups/nightly_filetypes_html_frozen`, `filetypes/html`, `general`. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 391,078 (65,868 mal / 325,210 ben) |
| Feature spec | 19224 features (`accepted_pinned`) |
| n_estimators | 250 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0 / 1 |
| early_stopping_rounds | 25 |
| device | cpu |
