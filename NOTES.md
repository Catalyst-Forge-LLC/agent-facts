# Project Notes - AgentFacts

> Working notes for maintainers/agents picking up this project. Not published to the site.
> Last updated: 2026-08-03 (v0.1 local scaffold).

## What this is

AgentFacts (agentfacts.dev) is a "Nutrition Facts" label for AI agents - third label
in the xFacts family after [AppFacts](https://appfacts.dev) and
[ModelFacts](https://modelfacts.dev). AppFacts = body, ModelFacts = brain,
AgentFacts = hands. Tagline: *"Know what it can reach before you let it run."*

**Actor vs instrument:** AgentFacts labels the *actor* (configuration, permissions,
leash). ToolFacts (`tool-facts`) labels the *instrument* (per-tool side
effects). MCP servers get ToolFacts, not AgentFacts. The worked example is a coding
agent *configuration* that uses the ForgeKit MCP server via `tools.toolsets`.

Suite vision: `catalyst-forge/docs/xfacts-suite-vision.md`.

## State as of 2026-08-03

Local scaffold on `main`. Remote intended at
`git@github.com:Catalyst-Forge-LLC/agent-facts.git` (owner creates and pushes -
**never push without explicit ask**).

| Piece | Where | Status |
|---|---|---|
| Bootstrap | `GENESIS.md` | Authoritative intent; kept. |
| Formal spec v0.1.0 | `SPEC.md` | Done. Six fact groups: model, tools, reach, autonomy, memory, egress (+ identity). Closed enums; `undisclosed` convention; ToolFacts boundary. |
| Canonical JSON Schema | `site/schema/agent-facts.schema.json` | Done (draft-07). `$id` = agentfacts.dev URL. |
| Examples | `examples/AGENT_FACTS.md` (ForgeKit Reference Agent), `examples/AGENT_FACTS.template.md` | Both pass validation. |
| Validator CLI | `validator/` | TypeScript ESM, pnpm, tsx + ajv + yaml. CI-friendly exit codes. |
| Generator CLI | `generator/` | README stub only. Build after ToolFacts MCP introspection core. |
| Site | `site/` | Static, Cloudflare Pages-ready (root = `site`, no build). Amber accent (`#f6ad55` / `#fbd38d`). |

## Key design decisions (and why)

- **Frontmatter is the sole source of truth; the Markdown body is a rendered view** -
  identical to AppFacts / ModelFacts. Body may drift; tooling doesn't verify
  body-vs-frontmatter.
- **Configuration, not codebase.** Same binary + different tools/permissions = new
  file. Resist labeling every host tweak; label shipped defaults.
- **Golden Rule + `undisclosed`.** Reach/egress non-disclosure is the teeth.
- **Closed enums** for `kind`, bindings, reach, autonomy, memory, telemetry,
  `approval_required_for` so files are comparable.
- **Composition:** `model.models` → `MODEL_FACTS.md`; `tools.toolsets` →
  `TOOL_FACTS.md`. Ecosystem story on the site.
- **Worked example is not an MCP server.** ForgeKit Reference Agent (`kind: cli-agent`)
  attaches ForgeKit via `toolsets`; itemized tools live in ToolFacts. GENESIS sketch
  kept tight leash (`filesystem: none`, no shell/browse from attached tools).
- **Licensing:** spec & schema CC0, tooling MIT.
- **pnpm + TypeScript + ESM only.** Commit after substantive work; never push without
  ask.

## Honest headwinds (from GENESIS)

- Anthropic/OpenAI may ship an official agent manifest. Mitigation: be first with the
  vocabulary, keep the spec CC0 so an official standard can absorb it.
- Self-reported autonomy/safety without verification drifts toward trust-washing. Keep
  "certified" out of public copy until a harness measures. MCP introspection
  partially verifies tool claims.
- Configuration explosion: label shipped defaults; note hosts can change them.

## Strategy (ModelFacts lesson, applied)

A standard asking for adoption loses; a useful site that emits the standard wins.
Dogfood the ForgeKit reference config, then seed a directory of labeled public agents
(CLI / IDE / autonomous / chatbot) with human-reviewed judgment fields. Shared MCP
ecosystem crawl feeds ToolFacts (itemized) and AgentFacts (rollups).

## Next steps (rough priority)

1. Scaffold ToolFacts + its MCP introspection generator (shared core).
2. Implement AgentFacts generator: config + MCP rollup, optional LLM for judgment
   fields only; self-validate before write.
3. Owner: create GitHub repo, push, Cloudflare Pages (root = `site`) + DNS for
   agentfacts.dev.
4. Directory seed (with ToolFacts crawl): 50–100 labeled agents / configs.
5. Badge + portable label later (AppFacts `af1` pattern).

## Open decisions

1. **Tagline.** Picked for v0.1 site/README: "Know what it can reach before you let
   it run." Alternatives still in GENESIS.
2. **Accent.** Picked for v0.1: amber `#f6ad55` / soft `#fbd38d`. Confirm on four-site
   family footer when ToolFacts/SkillFacts land.
3. **`kind` enum.** v0.1: `cli-agent | ide-extension | autonomous-service | chatbot |
   workflow`. Is a Cursor-style IDE agent one kind or several?
4. **`reach.destinations`.** v0.1 accepts domains or full URL patterns; tighten later.

## Gotchas / environment notes

- Worked example `toolsets` points at `../tool-facts/examples/TOOL_FACTS.md` (sibling
  not scaffolded yet). Path is intentional composition; file may be missing until
  ToolFacts milestone 1.
- Validator mirrors ModelFacts: named `Ajv` import, `moduleResolution: "Bundler"`,
  schema path `../../site/schema/agent-facts.schema.json`.
- Do not use an MCP server as an AgentFacts worked example (actor/instrument boundary).
