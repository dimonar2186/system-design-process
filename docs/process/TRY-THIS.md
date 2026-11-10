# Try this in ~5 minutes (product repo)

Goal: run **Product Owner** on a real task through **Frame (1–5) + stories per epic (`to-spec`)**. Profile: `through-stories`.

## 0. Prerequisites

- Cursor (or harness that loads project `skills/`)
- A **product** git repo for the real system (empty or existing)
- This pack available (clone/submodule/copy) — see below
- Matt skills (`to-spec`, `grilling`, …) are **already inside this pack** under `skills/`

## 1. Drop the pack into the product repo

From the product repo root:

```bash
# Example: submodule
git submodule add <url-of-system-design-process> .agents/system-design-process

# Link or copy skills + process docs into places your agent reads:
mkdir -p skills docs/process docs/agents
cp -R .agents/system-design-process/skills/* skills/
cp .agents/system-design-process/docs/process/FLOW.md docs/process/
cp .agents/system-design-process/docs/process/MATT-SKILLS.md docs/process/
cp .agents/system-design-process/docs/process/TRY-THIS.md docs/process/
cp .agents/system-design-process/docs/agents/process-state.md docs/agents/
cp .agents/system-design-process/docs/agents/HANDOFF-TEMPLATE.md docs/agents/
# Optional: merge AGENTS.md pointers from the pack
```

Or copy `skills/`, `docs/process/`, `docs/agents/process-state.md`, `docs/agents/HANDOFF-TEMPLATE.md` without submodule.

Confirm agent can see skill `product-owner` (slash or skill picker).

## 2. Matt setup (once per product repo)

Matt skill **files** come with the pack copy. Still run once:

```text
/setup-matt-pocock-skills
```

(issue tracker, triage labels, doc layout). Needed for smooth **6a** (`to-spec`) / tickets.

## 3. Start (Chat A — steps 1–3 only)

```text
/product-owner start through-stories
```

Approve gates with **who**. Inside a segment use `/product-owner continue`.

After **build order** approve, PO must write `docs/agents/handoff-after-epics.md` and **stop**. Open a **new** chat.

## 4. Chat B — BRD + architecture

```text
/product-owner resume handoff-after-epics
```

Finish steps 4–5. After Chosen + ADRs → `handoff-after-architecture.md` → **stop**. New chat(s) for epics.

## 5. Chat C… — one epic per chat

```text
/product-owner spawn epic E1
```

`to-spec` → approve stories → stop (or handoff-epic-E1). Next epic = **another** new chat (`spawn epic E2`). Do not chain all epics in one window.

PO must **not** enter contracts / tickets / tests / UAT under `through-stories`.

## 6. Sanity check artifacts

```text
docs/agents/process-state.md
docs/agents/handoff-after-epics.md
docs/agents/handoff-after-architecture.md
docs/product/outcomes.md
docs/product/scope.md
docs/product/nfr.md
docs/product/epics.md
docs/product/BRD.md
docs/architecture/options.md
docs/adr/ADR-*.md
# plus epic specs/stories from to-spec
```

## 7. If something blocks

| Symptom | What to do |
|---------|------------|
| Skill not found | Check `skills/` copy and harness skill path |
| PO continues past cut in same chat | Stop it; open new chat with `resume` / `spawn` from handoff |
| Grilling skill missing | Embedded fallback — continue |
| `to-spec` missing | Install Matt pack or write stories manually, then `continue` |
| PO tries step 8–11 | Should stop with not-ready / out of profile |
| Want only Frame | `/product-owner start frame-only` |
| Want full SDLC later | Finish remaining skills; `set profile full` |

## 8. Time box tip

Keep the real task narrow (one motto, ≤3 outcomes, ≤3 epics). Respect context cuts — that is what keeps PO usable.
