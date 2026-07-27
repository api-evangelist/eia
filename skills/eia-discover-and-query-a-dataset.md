---
name: Discover and query an EIA dataset
description: Walk the EIA APIv2 route tree from the root to a leaf dataset, read its contract (frequencies, facets, data columns), resolve facet values, then pull filtered, sorted, paginated data. This is the universal pattern for all 225 routes.
api: openapi/eia-api-v2-openapi.yml
generated: '2026-07-27'
method: generated
source: https://www.eia.gov/opendata/documentation.php
operations:
  - GET /v2
  - GET /v2/electricity
  - GET /v2/electricity/retail-sales
  - GET /v2/electricity/retail-sales/facet
  - GET /v2/electricity/retail-sales/facet/{facet_id}
  - GET /v2/electricity/retail-sales/data
  - POST /v2/electricity/retail-sales/data
---

# Discover and query an EIA dataset

EIA APIv2 has essentially no operationIds (6 of 278, and the only meaningful one is a PHP
controller class name), so operations are addressed by **method + path**. The whole API is
three repeating shapes, which is why one skill covers all 225 routes.

## Before you start

- Get a free key at <https://www.eia.gov/opendata/register.php>. It arrives by email
  automatically — no review, no approval.
- The key goes in the **URL query string** as `api_key`. EIA will not read it from a header.
- Everything here is a **read**. Nothing in this API writes, so there is nothing to make
  idempotent and nothing to roll back.

## Step 1 — list the top-level families

`GET /v2?api_key=…`

Returns `response.routes[]` — the 15 families: `electricity`, `natural-gas`, `coal`,
`crude-oil-imports`, `densified-biomass`, `nuclear-outages`, `co2-emissions`,
`international`, `seds`, `total-energy`, `steo`, `aeo`, `ieo`, and so on.

## Step 2 — walk down to a leaf

`GET /v2/electricity?api_key=…`

Any request that does **not** end in `/data` returns metadata, not values. Append the child
`id` from `response.routes[]` and repeat until the response stops carrying `routes[]` and
starts carrying `frequency[]`, `facets[]` and `data{}` — that is a leaf dataset.

## Step 3 — read the leaf's contract

`GET /v2/electricity/retail-sales?api_key=…`

Read four things off the response and do not guess any of them:

| Field | Use |
|---|---|
| `frequency[]` | valid `frequency=` values, each with its `format` (e.g. `YYYY-MM`) |
| `facets[]` | the filterable dimensions (e.g. `stateid`, `sectorid`) |
| `data{}` | the selectable measure columns, with `alias` and `units` |
| `startPeriod` / `endPeriod` | the real coverage window |

## Step 4 — resolve facet values

`GET /v2/electricity/retail-sales/facet` lists the facets;
`GET /v2/electricity/retail-sales/facet/sectorid?api_key=…` lists their valid values
(`RES`, `COM`, `IND`, `TRA`, `OTH`, `ALL`).

A facet value that does not exist is **not an error** — it returns HTTP 200 with zero rows.
Always resolve values here rather than assuming them.

## Step 5 — query the data

```
GET /v2/electricity/retail-sales/data
  ?api_key=…
  &data[]=price&data[]=revenue
  &facets[sectorid][]=RES&facets[stateid][]=CO
  &frequency=monthly
  &start=2008-01-31&end=2008-03-01
  &sort[0][column]=period&sort[0][direction]=desc
  &offset=0&length=5000
```

Rules that bite:

- **`data[]` is mandatory to get numbers.** Without it you get dimension columns and no
  values. This is the single most common "no error but no data" report in EIA's own FAQ.
- **Date bounds compare lexically.** For monthly data, `start=2008-02-01` *excludes* the
  `2008-02` point — use `2008-01-31`. Since v2.1.11 an identical `start` and `end` on a
  lower-periodicity series returns the full inclusive range instead of zero rows.
- **Values are JSON strings, not numbers**, since v2.1.6 (Jan 2024). Cast before arithmetic.
- Each requested column comes back with a companion `<column>-units` field. Never assume
  units — read them.

## Step 6 — page through the result

The API returns at most **5,000 rows** (300 in XML). `response.total` always reports the full
responsive count regardless of `offset`/`length`.

```
loop:
  request with offset = n * 5000, length = 5000
  stop when (n * 5000) >= response.total
```

If the payload carries
`{"warning":"parameter out of range","description":"The API can only return 5000 rows…"}`
you were truncated — page, or narrow with facets and dates.

## Long queries

If the URL gets too long, use `POST /v2/<route>/data` with a JSON body matching the
`DataParams` schema (`data`, `facets`, `frequency`, `start`, `end`, `sort`, `length`,
`offset`), or send `application/x-www-form-urlencoded` parameters in the GET body. **The
`api_key` still has to be in the URL.** The POST form is a read — it returns the same
`DataResponse`.

## Errors and throttles

| Condition | Response |
|---|---|
| no key | 403 `{"error":{"code":"API_KEY_MISSING",…}}` |
| bad key | 403 `{"error":{"code":"API_KEY_INVALID",…}}` |
| bad parameter | 400 `{"error":"Invalid frequency 'millenially' provided…","code":400}` |
| unknown route | 404 `{"error":"Not found.","code":404}` |

Stay under **~9,000 requests/hour sustained and 5/second burst**, or the key is automatically
suspended for seconds-to-minutes and then automatically reactivated. Back off on 403 rather
than retrying hot. Since v2.1.10 the HTTP status always agrees with the body — before that it
did not, so do not trust status alone on cached or mirrored responses.

If you are about to walk the whole tree, **stop and use the bulk facility instead** — see
`eia-bulk-download.md`.

Details: `conventions/eia-conventions.yml`, `errors/eia-problem-types.yml`,
`rate-limits/eia-rate-limits.yml`, `examples/eia-api-v2-examples.yml`.
