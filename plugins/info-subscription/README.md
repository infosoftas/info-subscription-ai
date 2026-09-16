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

### ChatGPT / Codex (Agent Plugins, via `.agents/plugins/marketplace.json`)

```bash
codex plugin marketplace add "C:\Temp\info-subscription-ai"
codex plugin marketplace list
```
Then restart the ChatGPT desktop app, open the Plugins Directory, pick the
`info-subscription-ai` source, and install **INFO-Subscription**.

Plain ChatGPT chat (not Codex mode) doesn't use this file at all — see
[Connect and test your plugin](https://developers.openai.com/plugins/deploy/connect-chatgpt)
for the Developer Mode connector flow instead (paste the MCP URL directly).

### GitHub Copilot CLI (via `.github/plugin/marketplace.json`)

```powershell
copilot plugin marketplace add "C:\Temp\info-subscription-ai"
copilot plugin install info-subscription@info-subscription-ai
```

### Claude Code (via `.claude-plugin/marketplace.json`)

```
/plugin marketplace add C:\Temp\info-subscription-ai
/plugin install info-subscription@info-subscription-ai
```
If the install summary says `Run /reload-plugins to activate.`, run that.

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
