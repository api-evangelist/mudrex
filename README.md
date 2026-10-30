# Mudrex

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

Mudrex is a US-headquartered, Bengaluru-based crypto investment and trading platform founded in 2018 and registered with India's Financial Intelligence Unit (FIU-IND). It serves retail and pro traders with spot trading, curated Coin Sets, and USDT- and INR-margined perpetual futures. Its developer surface is the Mudrex Futures API — a REST trading API under https://trade.mudrex.com/fapi/v1 covering wallet transfers, asset discovery, leverage and margin type, order create/amend/cancel, position management with stop-loss/take-profit, liquidation pricing and fee history — plus a public, unauthenticated market-data surface (historical price and mark-price klines over REST, live kline/mark-kline/ticker streams over WebSocket) and an officially hosted MCP server at https://mudrex.com/mcp that exposes 20 trading tools to AI agents. Authentication is a single X-Authentication API-key header issued after KYC and TOTP two-factor enrollment. An official Python SDK ships on PyPI as mudrex-sdk.

**Areas:** Company · Cryptocurrency · Trading · Futures · Financial Services · Fintech · Market Data · Exchange · India

## Mudrex on APIs.io

Everything profiled for Mudrex is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/mudrex/](https://apis.io/providers/mudrex/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Mudrex Futures Trading API](https://apis.io/apis/mudrex/mudrex-futures-trading-api/) — Programmatic control over a Mudrex futures trading account. Transfer funds between the spot and futures wallets (USDT and INR), list tradeable instruments…
- [Mudrex Market Data API](https://apis.io/apis/mudrex/mudrex-market-data-api/) — Public, unauthenticated market-data surface for Mudrex linear perpetual futures. Over REST it returns bulk historical OHLCV price klines (GET /price/kline,…
- [Mudrex MCP Server](https://apis.io/apis/mudrex/mudrex-mcp-server/) — Mudrex's official hosted Model Context Protocol server, which exposes the Mudrex Futures Trading API to MCP-capable AI assistants as 20 tools across orders,…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Mudrex Market Data Streams](https://apis.io/asyncapis/mudrex/mudrex-market-data-streams/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [mudrex](https://apis.io/servers/mudrex/mudrex/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Mudrex Authentication](https://apis.io/security/mudrex/mudrex-authentication/)
- [Mudrex Domain Security](https://apis.io/security/mudrex/mudrex-domain-security/)
- [Mudrex Trust Center](https://apis.io/security/mudrex/mudrex-trust-center/)

#### Rate limits (1)

Published request limits.

- [Mudrex Rate Limits](https://apis.io/rate-limits/mudrex/mudrex-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://mudrex.com/)
- [Documentation](https://docs.trade.mudrex.com/docs/overview)
- [Getting started](https://docs.trade.mudrex.com/docs/quickstart)
- [API reference](https://docs.trade.mudrex.com/docs/quick-reference)
- [Pricing](https://mudrex.com/fee-and-compliance)
- [Sign up](https://mudrex.com/login)
- [Support](https://mudrex.com/support)
- [Blog](https://mudrex.com/blog/)
- [Compliance](https://mudrex.com/security)
- [Terms of service](https://mudrex.com/terms)
- [Privacy policy](https://mudrex.com/privacy)
- [GitHub](https://github.com/mudrex)

## API Evangelist rating

**Kin Score 42.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 39.0 |
| Contract governance | 18.2 |
| Operational transparency | 50.0 |
| Developer ergonomics | 49.4 |
| Access clarity | 28.9 |

**Agent readiness 29.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 20.4** — Securities & Market Data

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/mudrex/](https://apis.io/providers/mudrex/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Mudrex: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/mudrex/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
