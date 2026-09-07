---
name: eu-open-data-portal-publish-dataset
description: Create or update a DCAT-AP dataset in a data.europa.eu catalogue you are responsible for — obtain a token, check before you write, upsert by originalId, and undo.
api: eu-open-data-portal:eu-open-data-portal-registry-api
operations:
  - getCatalogueResourcesOrigin
  - putCatalogueResourcesOrigin
  - postCatalogueResources
  - listCatalogueResources
  - getDCATResource
  - deleteCatalogueResourcesOrigin
  - deleteDCATResource
  - createDatasetDraft
  - publishDatasetDraft
  - hideDataset
  - checkIdentifierEligibility
  - createDatasetIdentifier
generated: '2026-09-07'
method: generated
source: >-
  openapi/eu-open-data-portal-hub-repo-openapi.yaml and
  https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/
---

# Publish a dataset to data.europa.eu

Base URL: `https://data.europa.eu/api/hub/repo`. **This surface writes to the European Union's public metadata record.** You need write access to a catalogue, which the portal team grants — it is not self-service.

## 1. Get a token

Two documented routes (see `authentication/eu-open-data-portal-authentication.yml`):

- **Service account** — `POST https://data.europa.eu/auth/middleware/login/service` with `{"client_id": "...", "client_secret": "..."}`; the response carries `access_token`.
- **EU Login user** — `POST https://data.europa.eu/auth/realms/DEU/protocol/openid-connect/token` with `grant_type=password` to get a user token, then the same endpoint with `grant_type=urn:ietf:params:oauth:grant-type:uma-ticket` and `audience=piveau-hub-repo` to exchange it for a **party token**.

Send it as `Authorization: Bearer <token>`. Tokens expire in **300 seconds** — refresh rather than caching.

A catalogue-scoped API key in the `X-API-Key` header is the alternative the contract declares.

## 2. Check before you write

The upsert key is the pair (`catalogueId`, `originalId`) — an id **you** choose. The manual is explicit: `GET` first, or you will silently update someone else's record instead of creating yours.

`GET /catalogues/{catalogueId}/resources/origin?originalId=<your id>` (`getCatalogueResourcesOrigin`) — `404` means the id is free.

## 3. Validate the graph

Run it through `POST https://data.europa.eu/api/mqa/shacl/validation/report` first. See `eu-open-data-portal-validate-dcat-ap.md`.

## 4. Upsert

`PUT /catalogues/{catalogueId}/resources/origin?originalId=<your id>` (`putCatalogueResourcesOrigin`) with the DCAT-AP graph in Turtle, RDF/XML, JSON-LD, N-Triples, N-Quads, TriG, TriX or N3 (set `Content-Type` accordingly).

Responses: `201` created, `204` updated, `304` **not modified** — the graph you sent is identical to the stored one, so nothing changed. `409` means the originalId collides with a resource of a different type. `401`/`403` mean the token does not carry write access to that catalogue.

Note the deprecation: the `/catalogues/{catalogueId}/datasets*` and `/datasets*` paths still work but are marked deprecated in the contract, which names the general DCAT Resources API above as the replacement. Write new integrations against `/resources`.

## 5. Undo

There is no restore window published, so treat every write as final and keep your own copy of the graph.

- `DELETE /catalogues/{catalogueId}/resources/origin?originalId=...` (`deleteCatalogueResourcesOrigin`) or `DELETE /resources/{resourceId}` (`deleteDCATResource`) removes it.
- To un-publish rather than delete, use the draft surface: `POST /drafts/datasets` (`createDatasetDraft`), `PUT /drafts/datasets/publish/{id}` (`publishDatasetDraft`), `PUT /drafts/datasets/hide/{id}` (`hideDataset`).
- Prior states are readable — `GET /datasets/revisions/{revisionId}` and `GET /datasets/{datasetId}/diff` — so a previous graph can be recovered and re-PUT by you. No retention period is documented, so do not rely on it.

## 6. Persistent identifier (optional)

`GET /identifiers/datasets/{datasetId}/eligibility` (`checkIdentifierEligibility`) before `PUT /identifiers/datasets/{datasetId}` (`createDatasetIdentifier`). A `422` on the PUT means the dataset is not eligible; the eligibility call tells you why first.

## Rules

- **No idempotency key exists.** Safety comes from using `PUT` with your own `originalId`. Never retry a `POST /catalogues/{catalogueId}/resources` on a timeout — it creates a duplicate. Retry the `PUT` instead; it is safe to repeat and answers `304` when nothing changed.
- Bulk: `PUT /bulk/datasets` on hub-search returns a per-item `{success, status, message, id}` array rather than failing the whole batch.
- `POST /action` is a JSON-RPC 2.0 surface (string `id`, object `params`, no batching) — not a REST operation.
