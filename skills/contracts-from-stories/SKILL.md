---
name: contracts-from-stories
description: Grill interface boundaries then draft docs/architecture/contracts/catalog.md plus per-epic contract files (OpenAPI/WSDL/proto/…). Ours always get draft files; external are path-registered or copied in. Use after to-spec or when product-owner is on step 6.
---

# Contracts from stories

Turn story/spec intent into **explicit contracts** without implementing them. Always grill first with focus on **interface boundaries** and **ownership** (`ours` | `external`).

## Layout

```text
docs/architecture/contracts/
├── catalog.md              # registry + per-epic Status
├── E1/
│   ├── orders-api.yaml     # free meaningful names; flat inside epic
│   └── ...
└── E2/
    └── ...
```

- **Index:** always maintain `catalog.md` — links to every contract file **or** external git path, and links to epics.
- **Per epic:** folder `E<id>/`, files **flat** inside (no nested type folders required).
- Formats as technology demands, typically:
  - REST → OpenAPI YAML
  - SOAP → WSDL / XSD
  - async / gRPC → `.proto` (or other stack-native IDL)
  - other formats OK when ADR/tech requires them

## Ownership

| Kind | Behaviour |
|------|-----------|
| **ours** | System under design **provides** the interface. Skill **always** writes a draft contract file under `E<id>/`. |
| **external** | Interface owned elsewhere. If reachable via git — **register path/URL in catalog only** (no mandatory copy). If the user has a concrete file — **place it in our repo** under the epic folder (flat) and catalog it as `mirrored`. |

## Format choice

Do **not** ask format by default. Infer from `arch-options` / ADRs + grilling. If still ambiguous — ask once.

File names: **free and meaningful** (`orders-api.yaml`, `dispatch-events.proto`), not rigid prefixes.

## Coverage

- Stories **may** have no contracts (UI-only / no new interface) — no forced row.
- Skill still maps contracts it creates back to driving stories/BRs in `catalog.md` when known.

## Approve

**Per epic** in `catalog.md` (not whole-catalog-only):

```markdown
### E1 — <epic title>
Status: draft | approved
Approved by:
Approved at:
```

Agent sets `approved` only on explicit approve for **that epic** + named who.

## Steps

### 1. Content language

Ask once if needed. `catalog.md` headings stay English; IDL files follow their ecosystem norms (usually English identifiers).

### 2. Always grill (contracts contour)

Call `grilling` (or `grill-me` / `grill-with-docs`). Focus: what interfaces exist, ours vs external, sync/async style already decided, payloads at contract level, errors worth naming.  
Fallback: embedded interview. Do not skip because a parent already interviewed.

Read (read-only): epic spec/stories, BRD section for the epic, ADRs, `arch-options`, `nfr.md` as needed.

### 3. Write / update catalog + files

1. Ensure `docs/architecture/contracts/catalog.md` exists; upsert the epic section.
2. For each **ours** contract → draft IDL/OpenAPI/WSDL/… under `E<id>/`.
3. For each **external** → catalog git path **or** copy user-provided file into `E<id>/` + mark `mirrored`.
4. Mark unknowns in catalog as `TBD` with the story/BR that forces the decision.

### 4. Gate

Skill done for the epic when catalog section exists, every identified **ours** contract has a draft file, externals are path-registered or mirrored, Status is `draft` (until approve).  
Then ask approve for **this epic**.

## Template — `catalog.md`

```markdown
# Contract catalog

Content language: ...

## Epics

### E1 — <title>
Status: draft
Approved by:
Approved at:
Epic doc / backlog: docs/product/epics.md#… (or tracker link)

| ID | Name | Ownership | Format | Path or git ref | Stories / BR | Notes |
|----|------|-----------|--------|-----------------|--------------|-------|
| C-E1-01 | orders-api | ours | openapi | E1/orders-api.yaml | S1, BR-E1-02 | ... |
| C-E1-02 | billing-quote | external | wsdl | git: org/billing@path/api.wsdl | S3 | ... |
| C-E1-03 | legacy-pay | external | openapi | E1/legacy-pay.yaml (mirrored) | S3 | provided by user |

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Implementing handlers, changing ADR Status, inventing architecture concepts (read them), forcing contracts onto every story.
