# Researcher context checkpoint

- HANDOFF OVERRIDE: all prior candidate and promotion records were removed.
  Treat the roadmap, quota manifest, and objective inventory as the only
  active planning state.

## Role and routing

- Owner: canonical terms, definitions, period/geography claims, family assignment, and uncertainty.
- Required judgment model: Luna-medium.
- Qwen is allowed only for bounded extraction/checks; batch-003 visual first passes used local Ollama `qwen3-vl:8b`.
- Luna-medium was unavailable in the last run (local Ollama had no manifest; delegated provider capacity was exhausted). Do not silently substitute another judgment model.
- Hold unresolved boundary cases, missing geography, unsupported subtypes, and incomplete identity evidence outside quota counts.
- Shared target inventory: `research-targets/OBJECTIVE_FURNISHINGS.md`.

## Promoted library IDs

- `RV8-C-000006` — p2 / g1 / surfaces; institutional “Tile with Adam and Eve.” No narrower Lambeth-ware claim promoted.
- `RV8-C-000008` — p2 / g2 / furniture; institutional “Side chair.” Cane seat/back and cabriole-leg features remain descriptors.
- `RV8-C-000009` — p2 / g4 / furniture; institutional “Wig cabinet (cabinet de coiffure).” Two-tier/hexagonal features remain descriptors.

These are the only currently promoted records visible in `library/`.

## Staged or rework IDs

- `RV8-C-000004` — research-needed; p5 / g10 / lighting. Dragonfly lamp terminology, attribution split, and remaining review gates are open.
- `RV8-C-000005` — research-needed; currently provisional p5 / g10 / plumbing, but 1892–1903 crosses p4/p5. Basin/set identity and visual review remain open; do not count.
- `RV8-C-000007` — research-needed; p4 / g1 / plumbing. Institutional “Basin” retained; group-framed image and basin subtype remain open.
- `RV8-C-000010` — research-needed; provisional p4 / g11 / decorative. Canonical term “Panel (drawnwork textile)”; period remains p3/p4.
- `RV8-C-000001`–`RV8-C-000003` — pilot-001 rework; not promoted or counted.

The staging validator report covers staging only and therefore reports zero promoted staging records; the three IDs above are already present in `library/`.

## Current terminology and assignment adjudications

- `B2-02`: retain generic “Tile”; Northwestern Iran supports g7; 1550–1650 remains p1/p2.
- `B2-08`: retain generic “Basin”; Germany supports g4; 1745–1755 remains p2/p3. Do not invent “pewter” or a subtype without source evidence.
- `B2-15`: retain “Wallpaper”; 1800–1900 remains p3/p4; geography is unknown until manufacture/use place is sourced.
- `RV8-C-000006`: source-bounded institutional tile title; visual evidence supports tile form, not a narrower ware name.
- `RV8-C-000008`: “Side chair”; cane/cabriole descriptors only, no unsupported subtype.
- `RV8-C-000009`: “Wig cabinet (cabinet de coiffure)”; two-tier/hexagonal descriptors only.
- `RV8-C-000010`: “Panel (drawnwork textile)”; removable textile panel belongs in the closest controlled family, `decorative`, not `surfaces`. Geography g11 is supported by “Made in Mexico.”

## Open period and family questions

- `RV8-C-000005`: resolve 1892–1903 against half-open p4/p5 bands; confirm standalone wash basin versus matched sanitary-set component.
- `RV8-C-000010`: narrow “19th century” to p3 or p4; retain `decorative` provisionally and avoid expanding the medium beyond source-bounded drawnwork textile.
- `B2-02`, `B2-08`, and `B2-15`: keep staged/uncounted until their boundary dates and, for B2-15, primary geography are resolved.
- Continue to treat generic institutional titles as canonical when evidence does not support a named subtype.

## Next action

On resume, use browser/source evidence to resolve `RV8-C-000005`’s p4/p5 boundary and basin/set identity, obtain librarian confirmation for `RV8-C-000010`’s `decorative` assignment, then rerun the staging validator. Do not change `library/` or add quota counts for any unresolved record.
