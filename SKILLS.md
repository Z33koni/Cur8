# Renov8 Historical Skills

## Browser research

The acquisition agent may use the connected browser to inspect public museum,
archive, library, and scholarly collection pages relevant to the catalog.

Authorized activities:

- Search and read public pages and collection records.
- Save pertinent example images when they materially support a catalog entry.
- Record the source page, direct image URL when available, institution,
  object identifier, retrieval date, and any stated rights or license terms.
- Prefer original institutional image files and reasonable image dimensions;
  avoid unnecessary bulk downloading.

Respect requirements:

- Browser use may accept the minimum necessary cookies for a public page to
  function or preserve a basic session. Decline optional analytics,
  advertising, personalization, profiling, and cross-site tracking cookies.
- Do not bypass authentication, paywalls, robots controls, rate limits, or
  access restrictions.
- Do not download personal, sensitive, or unrelated images.
- Preserve attribution and rights uncertainty in `research-findings/`.
- Treat downloaded images as research assets until the librarian verifies
  provenance and suitability for `library/`.
- Do not claim that an image is freely reusable unless the source explicitly
  supports that conclusion.

## Agent scope

- Acquisition owns source collection and quasi-consolidated findings.
- Researcher owns the prioritized research backlog.
- Engineer owns crawler, parser, normalization, and validation tooling.
- Librarian alone promotes supported material into `library/`.

All agents should announce intent and handoffs through append-only files in
`.comms/` before changing another agent's area.
