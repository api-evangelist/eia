---
name: Bulk-download EIA datasets without an API key
description: Read the EIA bulk manifest and pull whole datasets as zipped newline-delimited JSON — the correct alternative to recursively scraping APIv2, and the only EIA surface that needs no API key at all.
api: https://www.eia.gov/opendata/bulk/manifest.txt
generated: '2026-07-27'
method: generated
source: https://www.eia.gov/opendata/bulkfiles.php, https://www.eia.gov/opendata/bulk/manifest.txt
operations:
  - GET /opendata/bulk/manifest.txt
  - GET /opendata/bulk/{dataset}.zip
---

# Bulk-download EIA datasets without an API key

If you are about to write a recursion routine that walks the APIv2 route tree, stop. EIA
publishes every one of these datasets as a single zip and asks nothing of you — **no API key,
no registration, no terms click-through at the transport layer**. This is also the only way to
get whole datasets without burning your key's throttle budget.

## Step 1 — read the manifest

```
GET https://www.eia.gov/opendata/bulk/manifest.txt
```

Returns a JSON catalog in Project Open Data style: a single `dataset` object keyed by dataset
id, each entry carrying `identifier`, `name`, `title`, `description`, `keyword[]`,
`publisher`, `person`, `mbox`, `accessLevel`, `accessURL` and `last_updated`.

Verified 2026-07-27: **29 datasets**, retrieved anonymously.

> **Host note.** The historical endpoint `https://api.eia.gov/bulk/manifest.txt` now returns
> **HTTP 301** to `https://www.eia.gov/opendata/bulk/manifest.txt`, and every `accessURL` in
> the manifest points at `www.eia.gov/opendata/bulk/`. Follow redirects, and prefer the
> `www.eia.gov` form — it is the canonical one the manifest itself publishes.

## Step 2 — pick datasets from the manifest, not from memory

Never hard-code a filename. Read `accessURL` off the manifest entry. As of 2026-07-27 the
catalog includes:

| id | title | updated |
|---|---|---|
| `EBA` | U.S. Electric System Operating Data (Older Than 7 Days) | 2026-07-27 |
| `ELEC` | Electricity | 2026-07-22 |
| `NG` | Natural Gas | 2026-07-23 |
| `PET` | Petroleum and other liquid fuels | 2026-07-22 |
| `PET_IMPORTS` | Petroleum Imports | 2026-06-30 |
| `COAL` | Coal | 2026-06-23 |
| `NUC_STATUS` | Nuclear outages | 2026-07-27 |
| `EMISS` | Emissions | 2023-07-12 |
| `INTL` | International Energy Data | 2026-07-22 |
| `SEDS` | State Energy Data System | 2026-06-26 |
| `STEO` | Short-Term Energy Outlook | 2026-07-07 |
| `TOTAL` | Total Energy | 2026-06-24 |
| `IEO`, `IEO.2017/2019/2021/2023` | International Energy Outlook + vintages | |
| `AEO.2014`–`AEO.2026` | Annual Energy Outlook vintages | `AEO.2026` 2026-03-26 |

Note the gaps and the vintage pattern: outlook releases are frozen snapshots kept forever
(there is no `AEO.2024`), while the operational datasets are refreshed.

## Step 3 — pull the archive

```
GET https://www.eia.gov/opendata/bulk/ELEC.zip
```

These are large — `ELEC.zip` was ~292 MB on a 2026-07-27 check. Stream to disk, do not buffer
in memory. Each zip contains **newline-delimited JSON**: one JSON object per line, mixing
series records (with their full observation arrays) and category records. Parse line-by-line;
never `json.load()` the whole file.

## Step 4 — refresh on the published cadence

Bulk files are regenerated **twice daily, 5 a.m. and 3 p.m. Eastern**. Compare
`last_updated` in the manifest against your local copy and only re-download changed datasets —
the manifest is a few tens of KB, the archives are hundreds of MB.

## Choosing bulk vs API

| Use bulk when | Use APIv2 when |
|---|---|
| you need a whole dataset or long history | you need a narrow slice (a few facets, a date window) |
| you would otherwise make thousands of calls | you need data fresher than the last bulk run |
| you have no API key | you need the hourly window `EBA` excludes (last 7 days) |
| you want deterministic offline reprocessing | you want the route/facet metadata contract |

## Caveats

- Bulk series carry **APIv1-style series IDs**, not APIv2 route paths. Use
  `https://www.eia.gov/opendata/#translate` or `GET /v2/seriesid/{APIv1-SERIESID}` to map a
  bulk series onto an APIv2 route, and remember EIA's own warning that the mapping is not
  exactly 1:1.
- `EBA` is explicitly "Older Than 7 Days" — the recent week is API-only.
- The bulk facility carries no key, but the attribution and no-endorsement terms in EIA's API
  Terms of Service and Copyrights and Reuse Policy still apply to the data.

Details: `lifecycle/eia-lifecycle.yml`, `rate-limits/eia-rate-limits.yml`.
