# AgentFacts validator

A tiny CLI that checks the YAML frontmatter of an `AGENT_FACTS.md` file against the
canonical JSON Schema ([`site/schema/agent-facts.schema.json`](../site/schema/agent-facts.schema.json),
served at [agentfacts.dev/schema/agent-facts.schema.json](https://agentfacts.dev/schema/agent-facts.schema.json)).

The command is `agentfacts validate <file>` from `@xfacts/agentfacts` (Node 22.18 or newer). In this repository, `pnpm validate` runs the same program.

## Usage

```bash
cd validator
pnpm install

# validate one or more files (exit code 1 on any failure - CI-friendly)
pnpm validate ../examples/AGENT_FACTS.md
pnpm validate ../examples/AGENT_FACTS.template.md
pnpm validate path/to/your/AGENT_FACTS.md
```

TypeScript, ESM. The published command is compiled JavaScript. Uses [ajv](https://ajv.js.org/) (draft-07) with
`ajv-formats` and [yaml](https://eemeli.org/yaml/).
