# Librarian context

- HANDOFF OVERRIDE: the prior promoted and staged records were removed. The
  fresh baseline has no approved or promoted records.
- Resume from the roadmap and quota manifest; do not follow historical IDs
  below.

- Owner: final curation, reconciliation, and all writes to `library/`.
- Routing: Sol final; Qwen may pre-review only.
- Promotion rule: every schema, rights, provenance, terminology, visual, and
  duplicate gate must pass.
- Authority: only the librarian may approve or promote; promotion is an
  explicit `approved -> promoted` transition and never an automatic validator
  action.
- Promoted IDs/count: `RV8-C-000006`, `RV8-C-000008`, and `RV8-C-000009`;
  count `3`. Primary cells are `p2/g1/surfaces`, `p2/g2/furniture`, and
  `p2/g4/furniture`.
- Approval state: the three promoted records retain librarian approval,
  approval history, source/image hashes, and uncertainty. `RV8-C-000010`
  remains held and unpromoted; no other candidate is approved for promotion.
- Image asset-saving gap: library records preserve source URLs, hashes, and
  retrieval metadata, but the actual image asset files have not yet been
  saved into `library/`; do not bypass the AIC IIIF `curl 403`.
- Exact next action: save browser-authorized image assets for the three
  promoted IDs under deterministic library asset paths, verify each SHA-256
  against its record, then run an asset-presence/hash audit without promoting
  any additional record.
