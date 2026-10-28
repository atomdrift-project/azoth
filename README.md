# Specialist update — 2026-10-28

Updated 14 specialists. The general and filegroup models, their fallback thresholds, and unrelated filetype policies are preserved from the installed nightly bundle.

Thresholds and policies were fitted on captured development rows; this table reports the locked test partition. General/filegroup scores are preserved from the nightly snapshot. Updated specialists use currently available reports.

| Filetype | Previous L25 recall | New L25 recall | Previous FP | New FP |
| --- | ---: | ---: | ---: | ---: |
| applescript | 40.00% | 60.00% | 0 | 0 |
| cargo.toml | 0.00% | 12.50% | 0 | 2 |
| chm | 0.00% | 0.00% | 0 | 0 |
| crx | 33.01% | 39.87% | 2 | 0 |
| dmg | 0.00% | 0.00% | 0 | 0 |
| dockerfile | 0.00% | 100.00% | 0 | 1 |
| elf | 84.16% | 96.14% | 0 | 1 |
| gem | 88.24% | 88.24% | 3 | 0 |
| java | 7.49% | 46.14% | 3 | 8 |
| json | 45.45% | 45.45% | 0 | 0 |
| markdown | 0.00% | 33.33% | 2 | 0 |
| npm | 25.13% | 72.44% | 0 | 2 |
| rust | 32.73% | 49.09% | 9 | 41 |
| whl | 12.79% | 14.53% | 0 | 0 |

Held back VSIX, XML, makefile, and plist because their candidate decisions were worse on the locked test set. Their installed models and policies are retained.

See [full test evaluation](route_policy_eval_oof.md) and [global policy metrics](global_policy_metrics.md).
The general model documentation remains in [GENERALIST_MODEL.md](GENERALIST_MODEL.md).
