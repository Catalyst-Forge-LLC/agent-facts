---
agent_facts_version: "0.1.0"
name: CI Triage Workflow Agent
developer: Catalyst Forge (illustrative)
kind: workflow
status: active
license: Apache-2.0
version: "0.3.0"
model:
  binding: bring-your-own
  models: []
tools:
  count: 5
  executes_shell: false
  browses_web: false
  categories: [github, triage]
  toolsets:
    - ../../tool-facts/examples/github-mcp/TOOL_FACTS.md
reach:
  filesystem: none
  network: allowlist
  destinations: [api.github.com]
  credentials_required: [GITHUB_TOKEN]
autonomy:
  level: supervised
  approval_required_for: [writes, destructive]
  self_looping: false
memory:
  persistence: session
  location: CI job logs only
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

# Agent Facts - CI Triage Workflow Agent

| | |
|---|---|
| **Developer** | Catalyst Forge (illustrative) |
| **Kind** | workflow |
| **Status** | active |
| **License** | Apache-2.0 |
| **Version** | 0.3.0 |

*Illustrative CI workflow config: runs in a pipeline with GitHub tool access,
BYO model, session-only memory. Writes and destructive GitHub actions still
require approval even inside automation.*

## Model

| | |
|---|---|
| Binding | bring-your-own |
| Models | (pipeline secret / config) |

## Tools

| | |
|---|---|
| Count | 5 |
| Executes shell | false |
| Browses web | false |
| Categories | github, triage |
| Toolsets | github-mcp |

## Reach

| | |
|---|---|
| Filesystem | none |
| Network | allowlist |
| Destinations | api.github.com |
| Credentials required | GITHUB_TOKEN |

## Autonomy

| | |
|---|---|
| Level | supervised |
| Approval required for | writes, destructive |
| Self-looping | false |

## Memory

| | |
|---|---|
| Persistence | session |
| Location | CI job logs only |

## Egress

| | |
|---|---|
| Telemetry | anonymous |
| Data shared | usage metrics |

---
*Generated with [AgentFacts](https://agentfacts.dev) · Built by [Catalyst Forge](https://www.catalystforge.com/)*
