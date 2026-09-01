# Librarian checkpoint: place/time index

`library/indexes/catalog-facets.json` is the navigation index. Primary facets
are exact source-backed `claims.place.label` and `claims.period.label` values.
Secondary facets remain in canonical records: material, form, function, status,
rights, asset kind, and named-element evidence. Do not normalize uncertain
geographies or dates into invented buckets.

After the current intake, catalog size is 102 records. The index includes the
eight new credenza/curio records, the 13 modern-home/fixtures/finish records,
and six plumbing-gap controls. Every record with a non-null raw place/period
label must occur exactly once in each primary index; restricted/no-image
records remain indexed rather than omitted.
Rijksmuseum volume reconciliation (2026-09-01): ten distinct candidate records
match ten local WebP assets and remain indexed by exact packet place/time labels.
No duplicates, promotions, or library asset bindings were made: all ten image
rights statements still say object-specific verification pending; six records
lack material evidence; the Settala item is a print/display control and
attribution uncertainty remains explicit. Live audit: 132 examples, 48 labels,
118 combined images, 61 curated/69 candidates/2 needs_review, zero
missing/invalid records. Next gate: object-specific reusable-rights evidence
plus the six material fields.
Rijks gate repair close (2026-09-01): the ten packet assets now bind to their
matching records through local paths and direct IIIF source entries. Nine
distinct furnishing records are curated; the Settala image remains a candidate
display-print control. Download controls and IIIF retrieval are verified, while
the absence of a separately exposed object-level licence label remains explicit
in source and asset rights. Live audit: 132 examples, 48 labels, 69 local +
59 research = 128 combined images; 70 curated/60 candidates/2 needs_review;
zero missing/invalid records. No duplicate records were created.
