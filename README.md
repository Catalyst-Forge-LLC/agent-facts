<h1 align="center">AgentFacts</h1>

<p align="center">
  <strong>A "Nutrition Facts" label for AI agents.</strong>
</p>

<p align="center">
  A tiny, standardized <code>AGENT_FACTS.md</code> that labels a
  <em>configuration</em>, not a codebase, and answers one question in under a minute:
  <em>what can this agent reach before I let it run?</em>
</p>

<p align="center">
  <a href="https://agentfacts.dev">agentfacts.dev</a> ·
  <a href="./SPEC.md">Spec</a> ·
  <a href="https://agentfacts.dev/schema/agent-facts.schema.json">Schema</a> ·
  <a href="./examples/AGENT_FACTS.md">Example</a>
</p>

---

## What is this?

[AppFacts](https://appfacts.dev) labels the **body** of software. [ModelFacts](https://modelfacts.dev) labels the **brain**. **AgentFacts** labels the **hands**: what an agent can do, reach, and do without asking. [ToolFacts](https://toolfacts.dev) labels each **instrument** (per-tool side effects); AgentFacts rolls those up at the actor level.

**A label describes a configuration, not a codebase.** The same agent binary with different tools or permission defaults is a different agent. Label shipped defaults; a wider host policy is a new file.

**The Golden Rule:** if a piece of information is *subjective* ("this agent is very careful"), it does not belong in AgentFacts. If it is *objective* ("requires human approval before filesystem writes"), it does. When a fact isn't public, the file says `undisclosed`. An agent that will not say what it can touch is a louder red flag than a model that will not state its token count.

Useful for:

- **Operators** deciding whether to unclip an agent on a real workspace
- **Teams** comparing leash length, reach, and egress across configs
- **Harnesses** that need a structured rollup before attaching toolsets
- **Anyone** who wants ToolFacts detail behind an agent-level summary

## What it looks like

Every `AGENT_FACTS.md` has two halves. The **YAML frontmatter is the source of truth** - structured and validatable. The **Markdown body is a rendered label** for humans.

```markdown
---
agent_facts_version: "0.1.0"
name: ForgeKit Reference Agent
developer: Catalyst Forge
kind: cli-agent
status: active
license: Apache-2.0
model:
  binding: host-provided
tools:
  count: 29
  executes_shell: false
  browses_web: false
  toolsets:
    - ../tool-facts/examples/TOOL_FACTS.md
reach:
  filesystem: none
  network: none
autonomy:
  level: reactive
  self_looping: false
memory:
  persistence: none
  location: undisclosed
egress:
  telemetry: none
  data_shared: none
generated:
  date: 2026-08-03
  generator: hand-authored
---

# Agent Facts - ForgeKit Reference Agent

| | |
|---|---|
| Filesystem | none |
| Network | none |
| ... | ... |
```

See the [full worked example](./examples/AGENT_FACTS.md) (ForgeKit Reference Agent: a coding CLI config that *uses* the ForgeKit MCP server; the server itself is ToolFacts), the [template](./examples/AGENT_FACTS.template.md), and the [specification](./SPEC.md).

| Group | The label's… | Answers |
|---|---|---|
| `model` | Engine | Fixed, configurable, host-provided, or bring-your-own? |
| `tools` | Attachments | What can it invoke? Shell? Browser? Which toolsets? |
| `reach` | Blast radius | Filesystem scope, network, credentials. |
| `autonomy` | Leash | What runs unprompted vs with approval? Self-looping? |
| `memory` | Retention | What persists, and where? |
| `egress` | Outbound | Telemetry, logging, what leaves the machine. |

## Validating a file

The frontmatter conforms to [`site/schema/agent-facts.schema.json`](./site/schema/agent-facts.schema.json) (served at [agentfacts.dev/schema/agent-facts.schema.json](https://agentfacts.dev/schema/agent-facts.schema.json)) - any draft-07 validator works. This repo ships a small TypeScript CLI:

```bash
cd validator
pnpm install

# exit code 1 on any failure - CI-friendly
pnpm validate ../examples/AGENT_FACTS.md
pnpm validate ../examples/AGENT_FACTS.template.md
```

## Generating a label

The [generator](./generator/) is stubbed for this milestone. Planned sources: MCP `tools/list` (after ToolFacts ships the shared introspection core), local agent / MCP client configs, and package metadata. Optional LLM curation for judgment fields only, sanitized against the schema enums.

## Roadmap

- [x] Spec v0.1.0, canonical JSON Schema, worked example + template
- [x] Schema validator CLI (TypeScript)
- [ ] Generator: MCP introspection + config scan, optional LLM curation
- [ ] Site directory of labeled public agents
- [ ] Portable visual label and badges, mirroring AppFacts
- [ ] Family footer cross-links across AppFacts / ModelFacts / AgentFacts / ToolFacts

## Website

The static site for [agentfacts.dev](https://agentfacts.dev) lives in [`site/`](./site/). On Cloudflare Pages, set the project root to `site` - no build step. Local preview: `npx serve site -p 3003`.

| Path | Purpose |
|---|---|
| [`site/index.html`](./site/index.html) | Marketing / docs landing |
| [`site/schema/agent-facts.schema.json`](./site/schema/agent-facts.schema.json) | Canonical JSON Schema |

## Relationship to the family

Same philosophy, same file shape (frontmatter + rendered body), same origin. AppFacts = body, ModelFacts = brain, AgentFacts = hands, ToolFacts = toolbelt. An app that ships an agent can carry the labels side by side. `model.models` may point at `MODEL_FACTS.md`; `tools.toolsets` may point at `TOOL_FACTS.md`.

## Contributing

This is **v0.1.0** - the spec's required fields may still shift before v1.0. Issues and proposals on field taxonomy, `kind` enums, and reach conventions are welcome.

## License

- **Spec & schema:** [CC0](https://creativecommons.org/publicdomain/zero/1.0/) (public domain) - adopt them freely, no attribution needed.
- **Tooling (validator):** MIT.

---

<p align="center">
  Part of <a href="https://agentfacts.dev">agentfacts.dev</a> · Sibling of
  <a href="https://appfacts.dev">appfacts.dev</a> ·
  <a href="https://modelfacts.dev">modelfacts.dev</a> ·
  <a href="https://toolfacts.dev">toolfacts.dev</a>
</p>

<p align="center">
  <em>"Know what it can reach before you let it run."</em>
</p>
