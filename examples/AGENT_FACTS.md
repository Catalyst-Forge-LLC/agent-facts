---
agent_facts_version: "0.1.0"
name: ForgeKit Reference Agent
developer: Catalyst Forge
kind: cli-agent
status: active
license: Apache-2.0
version: "0.1.0"
homepage: https://www.catalystforge.com/
repository: https://github.com/Catalyst-Forge-LLC/forge-kit
model:
  binding: host-provided
  models: []
tools:
  count: 29
  executes_shell: false
  browses_web: false
  categories: [guidance, templates, audit]
  toolsets:
    - ../tool-facts/examples/TOOL_FACTS.md
reach:
  filesystem: none
  network: none
  destinations: []
  credentials_required: []
autonomy:
  level: reactive
  approval_required_for: []
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
credits:
  generated_with: https://agentfacts.dev
  built_by: "Catalyst Forge - https://www.catalystforge.com/"
---

# Agent Facts - ForgeKit Reference Agent

| | |
|---|---|
| **Developer** | Catalyst Forge |
| **Kind** | cli-agent |
| **Status** | active |
| **License** | Apache-2.0 |
| **Version** | 0.1.0 |

*Shipped configuration: a coding CLI agent with the ForgeKit MCP server attached as its
toolset. The MCP server itself is an instrument and is labeled separately in
[`TOOL_FACTS.md`](../../tool-facts/examples/TOOL_FACTS.md) (ToolFacts). This file labels
the actor configuration.*

## Model

| | |
|---|---|
| Binding | host-provided |
| Models | (host chooses) |

## Tools

| | |
|---|---|
| Count | 29 |
| Executes shell | false |
| Browses web | false |
| Categories | guidance, templates, audit |
| Toolsets | `../tool-facts/examples/TOOL_FACTS.md` |

## Reach

| | |
|---|---|
| Filesystem | none |
| Network | none |
| Destinations | (none) |
| Credentials required | (none) |

## Autonomy

| | |
|---|---|
| Level | reactive |
| Approval required for | (none beyond host defaults) |
| Self-looping | false |

## Memory

| | |
|---|---|
| Persistence | none |
| Location | undisclosed |

## Egress

| | |
|---|---|
| Telemetry | none |
| Data shared | none |

---
*Generated with [AgentFacts](https://agentfacts.dev) · Built by [Catalyst Forge](https://www.catalystforge.com/)*
