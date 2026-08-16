# AgentFacts generator (stub)

Not implemented in this milestone. The validator, spec, schema, and hand-authored
examples ship first.

## Planned shape

Mirror [ModelFacts generator](https://github.com/Catalyst-Forge-LLC/model-facts/tree/main/generator):

- TypeScript ESM CLI (`pnpm generate …`)
- `src/sources/` adapters returning a common facts shape
- Self-validation against [`site/schema/agent-facts.schema.json`](../site/schema/agent-facts.schema.json) before writing

## Planned sources (priority)

1. **MCP handshake** - connect, `tools/list`: tool count and names as deterministic
   ground truth. Prefer reusing the ToolFacts introspection core once that sibling
   lands (`tool-facts`); AgentFacts rolls up what ToolFacts itemizes.
2. **Config files** - `mcp.json` / client configs, agent manifests, permission
   settings.
3. **Package metadata** - name, license, version from `package.json` / `pyproject.toml`.
4. **LLM curation last** - local-first via Ollama (same provider set as ModelFacts),
   only for judgment fields from README/docs, sanitized against schema enums.
   Architecture-of-reach facts are never overridable by the LLM.

## Sequencing

Build the ToolFacts generator before this one. Then point AgentFacts at a reference
agent config (ForgeTrail MCP attached) and require deterministic fields (tool count,
names) to match with no LLM involved.

## Dogfood target

`examples/AGENT_FACTS.md` - ForgeTrail Reference Agent (`kind: cli-agent`), not the
MCP server itself.
