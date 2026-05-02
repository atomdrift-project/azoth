# Azoth Ensemble Design

Azoth is a routed ensemble for malware detection. It uses one general model and,
when available, one filegroup model and one filetype model. A scan may consult up
to three models, but the false-positive budget is owned by the routed decision,
not by any model in isolation.

The purpose is simple: let broad models handle the common case, let specialist
models recover signal that broad models average away, and still make a precise
claim such as "hostile level 5 is no more than 5 false positives per million
good files" over the whole calibration corpus.

## Repository Layout

Deployment artifacts live under one model root:

```text
azoth/
  config.json
  general/
    model.txt
    feature_spec.json
  filegroups/
    scripts/
      model.txt
      feature_spec.json
    native/
      model.txt
      feature_spec.json
    archive/
      model.txt
      feature_spec.json
    portable/
      model.txt
      feature_spec.json
  filetypes/
    elf/
      model.txt
      feature_spec.json
    pe/
      model.txt
      feature_spec.json
```

`config.json` is the contract between training and litmus. It lists the deployed
models, the filetype-to-filegroup map, and the routed thresholds for hostile and
suspicious decisions.

`general/` is required. If it is absent, corrupt, or incompatible with the
running litmus binary, startup fails. Specialists are optional unless
`config.json` marks a route as required.

The directory names are deployment names. They should be short and stable:

- `scripts`: JavaScript, Python, shell, PowerShell, PHP, Perl, Ruby, batch.
- `native`: PE, ELF, Mach-O.
- `portable`: bytecode or runtime-carried binaries such as JAR, Java class, PYC.
- `archive`: ZIP, tar, tar.gz, ZST, package archives.
- `documents`: PDF, Office, RTF, HTML when treated as document content.
- `source`: C, Go, Java source, Rust, C#, and similar source files.
- `config`: JSON, XML, YAML, TOML, INI, plist.
- `media`: image, audio, and video formats.

Names are not taxonomy. They are routing handles. If the filetype classifier
changes, the config changes with it.

## Feature Specs

The deployed bundle uses one extraction shape.

The simplest valid bundle points every route at `general/feature_spec.json`.
Specialist models are trained on the general feature space and may simply ignore
columns they do not split on. This lets litmus extract the report once and score
several LightGBM boosters against the same vector.

A bundle may use a specialist `feature_spec.json` only if it is a strict subset
of the general spec:

- same model ABI version
- every specialist feature name appears in the general spec
- identical extraction semantics for shared feature names
- no specialist-only feature groups

litmus must refuse to load a specialist that violates this rule. It should not
try to extract the same report three different ways during normal scanning.
Repeated extraction is slower and creates more chances for silent mismatch.

ABI mismatch policy:

- `general/` ABI mismatch: fatal; refuse to start
- specialist ABI mismatch: warn, drop that specialist, continue

Dropping a specialist changes the route. litmus must then use the remaining
configured thresholds only if `config.json` contains a fallback for that degraded
route. Otherwise the route is not valid for deployment.

## Runtime Decision

For a file with type `T` and group `G`, litmus loads the applicable route:

```text
general
filegroups/G      if present
filetypes/T       if present
```

If `T` is not in the filetype-to-filegroup map, the route is `general` only.
Unknown filetypes are ordinary inputs, not errors.

Each model returns a malware probability. A policy level supplies one threshold
per applicable model. The decision is an OR over threshold crossings:

```text
hostile =
    general_score >= general_hostile_threshold
 || group_score   >= group_hostile_threshold
 || type_score    >= type_hostile_threshold

suspicious =
    general_score >= general_suspicious_threshold
 || group_score   >= group_suspicious_threshold
 || type_score    >= type_suspicious_threshold
```

This looks like three independent detectors. It is not calibrated that way. The
thresholds are selected together, against the combined OR decision.

## False-Positive Ownership

The false-positive budget belongs to the route as a whole.

If level 5 means 5 hostile false positives per million good files, then this is
the measured object:

```text
FP(general OR group OR type) <= 5 per million good files
```

It is wrong to give each model its own 5 FP/M budget. It is also wrong to say
"filetype gets 5, group gets 4, general gets 3" unless the combined OR result is
then measured and shown to stay under 5. False positives do not have to overlap.
Independent budgets add risk faster than they add detection.

Training may use a budget allocation as a search hint. Deployment must use
thresholds proven against the combined routed decision.

## Calibration Corpus

Calibration uses the full labeled corpus at a pinned snapshot:

- good and bad labels included
- skipped rows excluded
- low-score rows included in the false-positive denominator
- deterministic train/test partition by canonical content hash

Training may focus on score-filtered rows. Calibration must measure the world
litmus will be judged against.

The pinned snapshot id is recorded in `config.json`. New database inserts do not
change an already calibrated model.

## Score Table

Calibration produces a persisted score table. It is not a temporary detail.

The key is:

```text
(snapshot_id, model_set_hash)
```

The table stores one row per calibration sample:

```text
sample_id
label
filetype
filegroup
general_score
group_score, if available
type_score, if available
```

The table is the artifact used by threshold search, promotion experiments, and
policy changes. Re-running threshold search with a new severity policy should be
seconds, not a full corpus rescore. Adding a candidate specialist should append
one score column and rerun search.

`config.json` records:

- calibration snapshot id
- score-table hash
- model-set hash
- search method and parameters
- generated timestamp

These fields make a deployed bundle reproducible from artifacts.

## Specialist Eligibility

A specialist may be trained when it has at least:

```text
50 bad training samples
50 good training samples
```

A specialist may be deployed only when it passes a stronger gate:

- enough held-out good samples to measure its tail behavior, or enough full-corpus
  calibration coverage through routed evaluation
- no regression in routed hostile recall at the configured false-positive budget
- no increase in routed false positives beyond budget
- stable feature extraction and Rust parity for its feature spec

The 50/50 rule is a training gate, not a deployment guarantee.

The same rule applies to filegroups and filetypes. A weak group model is worse
than no group model, because it consumes false-positive budget and adds latency.

## Threshold Search

For each candidate model set, the trainer builds a score table:

```text
sample_id
label
filetype
filegroup
general_score
group_score, if available
type_score, if available
```

For each level and severity, it searches thresholds that maximize recall subject
to the routed false-positive budget:

```text
maximize TP(general OR group OR type)
subject to FP(general OR group OR type) <= budget
```

The first implementation uses coordinate descent over the threshold tuple:

```text
t = best_general_only_threshold()
repeat:
    improved = false
    for coordinate in [general, group, type]:
        for candidate in sorted_cut_points(coordinate):
            t2 = t with coordinate = candidate
            if FP(route(t2)) <= budget and TP(route(t2)) > TP(route(t)):
                t = t2
                improved = true
    until !improved
return t
```

The starting point is general-only because it is always available and gives a
valid baseline. Coordinate descent then lets specialists either loosen their own
thresholds or force a stricter general threshold when that improves the combined
route.

The config records the search method, candidate pruning rules, and stopping
condition. Dynamic programming over sorted cut points is a possible later
optimization. The objective does not change.

## Severity Policy

Current guidance:

```text
hostile FP/M at level L     = L
suspicious FP/M at level L  = (L + 1) * 8
default level               = 5
```

Hostile is the primary policy. Suspicious is useful, but it must not force a
hostile regression.

When a tradeoff exists, choose the configuration with better hostile recall at
the same hostile false-positive budget. Suspicious should then be calibrated
within its own budget using the chosen route.

## Model Promotion

Every trained specialist is experimental until routed calibration proves it
helps. Promotion is based on the ensemble, not the standalone model.

A candidate specialist is promoted if:

- the routed ensemble has higher hostile recall at one or more deployment levels
- total routed false positives remain within budget
- the improvement is not explained by a tiny denominator artifact
- latency and memory cost are acceptable for production scanning

A candidate is rejected or left experimental if:

- it only improves broad metrics such as AUC while hurting strict FP recall
- it spends false-positive budget on cases the general model already catches
- it has too little benign coverage to estimate tail behavior
- it introduces feature compatibility risk

Candidate specialists may run in shadow mode. In shadow mode litmus loads the
model and logs scores, but the route ignores those scores when making a
decision. Shadow mode is for measuring routed value and latency before spending
false-positive budget in production.

## Litmus Evaluation Algorithm

At startup:

1. Read `azoth/config.json`.
2. Load `general`.
3. Load deployed filegroup and filetype models listed in the config.
4. Validate ABI versions and feature-spec subset rules.
5. Drop optional specialists that fail validation.
6. Build routing maps from filetype to group and from route to thresholds.

At scan time:

1. Extract the general feature vector once.
2. Score `general`.
3. Score the filegroup model if present.
4. Score the filetype model if present.
5. Apply the configured OR thresholds for the requested policy level.
6. Return the highest severity triggered.

If a specialist is missing, the route degrades to the models that exist. Missing
specialists are not errors unless `config.json` says they are required.

## Latency

The default route scores one model. Common specialist routes score two or three.
This is acceptable only if feature extraction and model inference remain cheap.

The implementation extracts once against the general feature spec. Specialists
must use that vector directly or a validated subset view. There is no routine
multi-spec extraction path in v1.

Deployment can cap specialists by value:

- always load `general`
- load high-value groups
- load filetypes that passed promotion
- leave the rest to general routing

## Research Questions

The first useful experiments are:

1. Does routed calibration beat the general model at hostile L0, L5, and L9?
2. Which specialists consume false-positive budget without recovering unique
   malware?
3. Are filegroup models useful after filetype models exist?
4. Are some filetypes better served by group models because their own denominators
   are too small?
5. How much latency does the third model add in litmus?
6. Is OR the best routing structure, or do strong specialists earn the right to
   acquit general-model hits inside their domain?

The answer that matters is not whether a specialist has better AUC. The answer
is whether the routed ensemble catches more malware at the same measured
false-positive budget.

## Non-Goals

Azoth does not try to make each specialist independently deployable. Specialists
are parts of a calibrated route.

Azoth does not use private source or provenance fields. The design must be
runnable by anyone with labels, filetype, and cleave output.

Azoth does not promise that every filetype gets a model. Filetypes earn a model
by data volume and routed value.

Azoth v1 does not let specialists downgrade general-model hits. That belongs in
research until a calibrated route shows it improves detection at the same
false-positive budget.
