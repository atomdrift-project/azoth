# `filegroup/documents`

LightGBM specialist for `doc`, `docm`, `docx`, `dotx`, `hta`, `html`, `msg`, `msi`, `ole`, `ole_doc`, `oledoc`, `ooxml`, `pdf`, `potm`, `potx`, `ppam`, `ppsm`, `ppt`, `pptm`, `pptx`, `rtf`, `sldm`, `sldx`, `xlam`, `xls`, `xlsb`, `xlsm`, `xlsx`, `xltm`, `xltx`. Member of the Azoth routed ensemble; bundle root: [../..](../..).

Level labels use the [shared pool-adjusted FP allowance](https://github.com/atomdrift-project/collimator/blob/main/LEVELS.md): L0 allows zero observed calibration FPs; L1 allows one; L25 adds an estimated 24 FP/100M beyond the initial FP.

## Performance

Training-time benchmark only (no test-partition rows for `documents`). ROC 0.999382, PR 0.999194, F1 0.9928 on 117,467 rows (54,328 mal / 63,139 ben).

## Routing

Files matching `documents` are scored by none. The ensemble's decisions apply the saved routing policy, including every level at or below the requested level. Ranking metrics use the signed distance from that policy's decision boundary. See [`route_policies.md`](../../route_policies.md).

## Training

| Parameter | Value |
|---|---:|
| Algorithm | LightGBM binary classifier |
| Train rows | 703,931 (327,471 mal / 376,460 ben) |
| Feature spec | 8479 features (`route_specific`) |
| n_estimators | 400 |
| num_leaves | 96 |
| max_depth | 12 |
| min_child_samples | 100 |
| learning_rate | 0.05 |
| subsample / colsample | 0.8 / 0.8 |
| reg_alpha / reg_lambda | 0.0 / 1.0 |
| early_stopping_rounds | 25 |
| device | auto |
