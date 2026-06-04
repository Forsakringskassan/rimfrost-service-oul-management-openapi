# FKPOC-794 — OpenAPI spec för att uppdatera sorteringsordning

## Background

The OUL management API manages operative tasks (uppgifter). Currently there is no way to control the order in which uppgifter are presented to handläggare clients.

## Requirements

- **REQ-OUL-SORT-001** The management API shall expose a mechanism to define a sort order for uppgifter.
- **REQ-OUL-SORT-002** The defined sort order is a system-wide configuration — it is not set per handläggare request.
- **REQ-OUL-SORT-003** One sort order specification must be designated as the default.
- **REQ-OUL-SORT-004** The default sort order spec is applied when handläggare clients retrieve uppgifter without specifying a sort order ID.
- **REQ-OUL-SORT-005** The sort order shall be persisted (survive restarts).
- **REQ-OUL-SORT-006** Each created sort order specification is assigned a unique ID (UUID) upon creation.
- **REQ-OUL-SORT-007** If no default exists at the time of creation, the newly created specification is automatically designated as the default.
- **REQ-OUL-SORT-008** The sort order is an ordered list of entries; the position in the list determines priority (first = highest).
- **REQ-OUL-SORT-009** Each entry contains an optional list of field+value constraints. If multiple constraints are specified, all must match (AND semantics).
- **REQ-OUL-SORT-010** An entry with no constraints is a catch-all: it matches all uppgifter not already placed by an earlier entry. A catch-all entry placed before other entries makes those entries unreachable.
- **REQ-OUL-SORT-011** Each entry has an optional "sort by" specifying a single field and direction (asc/desc) for ordering uppgifter within that entry.
- **REQ-OUL-SORT-012** The sort mechanism traverses the list in order; an uppgift is placed at the position of the first entry whose constraints all match.
- **REQ-OUL-SORT-013** Each uppgift appears at most once — if multiple entries match, only the highest-priority (earliest) entry applies.
- **REQ-OUL-SORT-014** Uppgifter matching the same entry are ordered among themselves according to that entry's "sort by" specification.
- **REQ-OUL-SORT-015** If no "sort by" is specified for an entry, the relative order of uppgifter within that entry is unspecified.
- **REQ-OUL-SORT-016** Uppgifter matching no entry fall to the bottom in unspecified order.
- **REQ-OUL-SORT-017** Uppgifter only go unmatched when no catch-all entry is present.
- **REQ-OUL-SORT-018** The list length is not fixed.
- **REQ-OUL-SORT-019** Supported constraint types per field:
  - `uppgift_id`: exact match (UUID) — allows pinning individual uppgifter to a specific position.
  - Date fields (`skapad`, `planerad_till`): fixed date interval (from/to), or relative interval as a duration offset from now (e.g. `-7d`).
  - String fields (`status`, `regel`, `roll`, `verksamhetslogik`, `beskrivning`): exact match or contains.

Example sort order configuration:

  | Position | Constraints |
  |----------|-------------|
  | 1 | `uppgift_id` = `a1b2c3d4-...` |
  | 2 | `skapad` within offset `-7d` to now |
  | 3 | `planerad_till` within 2026-06-01 – 2026-06-30 AND `beskrivning` contains "hund" |
  | 4 | `beskrivning` contains "katt" |

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
