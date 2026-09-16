# info-subscription-ai

Public home for INFO-Subscription's AI agent integrations: plugins,
marketplaces, and (over time) shared skills and instructions usable across
ChatGPT/Codex, GitHub Copilot CLI, Claude Code, and any other agent that
adopts one of these formats.

All plugins connect to the same hosted MCP server,
`https://mcp.info-subscription.com` (OAuth 2.0 via Azure AD B2C). See
[INFO-Subscription MCP Server docs](https://docs.info-subscription.com/en/latest/general/mcp-server.html).

## Repo layout

```
.agents/plugins/marketplace.json   <- marketplace catalog for ChatGPT / Codex (Agent Plugins)
.github/plugin/marketplace.json    <- marketplace catalog for GitHub Copilot CLI
.claude-plugin/marketplace.json    <- marketplace catalog for Claude Code
plugins/
  info-subscription/                <- the plugin, shared across all three ecosystems (see its README.md)
skills/                             <- shared, standalone skills (SKILL.md bundles) reusable outside a single plugin
instructions/                       <- shared instruction/prompt files (e.g. AGENTS.md-style guidance)
```

Three marketplace catalog files live at repo root because each ecosystem's
tooling looks for its catalog at a fixed, ecosystem-specific path, but all of
them resolve plugin `source` paths relative to this same repo root — so they
all point at the one shared `plugins/info-subscription/` folder. No content
is duplicated purely for packaging reasons.

## Quick install

| Ecosystem | Add marketplace | Install plugin |
|---|---|---|
| ChatGPT / Codex | `codex plugin marketplace add infosoftas/info-subscription-ai` | via ChatGPT desktop Plugins Directory |
| GitHub Copilot CLI | `copilot plugin marketplace add infosoftas/info-subscription-ai` | `copilot plugin install info-subscription@info-subscription-ai` |
| Claude Code | `/plugin marketplace add infosoftas/info-subscription-ai` | `/plugin install info-subscription@info-subscription-ai` |

Local testing instructions (using a filesystem path instead of a GitHub
reference) are in `plugins/info-subscription/README.md`.

## Public directory listings (separate from this repo)

Adding this repo as a marketplace only helps users who already know about it
and add it explicitly. To make the plugin *discoverable* to any user browsing
a vendor's built-in directory, submit separately:

- **OpenAI Plugins Directory** — submit via
  [platform.openai.com/plugins](https://platform.openai.com/plugins)
  ("With MCP"). Requires verified developer/business identity, tool
  annotations (`readOnlyHint`/`destructiveHint`), starter prompts, and 5
  positive / 3 negative test cases. Draft listing copy:
  `plugins/info-subscription/LISTING.md`.
- **Anthropic Connectors Directory** — submit via
  `claude.ai/admin-settings/directory/submissions/new` (Team/Enterprise org
  required). Requires OAuth 2.0 (have it), every tool annotated with a
  `title` + `readOnlyHint`/`destructiveHint`, public setup docs, and a
  privacy policy.

## Adding shared skills or instructions later

- Drop a new `skills/<name>/SKILL.md` for a standalone skill any plugin or
  agent in this repo can reference.
- Drop shared guidance under `instructions/`.
- When adding a second plugin, create `plugins/<new-plugin>/` following the
  same pattern as `plugins/info-subscription/`, then add an entry to each of
  the three root `marketplace.json` files.

## Contributing

This is a public repository — contributions (new plugins, marketplace
entries, skills, instructions, fixes) are welcome. See
[CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines. All commits must include
a `Signed-off-by` line (Developer Certificate of Origin — `git commit -s`).

## License

Licensed under the [MIT License](./LICENSE). This covers the
packaging/integration content in this repo (manifests, marketplace catalogs,
docs, skills, instructions) — it doesn't grant any rights to the underlying
INFO-Subscription service or MCP server, which remain subject to Infosoft's
own terms.
