# Plugin Submission — Listing Draft (INFO-Subscription)

Draft copy for platform.openai.com/plugins → **Create plugin → With MCP**.
Fill in the bracketed placeholders before submitting; everything else is
ready to paste.

## Info tab

**Plugin name**
```
INFO-Subscription
```

**Short description** (~1 sentence, shown in directory tiles)
```
Look up subscribers, subscriptions, invoices, orders and catalogue data from INFO-Subscription.
```

**Long description**
```
INFO-Subscription connects ChatGPT to your INFO-Subscription tenant so you can
ask questions about subscribers, subscription periods, billing, orders, and
the product catalogue in plain language — no portal navigation required.

What you can do:
- Find subscribers by name, GUID, or subscriber number, and pull their contacts.
- Review subscription periods, full period detail, and grouped lifetime
  renewal history for a subscriber.
- Search invoices, get full invoice detail, and look up reminders and credit
  notes by invoice number.
- Search orders and retrieve full order detail, including payment and
  transaction IDs.
- Browse and search packages, products, organizations, and billing frequencies
  in the catalogue.

Sign-in uses your organization's Azure AD B2C credentials. Only data your
account is authorized to see is returned.
```

**Category**
```
Productivity  (alternates to consider: Business / Finance, depending on final taxonomy)
```

**Website**
```
https://docs.info-subscription.com/en/latest/general/mcp-server.html
```

**Support URL / Privacy policy URL / Terms URL**
```
[FILL IN — must be public URLs under the verified publisher's domain]
```

**Developer Identity**
```
[Select the verified individual or business identity for Infosoft in the OpenAI Platform]
```

## MCP tab

**URL type**
```
Universal, unless you need per-tenant URLs — then use Template:
  Example MCP Server URL:  https://mcp.info-subscription.com/<a-real-tenant-guid>
  Template MCP Server URL: https://mcp.info-subscription.com/{tenant_id}
(Template requires prior OpenAI approval/relationship.)
```

**Authentication**
```
OAuth 2.0 (Azure AD B2C), discovered via
https://mcp.info-subscription.com/.well-known/oauth-protected-resource
Client ID: 09ddd06c-dd1b-4782-8716-820ce6077e41 (no client secret)
Provide reviewer demo credentials: [FILL IN — a test tenant login]
```

**Content Security Policy**
```
[FILL IN only if the server returns custom UI. Text-only tool results need no CSP.]
```

**Tool annotations** — set per tool during Scan Tools; all current capabilities
are read-only lookups, so the expected values are:
```
readOnlyHint: true
destructiveHint: false
openWorldHint: false   (bounded to the caller's own tenant, not the open internet)
```

## Starter prompts

```
Show me all active subscriptions for subscriber 10042
Find invoice number 88321 and summarize what was billed
Which subscribers have cancelled in the last 30 days?
What packages are available for organization Acme?
Give me the full renewal history for subscriber 10042
```

## Test cases

**Positive (5)** — tool should be called, expect a correct, grounded answer:

1. "Look up subscriber 10042 and list their contacts." → calls subscriber
   search/detail tool, returns contact list.
2. "What's the status of invoice 88321?" → calls invoice lookup-by-number
   tool, returns invoice status/detail.
3. "Show the lifetime subscription history for subscriber with GUID
   `[sample-guid]`." → calls grouped lifetime/renewal history tool.
4. "List all packages for organization Acme." → calls catalogue package
   search tool, returns matching packages.
5. "Get full detail for order [sample-order-id], including payment info." →
   calls order detail tool, returns payment/transaction IDs.

**Negative (3)** — tool should NOT be called:

1. "What's a good pricing strategy for a SaaS subscription business?" —
   general advice, no real tenant data involved; should answer without
   invoking any INFO-Subscription tool.
2. "Cancel subscriber 10042's subscription." — write/destructive action not
   exposed by this read-only plugin; model should explain it can't perform
   this action rather than call a tool.
3. "What's the weather in Berlin?" — unrelated request; no tool call.

## Release notes (first submission)

```
Initial submission: remote MCP server exposing read-only search/lookup tools
for subscribers, subscription periods, billing/invoices, orders, and
catalogue data. OAuth via Azure AD B2C. No custom UI.
```

---
**Before submitting:** run "Scan Tools" in the portal and replace the
placeholder tool/annotation assumptions above with the actual discovered tool
names and metadata; confirm sample identifiers (subscriber/order/tenant IDs)
used in test cases are real, reviewer-accessible demo data.
