---
name: eu-open-data-portal-assess-metadata-quality
description: Read the Metadata Quality Assurance (MQA) score for a catalogue, country, dataset or distribution on data.europa.eu, and find the specific DCAT-AP violations behind it.
api: eu-open-data-portal:eu-open-data-portal-mqa-metrics-cache-api
operations:
  - getGlobalMetrics
  - getCountryMetrics
  - getSingleCountryMetrics
  - getCatalogueMetrics
  - getSingleCatalogueMetrics
  - getHistoricSingleCatalogueMetrics
  - getCatalogueViolations
  - getCatalogueDistributionReachability
  - getSingleDatasetMetrics
  - getDistributionMetrics
generated: '2026-09-07'
method: generated
source: openapi/eu-open-data-portal-mqa-metrics-cache-openapi.yaml
---

# Assess metadata quality on data.europa.eu

Base URL: `https://data.europa.eu/api/mqa/cache`. Every read below is anonymous.

The MQA scores DCAT-AP metadata out of **450 points** across five dimensions, with these maxima stated in the contract: findability 100, accessibility 100, interoperability 110, reusability 75, contextuality 20.

## 1. Establish the baseline

`GET /global` (`getGlobalMetrics`) — the portal-wide score. `GET /global/history` for the series.

## 2. Compare the peer group

`GET /countries` (`getCountryMetrics`) ranks every country; `GET /countries/{id}` (`getSingleCountryMetrics`) and `GET /countries/{id}/history` drill into one.

`GET /catalogues` (`getCatalogueMetrics`) does the same across all catalogues (209 in the live response at the time of writing).

## 3. Score the catalogue you care about

`GET /catalogues/{id}` (`getSingleCatalogueMetrics`) for the current score, `GET /catalogues/{id}/history` (`getHistoricSingleCatalogueMetrics`) for the trend.

## 4. Turn a score into a work list

- `GET /catalogues/{id}/violations` (`getCatalogueViolations`) — the specific DCAT-AP violations to fix. This is the operation that makes the score actionable.
- `GET /catalogues/{id}/distributions/reachability` (`getCatalogueDistributionReachability`) — returns `202`; the reachability sweep runs asynchronously and there is no callback, so re-read the result rather than waiting on the response.
- `GET /datasets/{id}` (`getSingleDatasetMetrics`) and `GET /distributions/{id}` (`getDistributionMetrics`) narrow it to one record.
- `GET /distributions/{id}/validations` returns the validation detail as CSV.

## 5. Fix before you publish

Run the candidate graph through the SHACL validator first — see `eu-open-data-portal-validate-dcat-ap.md`. Fixing violations there is cheaper than publishing and re-scoring.

## Rules

- Admin operations (`POST /admin/refresh`, `/admin/clear`, `/admin/schedule`, `/admin/migratescore`) require an `X-API-Key` and are the portal team's, not an integrator's. They answer `202`.
- Scores are cached, not computed on request. A metadata fix will not move the number until the next refresh sweep.
- `404` means the scope id has no stored metrics document — not necessarily that the catalogue does not exist.
