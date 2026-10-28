# Agent Ready

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Agent Ready (agent-ready.dev) is an independent AI agent-readability scanner built and maintained by Mark Lavercombe. It scores any public website against the Vercel Agent Readability Spec, the llmstxt.org specification and the agent-protocol manifests (MCP server cards, A2A agent cards, agents.json, agent-permissions.json, UCP, ACP, x402, MPP, AP2, NLWeb, RFC 9727 API catalog, Web Bot Auth, Agent Skills Discovery) — 72 checks plus a separate 23-check WCAG 2.2 accessibility sub-score — and returns a 0-100 score with per-check remediation. The same scanner is exposed as an OpenAPI 3.1 REST API at https://agent-ready.dev/api/v1 (Pro API keys, Idempotency-Key on writes, RFC 8594 Sunset policy), a hosted Streamable HTTP MCP server at /api/v1/mcp plus a no-auth MCP Apps endpoint, an A2A 1.0 agent card, a stdio MCP package and CLI on npm, JavaScript and Python client SDKs, a GitHub Action, and pay-per-scan x402/MPP micropayments in USDC on Base. Free ($0) and Pro ($19/month) plans.

**Areas:** Agents · Agent Readiness · Website Scanning · Developer Tools · MCP · A2A · llms-txt · x402 · NLWeb · Accessibility · Agent-Native · Australia

## Agent Ready on APIs.io

Everything profiled for Agent Ready is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/agent-ready-dev/](https://apis.io/providers/agent-ready-dev/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [Agent Ready MCP Server](https://apis.io/apis/agent-ready-dev/agent-ready-mcp-server/) — Hosted Model Context Protocol server at https://agent-ready.dev/api/v1/mcp (Streamable HTTP, POST only, protocol version 2025-06-18, serverInfo agent-ready…
- [Agent Ready A2A Agent](https://apis.io/apis/agent-ready-dev/agent-ready-a2a-agent/) — Agent2Agent (A2A) surface: a signed agent card served from https://agent-ready.dev/.well-known/agent-card.json (protocolVersion 1.0, JSONRPC, version 1.0.0,…
- [Agent Ready MCP API](https://apis.io/apis/agent-ready-dev/agent-ready-dev-mcp-api/) — The MCP API from Agent Ready — 1 operation(s) for mcp.
- [Agent Ready NL Web API](https://apis.io/apis/agent-ready-dev/agent-ready-dev-nlweb-api/) — The NLWeb API from Agent Ready — 1 operation(s) for nlweb.
- [Agent Ready Scans API](https://apis.io/apis/agent-ready-dev/agent-ready-dev-scans-api/) — The Scans API from Agent Ready — 3 operation(s) for scans.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [agent-ready-dev-mcp.yml](https://apis.io/servers/agent-ready-dev/agent-ready-dev-mcp-yml/)
- [Agent Ready MCP Apps endpoint (no auth)](https://apis.io/servers/agent-ready-dev/agent-ready-mcp-apps-endpoint-no-auth/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Agent Ready Dev Agentic Access](https://apis.io/agentic-access/agent-ready-dev/agent-ready-dev-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Agent Ready Dev Openapi Overlay](https://apis.io/overlays/agent-ready-dev/agent-ready-dev-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Agent Ready Dev Authentication](https://apis.io/security/agent-ready-dev/agent-ready-dev-authentication/)
- [Agent Ready Dev Domain Security](https://apis.io/security/agent-ready-dev/agent-ready-dev-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Agent Ready Dev Scopes](https://apis.io/scopes/agent-ready-dev/agent-ready-dev-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Agent Ready Dev Plans Pricing](https://apis.io/plans/agent-ready-dev/agent-ready-dev-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Agent Ready Dev Rate Limits](https://apis.io/rate-limits/agent-ready-dev/agent-ready-dev-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://agent-ready.dev/)
- [Documentation](https://agent-ready.dev/docs)
- [Getting started](https://agent-ready.dev/quickstart)
- [API reference](https://agent-ready.dev/docs/api/reference)
- [Pricing](https://agent-ready.dev/pricing)
- [Sign up](https://agent-ready.dev/sign-up)
- [Support](https://agent-ready.dev/about)
- [Terms of service](https://agent-ready.dev/terms)
- [Privacy policy](https://agent-ready.dev/privacy)
- [GitHub](https://github.com/mlava)
- [Status](https://status.agent-ready.dev/)

## API Evangelist rating

**Kin Score 63.8** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 50.0 |
| Contract governance | 18.2 |
| Operational transparency | 44.7 |
| Developer ergonomics | 83.3 |
| Access clarity | 76.3 |

**Agent readiness 74.4** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | yes |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | self |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 42.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/agent-ready-dev/](https://apis.io/providers/agent-ready-dev/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Agent Ready: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/agent-ready-dev/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
