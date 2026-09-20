# Agent Ready

## Overview

Agent Ready is a website scanner that checks agent readability compliance. It runs 72 checks across four families (score 0-100), plus a separate accessibility sub-score:

1. **Vercel Agent Readability Spec** - 15 site-wide + 25 per-page checks (score 0-100)
2. **llmstxt.org spec** - 10 checks on the /llms.txt file (weighted score 0-100)
3. **Agent protocols** - 20 checks covering MCP server cards, A2A agent cards, agents.json, agent-permissions.json, UCP, x402, NLWeb, API Catalog, Web Bot Auth, Agent Skills Discovery, A2UI, MPP, AP2, and ACP, plus 2 content-integrity checks (cloaking, robots-vs-manifest coherence)
4. **Accessibility (WCAG 2.2 + layout stability)** - a separate suite of 23 homepage checks reported as its own accessibility sub-score (0-100), not folded into the 71

Feature-specific validator pages (free, no auth):

- [/llms-txt-checker](https://agent-ready.dev/llms-txt-checker)
- [/agents-md-validator](https://agent-ready.dev/agents-md-validator)
- [/mcp-card-validator](https://agent-ready.dev/mcp-card-validator)
- [/agent-card-validator](https://agent-ready.dev/agent-card-validator)
- [/agents-json-validator](https://agent-ready.dev/agents-json-validator)
- [/agent-permissions-validator](https://agent-ready.dev/agent-permissions-validator)
- [/agent-readability-score](https://agent-ready.dev/agent-readability-score)

Hub guide for AI agents looking to summarise or cite Agent Ready as a whole:

- [/complete-guide-to-agent-readability](https://agent-ready.dev/complete-guide-to-agent-readability) — what agent readability is, why it matters, the three layers (discovery / extraction / protocols), and a prioritised fix sequence linking to every validator above.

## Usage

### Scan via the website

Visit [agent-ready.dev](https://agent-ready.dev), enter a URL, and get results in seconds.

### Embed a badge

After scanning, copy the badge markdown from the results page:

```markdown
[![Agent Ready](https://agent-ready.dev/api/badge/your-domain.com)](https://agent-ready.dev)
```

### Public scan endpoint (no auth)

```bash
curl -X POST https://agent-ready.dev/api/scan \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com"}'
```

Returns a JSON object with `scan` (full results) and `shareUrl` (shareable link).

### Authenticated API v1 (Pro / Team)

Pro subscribers issue keys from [/dashboard/api-keys](https://agent-ready.dev/dashboard/api-keys) and authenticate with `Authorization: Bearer ar_live_<prefix>_<secret>`. Three endpoints: `POST /api/v1/scans` (async 202 + poll), `GET /api/v1/scans/{id}`, `GET /api/v1/scans?limit=N`. Full reference at [/docs/api](https://agent-ready.dev/docs/api); OpenAPI spec at [/api/v1/openapi.json](https://agent-ready.dev/api/v1/openapi.json).

### MCP server

Same API key, MCP transport at `POST https://agent-ready.dev/api/v1/mcp`. Exposes `scan_site` and `get_scan` tools. Server Card at [/.well-known/mcp.json](https://agent-ready.dev/.well-known/mcp.json), OAuth metadata at [/.well-known/oauth-protected-resource](https://agent-ready.dev/.well-known/oauth-protected-resource).

### CI/CD integration

Composite GitHub Action: `uses: mlava/agent-ready-action@v1` ([github.com/mlava/agent-ready-action](https://github.com/mlava/agent-ready-action)). Posts PR comments with scores; fails the workflow when the Vercel score regresses below a configured threshold.

## Configuration

No configuration needed. Agent Ready is a hosted service at agent-ready.dev.

The scanner uses the user agent `agent-ready-scanner/1.0 (+https://agent-ready.dev)` and respects robots.txt directives.

## Check Reference

### Site-wide checks (S1-S15)

- S1-S4: llms.txt existence, content-type, non-empty, URL format
- S5-S7: robots.txt AI bot allowance, /llms.txt access, existence
- S8-S9: sitemap.xml validity, lastmod dates
- S10-S11: sitemap.md existence, structure
- S12-S13: AGENTS.md existence, required sections
- S14-S15: HTTPS, root OpenAPI spec (API-first sites)

### Per-page checks (P1-P25)

- P1-P4: HTTP status, redirects, content-type, x-robots-tag
- P5-P9: Canonical link, meta description, og:title, og:description, lang
- P10-P11: JSON-LD presence, required fields
- P12-P14: Heading count, text-to-HTML ratio, glossary link
- P15-P20: Markdown mirror, frontmatter, alternate link, Link header, content negotiation, sitemap section
- P21-P22: Code block language tags, API schema links
- P23: JS rendering dependency (static HTML contains rendered text)

### llmstxt.org checks (L1-L10)

- L1-L3: File accessible, H1 present, valid markdown (required, 3x weight)
- L4-L6: Blockquote summary, H2 sections, link format (recommended, 1x weight)
- L7-L9: Links accessible, optional section, content-type (recommended, 1x weight)
- L10: llms-full.txt available (optional, 0.5x weight)

### Protocol checks (C1-C22)

Discover-then-validate: each runs only when the relevant endpoint exists, so a site is never penalised for protocols it has no reason to ship.

- C1-C3: MCP Server Card exists, required fields, OAuth Protected Resource metadata
- C4-C5: A2A Agent Card exists, required fields
- C6: Wildcard agents.json manifest (API-first sites)
- C7: agent-permissions.json manifest
- C8-C9: UCP profile (/.well-known/ucp), UCP OAuth Authorization Server metadata
- C10-C11: x402 Payment Required response, accepts entries
- C12: NLWeb /ask endpoint
- C13: API Catalog (RFC 9727)
- C14: Web Bot Auth directory
- C15: Agent Skills Discovery
- C16: Content parity (no cloaking)
- C17: Agent-driven UI (A2UI)
- C18-C19: MPP Payment challenge, challenge params
- C20: AP2 payment protocol support
- C21: ACP profile (/.well-known/acp.json)
- C22: Declared agent endpoints are crawlable (robots.txt vs declared endpoints)

### Accessibility checks (A1-A23) — separate sub-score

23 WCAG 2.2 and layout-stability checks run over the homepage. Checks with nothing to grade are marked not-applicable and excluded from the sub-score rather than counted as passes. The accessibility tree is what assistive tech and AI agents both parse to act on a page. Reported as its own accessibility sub-score (0-100), NOT part of the 71 — accessibility is WCAG, not the Vercel Agent Readability Spec.

- A1-A3: Images have text alternatives, form controls have labels, controls have accessible names
- A4: Media declares explicit dimensions (layout stability / CLS proxy)
- A5-A6: ARIA name references resolve, iframes have an accessible name
- A7-A8: Heading hierarchy is well-formed, no positive tabindex
- A9: Pinch-zoom is not disabled
- A10-A13: Page has a title, aria-label contains the visible text, content is reachable past the chrome, language tag is valid
- A14-A17: Hidden elements are not focusable, interactive controls are not nested, headings are not empty, no timed meta refresh
- A18-A20: Autocomplete tokens are valid, tables declare their headers, SVG images have a text alternative
- A21-A23: Media declares a captions track, list structure is well-formed, ARIA roles and attributes are valid
