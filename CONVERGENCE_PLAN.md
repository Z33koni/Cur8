# Renov8 convergence plan

Status: negotiated and ratified by acquisition, engineer, librarian,
researcher, and visual-interpreter on 2026-09-01.

Test-run note: the v2 communications protocol, specialized model routing, and
tool specifications were successful coordination mechanisms. Implementation
work is opt-in and should be driven by a demonstrated blocker or explicit
user request; specification and evidence artifacts remain valuable when code
is deferred.

The period × geography grid is the primary coverage-planning abstraction.
Family allocations are made within cells so spatial and temporal coverage
remain coherent while the global family quotas reconcile.

## Outcome

Build a provenance-first, image-grounded catalog in which every accepted
record has a defensible proper name, definition, visible design features,
material information, period/geography claims, and reusable image metadata.
Only librarian-approved records enter `library/`.

The scaled production target and its exact time/space quotas are defined in
[`1000_ITEM_ROADMAP.md`](1000_ITEM_ROADMAP.md). The 30-record pilot below is
the first gate toward that target, not the final scope.

## Pilot scope

The first release is a **30-record stratified pilot**, not a full-factorial
claim:

- 5 object families, 6 records each:
  furniture (including credenzas), lighting, plumbing, surface treatments,
  and decorative objects;
- 3 broad periods, 10 records each:
  1450–1750, 1750–1900, and 1900–present;
- 3 geography buckets, 10 records each:
  Britain, France, and North America;
- at least one record in every selected period × geography cell;
- remaining category/cell gaps are recorded explicitly and drive the next
  research queue.

This pilot tests the workflow across the full time span without implying that
it represents every region, style, or category combination.

## Staged execution

### 1. Define the matrix and data contract

Researcher and librarian maintain
`research-targets/OBJECTIVE_FURNISHINGS.md`, partitioned by
object/component, period, and geography. Each matrix cell is
`unstarted`, `partial`, or `researched`.

The contract must separate:

- canonical name, aliases, candidate names, and dictionary definition;
- direct visual observation versus historical inference;
- shape, construction, material, finish, and aesthetic features;
- period and geography claims with independent confidence values;
- source identifiers, URLs, retrieval date, attribution, and rights status;
- image ID/path, hash when available, and annotation status;
- a saved local image asset and relative path for every accepted training image,
  not only a source URL;
- uncertainties, disputes, reject history, and approval status.

Engineer reviews the contract for machine-validity but does not decide
historical labels. A tool specification may be delivered without immediate
implementation when the current test does not require executable tooling.

### 2. Build the pre-collection gate

Engineer creates a minimal deterministic validator and fixture records. Before
images are collected it checks stable IDs, required fields, controlled
vocabularies, provenance structure, rights fields, confidence/uncertainty
fields, record status, and schema-level duplicate IDs/filenames.

It must not make semantic historical judgments. Image readability, perceptual
deduplication, split leakage, and coverage reporting are added once pilot
records exist.

### 3. Research and acquire evidence packets

Researcher supplies ranked targets, terminology, period/geography questions,
confusable terms, and authoritative source targets. Acquisition converts these
into source and image packets, preserving URLs, access dates, creator,
license/rights evidence, retrieval context, and explicit asset-materialization
status.

No candidate is collected solely because it is visually attractive.

### 4. Interpret candidate images

Visual-interpreter receives candidate images and records:

- stable image/source identity and provenance;
- visible object/component, shape, construction, material appearance, finish,
  ornament, and spatial context;
- image quality, crop, occlusion, restoration, reproduction, and AI-generation
  risk flags;
- generic descriptive label plus candidate proper names, evidence, and
  confidence;
- result: `accept`, `accept-with-ambiguity`, `research-needed`, or `reject`.

Observation is never silently upgraded to historical fact. Ambiguous items
retain generic labels, competing names, evidence, and an assigned follow-up.

### 5. Reconcile and promote

Librarian alone decides canonical terminology, relationships, uncertainty,
acceptance, and promotion into `library/`. Rejected or contested material
remains outside `library/` with a reason and revision history.

Acceptance gates:

1. identity and proper-name evidence;
2. definition and synonym reconciliation;
3. visual subject identity and annotation;
4. period and geography provenance;
5. material/finish claim discipline;
6. image provenance, quality, rights, deduplication, and existence of the
   saved local asset;
7. machine-readable stable metadata;
8. no unresolved contradiction with accepted records.

`accept-with-ambiguity` may enter only with a generic canonical label and
explicit librarian approval; an unsupported specific term may not become
canonical.

### 6. Validate and release the pilot

Engineer validates librarian-approved candidates, generates a coverage and
reject report, hashes images, detects near-duplicates, and checks that related
views or source copies cannot leak across future train/validation/test splits.

The pilot release is complete only when it has zero blocking validator errors,
traceable provenance for every accepted record, documented coverage gaps, and
release notes listing additions, corrections, contested items, and known
limitations.

### 7. Expand by measured gaps

The next queue is chosen from missing period × geography × family cells,
high-value modern-home objects, repeated reject reasons, and unresolved proper
terms. Scale acquisition only after the 30-record pilot passes all gates.
Advanced split/export/report tooling follows the stabilized contract.

## Ownership and handoffs

- **Researcher:** target matrix, historical terminology, period/geography
  research, unresolved questions; writes `research-targets/` and findings.
- **Acquisition:** source/image discovery, retrieval, rights, and provenance;
  writes research packets outside `library/`.
- **Visual-interpreter:** observable image features and ambiguity flags; never
  independently asserts final historical identity.
- **Engineer:** schema, validators, manifests, hashes, deduplication, splits,
  reports, and tests; does not curate historical facts.
- **Librarian:** sole writer/approver of `library/`; reconciles names,
  evidence, uncertainty, and release decisions.

Every handoff names a stable record or candidate ID and includes claims,
evidence references, confidence, open disputes, and the requested next action.

## Reject taxonomy

Use one or more of: `source`, `terminology`, `visual ambiguity`,
`historical uncertainty`, `rights`, `schema`, `duplicate`, or `insufficient
coverage`. A reject must state the distinguishing missing evidence so it can
be repaired rather than blindly resubmitted.

## Convergence controls

- Keep all raw findings and drafts outside `library/`.
- Preserve uncertainty; never infer unsupported precision.
- Review decisions through the append-only `.comms/` protocol.
- Re-evaluate channels after 15 minutes and 1 hour on a live run.
- Compact only resolved communication threads; preserve unresolved IDs.
- Do not broaden the matrix or pilot size until the current release passes its
  gates.
