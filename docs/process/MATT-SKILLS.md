# Matt Pocock skills (vendored)

Engineering + productivity skills from [mattpocock/skills](https://github.com/mattpocock/skills) are **copied into this repo** under `skills/<name>/` (flattened).

Provenance: [`vendor/mattpocock-skills.md`](../../vendor/mattpocock-skills.md)  
License: [`vendor/mattpocock-skills.LICENSE.txt`](../../vendor/mattpocock-skills.LICENSE.txt) (MIT)

You do **not** need a separate `npx skills add mattpocock/skills` for this pack to see `to-spec`, `tdd`, `implement`, etc. — they ship beside the PO skills.

Still run **`/setup-matt-pocock-skills` once per product repo** (issue tracker, triage labels, doc paths).

## Referenced by Product Owner

| Skill | When |
|-------|------|
| `grill-with-docs` / `grill-me` / `grilling` | Inside drafting skills (and fallbacks) |
| `to-questionnaire` | Async stakeholder answers |
| `research` | External NFR/standards |
| `wayfinder` | Foggy multi-session planning only (not epic value ranking) |
| `to-spec` | Step 6a stories |
| `to-tickets` | Step 6c |
| `prototype` | Step 5 design questions |
| `domain-modeling` | Steps 5, 7 when glossary shifts |
| `codebase-design` | Step 5 when seams matter |
| `tdd` | Steps 8–9 |
| `implement` / `implement-spec` | Step 9 |
| `code-review` | Steps 9–10 |
| `pr` | Step 9 |
| `diagnosing-bugs` | Step 10 if red |
| `triage` | Incoming post-demo only |
| `wizard` | Step 11 human-only ops |
| `retro` | Step 11 agent-environment improvement |
| `handoff` | Context moves across directories/sessions |
| `ask-matt` | Router over Matt flows |

If a user-invoked Matt skill cannot be Skill-tool'd from `product-owner`, the PO stops and asks the human to run the slash command, then `/product-owner continue`.
