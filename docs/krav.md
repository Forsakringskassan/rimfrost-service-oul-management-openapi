# FKPOC-794 — OpenAPI spec för att uppdatera sorteringsordning

## Background

The OUL management API manages operative tasks (uppgifter). Currently there is no way to control the order in which uppgifter are presented to handläggare clients.

## Requirements

- The management API shall expose a mechanism to define a sort order for uppgifter.
- The defined sort order is a system-wide configuration — it is not set per handläggare request.
- One sort order specification must be designated as the default; this is the spec applied when handläggare clients retrieve uppgifter without specifying a sort order ID.
- The sort order shall be persisted (survive restarts).
- Each created sort order specification is assigned a unique ID (UUID) upon creation.

## Scope

Update the OpenAPI spec (`openapi.yaml`) to add endpoints on the management side for:

1. Creating a new sort order specification (returns its generated ID).
2. Getting all sort order specifications.
3. Getting the default sort order specification (`/sorteringsordning/default`).
4. Setting a specific sort order specification as the default (`PUT /sorteringsordning/{id}/default`).
5. Getting a specific sort order specification by ID.
6. Deleting a sort order specification by ID.
7. Previewing the result of a full sort order spec provided inline, without persisting it.

`GET /uppgifter` and `POST /sorteringsordning/preview` support offset-based pagination via `limit` and `offset` parameters and return a paginated envelope `{ total, items }` where `total` is the total number of matching uppgifter. `GET /uppgifter` also accepts an optional `sorteringsordningId` query parameter — if omitted, the default sort order spec is applied.

No changes to the handläggare-facing API are required — the sort order is applied transparently on the service side.<br>
A possible future extension could be to apply different sort order specs to different handläggare.


## Requirements (sort order specification)

- The sort order is an ordered list of entries; the position in the list determines priority (first = highest).
- Each entry contains one or more field+value constraints (all must match, AND semantics) and an optional "sort by" specifying a single field and direction (asc/desc) within the entry.
- The sort mechanism traverses the list in order; an uppgift is placed at the position of the first entry whose constraints all match. Each uppgift appears at most once — if multiple entries match, only the highest-priority (earliest) entry applies.
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
