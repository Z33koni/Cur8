# Engineer context

- HANDOFF OVERRIDE: implementation code, tests, and candidate data were
  removed. Durable contracts in `tools/SPEC/` are retained for future work.
- Do not resume the historical materializer task below unless explicitly
  requested or a fresh workflow demonstrates the blocker.

- Owner: deterministic tools, schemas, validators, and tests.
- Routing: `qwencode-high` / Ollama `qwen3-coder:30b`.
- Provider evidence: direct Ollama smoke tests returned
  `QWEN_CODER_DUPLICATE_CHECK_SMOKE_OK` and
  `QWEN_CODER_MATERIALIZER_SMOKE_OK`; do not claim Qwen routing without a
  direct execution result.
- Validator: `tools/validate_records.py`.
- Contract: `tools/SPEC/VALIDATION_PLAN.md`.
- Current validator changes: boundary-period and missing-geography holds;
  deterministic duplicate/leakage gates for exact `content_hash`,
  `physical_object_or_group_id`, and explicit source-lineage IDs. Promoted
  collisions block; non-promoted collisions warn.
- Active task: finish `tools/materialize_images.py`, which stages promoted
  record image downloads/local-path reuse atomically per record, writes
  deterministic `<record-id>/images/` assets, updates relative paths,
  SHA-256, byte size, and UTC retrieval timestamps, and supports dry-run JSON
  reports.
- Owned files:
  `tools/validate_records.py`,
  `tools/test_validate_records.py`,
  `tools/materialize_images.py`,
  `tools/test_materialize_images.py`,
  `tools/SPEC/IMAGE_MATERIALIZATION.md`.
- Test status: validator/duplicate tests pass; combined suite is currently
  `25 passed, 1 error` because the materializer test helper does not create
  its temporary `records/` directory.
- Open blockers: fix that test fixture setup, rerun the complete suite,
  perform final Qwen Coder review of the materializer, and verify no partial
  output remains after a per-record download failure.
- Next action: create parent directories in the materializer test helper,
  then run `python -m unittest discover -s tools -p 'test_*.py'` and record
  the final result.
- Current staging: 7 records, 0 promoted; `library/` is out of scope.
