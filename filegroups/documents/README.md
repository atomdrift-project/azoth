# `filegroup/documents`

LightGBM specialist for `doc`, `docm`, `docx`, `dotx`, `hta`, `html`, `msg`, `msi`, `ole`, `ole_doc`, `oledoc`, `ooxml`, `pdf`, `potm`, `potx`, `ppam`, `ppsm`, `ppt`, `pptm`, `pptx`, `rtf`, `sldm`, `sldx`, `xlam`, `xls`, `xlsb`, `xlsm`, `xlsx`, `xltm`, `xltx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

## Performance

Training-time benchmark only (no test-partition rows for `documents`). ROC 0.974721, PR 0.971967, F1 0.9089 on 117,210 rows (54,177 mal / 63,033 ben).

## Routing

Files matching `documents` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 627,979 (252,226 mal / 375,753 ben) |
| Feature spec | 16511 features (`route_specific`) |
| n_estimators | 300 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 150 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 2.0 |
| early_stopping_rounds | 30 |
| device | auto |
