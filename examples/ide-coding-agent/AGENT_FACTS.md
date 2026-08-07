---
agent_facts_version: "0.1.0"
name: IDE Coding Agent (supervised defaults)
developer: Catalyst Forge (illustrative)
kind: ide-extension
status: active
license: Apache-2.0
version: "0.1.0"
model:
  binding: configurable
  models: []
tools:
  count: 7
  executes_shell: true
  browses_web: false
  categories: [filesystem, shell, edit]
  toolsets:
    - ../../tool-facts/examples/filesystem-mcp/TOOL_FACTS.md
    - ../../tool-facts/examples/shell-mcp/TOOL_FACTS.md
reach:
  filesystem: read-write
  network: none
  destinations: []
  credentials_required: []
autonomy:
  level: supervised
  approval_required_for: [writes, shell, destructive]
  self_looping: false
memory:
  persistence: local
  location: workspace .agent/ memory files
egress:
  telemetry: anonymous
  data_shared: usage metrics
generated:
  date: 2026-08-07
  generator: hand-authored
credits:
  generated_with: https://agentfacts.dev
  built_by: "Catalyst Forge - https://www.catalystforge.com/"
---

# Agent Facts - IDE Coding Agent (supervised defaults)

| | |
|---|---|
| **Developer** | Catalyst Forge (illustrative) |
| **Kind** | ide-extension |
| **Status** | active |
| **License** | Apache-2.0 |
| **Version** | 0.1.0 |

*Illustrative IDE agent defaults: can edit the workspace and run shell, but
writes/shell/destructive actions require approval. Not a product certificate.*

## Model

| | |
|---|---|
| Binding | configurable |
| Models | (user / host selects) |

## Tools

| | |
|---|---|
| Count | 7 |
| Executes shell | true |
| Browses web | false |
| Categories | filesystem, shell, edit |
| Toolsets | filesystem-mcp, shell-mcp |

## Reach

| | |
|---|---|
| Filesystem | read-write |
| Network | none |
| Destinations | (none) |
| Credentials required | (none) |

## Autonomy

| | |
|---|---|
| Level | supervised |
| Approval required for | writes, shell, destructive |
| Self-looping | false |

## Memory

| | |
|---|---|
| Persistence | local |
| Location | workspace `.agent/` memory files |

## Egress

| | |
|---|---|
| Telemetry | anonymous |
| Data shared | usage metrics |

---
*Generated with [AgentFacts](https://agentfacts.dev) · Built by [Catalyst Forge](https://www.catalystforge.com/)*
