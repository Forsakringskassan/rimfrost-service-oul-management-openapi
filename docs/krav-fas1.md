# FKPOC-794 — Fas 1: Partiell implementation av sorteringsordning

## Background

This document defines the requirements for a partial, incremental release of the sort order feature described in [krav.md](krav.md). The full OpenAPI spec applies without modification — this document scopes down which endpoints must be implemented and relaxes certain system requirements.

## Relaxed requirements

The following requirements from `krav.md` do **not** apply in fas 1:

- **REQ-OUL-SORT-005** (persistence) — the sort order does not need to survive service restarts. An in-memory store is sufficient.
- **REQ-OUL-SORT-003** (mandatory default) and **REQ-OUL-SORT-006** (unique ID per creation) are partially relaxed: only one sort order specification is supported at a time. Creating a new one replaces the existing one and is always the default.

## Endpoints

### Required

| Endpoint | Notes |
|----------|-------|
| `POST /sorteringsordning` | Creates the sort order, replacing any existing one. Always designated as default. Returns a new UUID each time. |
| `GET /sorteringsordning/default` | Returns the current (only) sort order, or `404` if none has been created yet. |
| `GET /uppgifter` | Must apply the active sort order. The `sorteringsordningId` parameter may be ignored — if provided, it should be accepted without error as long as it matches the current spec's ID. |

### Optional but recommended

| Endpoint | Notes |
|----------|-------|
| `GET /sorteringsordning` | Returns a list of zero or one item. |
| `GET /sorteringsordning/{id}` | Returns the current spec if the ID matches; `404` otherwise. |
| `POST /sorteringsordning/preview` | Useful for testing sort order configurations without persisting. |

### Not required

| Endpoint | Reason |
|----------|--------|
| `PUT /sorteringsordning/{id}/default` | No-op in fas 1 — the single spec is always the default. May return `204` without side effects. |
| `DELETE /sorteringsordning/{id}` | Not required. May return `405 Method Not Allowed` or be left unimplemented. |

## Deviations from full spec behaviour

- The `409` response on `DELETE` (protecting the default from deletion, see **REQ-OUL-SORT-003**) does not apply — `DELETE` is not required.
- **REQ-OUL-SORT-007** (auto-designation) is trivially satisfied since there is always at most one spec.
- `GET /sorteringsordning` will return at most one item; `total` in `UppgiftPage` reflects the actual count of uppgifter matching the query.

## Upgrade path

No API changes are required to move from fas 1 to full implementation. Clients built against the spec in fas 1 will continue to work unchanged.
