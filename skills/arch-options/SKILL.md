---
name: arch-options
description: Grill then draft conceptual architecture option(s) in docs/architecture/options.md. One sound option is enough; offer more; create extras only on request. After human choice, write proposed ADR(s). No brand-level tech lock-in.
---

# Architecture options

Own the **architecture concept** — contours and styles, not detailed design. Always grill first. Help the human choose; do not silently lock a stack.

## Artifact

Path: `docs/architecture/options.md`

```markdown
Status: draft | approved
Approved by: <name or role>
Approved at: <ISO-8601 datetime with offset>
Content language: ...
Chosen: <none | Option A | ...>
```

ADRs (after choice only): `docs/adr/ADR-NNNN-title.md` (same naming as `adr-lite`)  
Optional tracker issue: offer; create only after explicit yes.

## Concept bar (in / out)

**In:** deployment/boundary shape (modular monolith vs services…), integration style (sync/async), consistency approach, identity of major subsystems at C4 L1/L2 (prose or mermaid), how must-NFR are addressed at concept level.

**Out:** class diagrams, per-BR sequences, table schemas, API field layouts, brand technologies as the decision (Postgres, Kafka, K8s as *the* pick). Prefer capability classes («relational store», «managed queue»). If a concrete product must be chosen later → `## Open questions`.

## Inputs (read-only)

- Prefer: `docs/product/BRD.md`, `docs/product/nfr.md` (must-have), `docs/product/scope.md`, `docs/product/epics.md`, existing `docs/adr/`.
- Pull **Proposed NFR** from the BRD into comparison (marked proposed/assumption).
- Never edit outcomes/scope/nfr/BRD/epics from this skill.

## Assumptions (always)

`## Assumptions` is **always** present.  
If any driver (must NFR measure, Proposed NFR, BR constraint) is TBD or weak, state explicitly that option fit is **under assumed parameter values** (name the assumption). Do not pretend TBD SLOs are locked.

## How many options

- **One** sound conceptual option is enough to complete a draft.
- After presenting it, **offer** to create alternative(s) («могу набросать Option B под другой контур — нужно?»).
- Create Option B/C **only** on explicit user request — not invent strawmen by default.

## Comparison

When ≥1 option exists, keep a comparison table:

| Concern | Option A | Option B… |
|---------|----------|-----------|
| must NFR (from nfr.md) | … | … |
| Proposed NFR (from BRD) — mark `proposed/assumption` | … | … |

Every must-have NFR and every Proposed NFR used as a driver gets a row (or an explicit «not an architecture driver» note in Assumptions).

## Steps

### 1. Content language

Ask once. Headings English.

### 2. Always grill (architecture-concept contour)

Call `grilling` (or `grill-me` / `grill-with-docs`). Cover: forces from BR/NFR, constraints, risks, what must stay undecided as Open questions, whether more than one option is wanted.  
Fallback: embedded interview. Do not skip because a parent already interviewed.  
Detailed design / brand lock-in → Open questions or Handoff, not fake certainty.

### 3. Write `options.md` (draft)

Include Context, Assumptions (always), Option(s), Comparison, Open questions, non-binding Recommendation (may point at the only option), Handoff for PO.  
`Chosen: none`, `Status: draft`.

### 4. Offer more options

Explicitly offer alternatives. Stop unless the user asks to add one; then append and refresh Comparison.

### 5. Gate — human chooses

User names the option + who. Set `Chosen`, `Status: approved`, `Approved by/at`.  
Recommendation stays historically non-binding; Chosen is the gate result.

### 6. ADR after choice only

Only after step 5, create ADR(s) with `Status: proposed` (contestable / refinable at epic time):

- Collect the distinct decision questions implied by the chosen concept (integration style, deploy shape, data ownership, …).
- If **decision questions ≤ 3** → **one** ADR file covering them.
- If **> 3** → **separate** ADR file per question (or per tight cluster), still `proposed`.
- Link ADR(s) from `options.md` (e.g. `## ADRs`).
- Note in each ADR: may be challenged or refined when a specific epic is detailed.

Do not mark ADR `accepted` here unless the user explicitly upgrades them later.

## Template — `docs/architecture/options.md`

```markdown
# Architecture options

Status: draft
Approved by:
Approved at:
Content language: ...
Chosen: none

## Context
...

## Assumptions
- ...
- (If TBD drivers:) Option fit assumes <parameter> ≈ <assumed value> because <source BR/NFR> is TBD.

## Options

### Option A — <conceptual name>
- Contour (C4 L1/L2 prose or mermaid)
- Addresses NFR / Proposed NFR: ...
- Risks: ...
- Cost / complexity (qualitative): ...
- Rollback / exit: ...

## Comparison
| Concern | A | B |
|---------|---|---|
| N1 … (must) | ... | ... |
| Proposed: … (proposed/assumption) | ... | ... |

## Recommendation (non-binding)
...

## Open questions
- Concrete technology products to select later: ...

## ADRs
- (filled after Chosen)

## Handoff / tensions for PO
- ...
```

## Out of scope for this skill

Implementing systems, editing BRD/NFR files, accepting ADRs as final at epic depth, brand-level procurement picks.
