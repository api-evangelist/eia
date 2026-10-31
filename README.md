# EIA

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

The U.S. Energy Information Administration (EIA) is the independent statistical and analytical agency within the U.S. Department of Energy, created by the Department of Energy Organization Act of 1977, that collects, analyzes, and disseminates energy information for the United States. EIA sits at the measurement layer of the American energy value chain rather than the operating layer - it does not generate, transmit, distribute, or retail energy, and it does not regulate anyone. Instead it compels the industry to report through mandatory survey forms (EIA-860, EIA-861, EIA-923, EIA-176, EIA-914, EIA-930 and dozens more) and then publishes the result as the reference statistics for electricity, natural gas, petroleum, coal, nuclear, renewables, emissions, and international energy. EIA's API posture is the strongest of any organization in this sector and a genuine benchmark for government data anywhere. The Open Data APIv2 at api.eia.gov/v2 is a fully RESTful, self-documenting, hierarchically routed API covering more than two million time series, described by a real downloadable OpenAPI 3.0.0 contract carrying 225 paths and 278 operations, opened by a free API key that is emailed automatically from a public registration form with no review, no accreditation, and no licence to sign. A companion bulk download facility at api.eia.gov/bulk serves the same data as manifest-indexed zip archives and requires no key at all. The split that defines this sector is absolute here. EIA's market, system, and grid data is wide open - hourly balancing-authority demand and interchange, wholesale and spot prices, generator-level capacity and operations - while EIA publishes no consumer energy data API of any kind. There is no Green Button, no ESPI, no Download My Data, no Connect My Data, no consent flow, and no customer usage or billing endpoint, because individual customer data is never collected by EIA in the first place; its surveys arrive already aggregated from utilities and are further protected by statutory confidentiality. EIA is therefore the clearest instance of the recurring finding in this series - a federal data agency that publishes a far better documented, far more accessible API than the regulated utilities whose numbers it reports.

**Areas:** Energy · United States · Energy Markets · Electricity · Natural Gas · Petroleum · Coal · Nuclear · Renewables · Grid · Emissions · Government

## EIA on APIs.io

Everything profiled for EIA is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/eia/](https://apis.io/providers/eia/)** — or go straight to one of the APIs or properties below.

### APIs (17)

- [EIA Bulk Download Facility](https://apis.io/apis/eia/eia-bulk-download-facility/) — EIA's bulk data distribution surface, served from the same api.eia.gov host as APIv2 but requiring no API key whatsoever. A single manifest at…
- [EIA AEO API](https://apis.io/apis/eia/eia-aeo-api/) — Access to Annual Energy Outlook Data
- [EIA COAL API](https://apis.io/apis/eia/eia-coal-api/) — Access to Coal Data
- [EIA CRUD IMPORTS API](https://apis.io/apis/eia/eia-crud-imports-api/) — Access to Crude Oil Imports Data
- [EIA DBF API](https://apis.io/apis/eia/eia-dbf-api/) — Access to Densified Biomass Data
- [EIA ELEC API](https://apis.io/apis/eia/eia-elec-api/) — Access to Electricity Data
- [EIA EMISS API](https://apis.io/apis/eia/eia-emiss-api/) — Access to CO2 Emissions Data
- [EIA IEO API](https://apis.io/apis/eia/eia-ieo-api/) — Access to International Energy Outlook Data
- [EIA INTL API](https://apis.io/apis/eia/eia-intl-api/) — Access to International Data
- [EIA NG API](https://apis.io/apis/eia/eia-ng-api/) — Access to Natural Gas Data
- [EIA NUC STATUS API](https://apis.io/apis/eia/eia-nuc-status-api/) — Access to Nuclear Outages Data
- [EIA Root API](https://apis.io/apis/eia/eia-root-api/) — Available EIA API Datasets
- [EIA RTO API](https://apis.io/apis/eia/eia-rto-api/) — Access to Daily Electricity Data
- [EIA SEDS API](https://apis.io/apis/eia/eia-seds-api/) — Access to State Energy Data Systems (SEDS) Data
- [EIA SEP API](https://apis.io/apis/eia/eia-sep-api/) — Access to State Electricity Profiles
- [EIA STEO API](https://apis.io/apis/eia/eia-steo-api/) — Access to Short Term Energy Outlook Data
- [EIA TOTAL API](https://apis.io/apis/eia/eia-total-api/) — Access to Total Energy Data

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [No first-party MCP server; two community stdio servers over APIv2, plus a derived candidate tool set](https://apis.io/servers/eia/no-first-party-mcp-server-two-community-stdio-servers-over-apiv2-plus-a-derived-candidate-tool-set/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Eia Agentic Access](https://apis.io/agentic-access/eia/eia-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [EIA APIv2](https://apis.io/collections/eia/open-eia-api-v2/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Eia Api V2 Overlay](https://apis.io/overlays/eia/eia-api-v2-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Eia Authentication](https://apis.io/security/eia/eia-authentication/)
- [Eia Domain Security](https://apis.io/security/eia/eia-domain-security/)
- [Eia Vulnerability Disclosure](https://apis.io/security/eia/eia-vulnerability-disclosure/)

#### Rate limits (1)

Published request limits.

- [Eia Rate Limits](https://apis.io/rate-limits/eia/eia-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.eia.gov)
- [Documentation](https://www.eia.gov/opendata/documentation.php)
- [Getting started](https://www.eia.gov/opendata/documentation.php)
- [API reference](https://www.eia.gov/opendata/browser/)
- [Sign up](https://www.eia.gov/opendata/register.php)
- [Support](https://www.eia.gov/opendata/faqs.php)
- [Changelog](https://www.eia.gov/opendata/documentation.php)
- [Blog](https://www.eia.gov/todayinenergy/)
- [Security](https://www.energy.gov/cio/articles/vulnerability-disclosure-policy)
- [Terms of service](https://www.eia.gov/opendata/register.php)
- [Privacy policy](https://www.eia.gov/about/privacy_security_policy.php)
- [GitHub](https://github.com/EIAgov)

## API Evangelist rating

**Kin Score 48.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 47.1 |
| Contract governance | 4.5 |
| Operational transparency | 57.9 |
| Developer ergonomics | 66.1 |
| Access clarity | 34.2 |

**Agent readiness 27.5** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
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
| Operation Distinctiveness | mostly (partial credit) |

**Regulatory alignment 25.4** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/eia/](https://apis.io/providers/eia/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for EIA: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/eia/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
