# info-subscription plugin

Single plugin folder shared across every AI agent ecosystem this repo
supports. Each ecosystem reads its own manifest file(s) from this same
directory — nothing is duplicated except the (necessarily different)
manifest formats.

```
plugins/info-subscription/
├── plugin.json            <- Agent Plugins 1.0 manifest (ChatGPT / Codex / GitHub Copilot CLI)
├── mcp.json                <- Agent Plugins 1.0 MCP config (same audience as above)
├── .claude-plugin/
│   └── plugin.json         <- Claude Code plugin manifest
├── .mcp.json                <- Claude Code native MCP config
└── LISTING.md               <- draft copy for public directory/marketplace submissions
```

All manifests point at the same remote MCP server:
`https://mcp.info-subscription.com` (OAuth 2.0 / Azure AD B2C, discovered
automatically via `.well-known/oauth-protected-resource`). No secrets live in
any of these files.

## Install / test per ecosystem

These use the published GitHub repo (`infosoftas/info-subscription-ai`)
directly — no local clone needed. See
[Developing this plugin locally](#developing-this-plugin-locally) below if
you're editing the plugin itself and need to test uncommitted changes.

### ChatGPT / Codex (Agent Plugins, via `.agents/plugins/marketplace.json`)

```bash
codex plugin marketplace add infosoftas/info-subscription-ai
codex plugin marketplace list
```
Then restart the ChatGPT desktop app, open the Plugins Directory, pick the
`info-subscription-ai` source, and install **INFO-Subscription**.

Plain ChatGPT chat (not Codex mode) doesn't use this file at all — see
[Connect and test your plugin](https://developers.openai.com/plugins/deploy/connect-chatgpt)
for the Developer Mode connector flow instead (paste the MCP URL directly).

### GitHub Copilot CLI (via `.github/plugin/marketplace.json`)

```powershell
copilot plugin marketplace add infosoftas/info-subscription-ai
copilot plugin install info-subscription@info-subscription-ai
```

### Claude Code (via `.claude-plugin/marketplace.json`)

```
/plugin marketplace add infosoftas/info-subscription-ai
/plugin install info-subscription@info-subscription-ai
```
If the install summary says `Run /reload-plugins to activate.`, run that.

The plugin's `.mcp.json` bundles a public, pre-registered OAuth client ID
(`09ddd06c-dd1b-4782-8716-820ce6077e41`, also published at
[docs.info-subscription.com](https://docs.info-subscription.com/en/latest/general/mcp-server.html))
plus a fixed `callbackPort` (`7777`, matching the `http://localhost:7777/callback`
redirect URI registered with the identity provider). This is required —
without it, Claude Code falls back to Dynamic Client Registration (RFC 7591),
which Azure AD B2C doesn't support, and the server shows as
`Incompatible auth server: does not support dynamic client registration`.

If you're adding the server manually (outside the plugin) instead of through
`/plugin install`, use:

```
claude mcp add --transport http --client-id 09ddd06c-dd1b-4782-8716-820ce6077e41 \
  --callback-port 7777 info-subscription https://mcp.info-subscription.com
claude mcp login info-subscription
```

## Developing this plugin locally

If you're changing files in this plugin (or a marketplace catalog) and want
to test before pushing, point each tool at your local clone instead of the
GitHub repo:

```bash
git clone https://github.com/infosoftas/info-subscription-ai.git
cd info-subscription-ai
```

```bash
# ChatGPT / Codex
codex plugin marketplace add /path/to/cloned/repository
codex plugin marketplace list

# GitHub Copilot CLI
copilot plugin marketplace add /path/to/cloned/repository
copilot plugin install info-subscription@info-subscription-ai

# Claude Code
/plugin marketplace add /path/to/cloned/repository
/plugin install info-subscription@info-subscription-ai
```

On Windows, use the full path in quotes, e.g. `"C:\code\info-subscription-ai"`.

After editing a manifest, re-run the ecosystem's `marketplace update`/
`marketplace upgrade` command (see [Updating](#updating) below) — most tools
don't auto-detect local file changes.

## Updating

Bump `version` in `plugin.json` and `.claude-plugin/plugin.json` (and in the
matching entry of each `marketplace.json` at the repo root, where present),
commit, push. Users refresh with:

- Codex: `codex plugin marketplace upgrade info-subscription-ai`
- Copilot CLI: `copilot plugin marketplace update` then `copilot plugin update info-subscription`
- Claude Code: `/plugin marketplace update`

## Public directory submission

Getting listed so any user can discover it (not just people who add this
repo) is a separate process per vendor — see `LISTING.md` for the drafted
OpenAI plugin-submission-portal copy, and the repo root README for the
Anthropic Connectors Directory requirements.
