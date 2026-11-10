# Product Owner process skills

Agent skills for greenfield system development. Entrypoint: **`product-owner`** — thin dispatcher with human gates, run profiles, and **context handoff cuts** so one chat does not swallow the whole flow.

Repo: [dimonar2186/system-design-process](https://cursor.com/codebase/dimonar2186/system-design-process)

## Process (steps)

### Phase A — Frame (once per system)

| Step | What happens | Pack skill | Gate |
|------|----------------|------------|------|
| 1 | Motto, problems, desired outcomes | `outcome-canvas` | Approve outcomes |
| 2 | Stakeholders, in/out scope, NFR | `scope-nfr` → `scope.md` + `nfr.md` | Approve each file |
| 3 | User-valued epics + build order | `epic-backlog` → `prioritize-epics` | Approve backlog, then order |
| — | **Context cut** | `handoff-after-epics` | New agent chat |
| 4 | System BRD (BR → epic), optional Proposed NFR | `to-brd` | BRD freeze |
| 5 | Architecture **concept** + proposed ADR(s) | `arch-options` | Choose option + who |
| — | **Context cut** | `handoff-after-architecture` | New agent chat(s) |

### Phase B — Per epic (build order; prefer one epic per chat)

| Step | What happens | Skill | Gate | In `through-stories`? |
|------|----------------|-------|------|------------------------|
| 6a | User stories / epic spec | `to-spec` (**Matt**) | Approve stories | **Yes** |
| 6b | Contracts (ours/external IDL + `catalog.md`) | `contracts-from-stories` | Approve contracts for epic | No |
| 6c | Tracer-bullet tickets | `to-tickets` (**Matt**) | Approve breakdown | No |
| 7 | Epic tech ADR pool | `adr-lite` | Batch-approve all ADRs | No |
| 8 | Failing tests from AC | `ac-to-tests` → `tdd` (Matt) | Batch-approve test maps | No (`full` only) |
| 9 | Build | `implement` / `implement-spec` (Matt) | Merge policy | No |
| 10 | UAT pack | `uat-pack` | Pack approve → Verdict; tickets if ≠ pass | No (`full` only) |
| 11 | Outcomes check + retro | `outcome-check` → optional `retro` (Matt) | Approve outcome-log section; next / stop | No (`full` only) |

**Default test profile `through-stories`:** steps 1–5 + 6a only, then done.

```text
/product-owner start through-stories
/product-owner resume handoff-after-epics
/product-owner spawn epic E1
```

Setup: [`docs/process/TRY-THIS.md`](docs/process/TRY-THIS.md). Full map: [`docs/process/FLOW.md`](docs/process/FLOW.md).

## Skills status

### Ready (grilled + usable)

| Skill | Role |
|-------|------|
| `product-owner` | Orchestrator: profiles, gates, handoff cuts, spawn epic, Not-ready stops |
| `outcome-canvas` | Outcomes canvas |
| `scope-nfr` | Scope + NFR |
| `epic-backlog` | Epic list + outcome trace |
| `prioritize-epics` | Build order in `epics.md` |
| `to-brd` | System BRD |
| `arch-options` | Architecture concept + proposed ADRs |
| `adr-lite` | Epic ADR pool, batch approve |
| `contracts-from-stories` | `contracts/catalog.md` + per-epic IDLs |
| `ac-to-tests` | Failing AC + ours-contract tests; maps + `test_results.md` |
| `uat-pack` | Human UAT pack in `docs/product/uat/E*.md`; Verdict + follow-up tickets |
| `outcome-check` | Append `outcome-log.md` for epic-traced outcomes; approve section |

### Not ready (draft)

Нет — все **наши** process skills прошли гриль и помечены Ready.

### Matt Pocock (vendored in this repo)

Copied into `skills/` from [mattpocock/skills](https://github.com/mattpocock/skills) (engineering + productivity). See [`docs/process/MATT-SKILLS.md`](docs/process/MATT-SKILLS.md) and [`vendor/mattpocock-skills.md`](vendor/mattpocock-skills.md).

Includes among others: `grilling`, `grill-me`, `grill-with-docs`, `to-spec`, `to-tickets`, `tdd`, `implement`, `implement-spec`, `code-review`, `pr`, `retro`, `handoff`, `ask-matt`, …

Once per product repo: `/setup-matt-pocock-skills`.

## Docs

| Doc | Purpose |
|-----|---------|
| [`docs/process/FLOW.md`](docs/process/FLOW.md) | Step map + profiles + cuts |
| [`docs/process/TRY-THIS.md`](docs/process/TRY-THIS.md) | 5-minute product-repo start |
| [`docs/process/MATT-SKILLS.md`](docs/process/MATT-SKILLS.md) | Matt companion skills |
| [`docs/agents/process-state.md`](docs/agents/process-state.md) | Live PO state |
| [`docs/agents/HANDOFF-TEMPLATE.md`](docs/agents/HANDOFF-TEMPLATE.md) | Context-cut handoff |
| [`skills/product-owner/PHASES.md`](skills/product-owner/PHASES.md) | Recipes + readiness |

## Design choices

- Human gates with named approver; grill **inside** each skill (step isolation).
- Tracer bullets over horizontal layers.
- Context cuts after epic ranking and after architecture; one epic per chat.
- Draft skills: PO **stops cleanly** (no crash, no fake artifacts).
- State on disk (`process-state` + handoffs), not chat memory.

## Local use in an application repo

Copy or submodule this pack; load `skills/`; keep `docs/process/` + `docs/agents/`. Details in TRY-THIS.md.
