---
agent_facts_version: "0.1.0"
name: Customer Support Chatbot
developer: Catalyst Forge (illustrative)
kind: chatbot
status: active
license: UNKNOWN
version: "2.1.0"
model:
  binding: fixed
  models: [undisclosed]
tools:
  count: 4
  executes_shell: false
  browses_web: false
  categories: [kb-search, ticket, refund-lookup]
reach:
  filesystem: none
  network: allowlist
  destinations: [api.example-support.invalid, kb.example-support.invalid]
  credentials_required: [SUPPORT_API_KEY]
autonomy:
  level: reactive
  approval_required_for: [credentials]
  self_looping: false
memory:
  persistence: cloud
  location: vendor conversation store (undisclosed region)
egress:
  telemetry: identified
  data_shared: prompts, conversation transcripts, usage metrics
generated:
  date: 2026-08-07
  generator: hand-authored
credits:
  generated_with: https://agentfacts.dev
  built_by: "Catalyst Forge - https://www.catalystforge.com/"
---

# Agent Facts - Customer Support Chatbot

| | |
|---|---|
| **Developer** | Catalyst Forge (illustrative) |
| **Kind** | chatbot |
| **Status** | active |
| **License** | UNKNOWN |
| **Version** | 2.1.0 |

*Illustrative hosted chatbot: no shell/FS, allowlisted vendor APIs, cloud
transcript retention, identified telemetry. License and model names often stay
`UNKNOWN` / `undisclosed` for closed products - that silence is the signal.*

## Model

| | |
|---|---|
| Binding | fixed |
| Models | undisclosed |

## Tools

| | |
|---|---|
| Count | 4 |
| Executes shell | false |
| Browses web | false |
| Categories | kb-search, ticket, refund-lookup |

## Reach

| | |
|---|---|
| Filesystem | none |
| Network | allowlist |
| Destinations | api.example-support.invalid, kb.example-support.invalid |
| Credentials required | SUPPORT_API_KEY |

## Autonomy

| | |
|---|---|
| Level | reactive |
| Approval required for | credentials |
| Self-looping | false |

## Memory

| | |
|---|---|
| Persistence | cloud |
| Location | vendor conversation store (undisclosed region) |

## Egress

| | |
|---|---|
| Telemetry | identified |
| Data shared | prompts, conversation transcripts, usage metrics |

---
*Generated with [AgentFacts](https://agentfacts.dev) · Built by [Catalyst Forge](https://www.catalystforge.com/)*
