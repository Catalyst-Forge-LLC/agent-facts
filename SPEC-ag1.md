# AgentFacts compact viewer payload — `ag1`

Companion to [`SPEC.md`](./SPEC.md). Portable `/v` fragment. Codec matches
AppFacts `af1` (zlib + base64url).

## URL shape

```
https://agentfacts.dev/v#ag1.<payload>
https://agentfacts.dev/v?face=raw#ag1.<payload>
```

## Compact JSON (`ag1`)

| Key | Source | Required |
|---|---|---|
| `v` | payload version | yes (`1`) |
| `name`, `developer`, `kind`, `status`, `license` | identity | yes |
| `version` | optional identity | no |
| `model`, `tools`, `reach`, `autonomy`, `memory`, `egress` | fact groups | yes |
| `homepage`, `repository` | URLs | no |
| `raw`, `truncated` | viewer UX | no |

Enums stay identical to frontmatter (no second vocabulary).

## Shrinkage

1. Drop URLs.
2. Drop `raw`.
3. Drop `tools.toolsets` paths if needed (keep count / shell / browse flags).
4. Set `truncated: true` when dropping material fields.

## License

CC0 — public domain. No attribution required.
