---
name: scan-agent-readiness
description: Agent Ready (agent-ready.dev) scores any website against 72 agent-readability checks (site, page, llms.txt, agent protocols) and returns per-check pass/fail with fix guidance.
license: MIT
---

# Scan a website for agent readiness

Score any URL against the Agent Ready check suite — 72 checks across four
families: the Vercel Agent Readability Spec (40 site + page checks),
llmstxt.org (10), and the agent-protocol specs (22: MCP, A2A, agents.json,
agent-permissions.json, UCP, x402, MPP, AP2, ACP, NLWeb, api-catalog, Web Bot
Auth). Returns a 0–100 score, per-check pass/fail, and remediation text for
every failure.

## When to use this skill

Use when a user asks any of:

- "Is this site agent-ready?"
- "Why aren't agents picking up my site?"
- "What's my LLM-readability score?"
- "Does this site publish an agents.json / MCP card / llms.txt?"

Do **not** use this skill for general SEO audits — it specifically targets
machine/agent consumption, not search ranking.

## How to call

Send an HTTP POST to the public scan endpoint. No API key needed for
single-URL scans:

```http
POST https://agent-ready.dev/api/scan
Content-Type: application/json

{ "url": "https://example.com" }
```

The scan runs synchronously — expect several seconds — and returns `201` with
the finished result: `{ "scan": { … }, "shareUrl": "/scan/<token>" }`.

Add `"stream": true` to the body to get Server-Sent Events instead: `status`,
`site-checks`, `page-result`, `llmstxt-checks` and `score` progress events,
then a terminal `complete` event carrying the same scan object.

With an API key, use the versioned REST API instead (start scan + poll):

```http
POST https://agent-ready.dev/api/v1/scans
Authorization: Bearer <key>
Content-Type: application/json

{ "url": "https://example.com" }
```

That returns `202` with `{ "id", "status": "running", "url", "pollUrl" }`. Then
`GET` the `pollUrl` (`/api/v1/scans/{id}`) until `status` is `"completed"` —
`"failed"` means no page could be read, and such a scan carries no usable
score. The OpenAPI 3.1 spec at <https://agent-ready.dev/api/v1/openapi.json>
documents request and response schemas.

## Interpreting the result

Checks arrive in `siteChecks`, `llmstxtChecks`, `protocolResults`, and
`pageResults[].checks`. Each entry has a `checkId` (e.g. `P11`, `S15`, `L9`,
`C6`), a `status` of `pass` | `fail` | `warn` | `error`, a `message`, and
`howToFix` text on anything that did not pass. The ID prefix gives the family:

- **S** (Site) — origin-level: llms.txt presence, robots.txt, sitemap.xml,
  AGENTS.md, HTTPS, OpenAPI spec
- **P** (Page) — per-page: canonical, meta description, JSON-LD, heading
  structure, markdown mirror, content negotiation
- **L** (llms.txt) — llms.txt structure and link health per llmstxt.org
- **C** (Protocol) — MCP server card, A2A agent card, agents.json,
  agent-permissions.json, and the other agent-protocol manifests
- **A** (Accessibility) — WCAG 2.2 / layout stability. These ride in
  `protocolResults` but are scored separately as `accessibilityScore` and are
  deliberately NOT part of the 72

`vercelScore` is the headline 0–100 and bands into `vercelRating`:
`excellent` ≥ 90, `good` ≥ 70, `fair` ≥ 50, `needs_improvement` below that.
`llmstxtScore` is a separate 0–100 sub-score for the llms.txt file itself, so a
site with no llms.txt scores 0 there while still rating well overall.

## Rate limits

- Anonymous (no key, no account): 3 scans / 30 days per IP
- Signed-in free tier: 10 scans / 30 days
- API key (Pro): 50 scans / month, 10 scans/min, 200 scans/day

See <https://agent-ready.dev/pricing> for tier details.

## Related resources

- API catalog: <https://agent-ready.dev/.well-known/api-catalog>
- MCP server card: <https://agent-ready.dev/.well-known/mcp.json>
- agents.json manifest: <https://agent-ready.dev/.well-known/agents.json>
- Methodology: <https://agent-ready.dev/methodology>
