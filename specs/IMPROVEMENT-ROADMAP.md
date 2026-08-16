# AgentFacts — improvement roadmap (from suite value assessment)

> Derived from x-facts
> [`SUITE-VALUE-AND-NETWORK-EFFECTS.md`](../../x-facts/specs/SUITE-VALUE-AND-NETWORK-EFFECTS.md).
> AgentFacts is the **composition hub** of the AI-layer labels: model binding +
> tool rollup + leash. It should follow ToolFacts’ emitter, not lead it.

**Status:** planned.  
**Role in the flywheel:** Make “configuration, not codebase” legible; turn
ToolFacts/ModelFacts links into a full actor picture operators can gate on.

---

## Where AgentFacts stands

SPEC/schema/validator, all five `kind` exemplars, ToolFacts composition paths,
`llms.txt`, `/v#ag1` flip/copy, encode-viewer. Generator stubbed (waits on
ToolFacts MCP core). No public agent directory yet.

## Gaps vs the value thesis

| Gap | Why it matters |
|---|---|
| Generator depends on ToolFacts | Correct sequencing; do not invent a parallel MCP core. |
| Config explosion | Labeling every host tweak kills the format. |
| Weak live ModelFacts links | Composition incomplete until modelfacts.dev is live. |
| No directory | Operators need shortlists (CLI vs IDE vs autonomous). |
| Autonomy self-report | Easy to trust-wash without verification. |

## Improvements (ordered)

### Near-term

1. Deploy agentfacts.dev; hub status update when live.
2. Keep exemplars honest: shipped defaults only; note “wider host = new file.”
3. When ToolFacts generator lands, implement AgentFacts generator: config scan +
   tool rollup from ToolFacts; LLM only for judgment enums.
4. Retarget `tools.toolsets` / `model.models` to **https** URLs once siblings are
   deployed (not only sibling relative paths) — per suite
   [discovery contract](../../x-facts/specs/DISCOVERY-AND-PUBLICATION.md).

### Mid-term

5. Directory seed (shared crawl with ToolFacts): popular agent configs by kind.
6. Operator-facing presets: “tight leash”, “supervised IDE”, “autonomous research”
   as URL filters (ModelFacts selection lesson — objective fields first).
7. ForgeTrail Reference Agent as permanent dogfood; regenerate when tools change.
8. Bootstrap snippet for AGENTS.md: “read AGENT_FACTS before widening permissions.”

### Later

9. Portable badge/QR from generator.
10. Drift detection: re-scan production MCP attachment vs labeled config (enterprise).
11. Measurement story for autonomy claims — until then, no “safe agent” marketing.

## Roadmap phases

| Phase | Outcome | Exit |
|---|---|---|
| A | Live | Deploy + discoverable `llms.txt` |
| B | Emitter | Generator after ToolFacts core; validates rollups |
| C | Composition | Exemplars link live ModelFacts + ToolFacts URLs |
| D | Directory | Seeded catalog by kind / autonomy / reach |
| E | Load-bearing | A harness or CF product gates on AgentFacts fields |

## Non-goals

- Labeling MCP servers as agents (actor/instrument boundary).
- One file per ephemeral host permission toggle.
- Certified safety scores.

## Success signals

- Teams compare two agent configs with the same enums before unclipping.
- Full panel demos always include AGENT_FACTS pointing at real tool/model labels.
- “Different tools enabled ⇒ different agent” is understood without debate.

## Related

- [`REVIEW-AND-PLAN.md`](./REVIEW-AND-PLAN.md), [`PORTABLE-VIEWER.md`](./PORTABLE-VIEWER.md), [`../SPEC-ag1.md`](../SPEC-ag1.md)
- Suite index: [`x-facts/specs/ROADMAPS.md`](../../x-facts/specs/ROADMAPS.md)
