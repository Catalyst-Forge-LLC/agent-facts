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
  <a href="./examples/">Examples</a> ·
  <a href="https://agentfacts.dev/llms.txt">llms.txt</a>
</p>

---

## What is this?

[AppFacts](https://appfacts.dev) labels the **body**. [ModelFacts](https://modelfacts.dev)
labels the **brain**. **AgentFacts** labels the **hands**: what an agent can do, reach,
and do without asking. [ToolFacts](https://toolfacts.dev) labels each **instrument**;
AgentFacts rolls those up at the actor level. [SkillFacts](https://skillfacts.dev) labels
the **playbook** an agent may be taught to follow.

**A label describes a configuration, not a codebase.** The same agent binary with different
tools or permission defaults is a different agent.

**The Golden Rule:** subjective vibes stay out; objective reach/autonomy/egress stay in.
`undisclosed` beats guessing. An agent that will not say what it can touch is a loud red flag.

## Exemplars

One configuration per `kind`:

| Slug | Kind | Autonomy | FS | Network |
|---|---|---|---|---|
| [forgetrail-reference](./examples/forgetrail-reference/AGENT_FACTS.md) | cli-agent | reactive | none | none |
| [ide-coding-agent](./examples/ide-coding-agent/AGENT_FACTS.md) | ide-extension | supervised | read-write | none |
| [autonomous-researcher](./examples/autonomous-researcher/AGENT_FACTS.md) | autonomous-service | autonomous | scoped | unrestricted |
| [support-chatbot](./examples/support-chatbot/AGENT_FACTS.md) | chatbot | reactive | none | allowlist |
| [ci-workflow](./examples/ci-workflow/AGENT_FACTS.md) | workflow | supervised | none | allowlist |

Catalog: [`examples/index.json`](./examples/index.json). Template:
[`examples/AGENT_FACTS.template.md`](./examples/AGENT_FACTS.template.md).

## Fact groups

| Group | Answers |
|---|---|
| `model` | Fixed, configurable, host-provided, or bring-your-own? |
| `tools` | What can it invoke? Shell? Browser? Which ToolFacts? |
| `reach` | Filesystem scope, network, credentials. |
| `autonomy` | What runs unprompted vs with approval? Self-looping? |
| `memory` | What persists, and where? |
| `egress` | Telemetry and what leaves the machine. |

## Validating a file

```bash
cd validator
pnpm install
pnpm validate ../examples/forgetrail-reference/AGENT_FACTS.md
pnpm validate ../examples/*/AGENT_FACTS.md
```

## Generating a label

Generator stubbed. Planned after ToolFacts MCP introspection core. See
[`generator/README.md`](./generator/README.md).

## Roadmap

- [x] Spec v0.1.0, schema, template, validator
- [x] Multi-kind exemplar ladder + `/examples/index.json` + `llms.txt`
- [x] Portable `/v#ag1.…` viewer with flip-to-raw + copy; exemplars deep-link in
- [ ] Generator
- [ ] Public agent directory
- [ ] QR / badge emission from generator

## Website

| Path | Purpose |
|---|---|
| [`site/index.html`](./site/index.html) | Landing |
| [`site/schema/`](./site/schema/) | JSON Schema |
| [`site/examples/`](./site/examples/) | Fetchable exemplars |
| [`site/llms.txt`](./site/llms.txt) | Agent entrypoint |

Session plan: [`specs/REVIEW-AND-PLAN.md`](./specs/REVIEW-AND-PLAN.md).

## License

- **Spec & schema:** CC0
- **Tooling (validator):** MIT

---

<p align="center">
  <em>"Know what it can reach before you let it run."</em>
</p>
