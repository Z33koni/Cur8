# Image materialization

`tools/materialize_images.py` materializes `promoted` JSON records without
touching `library/` directly.

```sh
python tools/materialize_images.py \
  --records path/to/promoted-records \
  --output-root path/to/materialized \
  --json-report
```

For each record, assets are written under:

```text
<output-root>/<record-id>/images/<ordinal>-<image-id>.<suffix>
```

The output record is `<output-root>/<record-id>.json`; each image receives a
relative `path` such as `RV8-I-000100/images/001-image-1.bin`, its SHA-256
`content_hash`, `byte_size`, and UTC `retrieved_at`. Existing accessible local
`path` assets are copied and preferred over `url`, so they are not downloaded
again.

Each record is staged independently. If any image cannot be read or downloaded,
that record's staged assets and JSON update are discarded; other records may
still complete. Use `--dry-run --json-report` to inspect planned downloads and
local reuse without fetching or writing.
