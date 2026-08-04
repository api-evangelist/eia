# EIA (eia)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The U.S. Energy Information Administration (EIA) is the independent statistical and analytical agency within the U.S. Department of Energy, created by the Department of Energy Organization Act of 1977, that collects, analyzes, and disseminates energy information for the United States. EIA sits at the measurement layer of the American energy value chain rather than the operating layer — it does not generate, transmit, distribute, or retail energy, and it does not regulate anyone. Instead it compels the industry to report through mandatory survey forms (EIA-860, EIA-861, EIA-923, EIA-176, EIA-914, EIA-930 and dozens more) and then publishes the result as the reference statistics for electricity, natural gas, petroleum, coal, nuclear, renewables, emissions, and international energy. EIA's API posture is the strongest of any organization in this sector and a genuine benchmark for government data anywhere. The Open Data APIv2 at api.eia.gov/v2 is a fully RESTful, self-documenting, hierarchically routed API covering more than two million time series, described by a real downloadable OpenAPI 3.0.0 contract carrying 225 paths and 278 operations, opened by a free API key that is emailed automatically from a public registration form with no review, no accreditation, and no licence to sign. A companion bulk download facility at api.eia.gov/bulk serves the same data as manifest-indexed zip archives and requires no key at all. The split that defines this sector is absolute here. EIA's market, system, and grid data is wide open — hourly balancing-authority demand and interchange, wholesale and spot prices, generator-level capacity and operations — while EIA publishes no consumer energy data API of any kind. There is no Green Button, no ESPI, no Download My Data, no Connect My Data, no consent flow, and no customer usage or billing endpoint, because individual customer data is never collected by EIA in the first place.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/eia/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/eia/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Energy Markets
- Electricity
- Natural Gas
- Petroleum
- Coal
- Nuclear
- Renewables
- Grid
- Emissions
- Government
- Open Data
- Energy Statistics

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### EIA Open Data API (APIv2)

EIA's public, fully RESTful open data API covering more than two million energy time series. Datasets are arranged in a discoverable tree — request a parent route such as `/v2/electricity` and the API returns its child routes, available frequencies, facets, and data columns as metadata; append `/data` to retrieve values, with facets, column selection, date range, sort, offset, and length all expressed as query parameters. Route families cover electricity (including hourly RTO and balancing-authority operating data), natural gas, petroleum, coal, nuclear outages, densified biomass, CO2 emissions, international energy, the State Energy Data System, state electricity profiles, and the Short-Term, Annual, and International Energy Outlook projections. Responses are JSON by default or XML with `out=xml`, capped at 5,000 rows per request with an explicit pagination warning returned in the payload. The legacy APIv1 series interface is deprecated but its identifiers remain reachable through the `/v2/seriesid/{id}` route. Verified live 2026-07-27 — an unauthenticated GET returns HTTP 403 with `API_KEY_MISSING` and a bogus key returns HTTP 403 with `API_KEY_INVALID`. Published API version at the time of review is 2.1.12 (March 2026).

- **Human URL:** [https://www.eia.gov/opendata/documentation.php](https://www.eia.gov/opendata/documentation.php)
- **Base URL:** `https://api.eia.gov/v2`

#### Tags

- Open Data
- Electricity
- Natural Gas
- Petroleum
- Coal
- Nuclear
- Emissions
- Energy Statistics
- Time Series

#### Properties

- [OpenAPI](openapi/eia-api-v2-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.eia.gov/opendata/documentation.php)
- [API Reference](https://www.eia.gov/opendata/browser/)
- [Portal](https://www.eia.gov/opendata/)
- [Signup](https://www.eia.gov/opendata/register.php)
- [Authentication](https://www.eia.gov/opendata/register.php)
- [Terms of Service](https://www.eia.gov/opendata/register.php)
- [Console](https://www.eia.gov/opendata/browser/)
- [Documentation](https://www.eia.gov/opendata/qb.php)
- [Privacy Policy](https://www.eia.gov/about/privacy_security_policy.php)

### EIA Bulk Download Facility

EIA's bulk data distribution surface, served from the same api.eia.gov host as APIv2 but requiring no API key whatsoever. A single manifest at `/bulk/manifest.txt` returns a JSON catalog of every bulk dataset with Project Open Data style metadata — identifier, title, description, keyword, publisher, person, mbox, accessLevel, accessURL, and last_updated — and each dataset is then downloadable as a zip archive of newline-delimited JSON, for example `/bulk/ELEC.zip`. Datasets include U.S. Electric System Operating Data (661,461 series), Electricity (285,080), Petroleum (53,464), Annual Energy Outlook releases back to 2014, International, SEDS, STEO, Coal, Natural Gas, CO2 Emissions, Crude Oil Imports, Nuclear Outages, and Total Energy. Updated twice daily at 5 a.m. and 3 p.m. Eastern. Verified live 2026-07-27 — `GET /bulk/manifest.txt` returned HTTP 200 anonymously and `GET /bulk/ELEC.zip` returned HTTP 200 with a 291,920,911-byte zip payload, both without a key.

- **Human URL:** [https://www.eia.gov/opendata/bulkfiles.php](https://www.eia.gov/opendata/bulkfiles.php)
- **Base URL:** `https://api.eia.gov/bulk`

#### Tags

- Open Data
- Bulk Data
- Energy Statistics
- Electricity
- Time Series

#### Properties

- [Documentation](https://www.eia.gov/opendata/bulkfiles.php)
- [Data Catalog](https://api.eia.gov/bulk/manifest.txt)
- [Portal](https://www.eia.gov/opendata/)

## Common Properties

- [Website](https://www.eia.gov)
- [Portal](https://www.eia.gov/opendata/)
- [Documentation](https://www.eia.gov/opendata/documentation.php)
- [Signup](https://www.eia.gov/opendata/register.php)
- [Console](https://www.eia.gov/opendata/browser/)
- [Privacy Policy](https://www.eia.gov/about/privacy_security_policy.php)
- [GitHub — EIAgov (a USER account, not an organization; 4 public repos, no SDKs)](https://github.com/EIAgov)
- [DOE Project Open Data catalog — 342 of its 483 datasets are published by EIA](https://www.energy.gov/data.json)
- [Tools](https://www.eia.gov/tools/)
- [EIA Excel Add-in — spreadsheet client for APIv2](https://www.eia.gov/opendata/excel/)
- [Hourly Electric Grid Monitor — web tool over the /v2/electricity/rto routes](https://www.eia.gov/electricity/gridmonitor/)
- [Wholesale Electricity Markets — link hub to the seven ISO/RTO data surfaces, not an EIA API](https://www.eia.gov/electricity/wholesalemarkets/)
- [EIA survey forms — the mandatory industry reporting that feeds every API route](https://www.eia.gov/survey/)

## Mandate Posture

- **Mandate regime:** `other` — no consumer energy data mandate applies to EIA. Not `cdr-energy`, not `green-button-ontario`, not `green-button-voluntary` (there is no Green Button or ESPI reference anywhere on eia.gov), not `smart-meter-infrastructure`. Two different obligations do apply: EIA's own statutory collection mandate compelling the industry to file mandatory survey forms (EIA-860, EIA-861, EIA-923, EIA-176, EIA-914, EIA-930) under the Federal Energy Administration Act of 1974 and the DOE Organization Act of 1977; and the federal open-data obligation under the OPEN Government Data Act that the API and bulk catalog discharge.
- **Mandate status:** `live-implemented` — verified against live endpoints, not press releases. `api.eia.gov/v2` returns `API_KEY_MISSING`, a bogus key returns `API_KEY_INVALID`, the OpenAPI zip returns HTTP 200 and parses, `/bulk/manifest.txt` and `/bulk/ELEC.zip` both return HTTP 200 anonymously, and `energy.gov/data.json` carries 342 EIA-published datasets.
- **Consumer data API:** none — no Green Button, no ESPI, no consent flow, no customer-level route in 225 paths. **Market data:** wide open, including hourly balancing-authority demand, generation, and interchange.
- **Data standard:** no energy data standard implemented. OpenAPI 3.0.0 as the API contract; Project Open Data style catalog metadata on the bulk manifest; a proprietary route/frequency/facet/data shape otherwise.
- **Access gate:** `self-serve` — complete a short form and the key arrives by email automatically, with no review, no accreditation, no licence, and no fee. The bulk facility needs no key at all.
- **Auth model:** API key in the `api_key` query parameter only (EIA documents that it will not be read from a header). No OAuth2, no OIDC, no mTLS. No numeric rate limits published; the only documented hard limit is the 5,000-row response cap.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
