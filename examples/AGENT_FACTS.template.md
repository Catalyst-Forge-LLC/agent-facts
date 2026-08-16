---
agent_facts_version: "0.1.0"
name: Your Agent Configuration
developer: Your Org
kind: cli-agent          # cli-agent | ide-extension | autonomous-service | chatbot | workflow
status: active
license: Apache-2.0
# version: "1.0.0"
# release_date: 2026-01-01
# homepage: https://example.com
# repository: https://github.com/org/agent
model:
  binding: host-provided   # fixed | configurable | host-provided | bring-your-own
  # models:
  #   - https://modelfacts.dev/.../MODEL_FACTS.md
tools:
  count: 0
  executes_shell: false
  browses_web: false
  # categories: [guidance, shell]
  # toolsets:
  #   - ../tool-facts/examples/forgetrail-mcp/TOOL_FACTS.md
reach:
  filesystem: none         # none | read | read-write | scoped
  network: none            # none | allowlist | unrestricted
  # destinations: []
  # credentials_required: []
autonomy:
  level: reactive          # reactive | supervised | autonomous
  # approval_required_for: [writes, shell]
  self_looping: false
memory:
  persistence: none        # none | session | local | cloud
  location: undisclosed
egress:
  telemetry: none          # none | anonymous | identified | undisclosed
  data_shared: none
generated:
  date: 2026-08-03
  generator: hand-authored
# credits:
#   generated_with: https://agentfacts.dev
#   built_by: "Your Name - https://example.com"
---

# Agent Facts - Your Agent Configuration

| | |
|---|---|
| **Developer** | Your Org |
| **Kind** | cli-agent |
| **Status** | active |
| **License** | Apache-2.0 |

## Model

| | |
|---|---|
| Binding | host-provided |

## Tools

| | |
|---|---|
| Count | 0 |
| Executes shell | false |
| Browses web | false |

## Reach

| | |
|---|---|
| Filesystem | none |
| Network | none |

## Autonomy

| | |
|---|---|
| Level | reactive |
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
*Generated with [AgentFacts](https://agentfacts.dev)*
