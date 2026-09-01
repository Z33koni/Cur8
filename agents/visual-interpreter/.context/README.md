# Visual-interpreter context

- HANDOFF OVERRIDE: prior image assets and review artifacts were removed.
  Resume with fresh saved staging images on the next hardware/model setup.

- Owner: direct image observations and visual quality gates.
- Routing: `qwenvision-high` first pass is mandatory and resolves to local
  Ollama `qwen3-vl:8b`; Sol only for flagged ambiguity/deep review.
- Separate observation from historical inference.

## Provider validation

- `codex.config.toml` maps `qwenvision-high` to provider `ollama`, model
  `qwen3-vl:8b`, high reasoning effort.
- Validation evidence: `research-findings/QWEN_ROUTING_CHECK_2026-09-01.md`.
  `ollama show qwen3-vl:8b` reported `completion`, `vision`, `tools`, and
  `thinking`; an image smoke test accepted a basin/pitcher image and returned
  a visual identification. Do not substitute text-only `qwen3:30b` for image
  review.

## Browser and image retrieval state

- Connected Chrome retrieval is working for institutional record pages and
  direct IIIF/image endpoints.
- AIC tile `RV8-C-000006`: record page encountered security verification;
  official IIIF image was opened directly in Chrome and browser-exported.
- Met basin `RV8-C-000007`: multiple IIIF views were retrieved; the primary
  useful view is a group-framed basin beside a matching pitcher, while another
  view is a maker-mark detail. Do not treat the detail as a shape view.
- Browser-exported assets currently live in ephemeral `/tmp/browser-use`
  bundles, not as durable repository assets.

## Latest visual reviews

- `research-findings/VISUAL_REVIEW_PILOT_001.md`: browser visual review of
  pilot 001; no library promotion.
- `research-findings/VISUAL_REVIEW_BATCH_002.md`: preliminary browser review;
  tile and basin observations recorded, but it predates the required Qwen-VL
  first pass.
- `research-findings/VISUAL_REVIEW_RV8-C-000006_QWENVL.md`: Qwen-VL first pass
  complete for the AIC tile; source-bounded label retained.
- `research-findings/VISUAL_REVIEW_BATCH_003.md`: Qwen-VL first passes complete
  for RV8-C-000008 through RV8-C-000010.
- `RV8-C-000007` still lacks its own durable Qwen-VL review artifact.

## Asset-saving gap

- Browser inspection and Qwen-VL can consume retrieved images, but the
  browser-exported files are not yet consistently copied into staged record
  assets with stable relative paths, SHA-256 hashes, byte sizes, and retrieval
  timestamps.
- Staged records may retain source URLs while still failing the durable asset
  and image-provenance gate. Do not promote on URL-only evidence.

## Exact next action

1. Materialize the browser-exported primary image for `RV8-C-000007` under
   `research-findings/staging/batch-002/assets/`, record its relative path,
   SHA-256, byte size, and retrieval timestamp in the staged JSON.
2. Run `qwenvision-high`/Ollama `qwen3-vl:8b` on that saved image and write
   `research-findings/VISUAL_REVIEW_RV8-C-000007_QWENVL.md`, keeping the
   basin/pitcher group boundary explicit.
3. Run the validator; escalate to Sol only if Qwen-VL flags genuine identity,
   named-term, or image ambiguity.
