# GENESIS — AgentFacts

> Bootstrap spec for a build session. Read this whole file before writing any code.
> Sibling repos to study first: `app-facts` (the pattern's origin) and
> `model-facts` (the most recent execution of it, including `NOTES.md`,
> whose strategy review applies here almost verbatim).

## What this is

AgentFacts (agentfacts.dev — domain owned, registered 2026-07-31) is the third label
in the xFacts family:

| Label | Labels the… | Answers |
|---|---|---|
| [AppFacts](https://appfacts.dev) | **Body** | What is this app built from? |
| [ModelFacts](https://modelfacts.dev) | **Brain** | What went into this model? |
| **AgentFacts** | **Hands** | What can this agent do, reach, and do without asking? |

An agent is where an app and a model meet the world. Nobody installing an MCP server
or wiring up an autonomous agent worries about parameter counts. They worry: can it
read my filesystem, can it run shell commands, where does my data go, what does it do
without a human in the loop, and what does it phone home? No existing format answers
that crisply. `AGENT_FACTS.md` does.

Working tagline (see Open Decisions): *"Know what it can reach before you let it run."*

## The core insight (do not lose this)

**A label describes a configuration, not a codebase.** The same agent binary with a
different tool config is effectively a different agent. AppFacts labels a repo;
AgentFacts labels a *shipped or shippable configuration* of an agent: this binary or
server, with these tools enabled, these permission defaults, this model binding. A
materially different configuration is a new file, the same way a quantized re-release
is a new `MODEL_FACTS.md`.

## Family conventions (inherited, non-negotiable)

- One small `AGENT_FACTS.md`. **YAML frontmatter is the sole source of truth**,
  structured and validatable. The Markdown body is a rendered nutrition label for
  humans. Tooling never verifies body-vs-frontmatter.
- **The Golden Rule:** objective facts only. "This agent is very careful" belongs in a
  README. "Requires human approval before filesystem writes" belongs here.
- **`undisclosed` over omission** for facts a developer knowingly withholds. It has
  more teeth here than anywhere else in the family: an agent that won't say what it
  can reach is a louder red flag than a model that won't state its token count.
- **Closed enums for judgment fields** so files are comparable across agents.
- **Licensing:** spec & schema CC0, tooling MIT.
- **Design:** the AppFacts design system with a distinct accent. ModelFacts uses
  violet (`--accent: #7c5cf0`). Suggest a warm amber/orange family for AgentFacts
  (hands, action); final pick is an open decision.
- **File format version starts at `"0.1.0"`** with the same versioning posture:
  required fields may shift before v1.0.
- Workspace conventions: **pnpm + TypeScript + ESM only** for Node code. Commit after
  substantive work. **Never push without the owner's explicit ask.**

## Draft fact taxonomy

Formalize this in `SPEC.md` the way ModelFacts formalized its draft. Six groups:

| Group | The label's… | Answers |
|---|---|---|
| `identity` | Product name | What kind of agent is this, who ships it? |
| `model` | Engine | What does it think with? Fixed, configurable, or bring-your-own? |
| `tools` | Attachments | What can it invoke? Shell? Browser? Which MCP tools? |
| `reach` | Blast radius | Filesystem scope, network destinations, credentials required. |
| `autonomy` | Leash length | What runs unprompted vs with approval? Does it self-loop? |
| `memory` | Retention | What persists across sessions, and where does it live? |
| `egress` | Outbound label | Telemetry, logging, what leaves the machine. |

Frontmatter sketch (starting point, not gospel — the build session owns the enums):

```yaml
---
agent_facts_version: "0.1.0"
name: ForgeKit MCP Server
developer: Catalyst Forge
kind: mcp-server        # mcp-server | cli-agent | ide-extension | autonomous-service | chatbot | workflow
status: active
license: Apache-2.0
model:
  binding: host-provided   # fixed | configurable | host-provided | bring-your-own
  models: []               # names, or URLs to MODEL_FACTS.md files (composition!)
tools:
  count: 29
  executes_shell: false
  browses_web: false
  categories: [guidance, templates, audit]
reach:
  filesystem: none         # none | read | read-write | scoped
  network: none            # none | allowlist | unrestricted
  destinations: []
  credentials_required: []
autonomy:
  level: reactive          # reactive | supervised | autonomous
  approval_required_for: []   # e.g. [writes, shell, network]
  self_looping: false
memory:
  persistence: none        # none | session | local | cloud
  location: undisclosed
egress:
  telemetry: none          # none | anonymous | identified | undisclosed
  data_shared: none
generated:
  date: 2026-07-31
  generator: hand-authored
---
```

**Composition is a family feature:** `model.models` may point at `MODEL_FACTS.md`
URLs, and an app that ships an agent can carry `APP_FACTS.md`, `MODEL_FACTS.md`, and
`AGENT_FACTS.md` side by side. Say this on the site; it is the ecosystem story.

## Generator strategy: deterministic first, LLM second

The ModelFacts lesson, doubled: hard facts never come from prose. AgentFacts has an
advantage no sibling has — **agents are introspectable**:

1. **MCP handshake** (the killer source): connect to an MCP server, call
   `tools/list`, and the tool count, names, and schemas are deterministic ground
   truth. Tool input schemas often reveal reach (paths, URLs, commands) mechanically.
2. **Config files:** `mcp.json` / client configs, agent manifests, permission
   settings files.
3. **Package metadata:** name, license, version from `package.json` / `pyproject.toml`.
4. LLM curation (local-first via Ollama, same provider set as the ModelFacts
   generator) only for judgment fields from README/docs text, sanitized against the
   schema's enums, with architecture-of-reach facts never overridable.

Reuse the ModelFacts generator's structure (`generator/src/sources/` adapters
returning a common facts shape, self-validation against the schema before writing).

## Launch strategy

Same as the ModelFacts verdict: a standard asking for adoption loses; a useful site
that emits the standard wins.

1. **Dogfood first:** ForgeKit's MCP server ships the first real `AGENT_FACTS.md`,
   generated by our own tool. Downpress and any other in-house agents follow.
2. **Directory at launch:** run the generator across popular public MCP servers
   (the official registry and top GitHub lists), human-review judgment fields, and
   launch agentfacts.dev as a "what can this server actually touch" comparison
   directory on day one. That is the SEO surface and the HN story — especially the
   `undisclosed` and `reach` columns.
3. **Badge/portable label later**, mirroring AppFacts (`SPEC-af1.md` /
   `BADGE_SPEC.md` show the pattern: zlib+base64url `/v#` payload, no backend).

## Honest headwinds (carry these into NOTES.md)

- Anthropic/OpenAI may ship an official agent manifest and steamroll the niche.
  Mitigation: be first with the vocabulary, be cited, keep the spec CC0 so an
  official standard can absorb it with zero friction.
- Self-reported autonomy/safety claims without verification drift toward
  trust-washing. Same rule as ModelFacts: the word "certified" stays out of
  everything public until there's a harness that measures instead of asks. The MCP
  introspection path partially solves this — verify tool claims mechanically.
- Configuration explosion: resist labeling every possible config. Label the shipped
  defaults; note that hosts can change them.

## Repo layout (mirror model-facts)

```
agent-facts/
  GENESIS.md            (this file)
  SPEC.md               formal spec v0.1.0
  README.md             family-style: centered header, tagline, what-is-this
  NOTES.md              maintainer/agent state snapshot, kept current
  examples/             AGENT_FACTS.md (worked: ForgeKit MCP), AGENT_FACTS.template.md
  validator/            TS ESM CLI, tsx + ajv + yaml, CI-friendly exit codes
  generator/            TS ESM CLI, sources/ adapters, MCP introspection first
  site/                 static, Cloudflare Pages root=site, no build step
    schema/agent-facts.schema.json   (canonical, $id = agentfacts.dev URL)
```

GitHub org: `Catalyst-Forge-LLC`, repo `agent-facts` (owner creates and pushes).

## Milestones

1. `SPEC.md` v0.1.0 + canonical JSON Schema + template + worked ForgeKit example
   (hand-authored, passes validation).
2. Validator CLI.
3. Generator: MCP introspection source + local config source, optional LLM curation.
4. Site landing page at agentfacts.dev (Cloudflare Pages) + schema served.
5. Directory seed: 50–100 labeled public MCP servers, human-reviewed.
6. Badge + portable label. Cross-link all three sites' footers as a family.

## Acceptance criteria

- The worked example and template both pass the validator.
- The generator, pointed at ForgeKit's MCP server, produces a draft whose
  deterministic fields (tool count, names) are exactly correct with no LLM involved.
- A stranger can read `AGENT_FACTS.md` for an MCP server and answer, in under a
  minute: can it touch my files, can it hit the network, what runs without approval,
  and what leaves my machine.
- No em dashes, no AI-smell vocabulary anywhere on the site or README. Match the
  AppFacts/ModelFacts register.

## Open decisions

1. **Tagline.** Candidates: "Know what it can reach before you let it run." /
   "Know the hands before you shake them." / "Read the leash before you unclip it."
2. **Accent color.** Amber/orange suggested; must sit well next to AppFacts' accent
   and ModelFacts violet on a shared family footer.
3. **`kind` enum finalization** — is a Cursor-style IDE agent one kind or several?
4. Whether `reach.destinations` lists domains only or full URL patterns.
