# Renov8 agent-collection test retrospective

Date: 2026-09-01

## What worked

The v2 append-only pairwise comms worked well:

- one channel per unordered agent pair;
- terse TSV-KV frames;
- explicit `REQ`, `RESP`, and `ACK` states;
- stable record IDs and artifact references;
- compact `.context/` checkpoints;
- visible uncertainty and blockers.

Keep this protocol as the default coordination surface.

The role-specific model split also worked well:

- acquisition owner plus bounded Qwen preprocessing;
- Qwen Coder for engineering/tool review;
- Sol for final librarian curation;
- Luna for research and acquisition judgment;
- Qwen-VL before deeper visual review.

The important properties were explicit ownership, bounded delegation, and
actual provider/model evidence.

The generated `tools/SPEC/` documents were valuable design artifacts. They
clarified contracts, inputs, outputs, gates, and fixtures even when executable
implementation was not needed.

### Spatial and temporal grid

The period × geography grid was especially effective. It made coverage gaps
visible, gave acquisition concrete targets, and allowed family allocations to
be made inside each cell without losing the global furniture/lighting/plumbing/
surface/decorative totals. Keep this grid as the primary planning abstraction,
not merely as a reporting view.

## What did not work

The test exposed an image-materialization gap: acquisition and promotion
preserved image URLs and hashes but did not reliably save binary assets under
`library/`, and promoted records lacked local `path` fields.

## Next-run priorities

1. Preserve the v2 comms and specialized model-routing rules.
2. Prefer concise contracts, specs, reports, and handoff evidence.
3. Treat implementation as opt-in: build code only for a demonstrated blocker
   or an explicit user request.
4. Require saved local image assets and relative paths before a record is
   considered training-ready.
5. Keep the 1,000-item time/space quota plan authoritative.
6. Plan each next batch from underfilled period × geography cells, then assign
   families within those cells using the manifest.

## Checkpoint

- Promoted records: 3
- Staged records: 10
- Comms: v2 pair channels active
- Tool specifications: retained as useful artifacts
- Implementation: not the primary success criterion for this test run
