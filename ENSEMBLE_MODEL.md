# Azoth — Routed Ensemble

## How a file is scored

1. `cleave` identifies the file's format — `elf`, `pe`, `pdf`, `javascript`, and so on.
2. `route_policies.json` answers: given that format and a severity level L0..L20, which routes are allowed, and at what calibrated thresholds?
3. Each allowed route scores the file with its own model and feature spec.
4. If any allowed route's score crosses its threshold, the file is flagged at that severity.

A route is one of: the general model, a filegroup specialist (`filegroups/<name>`), or a filetype specialist (`filetypes/<name>`). Specialists are trained only on files of their domain; the general model is trained on everything.

## Selection and reporting

Policy search selects route combinations and thresholds on dev raw scores from the exact exported ensembles. The locked test partition is used only to report saved decisions, without fitting a new calibrator, threshold, or combiner. Models, feature specs and policies stay fixed during publication.

## Routing policies

Per filetype per level, `azoth_route_policy_search.py` picks one of these policy forms by recall at the FP/M target, with F1 and fp-count tiebreaks. The chosen policy and its calibrated thresholds are written to `route_policies.json` and read by Scan at scan time:

- `joint_or_at_fp_N` — OR-rule across the allowed routes, with per-route thresholds calibrated to a joint FP/M target of N per million. The common case.
- `learned_blend_at_fp_N` — a logit blend `σ(b + Σ wᵢ · logit(pᵢ))` over raw route probabilities, thresholded to hit the FP/M target. Wins when route scores are complementary in a way a simple OR misses.
- `filetype_only` / `filetype_only_at_fp_N` — the specialist fires alone.
- `general_only`, `group_only`, `or_general_primary`, `group_primary_with_escape` — the single-route or single-primary variants.
- `calibrate_inherited` — the level inherits its threshold from a stricter level (no fresh calibration was warranted).
- `no_policy` — no configuration meets the FP/M target at this level; the route does not fire at this severity.

## Severity levels (L0..L20)

L0..L20 are measured strictness grades, not optimization targets. L0 is the 0-FP point (loosest threshold flagging no calibration benign). For each higher route level Lk, the threshold is the loosest score admitting at most the level's FP budget plus one benign (the +1 slack) — a real measured ceiling, never an extrapolation, so it can't overshoot on live traffic. Where benign volume can't separate adjacent levels, they share one ceiling (a flat run); finer steps emerge only as benign volume grows.

Litmus reads the per-level thresholds from `route_policies.json` and assigns severity per file.

Default deploy level: L25 (0.25 FP/M) (Scan loads the hostile threshold at that level; any suspicious band is derived consumer-side). Per-route thresholds and observed FP/100M live in [route_policies.md](route_policies.md) and each `filetypes/<name>/README.md`.
