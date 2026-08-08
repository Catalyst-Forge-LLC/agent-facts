# AgentFacts Specification - v0.1.1

> *"Know what it can reach before you let it run."*

AgentFacts is a "Nutrition Facts" label for AI agents - the sibling standard to
[AppFacts](https://appfacts.dev) and [ModelFacts](https://modelfacts.dev). AppFacts
describes the **body** of software; ModelFacts describes the **brain**; AgentFacts
describes the **hands**: what an agent can do, reach, and do without asking.

**Boundary with [ToolFacts](https://toolfacts.dev):** AgentFacts labels the *actor*
(configuration, permissions, leash). ToolFacts labels the *instrument* (per-tool side
effects and reach). An `AGENT_FACTS.md` references `TOOL_FACTS.md` files the same way
it may reference `MODEL_FACTS.md`. The `tools` / `reach` groups here are the rollup;
ToolFacts is the itemized detail. An MCP server is an instrument, not an actor - it
gets `TOOL_FACTS.md`, not `AGENT_FACTS.md`.

## File

A file named `AGENT_FACTS.md`, placed at the root of an agent project or next to the
shipped configuration it labels. An application that ships an agent may also include
one (or link to the agent's canonical copy) so the hands are documented next to the
`APP_FACTS.md` and `MODEL_FACTS.md` that document body and brain.

## The Golden Rule

If a piece of information is **subjective** (*"this agent is very careful"*), it does
**not** belong in AgentFacts. If it is **objective** (*"requires human approval before
filesystem writes"*), it does. When an objective fact is not publicly disclosed, say so
explicitly (`undisclosed`) rather than guessing. Non-disclosure of reach has more teeth
here than anywhere else in the family: an agent that will not say what it can touch is
a louder red flag than a model that will not state its token count.

## Configuration, not codebase

**A label describes a configuration, not a codebase.** The same agent binary with a
different tool config is effectively a different agent. AppFacts labels a repo;
AgentFacts labels a *shipped or shippable configuration*: this binary or host, with
these tools enabled, these permission defaults, this model binding. A materially
different configuration is a new file, the same way a quantized re-release is a new
`MODEL_FACTS.md`.

## Structure

The file has two parts:

1. **YAML frontmatter** - the **sole source of truth**. Structured, validated,
   machine-parseable.
2. **Markdown body** - a **rendered view** of the frontmatter for humans
   (nutrition-label style).

Hand edits to the body are fine for local readability, but the body **MAY drift** from
the frontmatter if either side is edited by hand. Tooling does **not** verify
body-vs-frontmatter consistency; regenerating the body from the frontmatter is how you
resync.

## Required frontmatter fields

| Field | Type | Description |
|---|---|---|
| `agent_facts_version` | string | Spec version this *file* conforms to, e.g. `"0.1.0"` |
| `name` | string | Configuration name, e.g. `ForgeKit Reference Agent` |
| `developer` | string | Organization (or person) that ships this configuration |
| `kind` | enum | One of: `cli-agent`, `ide-extension`, `autonomous-service`, `chatbot`, `workflow` |
| `status` | enum | One of: `active`, `deprecated`, `preview`, `archived` |
| `license` | string | SPDX identifier or the license's official name, e.g. `"Apache-2.0"`, or `"UNKNOWN"` |
| `model` | object | Model binding - see below |
| `tools` | object | Attached tool rollup - see below |
| `reach` | object | Blast radius - see below |
| `autonomy` | object | Leash length - see below |
| `memory` | object | Retention - see below |
| `egress` | object | Outbound label - see below |
| `generated` | object | `date`, `generator` |

### `model` (the "engine")

What the agent thinks with - fixed, configurable, or bring-your-own.

| Key | Type | Required | Description |
|---|---|---|---|
| `binding` | enum | ✅ | `fixed`, `configurable`, `host-provided`, `bring-your-own` |
| `models` | string list | | Model names, and/or URLs or paths to `MODEL_FACTS.md` files |

### `tools` (the "attachments")

What the agent can invoke in this configuration. Rollup only; point at ToolFacts for
itemized detail.

| Key | Type | Required | Description |
|---|---|---|---|
| `count` | integer | ✅ | Number of tools attached in this configuration (`≥ 0`) |
| `executes_shell` | boolean | ✅ | Whether any attached capability can run shell commands |
| `browses_web` | boolean | ✅ | Whether any attached capability can browse the open web |
| `categories` | string list | | Short tags, e.g. `[guidance, templates, audit]` |
| `toolsets` | string list | | URLs (preferred) or local paths to `TOOL_FACTS.md` files (the itemized detail) |

### `reach` (the "blast radius")

Filesystem scope, network destinations, credentials required.

| Key | Type | Required | Values / description |
|---|---|---|---|
| `filesystem` | enum | ✅ | `none`, `read`, `read-write`, `scoped` |
| `network` | enum | ✅ | `none`, `allowlist`, `unrestricted` |
| `destinations` | string list | | Domains or URL patterns the agent may contact (v0.1: either form accepted) |
| `credentials_required` | string list | | Credential names required before the agent works, e.g. `[GITHUB_TOKEN]` |

### `autonomy` (the "leash")

What runs unprompted vs with approval; whether the agent self-loops.

| Key | Type | Required | Values / description |
|---|---|---|---|
| `level` | enum | ✅ | `reactive`, `supervised`, `autonomous` |
| `approval_required_for` | string list | | Closed set items: `writes`, `shell`, `network`, `credentials`, `destructive` |
| `self_looping` | boolean | ✅ | Whether the agent may continue acting without a new human prompt |

### `memory` (the "retention")

What persists across sessions, and where it lives.

| Key | Type | Required | Values / description |
|---|---|---|---|
| `persistence` | enum | ✅ | `none`, `session`, `local`, `cloud` |
| `location` | string | ✅ | Where retained state lives, or `"undisclosed"` |

### `egress` (the "outbound label")

Telemetry, logging, what leaves the machine.

| Key | Type | Required | Values / description |
|---|---|---|---|
| `telemetry` | enum | ✅ | `none`, `anonymous`, `identified`, `undisclosed` |
| `data_shared` | string | ✅ | What leaves, e.g. `none`, `prompts`, `usage metrics`, or `"undisclosed"` |

## Optional fields

| Field | Type | Description |
|---|---|---|
| `release_date` | string (date) | First public release of this configuration |
| `homepage` | string (URL) | |
| `repository` | string (URL) | Code / config repo |
| `version` | string | Configuration or package version string |
| `credits.generated_with` | string (URL) | e.g. `"https://agentfacts.dev"` |
| `credits.built_by` | string | Author name + link |

## Conventions

- **Objective facts only** (the Golden Rule). Marketing language and vibes belong in the
  README, not here.
- **`undisclosed` over omission** for facts the developer knowingly withholds -
  especially reach, egress, and credentials.
- Label **shipped defaults**. Note in prose if hosts can widen permissions; a wider
  host config is a different `AGENT_FACTS.md`.
- One `AGENT_FACTS.md` per *configuration*. Changing tools, permission defaults, or
  model binding in a material way means a new file.
- Keep the body short enough to skim in under a minute: can it touch my files, can it
  hit the network, what runs without approval, and what leaves my machine.
- **Composition:** `model.models` may point at `MODEL_FACTS.md`; `tools.toolsets` may
  point at `TOOL_FACTS.md`. Across package boundaries those refs **SHOULD** be
  `https://` URLs to the canonical files. An app that ships an agent can carry
  `APP_FACTS.md`, `MODEL_FACTS.md`, and `AGENT_FACTS.md` side by side.
- **Canonical schema URL** (matches the schema `$id`):
  [`https://agentfacts.dev/schema/agent-facts.schema.json`](https://agentfacts.dev/schema/agent-facts.schema.json)
  Source in this repo: [`site/schema/agent-facts.schema.json`](./site/schema/agent-facts.schema.json).

## Publication & discovery

Suite contract: [x-facts `DISCOVERY-AND-PUBLICATION.md`](../x-facts/specs/DISCOVERY-AND-PUBLICATION.md).

| | |
|---|---|
| **Canonical file** | Next to shipped default config (or agent project root) `AGENT_FACTS.md` |
| **Primary pointer** | Product docs and host “about this agent” / attach UI |
| **Composition** | Graph of pointers: `toolsets` and model refs **SHOULD** be canonical URLs |
| **Fallback** | `/.well-known/x-facts/agent.md` on the product homepage |

## Versioning

- **This document:** v0.1.1 (publication & discovery; see revision history).
- **Files** declare `agent_facts_version` (currently `"0.1.0"`) so tooling can evolve
  independently of the prose document.
- Required-field list may still change before v1.0.

## Revision history

| Spec doc | Notes |
|---|---|
| **0.1.1** | Publication & discovery: host pointers; URL-preferred `toolsets` / model refs; link to suite discovery contract. |
| **0.1.0** | Initial specification, formalizing [`GENESIS.md`](./GENESIS.md): frontmatter + rendered body, six fact groups (model, tools, reach, autonomy, memory, egress) plus identity fields, closed enums, `undisclosed` convention, actor/instrument boundary with ToolFacts. |

## License

CC0 - public domain. No attribution required.
