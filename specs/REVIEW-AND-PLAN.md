# AgentFacts — review and plan (2026-08 flesh-out)

> Companion to `x-facts/specs/SUITE-FLESH-OUT-2026-08.md`.  
> Formal format remains root [`SPEC.md`](../SPEC.md) (v0.1.0).

**Status:** executed (2026-08-07).

---

## Review (current state)

### Already solid

- SPEC v0.1.0: configuration-not-codebase; six groups (model, tools, reach,
  autonomy, memory, egress); ToolFacts composition.
- Schema + validator + family-quality amber site.
- One worked example: ForgeTrail Reference Agent (`cli-agent`, tight leash).

### Gaps

| Gap | Why it matters (agent view) |
|---|---|
| Single `kind` demonstrated | Enum has five kinds; operators need contrast across leash/reach. |
| Weak composition demo | Only one `toolsets` path; should show filesystem/shell/network rollups. |
| No domain-fetchable exemplars / `llms.txt` | Same agent-entry gap as ToolFacts. |
| Generator | Still correctly deferred on ToolFacts MCP core. |

### What stays unchanged

- Spec taxonomy and enums.
- Generator stub.
- No large public-agent directory yet.

---

## Plan

### P1 — Exemplar ladder (`examples/<slug>/AGENT_FACTS.md`)

| Slug | `kind` | Signal |
|---|---|---|
| `forgetrail-reference` | `cli-agent` | Reactive, no FS/network; ForgeTrail toolset (existing). |
| `ide-coding-agent` | `ide-extension` | Supervised; scoped FS write; shell gated; approvals. |
| `autonomous-researcher` | `autonomous-service` | Self-looping; unrestricted/allowlist net; browse. |
| `support-chatbot` | `chatbot` | Cloud memory; identified telemetry; fixed model. |
| `ci-workflow` | `workflow` | Allowlisted network; no interactive leash; credentials. |

Keep template. Point `toolsets` at ToolFacts exemplars where rollup is real
(e.g. ide → filesystem + shell; researcher → fetch).

### P2 — Site agent surfaces

`site/examples/index.json` + per-slug `AGENT_FACTS.md`, `site/llms.txt`, CORS on
`/examples/*`.

### P3 — Docs / site

- `#examples` section with kind × autonomy × reach summary.
- README multi-example table; NOTES session update.
- Fix composition paths after ToolFacts slug move.

### Out of scope

- Generator implementation.
- Large directory / crawl.
- Badges / `/v`.

---

## Acceptance

- [x] All five `kind` values have an exemplar (or document intentional omission).
- [x] At least two exemplars reference ToolFacts paths/URLs.
- [x] `/llms.txt` + `/examples/index.json` ship.
- [x] Validator green on all exemplars.

---

## Completions

| Item | Status |
|---|---|
| Exemplar ladder | done |
| Site surfaces | done |
| README/site/NOTES | done |
| Validator green | done |
