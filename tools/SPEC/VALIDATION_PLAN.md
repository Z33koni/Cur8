# Promotion validation plan

Status: specification only. This document defines the minimum deterministic
checks required before a candidate may enter `library/`. It does not implement
the validator and does not authorize edits to `library/`.

## Scope and counting rule

The validator runs against a candidate packet plus the quota manifest and
current promotion ledger. It must distinguish:

- `candidate`: a packet item outside `library/`;
- `promoted`: a librarian-approved record counted in the 1,000-item target;
- `rejected`, `rework`, and `duplicate`: non-counting outcomes.

Only a record with status `promoted`, one unique stable ID, and one primary
period, geography, and family contributes to quota counts. A staged or
approved candidate must never increment the promoted ledger.

The validator reports blocking errors separately from warnings. A candidate
with any blocking error cannot be promoted.

## Minimum record contract

The exact serialization may be YAML or JSON, but the normalized object must
contain these fields:

```text
id
status
primary.period_id
primary.geography_id
primary.family_id
name.canonical
name.aliases[]
name.definition
claims.period
claims.geography
claims.materials[]
uncertainty[]
provenance.sources[]
provenance.images[]
rights.status
rights.evidence[]
review.researcher
review.visual_interpreter
review.librarian
review.history[]
```

Each source requires a stable source ID, URL or archival reference, title or
institution, creator/owner when known, and access date. Each image requires a
stable image ID, source ID, URL or local path, and content hash when the file
is available.

Controlled IDs must come from the manifest: `p1`–`p7`, `g1`–`g11`, and the five
family IDs. Unknown IDs, missing IDs, duplicate keys, null required values,
wrong scalar types, and extra primary assignments are blocking errors.
Aliases, secondary labels, materials, styles, and room contexts may be
many-valued; they do not create additional quota assignments.

## Checks before promotion

### 1. Schema and required values

Blocking checks:

1. Parse the record without duplicate keys or malformed dates.
2. Require the fields in the minimum contract with the declared types.
3. Require exactly one primary period, geography, and family.
4. Require a non-empty canonical name and definition.
5. Require claims to identify their evidence and confidence.
6. Require `id` to be stable, non-empty, and unique in the packet and ledger.
7. Reject forbidden placeholder values such as `TBD`, `unknown`, or empty
   evidence where the field is required. “Unknown” may be retained as an
   explicit uncertainty, but it cannot satisfy a required historical claim.
8. Reject records whose primary IDs do not exist in the manifest.

The validator checks structural validity only. It does not decide whether a
term is historically correct; that remains researcher/librarian work.

### 2. Stable IDs and identity consistency

IDs are immutable after first registration. A correction creates a revision
history entry; it does not silently overwrite the original record.

Blocking checks:

- candidate ID is unique across all packets and the promotion ledger;
- source IDs and image IDs are unique within their required namespace;
- an ID cannot be reused for a different physical object;
- if an ID contains human-readable routing text, that text must agree with the
  normalized primary assignment, or the candidate remains blocked until the
  ID is replaced through an explicit migration;
- revision records point to an existing prior ID and preserve the reason,
  actor, and timestamp.

The six pilot IDs are intentionally a fixture for this rule: `P1-BR-FURN-01`
through `P1-BR-FURN-03` have corrected primary period `p2`, and
`P5-NA-LIGHT-01` through `P5-NA-LIGHT-03` have corrected primary period `p4`.
They must not be counted or renamed silently. The packet may be repaired by
assigning opaque IDs or by recording an explicit ID migration before review.

### 3. Period, geography, and family quota accounting

For the promoted ledger, compute counts from records with status `promoted`
only:

```text
period_count[p]     = count(promoted records where primary.period_id == p)
geography_count[g]  = count(promoted records where primary.geography_id == g)
family_count[f]     = count(promoted records where primary.family_id == f)
cell_count[p,g]     = count(promoted records where primary period/geography match)
```

Blocking arithmetic checks:

1. Every marginal total is `<=` its manifest target.
2. No record contributes more than once to any marginal.
3. `sum(period_count) == sum(geography_count) == sum(family_count) ==
   number_of_promoted_records`.
4. No marginal can exceed 1,000 or its corresponding target.
5. For each applicable period×geography cell, the accepted/promoted count is
   not below its target at a release gate unless the manifest contains the
   documented research exception. A `partial` cell cannot be used as an
   arithmetic excuse for unsupported promotion.
6. If a manifest cell is `not-applicable`, require the stated rationale,
   researcher and librarian decision, and audited redistribution. The
   validator must preserve period and geography marginal totals after
   redistribution.
7. At final release, all period, geography, family, and applicable-cell
   counts equal their targets and the unique promoted ID count is exactly
   1,000.

Manifest self-checks, run before candidate accounting:

```text
sum(period targets)                    = 1,000
sum(geography targets)                 = 1,000
sum(family targets)                    = 1,000
sum(each period×geography row)         = its period target
sum(each period×geography column)      = its geography target
sum(all period×geography cells)        = 1,000
```

The current manifest must pass all of these checks. A validator must fail
closed if the manifest itself does not reconcile.

Period membership uses the manifest's half-open rule: lower bound inclusive,
upper bound exclusive. The snapshot endpoint must be represented
consistently; a record dated after `2026-09-01` cannot enter `p7`, and the
validator must reject an ambiguous endpoint representation rather than
inventing one.

### 4. Provenance and rights

Blocking checks:

- every period, geography, material, and canonical-name claim has at least one
  linked source reference;
- historical claims have an attributable institutional or authoritative
  source where available;
- every image links to its source and has retrieval/access metadata;
- source and image URLs or archival references are syntactically present and
  stable enough to audit;
- rights status is one of `public-domain`, `open-license`,
  `permission-recorded`, `restricted`, or `unknown`;
- `restricted` and `unknown` rights block promotion;
- `public-domain` and `open-license` require the evidence or institutional
  statement supporting that status, including license terms when applicable;
- `permission-recorded` requires the permission record, scope, and expiry or
  “no expiry stated”;
- attribution requirements are stored with the image record;
- missing, contradictory, or source-inferred rights are not treated as clear.

The three Met candidates have a rights-clear fixture state, subject to
preserving the Met Open Access evidence. The three V&A candidates remain
blocked until reuse rights are verified.

### 5. Duplicate and leakage checks

Run checks at three levels:

1. exact image content hash;
2. deterministic perceptual-image match, when image bytes are available;
3. physical-object and source-lineage identity.

An exact hash collision or same physical object represented by multiple views
is a blocking duplicate for promotion as separate items. Related views may be
stored under one record. A perceptual match above the configured threshold is
at least a blocking review flag until a human resolves whether it is the same
object, a reproduction, or a legitimately distinct object. The threshold and
hash algorithm must be recorded in the validation report.

Duplicate checks must include already promoted records and all candidates in
the current packet. Group IDs for one object must be retained so later train,
validation, and test splits cannot separate related views or reproductions.

### 6. Uncertainty and unsupported precision

Every uncertain or inferred value must be explicit, with:

- field or claim affected;
- value or competing values;
- uncertainty kind (`unknown`, `estimated`, `competing`, or
  `low-confidence`);
- rationale/evidence;
- confidence;
- assigned follow-up or resolving reviewer.

Blocking checks:

- no unresolved contradiction may be promoted;
- an estimated date must remain estimated and fit the declared period band;
- an unknown maker, provenance, subtype, or material cannot be silently
  serialized as a precise fact;
- a low-confidence or competing canonical term requires a generic canonical
  label plus librarian approval;
- confidence without rationale is invalid;
- resolved uncertainty must retain its prior history.

The pilot’s “probably Atterbury and Company,” inferred Spitalfields textile
origin, unknown makers, unresolved lamp subtype, and approximate chandelier
date are valid uncertainty fixtures, not grounds for deletion. They block only
if the record upgrades them to unsupported certainty or lacks the required
follow-up and review.

### 7. Status transitions and authority

Allowed status values:

```text
staged
research-needed
annotated
review
approved
promoted
rework
rejected
duplicate
```

Allowed transitions:

```text
staged -> research-needed | annotated | review | rejected
research-needed -> annotated | review | rework | rejected
annotated -> review | research-needed | rework | rejected
review -> approved | rework | rejected | duplicate
approved -> promoted | rework | rejected
promoted -> rework      # correction only; never silent deletion
rework -> research-needed | annotated | review | rejected
```

`duplicate` is terminal unless a reviewer reopens it through an auditable
revision. `rejected` is terminal for the current revision. `promoted` requires
the librarian as approving actor, completed researcher and visual-interpreter
reviews, and a validation report with zero blocking errors.

Blocking transition checks:

- actor is authorized for the transition;
- required evidence and review fields exist for the destination status;
- every transition has timestamp, actor, old status, new status, and reason;
- no transition skips required review gates;
- only `approved -> promoted` can add a record to the promoted ledger;
- a failed validation cannot be marked promoted;
- status history is append-only.

## Deterministic test fixtures

The first test suite should use small in-memory manifests and records plus one
fixture derived from the current packet. Tests must assert stable error codes,
not wording or dictionary iteration order.

### Fixture A: manifest arithmetic

Use the current manifest unchanged. Expected:

```text
period targets total                 1000
geography targets total              1000
family targets total                 1000
period×geography matrix total        1000
all seven row sums                   [60, 90, 115, 145, 180, 210, 200]
all eleven column sums               [130, 110, 95, 90, 85, 75, 55, 100, 65, 145, 50]
```

Mutations:

- change one cell by `+1`: expect `MANIFEST_ROW_TOTAL_MISMATCH` and
  `MANIFEST_COLUMN_TOTAL_MISMATCH`;
- remove one family: expect `MANIFEST_FAMILY_TOTAL_MISMATCH`;
- add an unknown period ID: expect `MANIFEST_UNKNOWN_ASSIGNMENT_ID`;
- mark a cell `not-applicable` without rationale/audit: expect
  `NOT_APPLICABLE_UNDOCUMENTED`.

### Fixture B: six-candidate packet

Load `research-findings/ACQUISITION_2026-09-01_PILOT_001.md` into the normalized
candidate shape. Expected:

- six unique candidate IDs;
- zero promoted contributions;
- three Britain/furniture candidates normalized to `p2/g1/furniture`;
- three North America/lighting candidates normalized to `p4/g10/lighting`;
- all six fail promotion while staged;
- all six fail the encoded-ID consistency check until IDs are made opaque or an
  explicit migration is recorded;
- three fail rights clearance because V&A rights are unresolved;
- all six retain uncertainty records and follow-up actions.

### Fixture C: valid minimal promoted record

Create one synthetic record with an opaque ID, `approved -> promoted` history,
one primary `p4/g10/lighting` assignment, a definition, linked source and
image, public-domain evidence, image hash, uncertainty rationale, all required
reviewers, and no duplicate group collision. Expected: zero blocking errors and
exactly one increment in each relevant marginal and cell.

### Fixture D: duplicate and leakage

Create two records with different IDs and identical image hash, then two
records with different hashes but the same physical-object/source-lineage ID.
Expected: exact-hash and lineage duplicate errors; neither may promote as a
second item. Add two views under one group ID and assert that the group remains
intact for split preparation.

### Fixture E: rights and uncertainty failures

Clone Fixture C while separately setting rights to `unknown`, omitting rights
evidence, replacing an estimated date with a precise unsupported date, and
removing uncertainty rationale. Each mutation must produce a distinct blocking
error and must not alter quota counts.

### Fixture F: status transition matrix

Generate every ordered pair of statuses. Assert that only the allowed
transitions above pass, that `review -> promoted` fails, that a non-librarian
cannot approve or promote, and that `approved -> promoted` increments counts
only once. Replaying the same promotion event must be idempotent and must not
create a second count.

## Required validation report

For each run, emit a deterministic report containing validator version,
manifest version, input packet IDs, counts by status, quota counts and
remaining capacity by period/geography/family/cell, duplicate groups, rights
summary, uncertainty summary, status-transition errors, stable error codes, and
overall `PASS`/`BLOCKED`. Sort IDs and error codes before serialization.

Promotion is permitted only when the report is `PASS`, the record is
`approved`, the librarian approval is present, and all quota updates are
recorded atomically with the promotion event.
