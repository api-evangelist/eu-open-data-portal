---
name: eu-open-data-portal-search-datasets
description: Find European open datasets on data.europa.eu — full-text search, facets, spatial and temporal filters, and deep paging — then resolve their download links.
api: eu-open-data-portal:eu-open-data-portal-search-api
operations:
  - searchGet
  - searchPost
  - scrollGet
  - readVocabularies
  - readVocabulary
  - listCatalogues
  - readCatalogue
generated: '2026-09-07'
method: generated
source: openapi/eu-open-data-portal-hub-search-openapi.yaml
---

# Search EU open datasets

Base URL: `https://data.europa.eu/api/hub/search`. No credential is required for any step below.

## 1. Search

`GET /search` (`searchGet`) — or `POST /search` (`searchPost`) when the query is too long for a URL.

Useful parameters, all from the published contract:

- `q` — the query string.
- `filters` — array of document types: `dataset`, `catalogue`, `dataservice`, `datasetseries`, `series`, `resource`, `vocabulary`, `organization`, `resource_editorial-content`. Prefer this over the deprecated `filter`.
- `facets` — a JSON object passed as a string, e.g. `facets={"catalog":["catalog-x"]}`.
- `page` and `limit` — paging. `limit` must be an integer; a non-numeric value returns `400` with a `text/plain` body.
- `minDate` / `maxDate` / `dateType` — temporal filter.
- `bboxMinLon` / `bboxMaxLon` / `bboxMinLat` / `bboxMaxLat` — spatial bounding box.
- `fields`, `includes` — sparse field selection; ask only for what you will use, responses are large (a single `limit=1` search returned 325 KB).
- `sort`, `boost`, `minScoring` / `maxScoring`, `showScore` — ranking control.
- `aggregation`, `aggregationFields`, `globalAggregation`, `facetOperator`, `facetGroupOperator` — faceting.

The response is `{"success": true, "result": {"count": <total>, "results": [...]}}`.

## 2. Page beyond the search window

For more than a few pages, switch to the cursor: `GET /scroll` (`scrollGet`), or pass `searchAfter`, `searchAfterSort` and `pitId` to `/search`. This is the Elasticsearch point-in-time pattern surfaced directly; `page`/`limit` alone will not walk a 1.9M-record corpus.

## 3. Constrain with real vocabulary values, not guesses

`GET /vocabularies` (`readVocabularies`) lists the 26 controlled vocabularies. `GET /vocabularies/{vocabulary}` (`readVocabulary`) returns the concepts with multilingual `pref_label`s.

Use them for facet and filter values — `data-theme` (14 concepts), `hvd-category` (96), `file-type` (229), `licence` (178), `country` (347), `language` (1,424), `eurovoc` (7,486). Filtering on a label you invented will silently return nothing.

## 4. Scope to a catalogue

`GET /catalogues` (`listCatalogues`) and `GET /catalogues/{id}` (`readCatalogue`) identify the national portal or institution to scope to; pass its id in `facets`.

## 5. Get the data itself

Each dataset in the result carries a `distributions` array with `access_url`, `download_url`, `format`, `media_type` and `byte_size`. Download from `download_url`; `access_url` may be a landing page or a data service rather than a file.

## Rules

- Errors are not RFC 9457. A `400` or `404` may arrive as `text/plain` ("Bad Request", "dataset <id> not found") even though the contract documents `{"success": false, "message": "..."}`. Do not assume a JSON error body.
- No rate limits are published and no `X-RateLimit-*`, `RateLimit-*` or `Retry-After` headers are returned. Be conservative on your own: serialise requests, back off exponentially on `500`, and do not parallelise a crawl of the corpus.
- `500` responses can carry a raw backend exception string; treat the body as diagnostic text, not a contract.
- `filter` and `superCatalogue` are deprecated parameters on `/search`.
