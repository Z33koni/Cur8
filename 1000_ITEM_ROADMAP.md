# 1,000-item production roadmap

Status: negotiated with all five specialist agents on 2026-09-01.

## Target and counting rule

The target is **exactly 1,000 librarian-promoted records**. A candidate,
annotated image, or rework item does not count. An item counts once, and only
once, after final QA and promotion into `library/`.

Every promoted record has exactly one primary:

- period band;
- geography bucket;
- object family.

Secondary influences, aliases, materials, styles, and room contexts may be
many-valued but never inflate quota counts.

## Exact marginal quotas

### Period: 1,000 total

| Period band | Quota |
|---|---:|
| 1450–<1600 | 60 |
| 1600–<1750 | 90 |
| 1750–<1830 | 115 |
| 1830–<1900 | 145 |
| 1900–<1945 | 180 |
| 1945–<1980 | 210 |
| 1980–2026-09-01 snapshot | 200 |
| **Total** | **1,000** |

### Geography: 1,000 total

| Geography bucket | Quota |
|---|---:|
| Britain | 130 |
| France | 110 |
| Italy | 95 |
| German-speaking Europe | 90 |
| Netherlands/Scandinavia | 85 |
| Iberia/Mediterranean | 75 |
| Ottoman/Islamic traditions | 55 |
| East Asia | 100 |
| South Asia | 65 |
| North America | 145 |
| Latin America | 50 |
| **Total** | **1,000** |

### Object family: 1,000 total

| Family | Quota |
|---|---:|
| Furniture, including credenzas | 300 |
| Lighting | 170 |
| Plumbing: basins, faucets, bathtubs, vanities | 220 |
| Surface treatments: paint, wallpaper, tile, stone, paneling | 180 |
| Decorative objects: curios, mirrors, ceramics, clocks, hardware | 130 |
| **Total** | **1,000** |

These are marginal quotas. They are not permission to fill a weakly supported
cell merely to satisfy arithmetic.

## Time × space coherence

The quota manifest contains all 77 period × geography cells. Before collection,
the researcher and librarian mark each cell `applicable`, `partial`, or
`not-applicable`, with a written reason for every `not-applicable` decision.

For every applicable period × geography cell, the final library must contain
at least two accepted records. A deterministic largest-remainder allocator
then assigns each cell a target while reconciling all period and geography
marginals exactly. Family assignments are made inside those cells until all
three marginal ledgers equal 1,000.

The three-way manifest must preserve, for every cell:

- target, accepted, remaining, and status;
- applicable/not-applicable decision and rationale;
- primary family allocation;
- source/image coverage;
- unresolved terminology and evidence gaps.

If a three-way family cell is historically impossible or lacks defensible
evidence, mark that family cell `not-applicable` and redistribute its quota to
the same period/geography cell or the nearest documented gap cell. Do not
change the period or geography marginals silently.

## Production phases

| Phase | New promoted items | Cumulative | Purpose |
|---|---:|---:|---|
| Pilot | 30 | 30 | Exercise the existing workflow |
| Coverage expansion | 270 | 300 | Reach every period, geography, and family with measured gaps |
| Depth expansion | 700 | 1,000 | Add variants, materials, components, and modern-home examples |

Release checkpoints occur at 100, 250, 500, 750, and 1,000 promoted items.
After each checkpoint, freeze the ledger, audit gaps, and redirect the next
batch toward underrepresented or weakly evidenced cells.

## Batch and throughput plan

- 40 release batches × 25 promoted items.
- Acquire approximately 30 complete candidate packets per batch, or 1,200
  candidates total, providing a 20% reserve over the 1,000-item target.
- If acceptance falls below 83.3%, acquire a targeted replacement batch; never
  relax a gate to preserve throughput.
- Keep a rolling two-batch queue so visual interpretation and librarian review
  do not idle while acquisition researches the next batch.
- Run a full coverage, rights, duplicate, and annotation-drift audit after
  every 100 promoted items.

## Minimum evidence per promoted item

- Proper name, aliases, and a dictionary or institutional definition.
- Sources mapped to the name, period, geography, and material/form claims.
- At least two attributable sources where available, including an authoritative
  historical or institutional source for historical claims.
- Stable image/source IDs, source URLs or archival references, access date,
  creator/institution, attribution, and rights status.
- At least four usable image views when the subject permits: context/full view,
  primary elevation, construction/side view, and diagnostic detail. Wall
  treatments may use appropriate single-view evidence.
- Structured shape, material, construction, aesthetic, and room-context
  observations.
- Confidence and uncertainty for terminology, period, geography, and material.
- Librarian approval, reviewer, timestamp, and quota-cell assignment.

## Quality and leakage controls

Deduplicate at three levels: exact file hash, perceptual image similarity, and
physical-object/source lineage. All views or reproductions of one object share
one split group. Engineer creates deterministic 70/15/15 train/validation/test
manifests only after grouping, never splitting individual images.

Visual QA runs every batch; a 10% random sample of accepted items receives
double review. Escalate low-confidence or conflicting visual interpretations
to researcher and librarian. Keep rejected and rework records outside
`library/` with coded reasons and revision history.

## Stop/go gates

Stop promotion if any of these fail:

1. accepted count would exceed 1,000;
2. any mandatory schema, provenance, rights, or definition field is missing;
3. duplicate object or cross-split lineage leakage is detected;
4. an applicable period × geography cell is below its target without a
   documented research exception;
5. a promoted label has unresolved contradiction or unsupported precision.

The roadmap is complete only when the ledger reports exactly 1,000 promoted
IDs, all three marginal ledgers reconcile to 1,000, every applicable time ×
space cell meets its minimum, and the final audit/release notes are complete.
