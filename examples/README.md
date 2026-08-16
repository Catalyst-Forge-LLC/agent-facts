# AgentFacts exemplars

One configuration per `kind` in the v0.1 enum.

| Slug | Kind | Autonomy | FS | Network |
|---|---|---|---|---|
| [forgetrail-reference](./forgetrail-reference/AGENT_FACTS.md) | cli-agent | reactive | none | none |
| [ide-coding-agent](./ide-coding-agent/AGENT_FACTS.md) | ide-extension | supervised | read-write | none |
| [autonomous-researcher](./autonomous-researcher/AGENT_FACTS.md) | autonomous-service | autonomous | scoped | unrestricted |
| [support-chatbot](./support-chatbot/AGENT_FACTS.md) | chatbot | reactive | none | allowlist |
| [ci-workflow](./ci-workflow/AGENT_FACTS.md) | workflow | supervised | none | allowlist |

Machine index: [`index.json`](./index.json). Template: [`AGENT_FACTS.template.md`](./AGENT_FACTS.template.md).

The flat [`AGENT_FACTS.md`](./AGENT_FACTS.md) remains the ForgeTrail dogfood copy for
older links; prefer slug paths for new references.
