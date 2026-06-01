# FKPOC-794 — OpenAPI spec för att uppdatera sorteringsordning

## Background

The OUL management API manages operative tasks (uppgifter). Currently there is no way to control the order in which uppgifter are presented to handläggare clients.

## Requirements

- The management API shall expose a mechanism to define a sort order for uppgifter.
- The defined sort order is a system-wide configuration — it is not set per handläggare request.
- Once set via the management API, the sort order applies to all handläggare clients when they retrieve uppgifter.
- The sort order shall be persisted (survive restarts).

## Scope

Update the OpenAPI spec (`openapi.yaml`) to add endpoints on the management side for:

1. Getting the current persisted sort order specification.
2. Setting/updating the persisted sort order.
3. Previewing the result of a sort specification against current uppgifter without committing it.

The get (sorted uppgifter) and preview endpoints shall support a `max` parameter to limit the number of returned uppgifter.

No changes to the handläggare-facing API are required — the sort order is applied transparently on the service side.

## Requirements (sort order specification)

- The sort order is an ordered list of entries; the position in the list determines priority (first = highest).
- Each entry contains one or more field+value constraints (all must match, AND semantics) and an optional "sort by" specifying a single field and direction (asc/desc).
- The sort mechanism traverses the list in order; an uppgift is placed at the position of the first entry whose constraints all match.
- Uppgifter matching the same entry are ordered among themselves according to that entry's "sort by" specification; if none is given, their relative order is unspecified.
- Uppgifter matching no entry fall to the bottom in unspecified order.
- The list length is not fixed.
- Supported constraint types per field:
  - `uppgift_id`: exact match (UUID) — allows pinning individual uppgifter to a specific position.
  - Date fields (`skapad`, `planerad_till`): fixed date interval (from/to), or relative interval as a duration offset from now (e.g. `-7d`).
  - String fields (`status`, `regel`, `roll`, `verksamhetslogik`, `beskrivning`): exact match or contains.
- Example sort order configuration:

  | Position | Constraints |
  |----------|-------------|
  | 1 | `uppgift_id` = `a1b2c3d4-...` |
  | 2 | `skapad` within offset `-7d` to now |
  | 3 | `planerad_till` within 2026-06-01 – 2026-06-30 AND `beskrivning` contains "hund" |
  | 4 | `beskrivning` contains "katt" |
