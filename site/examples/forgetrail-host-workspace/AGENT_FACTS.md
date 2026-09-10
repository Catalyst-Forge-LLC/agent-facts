---
agent_facts_version: "0.1.0"
name: ForgeTrail Reference Agent (host workspace)
developer: Catalyst Forge (illustrative)
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
  count: 31
  executes_shell: true
  browses_web: false
  categories: [guidance, templates, audit, filesystem, shell]
  toolsets:
    - ../../tool-facts/examples/forgetrail-mcp/TOOL_FACTS.md
reach:
  filesystem: read-write
  network: none
  destinations: []
  credentials_required: []
autonomy:
  level: supervised
  approval_required_for: [writes, shell]
  self_looping: false
memory:
  persistence: none
  location: undisclosed
egress:
  telemetry: undisclosed
  data_shared: undisclosed
generated:
  date: 2026-09-10
  generator: hand-authored
credits:
  generated_with: https://agentfacts.dev
  built_by: "Catalyst Forge - https://www.catalystforge.com/"
---

# Agent Facts - ForgeTrail Reference Agent (host workspace)

| | |
|---|---|
| **Developer** | Catalyst Forge (illustrative) |
| **Kind** | cli-agent |
| **Status** | active |
| **License** | Apache-2.0 |
| **Version** | 0.1.0 |

*Illustrative second configuration of the same ForgeTrail-attached agent. The
host also grants workspace read-write and shell. That attached capability is
why this file exists. It does not mean the narrower ForgeTrail-MCP-only label
constrains this host. Tool count 31 is illustrative (29 ForgeTrail tools plus
host workspace and shell). Host workspace tools are not given their own
ToolFacts files here. Configured approval for writes and shell is declared
intent, not proof the host enforces it on every run.*

## Model

| | |
|---|---|
| Binding | host-provided |
| Models | (host chooses) |

## Tools

| | |
|---|---|
| Count | 31 |
| Executes shell | true |
| Browses web | false |
| Categories | guidance, templates, audit, filesystem, shell |
| Toolsets | `forgetrail-mcp` plus unlabeled host workspace tools |

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
| Approval required for | writes, shell |
| Self-looping | false |

## Memory

| | |
|---|---|
| Persistence | none |
| Location | undisclosed |

## Egress

| | |
|---|---|
| Telemetry | undisclosed |
| Data shared | undisclosed |

---
*Generated with [AgentFacts](https://agentfacts.dev) · Built by [Catalyst Forge](https://www.catalystforge.com/)*
