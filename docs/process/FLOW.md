# System development flow

Process for **new systems** (greenfield). Change-to-existing is a separate track later.

Canonical recipes: [`skills/product-owner/PHASES.md`](../../skills/product-owner/PHASES.md).  
Entrypoint: `product-owner`.  
Handoff template: [`docs/agents/HANDOFF-TEMPLATE.md`](../agents/HANDOFF-TEMPLATE.md).

## Run profiles

| Profile | Covers | Use when |
|---------|--------|----------|
| `through-stories` | Steps 1–5, then per epic **stories only** (`to-spec`) | Default for first real-task tests |
| `frame-only` | Steps 1–5 | Stop before epic loop |
| `full` | Steps 1–11 | Only when all skills below are Ready |

Set profile in `docs/agents/process-state.md` (`Run profile`) or pass on start: `/product-owner start through-stories`.

## Context cuts (keep PO context thin)

```text
Chat A: start → steps 1–3 → handoff-after-epics          STOP / new chat
Chat B: resume handoff-after-epics → steps 4–5 → handoff-after-architecture  STOP
Chat C…: spawn epic E* → 6a (stories) → optional handoff-epic-E* → next epic in NEW chat
```

Do not continue past a cut inside the same bloated chat. Fresh agent + disk artifacts only.

## Phase A — system frame (once)

| Step | Name | Skills | Human gate |
|------|------|--------|------------|
| 1 | Outcomes | `outcome-canvas` (grill inside) | Approve outcomes |
| 2 | Scope + NFR | `scope-nfr` (grill inside) → two files | Approve `scope.md` and `nfr.md` (any order) |
| 3 | Epics + priority | `epic-backlog` → gate → `prioritize-epics` → gate | Approve backlog; then approve build order → **cut `after-epics`** |
| 4 | BRD | `to-brd` (after resume) | BRD freeze (soft if TBD sections) |
| 5 | Architecture concept | `arch-options` → choose → `proposed` ADR(s) | Choose option + who → **cut `after-architecture`** |

## Phase B — per epic (build order from step 3)

Prefer **one epic per new agent chat** (`/product-owner spawn epic E1`).

| Step | Name | Skills | Human gate | Ready? |
|------|------|--------|------------|--------|
| 6a | Stories | `to-spec` (Matt) | Approve epic spec / stories | **Yes** (needs Matt or manual slash) |
| 6b | Contracts | `contracts-from-stories` | Approve contracts for epic | Yes — **not** in `through-stories` |
| 6c | Tickets | `to-tickets` (Matt) | Approve ticket breakdown | Yes — **not** in `through-stories` |
| 7 | Detailed ADR | `adr-lite` (pool, batch approve) | Batch-approve ADR pool | Yes — not in `through-stories` |
| 8 | Tests first | `ac-to-tests` → `tdd` | Batch-approve test maps | **Yes** |
| 9 | Build | `implement` / `implement-spec` → `code-review` → `pr` | Merge policy | Matt — skip if missing |
| 10 | UAT | `uat-pack` (+ `code-review` / `diagnosing-bugs`) | Pack approve → Verdict+who; tickets if ≠ pass | **Yes** |
| 11 | Ship + outcomes | `outcome-check` → optional `retro` | Approve log section; next / stop | **Yes** |

Under `through-stories`: after 6a, mark `stories-done`, hand off to the **next** epic chat. **Do not** call 6b–11.

## Rules

- **User functions first**: vertical slices, not horizontal layers.
- **Step isolation**: grilling inside each drafting skill; PO does not double-grill.
- **Context cuts** after epic ranking and after architecture; epic work in fresh chats.
- **One step at a time**; stop cleanly on gates and Not-ready steps.
- **Matt skills** when installed; otherwise slash + `continue` inside the segment.
- **Product Owner** is the happy-path entrypoint (dispatcher, not a dump of all grills).
