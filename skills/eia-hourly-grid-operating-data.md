---
name: Pull hourly grid operating data from EIA
description: Retrieve hourly and daily balancing-authority demand, demand forecast, net generation, interchange and generation-by-fuel-type from the EIA APIv2 /electricity/rto route family — the Form EIA-930 data behind the Hourly Electric Grid Monitor.
api: openapi/eia-api-v2-openapi.yml
generated: '2026-07-27'
method: generated
source: https://www.eia.gov/opendata/documentation.php, https://www.eia.gov/electricity/gridmonitor/
operations:
  - GET /v2/electricity/rto
  - GET /v2/electricity/rto/region-data
  - GET /v2/electricity/rto/region-data/facet/{facet_id}
  - GET /v2/electricity/rto/region-data/data
  - POST /v2/electricity/rto/region-data/data
  - GET /v2/electricity/rto/fuel-type-data/data
  - GET /v2/electricity/rto/interchange-data/data
  - GET /v2/electricity/rto/region-sub-ba-data/data
  - GET /v2/electricity/rto/daily-region-data/data
  - GET /v2/electricity/rto/daily-fuel-type-data/data
  - GET /v2/electricity/rto/daily-interchange-data/data
  - GET /v2/electricity/rto/daily-region-sub-ba-data/data
---

# Pull hourly grid operating data from EIA

The `/v2/electricity/rto` family is the highest-frequency, most operationally useful data EIA
publishes: hourly electric system operating data collected from balancing authorities on Form
EIA-930. It is the same data that drives EIA's Hourly Electric Grid Monitor.

## The eight routes

Each exists in an **hourly** and a **daily** form, and each has the standard
`…/facet`, `…/facet/{facet_id}` and `…/data` (GET and POST) shape.

| Route | What it carries |
|---|---|
| `/v2/electricity/rto/region-data` | hourly demand, day-ahead demand forecast, net generation, total interchange per balancing authority |
| `/v2/electricity/rto/fuel-type-data` | hourly net generation by fuel type (coal, gas, nuclear, hydro, wind, solar, other) |
| `/v2/electricity/rto/interchange-data` | hourly interchange between each pair of balancing authorities |
| `/v2/electricity/rto/region-sub-ba-data` | hourly demand for sub-balancing-authority areas |
| `/v2/electricity/rto/daily-region-data` | daily rollup of region-data |
| `/v2/electricity/rto/daily-fuel-type-data` | daily rollup of generation by fuel type |
| `/v2/electricity/rto/daily-interchange-data` | daily rollup of interchange |
| `/v2/electricity/rto/daily-region-sub-ba-data` | daily rollup of sub-BA demand |

## Step 1 — enumerate the family

`GET /v2/electricity/rto?api_key=…` returns the eight child routes above.

## Step 2 — read the route contract

`GET /v2/electricity/rto/region-data?api_key=…`

Take `frequency[]` (hourly and local-hour variants exist on these routes), `facets[]` and the
`data{}` measure columns with their units from the response. Do not hard-code them — EIA has
added columns to this family before (v2.1.6 added sub-BA points).

## Step 3 — resolve the respondent and type facets

```
GET /v2/electricity/rto/region-data/facet/respondent?api_key=…
GET /v2/electricity/rto/region-data/facet/type?api_key=…
```

`respondent` is the balancing-authority identifier and `type` is the series type (demand,
day-ahead demand forecast, net generation, total interchange). These two facet ids are the
ones EIA's route metadata exposes on this family. **Read the value lists from the facet route
rather than assuming a code list** — balancing-authority membership changes as BAs are added,
merged or retired, and the value ids are the API's own, not the ISO/RTO's marketing names.

## Step 4 — query a window

```
GET /v2/electricity/rto/region-data/data
  ?api_key=…
  &frequency=hourly
  &data[]=<measure column from step 2>
  &facets[respondent][]=<respondent id from step 3>
  &facets[type][]=<type id from step 3>
  &start=<start in the route's dateFormat>
  &end=<end in the route's dateFormat>
  &sort[0][column]=period&sort[0][direction]=desc
  &offset=0&length=5000
```

Use the `format` string from the route's own `frequency[]` metadata for `start`/`end` —
hourly routes use an hour-resolution stamp, not a bare date.

## Step 5 — page, because hourly data overruns instantly

Hourly data blows past the 5,000-row cap fast: one balancing authority, one type, one year is
already ~8,760 rows, and an unfiltered request across all respondents and types is millions.

- Always filter by `respondent` **and** `type`.
- Always bound with `start`/`end`.
- Page on `offset`/`length` until `offset >= response.total`.
- Treat the `{"warning":"parameter out of range"}` object as "you were truncated", not as an
  error — the rows you got are still valid.

For multi-year, all-respondent extracts, do not loop the API — pull the
`EBA` bulk archive instead: `https://www.eia.gov/opendata/bulk/EBA.zip`, titled "U.S. Electric
System Operating Data (Older Than 7 Days)", no key required (see `eia-bulk-download.md`). Use
the API for the recent window the bulk file excludes, and the bulk file for history.

## Rate discipline

Fan-out across respondents is the classic way to trip the throttle. Keep sustained volume
under ~9,000 requests/hour and bursts under 5/second; on a 403 back off rather than retry —
key suspension is automatic, temporary and self-clearing.

## Caveats

- Values are JSON **strings** since v2.1.6; sub-BA identifiers carry leading zeroes, which is
  exactly why EIA moved off JSON numbers. Do not parse identifiers as integers.
- Data is updated continuously — APIv2 reads the public-facing databases directly. There is no
  `update` field (it existed in APIv1 and was removed for performance), so use `period` and
  re-query rather than looking for a last-modified signal.
- Timestamps: read the route's `dateFormat` and be explicit about UTC vs local-hour variants
  before comparing series across balancing authorities.

Details: `conventions/eia-conventions.yml`, `rate-limits/eia-rate-limits.yml`,
`data-model/eia-data-model.yml`.
